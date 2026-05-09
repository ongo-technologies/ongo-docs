# MyFatoorah Payment Gateway — Integration Reference

> Source: Issue #87 research by @JCortez132 | Completed: 2026-04-19 | Reviewed: 2026-04-22

---

## 1. Authentication

All requests use a Bearer token in the `Authorization` header:

```
Authorization: Bearer {API_TOKEN}
```

- Token is available in the demo/production portal under **Integration Settings**
- Up to 5 keys per account, each scoped to a single region/currency
- **Qatar token is separate from Kuwait and other regions** — must be configured specifically for QAR
- Sandbox token is found in the demo portal after login

---

## 2. Base URLs

| Environment | Base URL |
|---|---|
| Sandbox | `https://apitest.myfatoorah.com` |
| **Qatar (Production)** | **`https://api-qa.myfatoorah.com`** |
| Kuwait, Bahrain, Jordan, Oman | `https://api.myfatoorah.com` |

Qatar hosted payment portal: `https://qa.myfatoorah.com`

> **Important:** Do NOT use `api.myfatoorah.com` for Qatar in production — it will reject QAR transactions.

Use **API v2** for initiation endpoints and **v3** for status verification.

---

## 3. End-to-End Hosted Payment Flow

Ongo uses the redirect/hosted page flow — raw card data never touches our server.

```
1. [OUR SERVER]   POST /v2/InitiatePayment
                  { InvoiceAmount, CurrencyIso: "QAR" }
                  ← Returns available PaymentMethods with PaymentMethodId values

2. [OUR SERVER]   POST /v2/ExecutePayment
                  { PaymentMethodId, InvoiceValue, CallBackUrl, ErrorUrl, CustomerName, ... }
                  ← Returns { InvoiceId, PaymentURL }

3. [OUR SERVER]   HTTP 302 redirect customer to PaymentURL

4. [CUSTOMER]     Completes payment on MyFatoorah hosted page (card entry, 3DS, QPay auth)

5. [MYFATOORAH]   Redirects to CallBackUrl?paymentId={PaymentId}
                  OR ErrorUrl?paymentId={PaymentId} on failure

6. [OUR SERVER]   GET /v3/payments/{paymentId}
                  ← Verify Invoice.Status = "PAID" AND Transaction.Status = "SUCCESS"

7. [MYFATOORAH]   (Async) POST webhook to our WebhookUrl
                  ← Validate signature, update order status idempotently
```

Steps 6 and 7 are complementary. Both must be handled — the webhook may arrive before the customer redirect.

---

## 4. Key API Endpoints

### POST `/v2/InitiatePayment`

Returns all enabled payment methods and service charges. Call this to discover `PaymentMethodId` values — **never hardcode them**.

**Request:**
```json
{ "invoiceAmount": 150.00, "currencyIso": "QAR" }
```

**Response (`Data.PaymentMethods[]`):**
```json
{
  "PaymentMethodId": 7,
  "PaymentMethodEn": "QPay",
  "PaymentMethodCode": "np",
  "ServiceCharge": 2.50,
  "TotalAmount": 152.50
}
```

---

### POST `/v2/ExecutePayment`

Creates the invoice and returns the hosted payment URL.

**Request:**
```json
{
  "PaymentMethodId": 7,
  "InvoiceValue": 150.00,
  "CustomerName": "Ahmed Al-Thani",
  "CustomerEmail": "customer@example.com",
  "CallBackUrl": "https://api.ongo.qa/payments/callback",
  "ErrorUrl": "https://api.ongo.qa/payments/error",
  "Language": "EN",
  "CustomerReference": "ORDER-12345",
  "InvoiceItems": [
    { "ItemName": "Car Wash Service", "Quantity": 1, "UnitPrice": 150.00 }
  ]
}
```

**Response:**
```json
{
  "IsSuccess": true,
  "Data": {
    "InvoiceId": 927972,
    "PaymentURL": "https://qa.myfatoorah.com/.../Checkout?invoiceKey=...",
    "IsDirectPayment": false
  }
}
```

Store `InvoiceId` and `CustomerReference` before redirecting.

---

### GET `/v3/payments/{paymentId}`

Authoritative server-side status verification. Call after redirect callback.

**Key response fields:**
```json
{
  "Data": {
    "Invoice": { "Id": "6389662", "Status": "PAID" },
    "Transaction": { "Status": "SUCCESS", "PaymentMethod": "QPay" },
    "Customer": { "Reference": "ORDER-12345" },
    "Amount": { "BaseCurrency": "QAR", "ValueInBaseCurrency": "150.00", "ReceivableAmount": "146.75" }
  }
}
```

`Transaction.Status` values: `SUCCESS`, `FAILED`, `INPROGRESS`, `AUTHORIZE`, `CANCELED`

---

## 5. Supported Payment Methods — Qatar

| Method | Notes |
|---|---|
| **QPay** | Qatar's primary local debit scheme — equivalent to Kuwait's KNET |
| Visa / Mastercard | 3DS required on all transactions |
| Apple Pay | Requires separate Apple Pay merchant cert setup |
| STC Pay | Saudi-origin wallet, available in Qatar |
| Google Pay | Subject to account enablement |

**KNET is Kuwait-only** — Qatar uses QPay. There is no KNET option on a QAR account.

`PaymentMethodId` values are not static across accounts. Always match by `PaymentMethodCode` (e.g., `"np"` for QPay), not by hardcoded ID.

---

## 6. Webhooks

Configure in portal: **Integration Settings > Webhook Settings**. Must be public HTTPS with a valid cert.

Use **Webhook V2** (V1 is legacy). Retries up to 5 times, max 180s delay.

### Events

| Code | Name | When |
|---|---|---|
| 1 | `PAYMENT_STATUS_CHANGED` | Any payment status update |
| 2 | `REFUND_STATUS_CHANGED` | Refund update |

### Payload (`PAYMENT_STATUS_CHANGED`)

```json
{
  "Event": { "Code": 1, "Name": "PAYMENT_STATUS_CHANGED", "CountryIsoCode": "QAT" },
  "Data": {
    "Invoice": { "Id": "6389662", "Status": "PAID", "ExternalIdentifier": "ORDER-12345" },
    "Transaction": { "Status": "SUCCESS", "PaymentId": "07076..." },
    "Amount": { "BaseCurrency": "QAR", "ValueInBaseCurrency": "150.00" }
  }
}
```

### Signature Validation (Mandatory)

Header: `MyFatoorah-Signature` — HMAC-SHA-256, base64-encoded.

Signing string format for `PAYMENT_STATUS_CHANGED`:
```
Invoice.Id=6389662,Invoice.Status=PAID,Transaction.Status=SUCCESS,Transaction.PaymentId=07076...,Invoice.ExternalIdentifier=ORDER-12345
```

```csharp
bool ValidateSignature(string signingPayload, string receivedSignature, string secretKey)
{
    var keyBytes = Encoding.UTF8.GetBytes(secretKey);
    var payloadBytes = Encoding.UTF8.GetBytes(signingPayload);
    using var hmac = new HMACSHA256(keyBytes);
    var hash = hmac.ComputeHash(payloadBytes);
    var computed = Convert.ToBase64String(hash);
    return CryptographicOperations.FixedTimeEquals(
        Encoding.UTF8.GetBytes(computed),
        Encoding.UTF8.GetBytes(receivedSignature));
}
```

Use `CryptographicOperations.FixedTimeEquals` — never `==` for signature comparison (timing attack risk).

---

## 7. Test Cards

### Visa / Mastercard

| Card Number | Expiry | CVV | Result |
|---|---|---|---|
| `4508750015741019` | Any future | Any | Visa success ✅ (verified) |
| `2223000000000007` | 01/39 | 100 | Mastercard success |
| `5123450000000008` | 01/39 | 100 | Mastercard success |

### STC Pay (Sandbox)

| Mobile | OTP |
|---|---|
| `0557877988` | `1234` |

Cardholder name: any two-part name (e.g., `test test`).

QPay sandbox test cards are not publicly listed — use Visa/MC test cards in sandbox to simulate Qatar payment flows.

---

## 8. Qatar-Specific Reference

| Field | Value |
|---|---|
| Currency ISO | `QAR` |
| Country ISO (webhooks) | `QAT` (3-letter, not `QA`) |
| Production API | `https://api-qa.myfatoorah.com` |
| Hosted payment portal | `https://qa.myfatoorah.com` |
| Sandbox account registration | Select **Kuwait** when signing up for a sandbox account |

---

## 9. Implementation Gotchas

1. **`PaymentMethodId` is not globally stable** — match by `PaymentMethodCode` (e.g., `"np"` for QPay), never hardcode IDs
2. **No localhost for `CallBackUrl`/`ErrorUrl`** — use ngrok or a deployed staging URL during development; localhost is rejected at the API level
3. **Always verify server-side** — never trust the redirect URL alone; call `GET /v3/payments/{paymentId}` after every callback
4. **Webhook race condition** — webhook may arrive before redirect; make the callback handler idempotent; if already marked paid, skip re-processing
5. **Duplicate webhooks** — MyFatoorah may send the same event twice; deduplicate by `Invoice.Id` + `Transaction.Status`
6. **`ServiceCharge` / `TotalAmount`** — if the portal passes charges to the customer, use `TotalAmount` from InitiatePayment as `InvoiceValue` in ExecutePayment; mismatch causes a validation error
7. **HTTP 200 does not mean success** — always check `IsSuccess` in the response body; a `200 OK` with `IsSuccess: false` is a business error; handle the `ValidationErrors` array
8. **Respond to webhook immediately** — return HTTP 200 right away, then process async (queue the payload); slow responses trigger retries
9. **`ExternalIdentifier` for correlation** — pass your internal order/booking ID as `CustomerReference` in ExecutePayment; it comes back as `Invoice.ExternalIdentifier` in the webhook, allowing order lookup without querying by `InvoiceId`
10. **No official .NET SDK** — there is a community NuGet package (`MyFatoorah` v1.0.2, .NET Standard 2.1); for our Clean Architecture setup, calling the REST API directly with typed `HttpClient` DTOs is cleaner — only 3 endpoints cover the happy path

---

## 10. Clean Architecture Placement

```
Ongo.Infrastructure/Options/PaymentOptions.cs              — BaseUrl, ApiToken, WebhookSecretKey
Ongo.Application/Services/IPaymentService.cs               — interface
Ongo.Infrastructure/Services/MyFatoorahPaymentService.cs   — implements IPaymentService
Ongo.Application/Features/Payment/                         — request/response DTOs
Ongo.Api/Endpoints/PaymentWebhookEndpoints.cs              — receives POST, validates sig, dispatches event
```

---

## 11. External Resources

| Resource | URL |
|---|---|
| API Documentation | https://docs.myfatoorah.com/docs/overview |
| Test Cards | https://docs.myfatoorah.com/docs/test-cards |
| API Sandbox (Swagger) | https://apitest.myfatoorah.com/swagger/ui/index |
| Demo Portal | https://demo.myfatoorah.com |

---

## 12. Related Issues

| Issue | Description |
|---|---|
| [#87](https://github.com/moe-ongo/ongo/issues/87) | Research & API Study (this document) |
| [#24](https://github.com/moe-ongo/ongo/issues/24) | MyFatoorah Payment Gateway Implementation |

---
title: API Endpoints
description: Screen-derived REST API endpoint map for the CWS Qatar Mobile App and Web Admin Panel — 35 endpoints across 10 feature areas
icon: material/api
---

# API Endpoints

All endpoints are derived from screen-level data requirements. No endpoint exists without a screen that owns it.

**Stack:** .NET backend · PostgreSQL · Azure hosting
**Auth:** JWT returned on OTP verification, required on all non-public endpoints
**Base URL:** `/api/v1`

---

## API Planning Framework

Endpoints follow a UI-first derivation model:

1. **Start from the screen** — list every screen in the Mobile App and Web Admin. Each screen is a data requirement.
2. **Map data needs** — for each screen, identify what it reads (`GET`) and what it changes (`POST` / `PUT` / `DELETE`).
3. **Derive endpoints** — only create an endpoint when a screen needs it. Any endpoint with no screen owner is marked **DEFERRED**.

!!! warning "Golden Rule"
    If no screen in Mobile or Admin calls an endpoint, mark it **DEFERRED** and do not build it. Any existing placeholder with no screen owner should be deleted or deferred before Sprint 2.

---

## Mobile App Endpoints

16 endpoints supporting the Flutter customer app, organised by feature area.

### Auth & Profile

| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/auth/otp/send` | Send OTP to phone number |
| `POST` | `/auth/otp/verify` | Verify OTP — returns JWT token |
| `GET` / `PUT` | `/customers/me` | Read or update customer profile |
| `POST` | `/customers/vehicles` | Add vehicle to profile |
| `POST` | `/customers/addresses` | Save delivery address |

### Booking Flow

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/packages/standard` | List Quick / Shine / Detail packages |
| `GET` | `/vendors?lat&lng` | Find available vendors near address |
| `GET` | `/vendors/:id/packages` | Custom packages per vendor |
| `POST` | `/bookings` | Create booking (quick or custom) |
| `GET` | `/bookings/:id` | Booking detail and current status |
| `DELETE` | `/bookings/:id` | Cancel booking (within 5-minute window) |

### Payments

| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/payments/initiate` | Trigger payment gateway (SkipCash / MyFatoorah) |
| `POST` | `/payments/webhook` | Gateway callback — update payment status |
| `GET` | `/bookings/:id/receipt` | Itemised receipt for customer |

### Post-Service

| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/bookings/:id/ratings` | Submit star rating and pre-set feedback options |
| `GET` | `/customers/me/bookings` | Customer order history list |

---

## Web Admin Endpoints

19 endpoints supporting the Angular admin panel, organised by feature area.

### Vendor Management

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/admin/vendors` | List all vendors with approval status |
| `PUT` | `/admin/vendors/:id/approve` | Approve vendor account |
| `GET` | `/admin/vendors/:id/documents` | View vendor-submitted documents |
| `PUT` | `/admin/vendors/:id/commission` | Set commission rate for vendor |

### Packages & Services

| Method | Path | Description |
|--------|------|-------------|
| `GET` / `POST` | `/admin/packages/standard` | Manage Standard Service Packages (SSPs) |
| `GET` | `/admin/packages/custom` | Review pending custom packages |
| `PUT` | `/admin/packages/custom/:id/approve` | Approve or reject Custom Service Package (CSP) |

### Booking Oversight

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/admin/bookings` | All bookings with filters (status, date, vendor) |
| `PUT` | `/admin/bookings/:id/refund` | Trigger refund for a booking |
| `PUT` | `/admin/bookings/:id/resolve` | Resolve a booking dispute |

### Finance & Payouts

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/admin/revenue` | Revenue dashboard data |
| `GET` | `/admin/payouts` | List vendor payout cycles |
| `POST` | `/admin/payouts/:id/approve` | Approve payout for bank transfer |
| `GET` | `/admin/payouts/export` | Export payout CSV report |

### Users & Roles

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/admin/users` | All customers with account status |
| `PUT` | `/admin/users/:id/deactivate` | Disable a customer account |
| `GET` | `/admin/users/stats` | User overview dashboard data |

### Content & Config

| Method | Path | Description |
|--------|------|-------------|
| `GET` / `POST` / `PUT` | `/admin/cms` | Manage FAQs, Terms & Conditions, banners |
| `POST` | `/admin/notifications/broadcast` | Send mass push notification |
| `GET` / `PUT` | `/admin/settings` | App-wide config (commission rate, service radius, etc.) |

---

## Endpoint Count Summary

| Consumer | Count | Feature areas |
|----------|-------|---------------|
| Mobile App (Flutter) | 16 | Auth, Booking, Payments, Post-Service |
| Web Admin (Angular) | 19 | Vendors, Packages, Bookings, Finance, Users, Config |
| **Total** | **35** | |

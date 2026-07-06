---
title: Requirements
description: As-built MVP requirements for Ongo — organized by platform
icon: material/clipboard-list-outline
---

# Requirements

!!! info "Document Info"
    This document reflects the **as-built MVP scope**, reconciled against the four codebases in **July 2026** (Week 3 of the delivery sprint). It **supersedes** the design-time *Ongo Feature List MVP v4\_S* (Feb 8, 2025), which described the originally-planned scope. Where the build deliberately diverged from that plan, this document describes what is actually being delivered. See **Scope Evolution** at the end for the significant pivots.

---

## MVP Scope

The MVP focuses on features that **directly enable booking and fulfilment**. Everything else is deferred to post-MVP.

<div class="stats-grid">
  <div class="stat-card">
    <div class="stat-value">4</div>
    <div class="stat-label">Platforms</div>
  </div>
  <div class="stat-card">
    <div class="stat-value">Flutter</div>
    <div class="stat-label">Customer App</div>
  </div>
  <div class="stat-card">
    <div class="stat-value">Angular</div>
    <div class="stat-label">Vendor & Admin</div>
  </div>
  <div class="stat-card">
    <div class="stat-value">Flutter</div>
    <div class="stat-label">On-Road Units</div>
  </div>
</div>

The platform runs an **on-demand dispatch model**: a customer books a service, the request is broadcast to nearby available field units, and the **first unit to accept** fulfils it. This is closer to a ride-hailing flow than the vendor-selection flow in the original plan — see [Booking & Dispatch Model](#booking-dispatch-model).

### Deliberate MVP simplifications

These decisions keep the MVP lean and are described inline in each section:

| Area | Decision |
|------|----------|
| **Vendor app** | Web portal only — no vendor native mobile app |
| **Pricing** | Flat commission model; dynamic pricing deferred |
| **Reviews** | Star rating + pre-set options only; no free text |
| **Customer tracking** | Status-message updates with fixed ETAs; no customer-facing live map |
| **Vendor self-service** | Vendor financials/analytics live in the **Admin** app for MVP, not the vendor portal |

!!! warning "Out of Scope — Deferred to Post-MVP"
    - **Auto-assign to highest-rated vendor** (MVP uses first-to-accept dispatch)
    - Customer-facing real-time GPS map during service
    - Vendor live fleet-monitoring map
    - Vendor native mobile app (Phase II)
    - Vendor self-serve financial & analytics dashboards (admin-only for MVP)
    - Cash on Delivery (COD)
    - Free-text reviews · Dynamic pricing · In-app messaging / chat
    - Booking dispute resolution · Payment refunds
    - CMS (FAQ / ToS / copy editing) · Bulk push-notification campaigns
    - Custom report generation & data export
    - Offline mode
    - SkipCash & QNB payment gateways (MyFatoorah only for MVP)
    - Scheduled-booking enhancements: vendor-side acceptance & near-time dispatch

!!! danger "Launch-critical dependency — the communications stack"
    Phone OTP (SMS/WhatsApp), booking SMS, and FCM push notifications **all** depend on **Twilio** and **Firebase** being taken to production ("go-live"), which is **not yet complete**. Until then, **social login is the dependable authentication path**. This is the single biggest launch risk and cuts across auth *and* notifications.

---

## Service Packages

Two package types exist. All vendors **must** support Standard packages. In both cases the customer chooses a **service** — never a specific vendor.

### Standard Service Packages (SSP)

Pre-set by Admin. Vendors toggle availability — they cannot change pricing.

| Package | Duration | Notes |
|---------|----------|-------|
| **Quick Wash** | ~30 min | Base tier |
| **Shine Wash** | ~60 min | Mid tier |
| **Detail Wash** | ~120 min | Premium tier |

When a customer books an SSP, the request goes to **nearby online field units across all vendors** (see dispatch model).

### Custom Service Packages (CSP)

Created by vendors, approved by Admin before going live.

- Vendor sets name, description, pricing, duration
- Can indicate special requirements (power outlet, water source)
- Subject to admin approval per vendor
- Can include promotional pricing

When a customer books a CSP, the request goes **only to the field units of the vendor who owns that service** (still geo-filtered — see below).

---

## Booking & Dispatch Model

This is the core engine of the platform. The customer selects a **service**, not a vendor; the system finds and assigns a field unit on demand.

!!! info "How dispatch works"
    1. Customer creates a booking for a service (SSP or CSP) at a location. **No vendor is assigned yet.**
    2. The system finds **nearby online field units** within a service radius (~5 km) using geo-filtering:
        - **SSP** → units across **all** vendors
        - **CSP** → units of the **owning vendor** only
    3. The request is pushed to those units in real time. The **first unit to accept wins** — that unit (and its vendor) is assigned the booking.
    4. If **no unit accepts within ~5 minutes**, the booking is marked **No Units Found** and the customer is informed.

### Booking status lifecycle

| Status | Meaning |
|--------|---------|
| **Searching** | Broadcast out; waiting for a unit to accept |
| **Accepted** | A field unit claimed the job |
| **On Way** | Unit has started the journey |
| **Arriving** | Unit is close (~3 mins away) |
| **In Progress** | Service has started |
| **Completed** | Service finished |
| **Cancelled** | Cancelled by customer/system |
| **No Units Found** | No unit accepted within the timeout |

### Instant vs Scheduled

- **Instant ("Now")** — dispatched immediately; a nearby unit accepts and heads over.
- **Scheduled** — the customer picks a future time. In MVP, scheduled bookings use the **same self-accept dispatch** as instant bookings.

!!! note "Scheduled booking — known MVP limitation"
    A scheduled booking is broadcast at the time it is created and needs a field unit **online at that moment** to claim it; otherwise it becomes **No Units Found**. Vendor-side acceptance of scheduled jobs and near-time re-dispatch are **post-MVP** improvements. "Online" means a unit is on shift within working hours.

---

## 1. Customer App — Flutter

### 1.1 Account Management

- **Sign in with Google or Apple** (social login) — the primary, production-ready path for MVP
- **Phone number sign-up (Qatar `+974`) with OTP** — SMS by default, WhatsApp available as a channel
- Profile: name, email (optional; seeded from social login on first sign-in), language preference
- **Multiple saved addresses**, each labelled (e.g. home/work) with building, floor, apartment, street, additional directions and a default flag; plus an **ad-hoc pinned location** per booking
- Saved vehicles: type, colour, plate number, optional photo
- Order history

!!! warning "Phone OTP is pending go-live"
    Google/Apple social login works today. **Phone OTP (SMS + WhatsApp via Twilio) is built but not yet production-ready** — WhatsApp is in sandbox and needs business go-live approval; SMS is untested in production. Treat social login as the reliable launch path. See the launch-critical dependency callout above.

### 1.2 Booking Flow

The customer picks a **service** and the system dispatches a unit. There is one flow, differing only by package type:

1. Enter/confirm location (pin on map + address details)
2. Choose vehicle (type, saved name, optional photo)
3. Select a service:
    - **Standard package** — Quick / Shine / Detail wash at pre-set pricing, or
    - **Custom package** — a vendor's custom service (with any special requests/notes)
4. Choose time: **Now** or **Schedule**
5. Confirmation page shows all details + total price
6. Pay
7. The app shows live booking status as a **nearby unit is found and accepts** (see dispatch model)

!!! note "No vendor selection"
    Customers do not browse or pick vendors. For standard packages the vendor is whoever accepts; for custom packages the vendor is the one who owns the chosen service.

### 1.3 Cancellation Policy

- Customer may cancel within **5 minutes** of booking confirmation at no charge
- After 5 minutes, standard cancellation policy applies

### 1.4 Location & Tracking

- Address pinning via map (no customer-facing live GPS map in MVP)
- **Status-based updates** delivered via SMS **and push** at key moments:

| Trigger | Notification sent |
|---------|-------------------|
| Booking confirmed | Confirmation + assigned unit's contact number |
| Unit starts journey | "Your provider is on the way — arriving ~20 mins" |
| Unit near location (~3 mins) | "Arriving soon" |
| Service started | "Service in progress — Est. 45 mins remaining" |
| Service complete | Completion confirmation + rating prompt |

!!! note "Fixed estimates"
    MVP uses **fixed estimates** (≈20 min journey, ≈45 min service) rather than live GPS-derived ETAs — a deliberate simplification. Field units do stream location, but only for **dispatch matching**, not for a customer-facing map.

### 1.5 Payments

| Method | Provider |
|--------|----------|
| Local debit/credit cards (Qatar) | **MyFatoorah** |
| Visa / Mastercard | MyFatoorah |
| Google Pay | MyFatoorah |
| Apple Pay | MyFatoorah |

- **MyFatoorah is the only gateway for MVP** (SkipCash / QNB deferred)
- Payment methods: card, Apple Pay, Google Pay — **no COD**
- Customer consent required to store card data for future use
- Itemised receipts available in order history
- QAR is the primary currency display

### 1.6 Notifications

- Push notifications (Firebase FCM) — customer must grant permission
- SMS for: booking confirmation, status updates, assigned unit's contact number post-booking

*(Delivery depends on the comms-stack go-live — see the launch-critical dependency callout.)*

### 1.7 Ratings & Reviews

- Post-service rating prompt (5-star)
- Pre-set compliment / complaint options — no free-text in MVP
- All reviews are **moderated by Admin** before publishing (customers are not informed of moderation)

!!! note "No customer-facing vendor browsing"
    Because customers book services and not vendors, there is **no vendor rating browse/filter** in the customer app. Ratings are still collected — they feed Admin quality control and vendor performance analytics.

### 1.8 Support

- In-app support button that **opens WhatsApp** to message the support team (replaces in-app chat)

---

## 2. Vendor Portal — Angular Web

!!! info "Vendor role in MVP"
    With on-demand self-accept dispatch, the vendor admin is a **monitor and configurator**, not a dispatcher. The portal covers onboarding, service management, personnel, and job monitoring. **Vendor financial and analytics dashboards are not in the vendor portal for MVP** — that visibility lives in the Admin app (a deliberate resourcing pivot).

### 2.1 Registration (Become a Partner)

- Business profile: valid email, phone number, trade name
- Online registration form with document uploads

!!! info "Required Registration Documents"
    Trade License · Commercial Registration · Qatar ID · Bank Letter · **Vehicle Registration** · **Insurance Certificate** · Other (optional catch-all — e.g. signed declaration, proof of any registration-fee payment).

    Logo and cover photo are captured as **profile branding**, not verification documents.

### 2.2 Service Management

- Toggle availability for each Standard Service Package (SSP) individually
- Add, manage, and price Custom Service Packages (CSP):
    - Service name, description, duration
    - Special requirements (power outlet, water source)
    - Pricing + optional promotional pricing
- CSPs require Admin approval before going live
- Service area definition: choose from a predefined location list **or** set a static radius

!!! note "Availability is per field unit, not per vendor"
    There is **no vendor-level online/offline toggle** in MVP. Whether a vendor can receive a job depends on whether its **field units are online** (on shift). A vendor may effectively "close" while keeping a unit on shift.

### 2.3 Booking Monitoring

- Real-time dashboard view of incoming and active bookings (now and scheduled)
- Monitor the service status of each on-road unit in the field
- View capacity across multiple on-road units

!!! note "Dispatch is automatic"
    The vendor admin does **not** accept/decline bookings or assign them to units — field units **self-accept** from the broadcast. Scheduled-day/week/month calendar views and vendor accept/decline/assign are not part of the MVP portal.

### 2.4 Financial (Admin-managed for MVP)

- Payment collection is automated by the gateway; commission is deducted per transaction
- Payout data exists in the backend, but **vendor-facing earnings, transaction history, and commission views are not in the vendor portal for MVP** — payouts are managed from the Admin app

### 2.5 User Management

- Update vendor admin profile details
- Add sub-users for each on-road unit (fleet/personnel accounts)

---

## 3. On-Road Unit App — Flutter

Used by on-road wash-unit staff via a **Flutter mobile app**, consistent with the customer-app codebase.

### 3.1 Home & Availability

- Home dashboard: current active job, upcoming jobs, and daily job-count / performance stats
- **Online / Offline toggle** — "online" means the unit is on shift and eligible to receive job requests; this drives dispatch
- Availability state persists and is restored on app start

!!! note "No earnings on the unit"
    The field unit sees job count and performance, but **not earnings** — payments route to the vendor, so earnings are not shown to units in MVP.

### 3.2 Receiving & Accepting Jobs

- New booking requests **pop up in real time** (push / SignalR) for nearby online units
- The unit **self-accepts** a job — first to accept wins
- On acceptance, view all job details:
    - Customer name + contact number (tap to call)
    - Vehicle details (type, colour, plate)
    - Location + address details
    - Package selected + special requests/notes
    - Scheduled time

### 3.3 Status Updates

- Update booking status at key moments (drives the customer notifications):
    - Journey started → **On Way**
    - Near location → **Arriving**
    - Service started → **In Progress**
    - Service completed → **Completed**

### 3.4 Service Quality Checklist

- Complete a quality checklist upon service completion
- Upload **before/after photos**
- **Customer signature / approval capture at completion is planned for MVP** but not yet built — the team will complete it if time allows

---

## 4. Admin Dashboard — Angular Web

!!! info "Primary MVP build"
    The Admin app is the most complete of the four and carries the platform's operational and analytics surface for MVP (including the vendor-facing metrics that were pulled from the vendor portal).

### 4.1 User Management

- Manage and search customer accounts
- Approve, suspend, and manage vendor accounts
- Manage on-road unit accounts
- User roles and permissions
- Overview dashboard: real-time user stats — new users, total vendors, new vendor registrations

*(Mass communication / bulk push to all users or segments is deferred to post-MVP.)*

### 4.2 Service Management

- Define and manage Standard Service Package (SSP) categories for all vendors
- Review and approve Custom Service Packages (CSP) per vendor
- Set a **flat commission rate** applied to all vendors

*(No COD commission handling — COD is out of scope.)*

### 4.3 Booking Oversight

- View all current and historical bookings
- Manage basic cancellations

*(Dispute resolution and refunds are deferred to post-MVP.)*

### 4.4 Financial Management

- Revenue dashboard (platform-wide and per vendor)
- Commission tracking
- **Vendor payouts** — generate payout batches and mark as paid

!!! note "Payout bank approval"
    A formal "approve vendor bank info before payout" gate is **not yet enforced** — payouts currently do not gate on it. This may be added; the doc will be updated if so.

### 4.5 Analytics & Reporting

- KPI cards: total bookings, revenue, customers, vendors, completion/cancellation rates, commission
- **Top vendors** ranking
- **Trend charts**: bookings, revenue, and user growth over time
- Filter by period

*(Custom report generation and data export are deferred to post-MVP.)*

### 4.6 App Configuration

- Manage app settings and feature parameters
- Feature toggles (where applicable)
- Manage third-party integrations (maps, payment gateways)

### 4.7 Quality Control

- Monitor vendor ratings and performance metrics
- **Moderate and approve customer reviews** before publishing
- Enforce service completion standards (via the on-road unit checklist)

---

## Non-Functional Requirements

### Performance

| Metric | Target |
|--------|--------|
| App launch time | < 3 seconds |
| Page transitions | 60 FPS |
| Memory usage (Flutter) | < 150 MB |
| Booking confirmation response | < 2 seconds |
| Search / filter response | < 1 second |
| Payment confirmation | < 5 seconds |
| Admin analytics endpoints | < 500 ms |

### Availability

| Metric | Target |
|--------|--------|
| Uptime (business hours 6 AM–11 PM QST) | 99.5% |
| Recovery time objective (RTO) | < 4 hours |
| Partial failure behaviour | Graceful degradation |

### Security

| Requirement | Standard |
|-------------|----------|
| Payment processing | PCI DSS compliant (via MyFatoorah hosted page — no raw card data handled client-side) |
| Data at rest | AES-256 encryption |
| Data in transit | HTTPS / TLS 1.3 |
| Security reviews | Regular audits |

### Architecture & Real-time

- Monolith-first backend (.NET) with a microservices-ready design; PostgreSQL 16 + PostGIS for geo-dispatch
- **SignalR real-time** is core infrastructure — it powers on-demand dispatch and live booking/job status across the customer and field apps
- Support **500+ concurrent users** in MVP
- Multi-environment deployment: `dev` → `staging` → `prod`

### Mobile & Device Support

| Platform | Minimum version |
|----------|----------------|
| iOS | 14+ |
| Android | 8+ (API 26) |
| PWA | Modern mobile browsers |
| Biometric auth | Supported where available |

*(Offline mode is not implemented — deferred to post-MVP.)*

### Localisation

| Requirement | Detail |
|-------------|--------|
| Languages | Arabic (RTL) + English — **planned**; the doc will be updated as it firms up at launch |
| Currency | QAR primary; amounts formatted with commas |
| Timezone | Qatar Standard Time (UTC+3) |
| Weekend | Friday–Saturday pattern |
| Calendar | Islamic calendar for prayer times, Ramadan, Eid, National Day |

---

## Scope Evolution

!!! abstract "How the MVP changed from the Feb 2025 plan"
    The original *Ongo Feature List MVP v4\_S* (Feb 8, 2025, Doha) described a leaner, SMS-first product. During execution the scope evolved in three significant ways, all reflected above:

    1. **Dispatch:** *auto-assign the highest-rated vendor* → **on-demand geo-dispatch, first unit to accept** (auto-assign-highest-rated is now a post-MVP goal).
    2. **Authentication:** *phone OTP only, defer social login* → **social login (Google/Apple) is the primary, production-ready path**, with phone OTP pending go-live.
    3. **Infrastructure:** *avoid real-time infrastructure, minimise integrations* → the platform now runs **SignalR real-time** plus Firebase, Twilio, and Azure Blob to support the dispatch model.

    Several features were also **pulled back** during the build — vendor-side dispatch/accept, vendor self-serve financials & analytics (moved to Admin), field-unit earnings visibility, offline mode, and customer-facing vendor browsing. See the Out of Scope list for the full deferred set.

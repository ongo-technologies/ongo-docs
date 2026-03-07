---
title: Requirements
description: MVP feature requirements for CarWash Qatar — organized by platform
icon: material/clipboard-list-outline
---

# Requirements

!!! info "Document Info"
    Based on **CWS Feature List MVP v4\_S** — last revised February 8, 2025, Doha, Qatar.
    This document reflects the finalized MVP scope for all four CWS platforms.

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

### Optimization Principles

| Principle | Decision |
|-----------|----------|
| **Integrations** | Minimize costly third-party integrations |
| **Tracking** | SMS-based status updates instead of real-time GPS tracking |
| **Service areas** | Static radius for MVP; dynamic radius deferred |
| **Vendor app** | Vendor mobile app deferred to Phase II — web portal only |
| **Pricing** | Simple flat commission model; dynamic pricing deferred |
| **Reviews** | Star rating + pre-set options only; no free text in MVP |

!!! warning "Deferred to Post-MVP"
    - Real-time GPS tracking for on-road units
    - Vendor native mobile app (Phase II)
    - Live map monitoring of fleet
    - Dynamic service radius
    - In-app messaging / chat
    - Cash on delivery (COD)
    - Email / social login
    - Free-text reviews

---

## Service Packages

Two types of packages exist across the platform. All vendors **must** support Standard packages.

### Standard Service Packages (SSP)

Pre-set by Admin. Vendors toggle availability — they cannot change pricing.

| Package | Duration | Notes |
|---------|----------|-------|
| **Quick Wash** | ~30 min | Base tier |
| **Shine Wash** | ~60 min | Mid tier |
| **Detail Wash** | ~120 min | Premium tier |

### Custom Service Packages (CSP)

Created by vendors, approved by Admin before going live.

- Vendor sets name, description, pricing, duration
- Can indicate special requirements (power outlet, water source)
- Subject to admin approval per vendor
- Can include promotional pricing

---

## 1. Customer App — Flutter

### 1.1 Account Management

- Sign up via phone number (Qatar `+974`) with WhatsApp OTP — no email or social login in MVP
- Profile creation: name, email (optional), language preference
- Single saved address (home/work) with building, floor, apartment, street, additional directions
- Saved vehicles: type, colour, plate number, optional photo
- Order history

### 1.2 Booking Flow

Two distinct booking routes based on package type:

=== "Route I — Standard Packages"

    1. Customer selects geographical area
    2. Phone verification (OTP or WhatsApp)
    3. Profile details entered (name + agree to terms)
    4. Vehicle information added (type, saved name, optional photo)
    5. Select standard package — Quick / Shine / Detail wash with pre-set pricing
    6. Option to add vehicle photo before confirming
    7. Pin address on map + add address details
    8. Choose time: **Now** or **Schedule**
    9. Confirmation page shows all details + total price
    10. Auto-assigned vendor based on algorithm (see below)
    11. Confirmation page shows tracking status + estimated arrival
    12. Payment deducted

=== "Route II — Custom Packages"

    1. Customer views list of vendors
    2. Browse vendor services, pricing, descriptions
    3. Select custom package
    4. Add special requests / notes
    5. View estimated arrival time
    6. Confirm and pay

!!! info "Vendor Auto-Assignment Algorithm (Route I)"
    When a customer books a standard package, the system auto-assigns a vendor by prioritising:

    1. **Highly rated** vendors first
    2. **Available** (online / not busy) vendors
    3. **Within the same city** or within the vendor's defined static radius

### 1.3 Cancellation Policy

- Customer may cancel within **5 minutes** of booking confirmation at no charge
- After 5 minutes, standard cancellation policy applies

### 1.4 Location & Tracking

- Address pinning via map (no real-time GPS tracking in MVP)
- Status-based updates delivered via SMS at key moments:

| Trigger | Notification sent |
|---------|-------------------|
| Booking confirmed | Confirmation + vendor contact number |
| Vendor starts journey | "Your provider is on the way — arriving ~20 mins" |
| Vendor near location (~3 mins) | "Arriving soon" |
| Service started | "Service in progress — Est. 45 mins remaining" |
| Service complete | Completion confirmation + rating prompt |

!!! note "Predictive Tracking"
    Fixed estimates are used in MVP (20 min journey, 45 min service) rather than live GPS. This is a deliberate cost-saving decision — no real-time tracking infrastructure required.

### 1.5 Payments

| Method | Provider |
|--------|----------|
| Local debit/credit cards (Qatar) | SkipCash / MyFatoorah / QNB Payment Gateway |
| Visa / Mastercard | Same gateways |
| Google Pay | Same gateways |
| Apple Pay | Same gateways |

- **No COD (Cash on Delivery)** in MVP
- Customer consent required to store card data for future use
- Itemised receipts available in order history
- QAR is the primary currency display

### 1.6 Notifications

- Push notifications (Firebase) — customer must grant permission
- SMS for: booking confirmation, status updates, vendor contact number post-booking

### 1.7 Ratings & Reviews

- Post-service rating prompt (5-star)
- Pre-set compliment / complaint options — no free-text in MVP
- Filter vendors by highest rated
- All reviews are **moderated by Admin** before publishing (customers are not informed of moderation)

### 1.8 Support

- Emergency contact options within the app

---

## 2. Vendor Portal — Angular Web

### 2.1 Registration (Become a Partner)

- Business profile: valid email, phone number, trade name
- Online registration form with document uploads

!!! info "Required Registration Documents"
    Trade License · Commercial Registration · Trademark (if applicable) · Qatar ID ·
    Power of Attorney (if applicable) · Bank Certificate · Signed email declaration ·
    Proof of registration fee payment · Logo · Cover Photo

### 2.2 Service Management

- Toggle availability for each Standard Service Package (SSP) individually
- Add, manage, and price Custom Service Packages (CSP):
    - Service name, description, duration
    - Special requirements (power outlet, water source)
    - Pricing + optional promotional pricing
- CSPs require Admin approval before going live
- Set operating hours and availability settings
- Service area definition: choose from predefined location list **or** set a static radius

!!! note "Static Radius — MVP Scope"
    Dynamic radius (adjusting based on vehicle movement) is a post-MVP feature. For MVP, vendors define a fixed service area.

### 2.3 Booking Management

- Real-time dashboard notifications for new bookings (now and scheduled)
- Accept or decline incoming booking requests
- View daily, weekly, and monthly schedule
- Manage capacity across multiple on-road units simultaneously
- **Online / Offline toggle** — per service package menu item + overall vendor toggle
- **Busy status** — signals customers to expect longer wait times

### 2.4 Fleet / Unit Management

- Assign accepted bookings to specific on-road units (job cart with client info)
- Monitor service status of each unit in the field

### 2.5 Financial

- View payment gateway earnings through the dashboard
- Automated payment collection via gateway
- Transaction history
- Commission deductions visible per transaction

### 2.6 Analytics & Performance

- Analytics dashboard: bookings, earnings, commission deductions
- View customer ratings and reviews
- Filter by date range and booking type

### 2.7 User Management

- Update vendor admin profile details
- Add sub-users for each on-road unit (fleet accounts)

---

## 3. On-Road Unit App — Flutter

Accessed by on-road wash unit staff via a **Flutter mobile app**. Controlled by on-road supervisor.

!!! info "Platform Decision"
    Built with Flutter, consistent with the customer app codebase and allowing a native mobile experience for on-road teams.

### 3.1 Booking View

- Receive notification (SMS or email) when a booking is assigned by Vendor Admin
- View all details of the assigned job:
    - Customer name + contact number
    - Vehicle details (type, colour, plate)
    - Location + address details
    - Package selected + special requests/notes
    - Scheduled time

### 3.2 Status Updates

- Update booking status at key moments (drives the customer SMS notifications):
    - Journey started
    - Near location
    - Service started
    - Service completed

### 3.3 Service Quality Checklist

- Complete a quality checklist upon service completion
- Collect customer signature / approval at job completion

---

## 4. Admin Dashboard — Angular Web

### 4.1 User Management

- Manage and search customer accounts
- Approve, suspend, and manage vendor accounts
- Manage on-road unit accounts
- User roles and permissions
- Overview dashboard: real-time user stats — new users, total vendors, new vendor registrations
- Mass communication tools: push notifications to all users or segments

### 4.2 Service Management

- Define and manage Standard Service Package (SSP) categories for all vendors
- Review and approve Custom Service Packages (CSP) per vendor
- Set flat commission rates (applied to all vendors in MVP)
- Manage COD commission rate separately (applied in-dashboard, not via gateway)

!!! info "Commission on COD"
    For any future COD payments, the commission rate is shown as debited in the vendor admin account. Digital payment commissions are applied automatically by the payment gateway.

### 4.3 Booking Oversight

- View all current and historical bookings
- Resolve booking disputes
- Manage cancellations and refunds

### 4.4 Financial Management

- Overall revenue dashboard (platform-wide and per vendor)
- Commission tracking
- Approve vendor bank account information before payouts

### 4.5 Content Management

- Manage FAQs, Terms of Service, app copy
- Push notification management (manual broadcast)
- Approve vendor promotional campaigns (for CSPs only)

### 4.6 Analytics & Reporting

- Comprehensive analytics dashboard
- Filter by booking type, vendor, date range, geography
- Generate and export custom reports (usage, revenue, user acquisition)

### 4.7 App Configuration

- Manage app settings and feature parameters
- Feature toggles (where applicable)
- Manage third-party integrations (maps, payment gateways)

### 4.8 Quality Control

- Monitor vendor ratings and performance metrics
- **Moderate and approve customer reviews** before publishing
- Enforce service completion standards (via on-road unit checklist)

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

### Availability

| Metric | Target |
|--------|--------|
| Uptime (business hours 6 AM–11 PM QST) | 99.5% |
| Recovery time objective (RTO) | < 4 hours |
| Partial failure behaviour | Graceful degradation |

### Security

| Requirement | Standard |
|-------------|----------|
| Payment processing | PCI DSS compliant |
| Data at rest | AES-256 encryption |
| Data in transit | HTTPS / TLS 1.3 |
| Security reviews | Regular audits |
| Message / payment encryption | End-to-end |

### Scalability

- Support **500+ concurrent users** in MVP
- Monolith-first architecture with microservices-ready design
- Multi-environment deployment: `dev` → `staging` → `prod`

### Mobile & Device Support

| Platform | Minimum version |
|----------|----------------|
| iOS | 14+ |
| Android | 8+ (API 26) |
| PWA | Modern mobile browsers |
| Biometric auth | Supported where available |
| Offline | Cached data browsable offline |

### Localisation

| Requirement | Detail |
|-------------|--------|
| Languages | Arabic (RTL) + English — seamless toggle |
| Currency | QAR primary; amounts formatted with commas |
| Timezone | Qatar Standard Time (UTC+3) |
| Weekend | Friday–Saturday pattern |
| Calendar integration | Islamic calendar for prayer times, Ramadan, Eid, National Day |

---
title: Roadmap
description: Milestones and timeline for Ongo
icon: material/flag-outline
---

# Development Roadmap

## Philosophy

Phased delivery with continuous deployment and stakeholder validation. Each milestone builds on the last—infrastructure first, then features, then refinement, then launch.

## Milestones

### Milestone 1: Foundation & Initial Deployment
**Period**: December 2025 – February 2026 (Q4 2025 – Q1 2026)
**Status**: ✅ Completed

**Goal**: Establish core infrastructure, CI/CD, and initial working versions of all platforms

**Deliverables**:

- API development with database connectivity (Azure PostgreSQL)
- CI/CD pipeline setup (GitHub Actions + Terraform for infrastructure)
- Initial development of admin and vendor web apps (Angular)
- Initial development of customer mobile app (Flutter)
- Mobile app deployed to Google Play Store
- Web apps deployed to Azure

**Success Criteria**:

- All apps running in production environments
- CI/CD pipeline fully operational
- Deployment to both Play Store and Azure confirmed

---

### Milestone 2: API Integration & UI Redesign
**Period**: March – April 2026 (Q1–Q2 2026)
**Status**: ✅ Completed

**Goal**: Connect all platforms through core booking API endpoints and refresh the user experience

**Delivered**:

- API endpoints covering the core booking feature (customer, admin, vendor, service unit)
- MyFatoorah payment gateway integration (sandbox configuration and API setup)
- Initial development of the on-road service unit mobile application
- Initial implementation of the end-to-end booking flow with live API integration across all platforms

!!! warning "Carried over to Milestone 3"
    The following items were not completed within the milestone window and are carried forward:

    - CI/CD pipeline extended to deploy mobile app to Apple App Store
    - UI/UX redesign for mobile app (customer app + service unit app)
    - UI/UX redesign for web apps (vendor portal + admin dashboard)
    - WhatsApp OTP integration for customer authentication and verification

---

### Milestone 3: Cultural Integration & Core Features
**Period**: May – July 2026 (Q2 2026)
**Status**: 🔄 In Progress

**Goal**: Deliver a polished, Qatar-ready experience with full cultural adaptations, feature completeness, and official product launch readiness

**Deliverables**:

*Carried over from Milestone 2:*

- CI/CD pipeline extended to deploy mobile app to Apple App Store
- UI/UX redesign for mobile app (customer app + service unit app)
- UI/UX redesign for web apps (vendor portal + admin dashboard)
- WhatsApp OTP integration for customer authentication and verification

*New:*

- Arabic RTL support across all platforms
- Standard service packages (Quick Wash, Shine Wash, Detail Wash)
- Custom vendor packages with individual pricing
- Status-based service tracking with estimated arrival times
- In-app ratings and reviews (star rating + pre-set options)
- SMS notifications for all booking events
- Google Maps integration (service location pinning, vendor proximity, arrival tracking)
- Vendor onboarding flow (registration, document submission, profile setup)
- Landing page for public-facing onboarding (customer and vendor acquisition)
- Product migration to official brand name across all platforms (Ongo)

**Success Criteria**:

- Arabic interface fully functional with no critical layout issues
- Complete booking flow with vendor assignment working end-to-end
- iOS deployment pipeline operational
- Redesigned interfaces approved by stakeholders
- WhatsApp OTP verification flow operational in staging
- Google Maps integrated with live location on all relevant screens
- Vendor onboarding flow end-to-end in staging
- Landing page live and accessible
- All platform surfaces reflect the Ongo brand
- Internal satisfaction score >4.0/5.0

---

### Milestone 4: Payments & Vendor Operations
**Target**: Q2–Q3 2026

**Goal**: Enable real transactions and equip vendors with complete operational tools

**Deliverables**:

- Payment integration (SkipCash, MyFatoorah, QNB — local cards, Visa, Google/Apple Pay)
- Vendor earnings dashboard with commission tracking
- Fleet management (multi-unit assignment by vendor admin)
- Quality control checklist for service completion
- Admin financial dashboard and vendor approval workflows
- Enhanced security and audit logging

**Success Criteria**:

- Payment failure rate <1%
- Vendors can manage bookings, units, and earnings independently
- Security review passed

---

### Milestone 5: Beta Launch
**Target**: Q3 2026

**Goal**: Real-world validation with selected vendors and live customers

**Deliverables**:

- 5–10 vendors onboarded and trained
- Customer support system (Arabic + English)
- Live transaction monitoring and dispute resolution
- Feedback collection system
- Vendor training and onboarding materials
- Performance optimization for production load

**Success Criteria**:

- 50+ successful transactions completed
- Customer satisfaction >4.0/5.0
- Vendor satisfaction >4.0/5.0
- System stable under real load

---

## Timeline Overview

| Milestone | Period | Status |
|-----------|--------|--------|
| Foundation & Initial Deployment | Dec 2025 – Feb 2026 | ✅ Completed |
| API Integration & UI Redesign | Mar – Apr 2026 | ✅ Completed |
| Cultural Integration & Core Features | May – Jul 2026 | 🔄 In Progress |
| Payments & Vendor Operations | Q3 2026 | Planned |
| Beta Launch | Q3–Q4 2026 | Planned |

## Key Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Payment gateway complexity | High | Start sandbox early, engage local specialists |
| App Store review delays | Medium | Submit early, use TestFlight for internal testing |
| Arabic RTL complexity | Medium | Incremental implementation, UX review at each stage |
| Low vendor adoption | High | Reduced early commissions, strong onboarding support |

---
title: User Stories
description: Epic structure and user stories for CarWash Qatar
---

# User Stories

## Epic 1: Foundation

### 1.1 Project Setup
**As a developer**, I want a configured monorepo so that the team can begin development with consistent tooling.

**Acceptance Criteria**:

- Monorepo with Flutter app, Angular portals, ASP.NET Core API
- Azure PostgreSQL connected with Entity Framework
- Redis configured for sessions and caching
- GitHub Actions CI/CD pipeline
- Development setup documentation

### 1.2 Authentication
**As a user**, I want secure login so that I can access personalized features.

**Acceptance Criteria**:

- Phone registration with +974 country code
- SMS verification via Qatar gateway
- JWT authentication with refresh tokens
- Password reset via SMS
- Biometric login for returning users

### 1.3 Provider Discovery
**As a customer**, I want to find nearby providers so that I can see available services.

**Acceptance Criteria**:

- Google Maps integration with user location
- Provider listing with name, rating, distance, price
- Radius filtering (5km, 10km, 25km)
- Map/list view toggle
- Arabic RTL support

---

## Epic 2: Booking

### 2.1 Provider Details
**As a customer**, I want detailed provider information so that I can make informed decisions.

**Acceptance Criteria**:

- Business info, services, pricing, hours
- Photo gallery
- Customer reviews with filters
- Real-time availability calendar
- Save/favorite functionality

### 2.2 Scheduling
**As a customer**, I want to select appointment times that fit my schedule.

**Acceptance Criteria**:

- Calendar with 30-minute slots
- Prayer time avoidance
- Conflict detection with alternatives
- Service duration estimates
- Reschedule/cancel capability

### 2.3 Payment
**As a customer**, I want secure local payment options.

**Acceptance Criteria**:

- QNB and QIIB integration
- Apple Pay, Google Pay support
- PCI DSS compliant forms
- Instant receipt generation
- Saved payment methods

---

## Epic 3: Provider Tools

### 3.1 Registration
**As a provider**, I want to register my business so customers can discover me.

**Acceptance Criteria**:

- Business registration form
- Document upload (license, insurance)
- Service catalog setup
- Operating hours with prayer breaks
- Service area definition

### 3.2 Booking Management
**As a provider**, I want to manage bookings efficiently.

**Acceptance Criteria**:

- Booking dashboard with status indicators
- Calendar views (daily, weekly, monthly)
- Accept/reject with customer notification
- Schedule optimization suggestions
- Mobile-responsive design

---

## Epic 4: Trust & Quality

### 4.1 Reviews
**As a customer**, I want to rate services to help others decide.

**Acceptance Criteria**:

- 5-star rating with categories
- Text review with photo upload
- 24-hour edit window
- Provider response capability
- Cultural sensitivity filters

### 4.2 Verification
**As a customer**, I want to see provider credentials for trust.

**Acceptance Criteria**:

- License verification workflow
- Insurance validation
- Verification badges on profiles
- Premium provider designation
- Badge explanation system

---

## Epic 5: Operations

### 5.1 Admin Dashboard
**As an admin**, I want tools to manage platform operations.

**Acceptance Criteria**:

- Real-time platform metrics
- User search and management
- Provider approval workflow
- Content moderation tools
- Audit logging

### 5.2 Analytics
**As an operator**, I want performance insights for optimization.

**Acceptance Criteria**:

- System health monitoring
- User behavior analytics
- Business metrics dashboard
- Geographic usage analysis
- Alerting for critical issues

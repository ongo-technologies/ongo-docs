---
title: Roadmap
description: Milestones and timeline for CarWash Qatar
icon: material/road-variant
---

# Development Roadmap

## Philosophy

Phased approach with weekly milestone validation. Early testing, cultural adaptation, and stakeholder feedback integration.

## Milestones

### Milestone 1: MVP Foundation
**Target**: Q1 2026

**Goal**: Functional platform with basic booking capability

**Deliverables**:

- Monorepo setup (Flutter, Angular, ASP.NET Core)
- User authentication with SMS verification
- Basic provider discovery with map
- Core booking flow (no payments yet)
- Simple admin dashboard

**Success Criteria**:

- Team can run all apps locally
- Core flows work in dev environment
- CI/CD pipeline operational

---

### Milestone 2: Testing Deployment
**Target**: Q1 2026

**Goal**: Production-like environments for testing

**Deliverables**:

- Flutter app on Google Play (internal) and TestFlight
- Angular apps on Azure with SSL
- Performance monitoring (APM)
- Security scanning
- Cross-device testing framework

**Success Criteria**:

- All stakeholders can access and test
- <3s load times, 99.5% uptime
- >80% test coverage on critical paths

---

### Milestone 3: Cultural Integration
**Target**: Q2 2026

**Goal**: Refined UX with Qatar-specific features

**Deliverables**:

- Arabic RTL support
- Prayer time integration
- Advanced booking (custom packages, scheduling)
- In-app messaging
- Basic analytics dashboard

**Success Criteria**:

- Zero critical bugs in core flows
- Arabic interface fully functional
- Internal satisfaction >4.0/5.0

---

### Milestone 4: Feature Complete
**Target**: Q2 2026

**Goal**: All planned features for market readiness

**Deliverables**:

- Full payment integration (QNB, QIIB, cards)
- Rating and review system
- Enhanced security and audit logging
- Provider analytics tools
- Performance optimization

**Success Criteria**:

- Payment failure rate <1%
- Security pen test passed
- Supports 500+ concurrent users

---

### Milestone 5: Beta Testing
**Target**: Q3 2026

**Goal**: Real-world validation with selected providers

**Deliverables**:

- 5-10 providers onboarded
- Customer support system (Arabic + English)
- Real transaction monitoring
- Feedback collection system
- Provider training materials

**Success Criteria**:

- 50+ successful transactions
- Customer satisfaction >4.0/5.0
- Provider satisfaction >4.0/5.0
- System stable under real load

---

## Timeline Overview

| Milestone | Target | Status |
|-----------|--------|--------|
| MVP Foundation | Q1 2026 | Planned |
| Testing Deployment | Q1 2026 | Planned |
| Cultural Integration | Q2 2026 | Planned |
| Feature Complete | Q2 2026 | Planned |
| Beta Testing | Q3 2026 | Planned |

## Key Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Payment gateway complexity | High | Start sandbox early, engage local specialists |
| Flutter learning curve | Medium | Training in M1, pair programming |
| Arabic RTL complexity | Medium | Incremental implementation, UX consultant |
| Low provider adoption | High | Reduced early commissions, strong onboarding |

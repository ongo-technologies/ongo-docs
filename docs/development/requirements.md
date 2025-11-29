---
title: Requirements
description: Functional and non-functional requirements for CarWash Qatar
icon: material/clipboard-check-outline
---

# Requirements

## Functional Requirements

### FR1: Provider Discovery
- GPS-based search within 25km radius
- Real-time availability status
- Map and list view with filters (distance, rating, price)

### FR2: Booking System
- Calendar scheduling with 30-minute slots
- Transparent pricing before payment
- Prayer time conflict avoidance
- Booking conflict detection with alternatives

### FR3: Authentication
- Phone verification (+974) via SMS OTP
- Role-based access (customer, provider, admin)
- Session timeout after 30 minutes inactivity

### FR4: Provider Management
- Service listing and pricing management
- Booking dashboard with accept/decline
- Revenue tracking and payout management

### FR5: Ratings & Reviews
- 5-star rating with category breakdowns
- Photo upload capability
- Review moderation system
- Provider response functionality

### FR6: Payments
- QNB and QIIB integration
- International cards (Visa, Mastercard)
- Digital wallets (Apple Pay, Google Pay)
- QAR primary currency display

### FR7: Admin Tools
- User search and management
- Provider verification workflow
- Content moderation
- Platform metrics dashboard

### FR8: Notifications
- SMS for confirmations and reminders
- Push notifications via Firebase
- In-app notification center

### FR9: Localization
- Arabic RTL support
- English with seamless switching
- Culturally appropriate imagery

### FR10: Cultural Timing
- Prayer time integration (Islamic calendar)
- Friday-Saturday weekend recognition
- Ramadan schedule support
- Holiday awareness

---

## Non-Functional Requirements

### Performance

| Metric | Target |
|--------|--------|
| App launch time | <3 seconds |
| Page transitions | 60 FPS |
| Memory usage | <150MB |
| Booking confirmation | <2 seconds |
| Search response | <1 second |
| Payment confirmation | <5 seconds |

### Availability
- 99.5% uptime during business hours (6 AM - 11 PM Qatar)
- <4 hour recovery time objective
- Graceful degradation during partial failures

### Security
- PCI DSS for payment processing
- AES-256 encryption at rest
- HTTPS/TLS 1.3 for all traffic
- Regular security audits

### Scalability
- Support 500+ concurrent users
- Monolith-first with microservices-ready design
- Multi-environment deployment (dev, staging, prod)

### Mobile
- iOS 14+ and Android 8+ support
- Offline browsing for saved data
- PWA functionality for web
- Biometric authentication support

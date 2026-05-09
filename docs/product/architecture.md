---
title: Architecture
description: Technology stack and system design for Ongo
icon: material/layers-outline
---

# Technical Architecture

## Technology Stack

| Component | Technology | Rationale |
|-----------|------------|-----------|
| Customer App | Flutter | Cross-platform, single codebase |
| Backend API | ASP.NET Core | Team expertise, Azure integration |
| Database | Azure PostgreSQL | Scalability, geospatial support |
| Web Apps | Angular | Modern SPA, TypeScript |
| Service Unit | Flutter | Cross-platform, consistent with customer app |
| Cloud | Microsoft Azure | Qatar region, integrated ecosystem |
| CI/CD | GitHub Actions + Terraform | Automated pipelines, infrastructure as code |

## External Integrations

### Critical (MVP)

| Service | Provider | Purpose |
|---------|----------|---------|
| Maps | Google Maps API | Location pinning, service area definition |
| Payments | SkipCash, MyFatoorah, QNB | Local card processing, Visa, Google/Apple Pay |
| Messaging | WhatsApp OTP | User verification and OTP |
| Notifications | SMS + Firebase FCM | Booking confirmations, status updates, push alerts |

## Security

### Authentication
- JWT tokens with refresh mechanism
- WhatsApp OTP verification
- Role-based access control
- Session timeout after 30 minutes

### API Security
- Rate limiting
- DDoS protection
- Regular vulnerability assessments

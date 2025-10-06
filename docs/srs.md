# StudyMate - Software Requirements Specification

> A collaborative study application designed to improve focus and productivity through group study sessions.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Node.js](https://img.shields.io/badge/Node.js-v18+-green.svg)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-brightgreen.svg)](https://www.mongodb.com/cloud/atlas)

## Table of Contents

- [Introduction](#introduction)
  - [Purpose](#purpose)
  - [Scope](#scope)
  - [Terms & Abbreviations](#terms--abbreviations)
- [System Overview](#system-overview)
  - [System Context](#system-context)
  - [Major Capabilities](#major-capabilities)
  - [User Categories](#user-categories)
  - [System Limitations](#system-limitations)
  - [User Flow](#user-flow)
- [Technical Architecture](#technical-architecture)
  - [Technology Stack](#technology-stack)
  - [System Dependencies](#system-dependencies)
- [Requirements](#requirements)
  - [Functional Requirements](#functional-requirements)
  - [Non-Functional Requirements](#non-functional-requirements)
- [External Interfaces](#external-interfaces)
- [Testing & Quality Assurance](#testing--quality-assurance)
- [References](#references)
- [Contributors](#contributors)

---

## Introduction

### Purpose

This document specifies the requirements for **StudyMate**, a collaborative study application. It serves as a reference for developers, testers, designers, and stakeholders by defining functional, non-functional, and technical requirements to guide development and ensure alignment with project goals.

### Scope

StudyMate is a web and mobile-friendly platform designed to improve focus and productivity through group study. The application enables students to:

- **Join or create study rooms** (public or private via link/code)
- **Use a customizable Pomodoro timer** with synchronized intervals
- **Chat with peers** in real-time within study rooms
- **Receive reminders and notifications** for session transitions
- **Track progress** with daily and weekly reports

**Key Benefits:**
- Overcome student isolation through collaborative study
- Increase accountability with group sessions
- Foster structured study habits using the Pomodoro Technique

### Terms & Abbreviations

| Term | Definition |
|------|------------|
| **Pomodoro** | Productivity method with alternating focus/break periods |
| **UI** | User Interface |
| **API** | Application Programming Interface |
| **DB** | Database |
| **HTTPS** | Hypertext Transfer Protocol Secure |
| **TLS** | Transport Layer Security |
| **JWT** | JSON Web Token |
| **FR** | Functional Requirement |
| **NFR** | Non-Functional Requirement |

---

## System Overview

### System Context

StudyMate runs as a **cloud-based web service**, accessible via modern browsers and mobile devices. The application leverages real-time communication technologies to provide synchronized study experiences across multiple users.

### Major Capabilities

- ✅ **Secure Authentication** - Login and registration with JWT-based security
- 🏠 **Study Room Management** - Create/join public or private study rooms
- 💬 **Real-Time Chat** - Communicate with study partners within rooms
- ⏱️ **Synchronized Pomodoro Timer** - Customizable focus/break intervals synced across all room members
- 🔔 **Smart Notifications** - Session transition alerts and reminders
- 📊 **Analytics Dashboard** - Track study sessions with detailed statistics

### User Categories

#### Guest Users
- **Access Level:** Limited
- **Capabilities:** Browse app information
- **Restrictions:** Cannot join rooms or access core features

#### Registered Users
- **Access Level:** Full
- **Capabilities:** Create/join rooms, use timers, chat, track progress
- **Authentication:** Email/password with JWT

#### Administrators
- **Access Level:** Elevated
- **Capabilities:** User management, room moderation, platform monitoring
- **Responsibilities:** Maintain platform health and community standards

### System Limitations

⚠️ **Critical Limitations:**
- Requires **stable internet connection** for real-time features
- Real-time synchronization affected by network latency
- **Supported Browsers:** Latest versions of Chrome, Firefox, and Edge
- **Offline Use:** Limited to view-only mode for cached data

### User Flow

```
1. User opens StudyMate application
   ↓
2. Register new account / Login to existing account
   ↓
3. Choose study room option:
   ├── Create new room (public or private)
   └── Join existing room
       ├── Public: Browse room list
       └── Private: Enter invite code/link
   ↓
4. Configure Pomodoro timer settings
   - Set focus interval duration
   - Set break interval duration
   ↓
5. Timer synchronizes across all room members
   ↓
6. Study session begins
   - Real-time chat collaboration
   - Synchronized timer countdown
   ↓
7. Session ends → Progress automatically logged
   ↓
8. View statistics and reports dashboard
```

---

## Technical Architecture

### Technology Stack

#### Backend
- **Runtime:** Node.js
- **Framework:** Express.js
- **Architecture:** MVC (Model-View-Controller)

#### Database
- **Primary DB:** MongoDB Atlas (cloud-hosted)
- **Data Structure:** NoSQL document-based

#### Real-Time Communication
- **Library:** Socket.io
- **Features:** Chat messaging, timer synchronization
- **Protocol:** WebSocket over TLS

#### Authentication
- **Library:** Passport.js
- **Token Type:** JWT (JSON Web Tokens)
- **Password Security:** Bcrypt hashing with salting

#### Deployment
- **Containerization:** Docker
- **Scaling:** Horizontal scaling via container orchestration

#### Testing
- **Unit/Integration:** Jest
- **End-to-End:** Cypress
- **Coverage Target:** ≥85%

### System Dependencies

**Required Services:**
- Node.js runtime environment
- MongoDB Atlas connection
- WebSocket-enabled server infrastructure
- Docker runtime for containerization

**Network Requirements:**
- HTTPS/TLS 1.3 support
- WebSocket protocol support
- Stable internet connection

---

## Requirements

### Functional Requirements

#### User Authentication

| ID | Requirement | Priority |
|----|-------------|----------|
| **FR1** | Users can register with email and password | High |
| **FR2** | Users can login securely using JWT authentication | High |
| **FR3** | Passwords must be stored with hashing and salting | Critical |

#### Room Management

| ID | Requirement | Priority |
|----|-------------|----------|
| **FR4** | Users can create public or private study rooms | High |
| **FR5** | System generates unique link/code for private rooms | High |
| **FR6** | Users can join rooms via list (public) or code (private) | High |
| **FR7** | Room creator can remove inactive users | Medium |

#### Pomodoro Timer

| ID | Requirement | Priority |
|----|-------------|----------|
| **FR8** | Users can customize focus and break intervals | High |
| **FR9** | Timer synchronizes across all room members | Critical |
| **FR10** | Users receive notifications at start/end of sessions | Medium |

#### Chat System

| ID | Requirement | Priority |
|----|-------------|----------|
| **FR11** | Real-time messaging within study rooms | High |
| **FR12** | Messages are restricted to specific rooms | High |
| **FR13** | System persists chat history for active sessions | Medium |

#### Progress Tracking

| ID | Requirement | Priority |
|----|-------------|----------|
| **FR14** | System logs completed Pomodoro sessions | High |
| **FR15** | Dashboard displays daily/weekly statistics | Medium |
| **FR16** | Counters reset daily at midnight | Low |

#### Notifications

| ID | Requirement | Priority |
|----|-------------|----------|
| **FR17** | System provides visual and audio alerts | Medium |
| **FR18** | Users can enable/disable notifications in settings | Low |

### Non-Functional Requirements

#### Performance

| ID | Requirement | Target |
|----|-------------|--------|
| **NFR1** | Support concurrent users | 10,000+ |
| **NFR2** | Timer synchronization delay | <1 second |

#### Security

| ID | Requirement | Standard |
|----|-------------|----------|
| **NFR3** | All communication encrypted | TLS 1.3 |
| **NFR4** | Password hashing algorithm | Bcrypt |
| **NFR5** | JWT token expiration | 24 hours |

#### Availability

| ID | Requirement | Target |
|----|-------------|--------|
| **NFR6** | System uptime | 99.5% |
| **NFR7** | Auto-recovery time | <5 minutes |

#### Scalability

| ID | Requirement | Implementation |
|----|-------------|----------------|
| **NFR8** | Horizontal scaling capability | Docker containers |

#### Usability

| ID | Requirement | Standard |
|----|-------------|----------|
| **NFR9** | Interface design | Intuitive, minimal learning curve |
| **NFR10** | Accessibility compliance | WCAG 2.1 AA |

#### Maintainability

| ID | Requirement | Target |
|----|-------------|--------|
| **NFR11** | Code architecture | Modular MVC pattern |
| **NFR12** | Automated test coverage | ≥85% |

---

## External Interfaces

### User Interface
- **Design Philosophy:** Minimalist, responsive
- **Accessibility:** WCAG 2.1 compliant (Level AA)
- **Responsiveness:** Mobile-first design approach
- **Browser Support:** Modern browsers (Chrome, Firefox, Edge)

### Hardware Interface
- **Requirements:** Any internet-enabled device
- **Compatibility:** Desktop, tablet, and mobile devices
- **Input Methods:** Touch and keyboard/mouse support

### Software Interface
- **Database:** MongoDB Atlas (NoSQL)
- **Real-Time:** Socket.io WebSocket connections
- **API:** RESTful endpoints for HTTP requests

### Communication Protocols
- **HTTP:** HTTPS for secure REST API requests
- **WebSocket:** TLS-encrypted for real-time features
- **Standards:** IETF RFC 6455 (WebSocket Protocol)

---

## Testing & Quality Assurance

### Testing Strategy

#### Unit Testing
- **Framework:** Jest
- **Modules Tested:**
  - Authentication logic
  - Timer functionality
  - Room management
  - User operations

#### Integration Testing
- **Scope:** API ↔ Database validation
- **Framework:** Jest with MongoDB integration
- **Focus Areas:**
  - Data persistence
  - API endpoint responses
  - Service layer interactions

#### End-to-End Testing
- **Framework:** Cypress
- **User Flows Tested:**
  - Complete authentication flow
  - Room creation and joining
  - Pomodoro timer sessions
  - Chat functionality
  - Statistics dashboard

#### Performance Testing
- **Tools:** Lighthouse, custom load testing
- **Metrics:**
  - Concurrent user capacity
  - Response time under load
  - Resource utilization

#### Accessibility Testing
- **Standard:** WCAG 2.1 Level AA
- **Tools:** Lighthouse accessibility audits
- **Focus:** Keyboard navigation, screen reader compatibility

### Quality Metrics

- **Code Coverage:** Minimum 85%
- **Performance Score:** Lighthouse score ≥90
- **Accessibility Score:** WCAG 2.1 AA compliance
- **Security:** OWASP Top 10 compliance

---

## References

- Cirillo, F. (2006). *The Pomodoro Technique*
- [Node.js Documentation](https://nodejs.org/docs/)
- [Express.js Documentation](https://expressjs.com/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Socket.io Documentation](https://socket.io/docs/)
- [Cypress Documentation](https://docs.cypress.io/)
- [OWASP Top 10 (2023)](https://owasp.org/www-project-top-ten/)
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [IETF RFC 6455 – WebSocket Protocol](https://tools.ietf.org/html/rfc6455)

---

## Contributors

This project was developed collaboratively by:

| Name | Contributions |
|------|---------------|
| **Mehakpreet Singh** | Drafted introduction, system overview, and timer/room requirements |
| **Bisheshwar Das (Biku)** | Defined authentication, chat, and customizable timer requirements; integrated Cypress testing |
| **Anusha** | Authored non-functional requirements and outlined system limitations |

---

## License

This project is part of an academic assignment. Please refer to your institution's policies regarding code sharing and usage.

---

**Last Updated:** October 2025  
**Document Version:** 1.0

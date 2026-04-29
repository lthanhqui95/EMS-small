Skylight EMS Clone — Active Development Save Point
Persistent Working Context for New Chats / Codex / Project Continuity

🎯 PROJECT IDENTITY
Project Name:
Skylight EMS Clone

Project Type:
Senior Mini Production-Style Element Management System (EMS)

Inspired By:
* Accedian Skylight
* Cisco Provider Connectivity Assurance

🧠 CORE DOMAIN TRUTH (LOCKED)
EMS means:
✅ Element Management System
NOT Energy Management System

System Purpose:
A platform for managing and monitoring network elements through:
Locked Functional Scope:
* Device Inventory
* Telemetry Ingestion
* Performance Monitoring
* Fault / Event Management
* Configuration Tracking
* SLA Monitoring
* EMS Dashboard

🏗️ ARCHITECTURE (LOCKED)
System Style:
✅ Modular Monolith

NOT:
❌ Microservices
❌ Kubernetes-first
❌ Over-engineered distributed system

Core Flow:

Device Simulator
     ↓
Device Registration
     ↓
Telemetry Ingestion API
     ↓
Queue / Processing
     ↓
Rule Engine
     ↓
PostgreSQL
     ↓
Analytics API
     ↓
EMS Dashboard


⚙️ TECH STACK (LOCKED)
Backend:
* Java 17
* Spring Boot 3.x
* Spring Security
* Spring Validation
* Spring Data JPA
* Spring Actuator

Database:
* PostgreSQL
* Flyway

Tooling:
* Maven Wrapper
* Docker
* Docker Compose
* Swagger / OpenAPI

📂 PACKAGE STRUCTURE (LOCKED)

com.skylight.ems
 ├── common
 ├── auth
 ├── inventory
 ├── telemetry
 ├── processing
 ├── alerting
 ├── config
 ├── analytics
 └── infrastructure


📄 SOURCE OF TRUTH FILES (LOCKED)
Repository Documents:
REQUIRED:
* README.md
* PROJECT_CONTEXT.md
* ARCHITECTURE.md
* SESSION_CONTEXT.md

File Roles:
README.md:
Public project overview
PROJECT_CONTEXT.md:
System scope + build blueprint
ARCHITECTURE.md:
Technical architecture
SESSION_CONTEXT.md:
Current active save state

🎯 CURRENT DEVELOPMENT STATUS
Current Phase:
Phase 0 — Blueprint & Architecture

Completed:
✔️ README.md
✔️ PROJECT_CONTEXT.md
✔️ ARCHITECTURE.md
✔️ SESSION_CONTEXT.md

Next Exact Step:
🚀 Phase 1 — Foundation Setup

Phase 1 Goals:
Step 1:
Spring Initializr project generation
Step 2:
Base package structure
Step 3:
Docker Compose (PostgreSQL)
Step 4:
Flyway baseline migration
Step 5:
Health check + Actuator

🧱 ENGINEERING STANDARDS (LOCKED)
Mandatory:
Architecture:
* Controller
* Application Service
* Domain Logic
* Repository Interface
* Infrastructure

Validation:
* DTO boundaries
* Bean Validation

Security:
* ROLE_ADMIN
* ROLE_OPERATOR

Reliability:
* Queue decoupling
* Structured logging
* Health checks

Testing:
* Unit
* Integration
* API

🚨 NON-NEGOTIABLE RULES
Rule 1:
Business logic NEVER inside controller.

Rule 2:
Telemetry input is always untrusted.

Rule 3:
Build production-correct, not enterprise-large.

Rule 4:
No scope drift without explicit decision.

Rule 5:
Project demonstrates senior system thinking, not CRUD.

📊 MVP DATA MODELS (LOCKED)
Core Tables:
device
metric
event
config_history
sla_rule
user

USER ROLES (LOCKED)
ROLE_ADMIN:
* Register device
* Manage config
* Manage thresholds

ROLE_OPERATOR:
* Monitor
* View alerts
* View analytics

❌ OUT OF SCOPE (LOCKED)
* Kafka cluster
* Kubernetes
* SNMP enterprise implementation
* AI/ML anomaly engine
* Full telecom topology engine

🧠 PROJECT THESIS
Build a realistic mini EMS platform that proves backend architecture, observability, operational design, and production engineering maturity.

🔥 ELEVATOR PITCH
“Skylight EMS Clone is a senior-style mini Element Management System inspired by Cisco/Accedian, designed to manage network devices, telemetry, events, configurations, and SLA through a modular production-grade architecture.”

📌 WHEN STARTING A NEW CHAT:
Paste this:

Use Skylight EMS Clone context:
- EMS = Element Management System
- Modular Monolith
- Java 17 + Spring Boot 3.x
- Source of truth:
  - PROJECT_CONTEXT.md
  - ARCHITECTURE.md
  - SESSION_CONTEXT.md
Current Phase:
- Phase 0 complete
Next:
- Phase 1 Foundation Setup
Rule:
- No scope drift
- Senior production-style only


🎯 FINAL SAVE POINT
You are here:
Blueprint locked
Architecture locked
Scope locked
NEXT:
Phase 1 — Build Foundation Properly

🧠 ONE-LINE TRUTH
“Small EMS. Senior architecture. Zero drift.”

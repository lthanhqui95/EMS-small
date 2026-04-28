Skylight EMS Clone — Senior Mini Production Blueprint
Source of Truth for System Scope, Architecture, and Engineering Standards

🎯 1. PROJECT IDENTITY
Project Name:
Skylight EMS Clone

Project Type:
Senior-level mini Element Management System (EMS) inspired by:
* Accedian Skylight
* Cisco Provider Connectivity Assurance

Core Objective:
Build a production-style EMS platform that manages:
Functional Domains:
* Device Inventory
* Telemetry Ingestion
* Performance Monitoring
* Fault / Event Management
* Configuration Tracking
* SLA Monitoring
* Operational Dashboard

🧠 2. DOMAIN DEFINITION (NON-NEGOTIABLE)
This project IS:
✅ EMS (Element Management System)
A system for managing and monitoring network elements operationally.

This project is NOT:
❌ Simple CRUD app
❌ Generic network dashboard only
❌ Full telecom-grade distributed platform

🏗️ 3. SYSTEM VISION

Device Simulator
     ↓
Device Registration
     ↓
Telemetry Ingestion API
     ↓
Queue / Processing Engine
     ↓
Rule Engine
     ↓
Inventory + Metrics + Events + Config DB
     ↓
Analytics API
     ↓
EMS Dashboard


📦 4. DOMAIN MODULE BOUNDARIES
🔹 MODULE A — DEVICE INVENTORY
Responsibility:
Manage lifecycle of network elements.
Includes:
* Register device
* Update device status
* Firmware tracking
* Region assignment
* Device ownership

Entity:
Device

device_id
hostname
ip_address
device_type
vendor
firmware_version
region
status
created_at
updated_at


🔹 MODULE B — TELEMETRY INGESTION
Responsibility:
Receive operational metrics from simulated devices.
Input:
* CPU
* Memory
* Latency
* Packet Loss
* Jitter

Rules:
* Validate all input
* Reject malformed metrics
* Queue accepted metrics
* Preserve ingestion logs

🔹 MODULE C — PROCESSING ENGINE
Responsibility:
Asynchronous metric processing.
Includes:
* SLA checks
* Threshold evaluation
* Rule matching
* Severity assignment

Example:

latency > threshold → WARNING
packet_loss > threshold → CRITICAL
device offline → CRITICAL


🔹 MODULE D — EVENT / ALERT MANAGEMENT
Responsibility:
Operational event history.

Event Types:
* DEVICE_OFFLINE
* HIGH_CPU
* HIGH_MEMORY
* HIGH_LATENCY
* PACKET_LOSS
* CONFIG_CHANGED

Entity:

event_id
device_id
severity
event_type
message
occurred_at
resolved_at


🔹 MODULE E — CONFIGURATION MANAGEMENT
Responsibility:
Track configuration state and changes.

Includes:
* Current config snapshot
* Config versioning
* Audit history

Entity:

config_id
device_id
config_version
config_payload
updated_by
updated_at


🔹 MODULE F — ANALYTICS
Responsibility:
Operational visibility APIs.

Required:
Summary:
* Avg latency
* Avg packet loss
* Active alerts
* Device health ratio
Drill-down:
* Device metrics history
* Event history
* SLA violation trends

🔹 MODULE G — USER & ACCESS CONTROL
Roles:
ROLE_ADMIN:
* Register device
* Change config
* Manage thresholds
ROLE_OPERATOR:
* View dashboard
* Monitor devices
* View alerts

🗄️ 5. DATABASE STANDARD
Primary DB:
PostgreSQL

Migration:
Flyway REQUIRED

Required Tables:
device
metric
event
config_history
sla_rule
user

Time-Series Priority:
All metrics must be queryable by:
device_id + timestamp

🌐 6. API CONTRACTS (MINIMUM REQUIRED)
DEVICE

POST   /api/devices
GET    /api/devices
GET    /api/devices/{id}
PATCH  /api/devices/{id}/status


TELEMETRY

POST   /api/metrics
GET    /api/metrics/timeseries
GET    /api/metrics/summary


EVENTS

GET    /api/events
GET    /api/events/{id}
PATCH  /api/events/{id}/resolve


CONFIG

POST   /api/configs/{deviceId}
GET    /api/configs/{deviceId}/history


AUTH

POST   /api/auth/login


🧱 7. ENGINEERING STANDARDS (MANDATORY)
Architecture:
REQUIRED:
* Controller
* Application Service
* Domain Model
* Repository Interface
* Infrastructure Layer

Validation:
REQUIRED:
* DTO separation
* Bean Validation
* Request/Response boundaries

Logging:
REQUIRED:
* requestId
* deviceId
* severity
* processing time

Observability:
REQUIRED:
* Spring Boot Actuator
* Health endpoint
* Metrics endpoint

Error Strategy:
REQUIRED:
* Global exception handler
* Typed exceptions

Testing:
REQUIRED:
* Unit tests
* Integration tests
* API tests

Security:
REQUIRED:
* Spring Security
* Role-based access
* Basic token/API key acceptable

📂 8. REPOSITORY STRUCTURE (MANDATORY)

ems-skylight-clone/
 ├── README.md
 ├── PROJECT_CONTEXT.md
 ├── ARCHITECTURE.md
 ├── docker-compose.yml
 ├── backend/
 │    ├── src/main/java/com/skylight/ems/
 │    │    ├── inventory/
 │    │    ├── telemetry/
 │    │    ├── processing/
 │    │    ├── alerting/
 │    │    ├── config/
 │    │    ├── auth/
 │    │    └── common/
 │    └── src/test/
 ├── probe-simulator/
 ├── frontend/
 └── docs/


🚨 9. OUT OF SCOPE (DO NOT BUILD)
Explicitly excluded:
* Kubernetes
* Kafka cluster
* SNMP enterprise implementation
* AI/ML anomaly prediction
* Microservice deployment complexity
* Distributed tracing platforms

🎯 10. SENIOR SIGNAL REQUIREMENTS
To qualify as “senior mini production project,” system MUST demonstrate:
Reliability:
* Health checks
* Graceful failure
* Queue decoupling

Maintainability:
* Configurable SLA rules
* Modular domain boundaries
* Flyway migrations

Observability:
* Structured logging
* Event history
* Alert lifecycle

Product Thinking:
* Device lifecycle
* Fault domain
* Config auditability

📊 11. DASHBOARD MVP REQUIREMENTS
Main Dashboard:
Fleet:
* Total devices
* Online/offline
* Active alerts

Device Detail:
* Health
* Metrics chart
* Config history
* Event timeline

Alerts:
* Severity
* Status
* Resolve action

🧠 12. DEVELOPMENT PHASES (LOCKED)
Phase 0 — Blueprint
Goal:
* Scope
* DB
* API
* Structure

Phase 1 — Foundation
Goal:
* Spring Boot
* Security
* Flyway
* Device Inventory

Phase 2 — Telemetry
Goal:
* Probe simulator
* Metrics ingestion
* Queue

Phase 3 — Operations
Goal:
* Rule engine
* Alerts
* SLA

Phase 4 — Dashboard
Goal:
* UI
* Analytics
* Drill-down

📌 13. GOLDEN RULES
Rule 1:
Business logic NEVER inside controller.

Rule 2:
All telemetry is untrusted input.

Rule 3:
EMS = Operational control system, not dashboard only.

Rule 4:
Build small, architect correctly.

🚀 14. FINAL PROJECT THESIS
This project exists to demonstrate senior backend + EMS operational architecture through a realistic but manageable clone of enterprise EMS concepts.

🔥 ONE-LINE TRUTH
“Build a small EMS. Think like Cisco.”

Skylight EMS Clone — System Architecture Blueprint
Technical Design Reference for Production-Style Mini EMS

🎯 1. ARCHITECTURAL PURPOSE
This document defines the technical architecture of the Skylight EMS Clone.

Primary Goal:
Design a small but production-correct EMS (Element Management System) that demonstrates:
Engineering Focus:
* Operational system design
* EMS domain separation
* Reliability
* Observability
* Extensibility
* Maintainability

🧠 2. HIGH-LEVEL SYSTEM MODEL
EMS Core Philosophy:
Manage devices + ingest telemetry + process operational signals + detect faults + track config + expose analytics

🌐 SYSTEM FLOW

┌─────────────────────┐
│   Device Simulator   │
│ (Probe / Router Mock)│
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│ Device Registration  │
│ & Inventory Service  │
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│ Telemetry Ingestion  │
│ REST API Layer       │
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│ Internal Queue       │
│ (Decoupling Layer)   │
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│ Processing Engine    │
│ SLA / Rules / Events │
└─────────┬───────────┘
          │
          ▼
┌─────────────────────────────────────┐
│ PostgreSQL                          │
│ Devices / Metrics / Events / Config │
└─────────┬───────────────────────────┘
          │
          ▼
┌─────────────────────┐
│ Analytics API        │
│ Summary / Drilldown  │
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│ EMS Dashboard        │
│ Ops Control Center   │
└─────────────────────┘


🏗️ 3. ARCHITECTURE STYLE
Core Style:
Layered Modular Monolith

Why?
Chosen because:
✅ Senior enough for production logic
✅ Easier than microservices
✅ Strong domain separation
✅ Easier local development
✅ Better portfolio clarity

❌ Explicitly NOT:
* Distributed microservices
* Full event bus infra
* Telecom-scale cluster

📦 4. CORE ARCHITECTURAL DOMAINS

🔹 A. INVENTORY DOMAIN
Purpose:
Source of truth for managed devices.

Responsibilities:
* Register devices
* Device lifecycle
* Firmware tracking
* Region ownership
* Status state

State:

ONLINE
OFFLINE
DEGRADED
MAINTENANCE
UNKNOWN



🔹 B. TELEMETRY DOMAIN
Purpose:
Receive operational metrics.

Data Types:
Required:
* CPU
* Memory
* Latency
* Packet Loss
* Jitter

Key Rule:
Ingestion MUST remain lightweight.
No heavy business logic here.

Pipeline:

Validate → Accept → Queue



🔹 C. PROCESSING DOMAIN
Purpose:
Operational intelligence layer.

Responsibilities:
* Threshold checks
* SLA validation
* Event generation
* Severity classification

Severity:

INFO
WARNING
CRITICAL


Processing Principle:
Ingestion and rule evaluation are separated.


🔹 D. CONFIGURATION DOMAIN
Purpose:
Track operational changes.

Responsibilities:
* Config snapshots
* Version history
* Change audit

Design Principle:
Config is operational truth.
Every change must be attributable.


🔹 E. ALERT DOMAIN
Purpose:
Fault/event lifecycle.

Lifecycle:

OPEN → ACKNOWLEDGED → RESOLVED


Rule:
Events are immutable history; status changes are tracked separately.


🔹 F. ANALYTICS DOMAIN
Purpose:
Operational visibility.

Functions:
Summary:
* Fleet health
* Avg latency
* SLA breach count
Drill-down:
* Device metrics
* Event timelines
* Config changes

🗄️ 5. DATA ARCHITECTURE
Primary DB:
PostgreSQL

Core Tables:

device
metric
event
event_status_history
config_history
sla_rule
user


RELATIONSHIPS:

device 1:N metric
device 1:N event
device 1:N config_history
event 1:N event_status_history


Index Priorities:
High Priority:

metric(device_id, timestamp)
event(device_id, occurred_at)
device(status)


🔥 Data Principle:
Optimize for operational query paths, not generic CRUD.

⚙️ 6. APPLICATION LAYER ARCHITECTURE
Standard Flow:

Controller
   ↓
Application Service
   ↓
Domain Service / Rules
   ↓
Repository Interface
   ↓
Infrastructure


RULE:
Controllers are transport only.
No business logic.

Example:

POST /metrics
→ MetricController
→ MetricIngestionService
→ Validation
→ QueuePublisher


🌐 7. API DESIGN PRINCIPLES
Standard:
RESTful + operationally meaningful

Example:
Good:

PATCH /api/events/{id}/resolve

Bad:

/doResolveEvent


Required Standards:
MUST:
* Versionable
* DTO separated
* Validation
* Typed responses

🔐 8. SECURITY ARCHITECTURE
MVP Security:
Authentication:
* JWT or API Token

Authorization:
* ROLE_ADMIN
* ROLE_OPERATOR

Security Boundaries:
* External telemetry input
* Internal operational actions

Security Rule:
Telemetry endpoints may use API key/device token.

📊 9. OBSERVABILITY ARCHITECTURE
REQUIRED:
Logging:
* requestId
* deviceId
* correlationId
* severity

Metrics:
* ingestion rate
* processing latency
* queue depth
* alert count

Health:

/actuator/health
/actuator/metrics


Principle:
The EMS itself must be observable.

🧪 10. TEST ARCHITECTURE
REQUIRED TEST LAYERS:
Unit:
* Rule engine
* SLA logic

Integration:
* Repository
* DB

API:
* Device registration
* Metric ingestion
* Alert resolution

Goal:
Business correctness + infrastructure confidence

🚀 11. DEPLOYMENT MODEL
MVP:
Docker Compose

Services:

backend
postgres
frontend
probe-simulator


Future-ready:
Can split later into services if needed.

❌ NOT REQUIRED:
* Kubernetes
* Service mesh
* Kafka cluster

🧭 12. FAILURE STRATEGY
Key Failure Cases:
A. Device sends invalid telemetry
Response:
Reject + log

B. Queue overloaded
Response:
Backpressure / bounded queue

C. DB unavailable
Response:
Health degraded

D. Rule engine failure
Response:
Metric preserved, event flagged

Principle:
Never silently fail.

📂 13. PACKAGE DESIGN

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


Rule:
Package by domain, not by technical layer only.

🧠 14. ENGINEERING TRADEOFFS
Chosen:
Modular Monolith

Sacrificed:
Less distributed realism

Gained:
Faster development
Cleaner understanding
Better interview explainability

🎯 15. ARCHITECTURAL SUCCESS CRITERIA
System is considered successful if:
Functional:
✔️ Devices manageable
✔️ Metrics ingested
✔️ Rules processed
✔️ Alerts generated
✔️ Config tracked

Engineering:
✔️ Clean architecture
✔️ Observability
✔️ Reliability
✔️ Security
✔️ Maintainability

🔥 FINAL ARCHITECTURAL TRUTH
This project is not a “device dashboard.”
It is a mini operational EMS platform designed to demonstrate production-grade backend and system architecture thinking.

📌 ONE-LINE SUMMARY
“Small system. Real EMS architecture.”

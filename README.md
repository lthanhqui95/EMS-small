# Skylight EMS-small

A production-style Element Management System (EMS) inspired by Accedian Skylight / Cisco Provider Connectivity Assurance.  
This project simulates how enterprise EMS platforms manage network devices, telemetry, alerts, configuration, and SLA monitoring in a simplified but architecturally correct way.

---

## 🎯 Project Purpose
This is not a simple CRUD dashboard.  
This project is designed to demonstrate:

- Production-style backend architecture
- EMS (Element Management System) domain understanding
- Device inventory + telemetry + event management
- Operational monitoring mindset
- SLA / alerting pipeline
- Senior-level Java + Spring Boot engineering practices

---

## 🧠 What is EMS?
EMS (Element Management System) is a control platform used to manage and monitor network elements such as:

- Routers
- Switches
- Probes
- Sensors
- Gateways

It combines:

### Core EMS Domains:

- **Inventory Management** – Track devices and lifecycle
- **Telemetry Monitoring** – Latency, packet loss, CPU, memory
- **Fault Management** – Device down, SLA violations, anomalies
- **Configuration Management** – Firmware, config history, audit trail
- **Alerting System** – Warning / Critical events
- **Analytics Dashboard** – Operational visibility

---

## 🏗️ System Architecture

```text
Device Simulator
     ↓
Device Registration Service
     ↓
Telemetry Ingestion API
     ↓
Internal Queue / Processing Engine
     ↓
Alert & Rule Engine
     ↓
PostgreSQL
     ↓
Analytics API
     ↓
EMS Dashboard
```

---

## 📦 Core Modules

### 1. Device Simulator
Simulates enterprise devices sending telemetry.

**Sample Metrics:**
- CPU
- Memory
- Latency
- Packet Loss
- Jitter

### 2. Device Inventory Service
Manages:
- Device registration
- Status
- Region
- Vendor
- Firmware

### 3. Telemetry Ingestion
Receives metrics through REST API.

**Responsibilities:**
- Validation
- DTO mapping
- Queueing
- Logging

### 4. Processing Engine
Processes telemetry asynchronously.

**Features:**
- Threshold rules
- SLA checks
- Anomaly detection
- Event creation

### 5. Alert Management
Generates:
- INFO
- WARNING
- CRITICAL

### 6. Configuration Tracking
Stores:
- Config versions
- Change history
- Audit trail

### 7. Dashboard
Provides:
- Fleet health overview
- Device table
- Alert feed
- SLA metrics
- Topology-style visibility

---

## 🗄️ Database Design

### Main Tables:

#### `device`
| Column | Description |
|---|---|
| device_id | Device identifier |
| hostname | Device hostname |
| ip_address | Device IP address |
| type | Device type |
| vendor | Device vendor |
| firmware_version | Firmware version |
| region | Region |
| status | Device status |
| created_at | Created timestamp |

#### `metric`
| Column | Description |
|---|---|
| metric_id | Metric identifier |
| device_id | Linked device |
| cpu | CPU usage |
| memory | Memory usage |
| latency | Latency |
| packet_loss | Packet loss |
| jitter | Jitter |
| timestamp | Metric timestamp |

#### `event`
| Column | Description |
|---|---|
| event_id | Event identifier |
| device_id | Linked device |
| severity | Event severity |
| event_type | Event type |
| message | Event message |
| occurred_at | Occurred timestamp |

#### `config_history`
| Column | Description |
|---|---|
| config_id | Config identifier |
| device_id | Linked device |
| config_version | Config version |
| config_payload | Config payload |
| updated_by | Updated by |
| updated_at | Updated timestamp |

---

## 🔐 User Roles

### ROLE_ADMIN
- Register devices
- Update configurations
- Manage thresholds

### ROLE_OPERATOR
- Monitor devices
- View alerts
- View SLA dashboards

---

## ⚙️ Tech Stack

### Backend
- Java 17
- Spring Boot 3.x
- Spring Security
- Spring Validation
- Spring Actuator
- Spring Data JPA

### Database
- PostgreSQL
- Flyway

### Testing
- JUnit 5
- Mockito
- Integration Tests

### DevOps
- Docker
- Docker Compose
- Swagger / OpenAPI

---

## 📊 Senior Engineering Standards

This project intentionally includes:

### Architecture
- Layered design
- Domain separation
- DTO boundaries
- Global exception handling

### Reliability
- Health checks
- Structured logging
- Async queue processing
- Rule engine

### Maintainability
- Config-driven thresholds
- Migration scripts
- Swagger docs
- Modular package design

---

## 🚀 Project Scope

### Included
- Device inventory
- Telemetry ingestion
- Event processing
- Alert engine
- SLA monitoring
- Config tracking
- Dashboard backend

### Excluded (intentionally)
- Full SNMP implementation
- Distributed Kafka cluster
- Kubernetes
- AI/ML analytics
- Multi-region infrastructure

---

## 🧪 Example Use Case

### Scenario
A simulated router in Singapore reports:
- CPU: 94%
- Latency: 180ms
- Packet Loss: 4%

### EMS Response
- Telemetry accepted
- Rule engine detects SLA breach
- Critical event created
- Alert visible on dashboard

---

## 📈 Learning Outcomes

By building this project, the developer demonstrates:
- EMS / NOC system understanding
- Event-driven backend design
- Production-style observability
- Operational support thinking
- Enterprise Java architecture

---

## 🛠️ Local Development (Planned)

```bash
./mvnw spring-boot:run
docker-compose up -d
```

---

## 📚 Future Extensions
- SNMP adapter
- Topology visualization
- Real device integration
- Notification channels (Email/Slack)
- Historical SLA reporting

---

## 🎯 Elevator Pitch

> “A senior-style mini EMS platform inspired by Accedian Skylight / Cisco, focused on device lifecycle management, telemetry ingestion, fault management, SLA monitoring, and operational visibility.”

---

## 📌 Key Philosophy
Build small. Think production.  
This repository is intentionally scoped to remain manageable while preserving:

### Senior Signals
- Architecture
- Reliability
- Observability
- Domain correctness

---

## 👤 Ideal Audience
This project is suitable for:
- Java Backend Engineers
- Application Support Engineers
- NOC / EMS domain learners
- System Design portfolio builders
- IT Operations candidates

---

## 📄 License
MIT (or your preferred license)

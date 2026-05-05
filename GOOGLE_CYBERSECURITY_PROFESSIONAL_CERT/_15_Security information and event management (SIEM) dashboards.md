# SIEM Tools & Log Analysis


---

## 1. Log Sources

A **log** is a record of events occurring within an organisation's systems and networks. Three main sources:

| Log Type | What It Records |
|---|---|
| **Firewall Log** | Attempted/established connections — inbound from internet, outbound from network |
| **Network Log** | Devices entering/leaving the network; connections between devices and services |
| **Server Log** | Events from services (websites, email, file shares) — logins, username/password requests |

> {Why it matters: Logs are the raw material for all SOC work. No logs = no visibility.}

---

## 2. What is a SIEM Tool?

**SIEM = Security Information and Event Management**

A SIEM tool **collects and analyses log data** to monitor critical activities in an organisation.

### Key capabilities:
- Real-time visibility into events
- Event monitoring and analysis
- Automated alerts
- Centralised log storage
- Indexes and minimises logs analysts need to manually review → **saves time, increases efficiency**

> {Think of SIEM as the analyst's command centre — it pulls everything into one place.}

**Important:** SIEM tools must be **configured and customised** per organisation. As threats evolve, the SIEM config must evolve too.

---

## 3. SIEM Dashboards

Dashboards turn raw log data into **visual representations** — charts, graphs, tables — for fast decision-making.

### Real-world example from the lecture:
- Alert: suspicious login attempt on Ymara's account
- Dashboard revealed: **500 login attempts in 5 minutes**, from unusual geographic locations, outside working hours
- Analyst quickly confirmed: **suspicious activity**

### Dashboard metrics include:
- Response time
- Availability
- Failure rate
- Volume of inbound/outbound traffic

> {Dashboards are what an analyst actually stares at during a shift. Knowing how to read them fast is a core SOC skill.}

Dashboards are **customisable** — different team members see what's relevant to their role.

---

## 4. Current vs Future SIEM

### Current state:
- Collect and analyse logs ✅
- Real-time monitoring ✅
- **Require human interaction** for analysis ⚠️

### Evolution of SIEM:

| Type | Description |
|---|---|
| **Cloud-Hosted** | Vendor manages infrastructure; accessed via internet; good for orgs that don't want to build own infra |
| **Cloud-Native** | Vendor-managed + designed to fully leverage cloud capabilities (availability, flexibility, scalability) |

### Drivers of future change:
- **IoT growth** → more devices = larger attack surface = more data
- **AI/ML integration** → better threat detection, improved dashboards, smarter data storage
- **Automation** → faster incident response without waiting for human action

---

## 5. SOAR

**SOAR = Security Orchestration, Automation, and Response**

A collection of apps, tools, and workflows that **automates responses to security events**.

- Handles common/repetitive incidents automatically
- Frees analysts to focus on **complex, unique incidents** that can't be automated
- Works alongside SIEM — they complement each other

> {SOAR handles the routine so you can focus on the interesting stuff. As a junior analyst, understanding what SOAR does and doesn't cover is important during triage.}

---

## Key Terms

| Term | Definition |
|---|---|
| Log | Record of events in systems/networks |
| SIEM | App that collects, analyses logs to monitor org activity |
| Dashboard | Visual interface showing security metrics and events |
| Metrics | Key technical attributes (response time, availability, failure rate) |
| SOAR | Automation layer that responds to security events |
| IoT | Internet of Things — interconnected internet-enabled devices |
| Cloud-Hosted SIEM | Vendor-managed, accessed over internet |
| Cloud-Native SIEM | Vendor-managed + built to maximise cloud capabilities |

---
---


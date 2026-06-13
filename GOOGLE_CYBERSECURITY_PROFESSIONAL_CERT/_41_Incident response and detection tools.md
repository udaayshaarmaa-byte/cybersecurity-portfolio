# Incident Response Lifecycle, CSIRT, SOC, Detection Tools & SIEM
---

## 1. What is an Incident?

**Event** = any observable occurrence on a network, system, or device.

**Security incident** = an event that actually or imminently jeopardises the confidentiality, integrity, or availability of information — or violates security policies, laws, or acceptable use policies.

> {Key distinction: all security incidents are events, but not all events are security incidents. A user resetting their own forgotten password = event. A malicious actor resetting someone else's password = event AND security incident.}

### The Five W's of an Incident:
- **Who** triggered the incident
- **What** happened
- **When** it took place
- **Where** it occurred
- **Why** it happened

These are captured in an **incident handler's journal** — your primary documentation tool throughout incident response.

---

## 2. NIST Incident Response Lifecycle

The lifecycle is **not linear** — it's a cycle. Steps can overlap as new discoveries are made.

```
Preparation
    ↓
Detection & Analysis
    ↓
Containment, Eradication & Recovery
    ↓
Post-Incident Activity
    ↓ (back to Preparation)
```

This course focuses on: **Detect → Respond → Recover** (last three functions of the NIST CSF).

---

## 3. CSIRT — Computer Security Incident Response Team

**CSIRT** = a specialised group of security professionals trained in incident management and response.

**Goals:**
- Manage incidents effectively and efficiently
- Provide resources for response and recovery
- Prevent future incidents

CSIRTs work **cross-functionally** — security and non-security professionals collaborate (HR, legal, PR, IT, management).

Also known as: **IHT** (Incident Handling Team), **SIRT** (Security Incident Response Team)

### Key CSIRT Roles:

| Role | Responsibilities |
|---|---|
| **Security Analyst** | Monitors for threats; investigates alerts; determines criticality; escalates or resolves |
| **Technical Lead** (Ops Lead) | Manages technical aspects; determines root cause; leads containment, eradication, and recovery; aligns with business priorities |
| **Incident Coordinator** | Coordinates cross-team communication; tracks activities; ensures response processes are followed; keeps all parties updated |

Other roles: communications lead, legal lead, planning lead, forensic investigator, threat hunter.

---

## 4. SOC — Security Operations Center

**SOC** = an organisational unit dedicated to monitoring networks, systems, and devices for security threats.

SOC is part of **blue team** operations — defending against threats.

### SOC Structure (Tiered):

| Tier | Role | Responsibilities |
|---|---|---|
| **L1 — Tier 1 Analyst** | Entry level | Monitor and prioritise alerts; create/close tickets; escalate to L2/L3 |
| **L2 — Tier 2 Analyst** | Experienced | Investigate escalated tickets; configure and refine security tools; report to SOC Lead |
| **L3 — SOC Lead** | Senior | Manage team operations; advanced detection (malware, forensics); report to SOC Manager |
| **SOC Manager** | Leadership | Hire/train/evaluate team; create performance metrics; develop reports; communicate to stakeholders |

**Specialised SOC roles:**
- **Forensic investigators** (usually L2/L3) — collect, preserve, and analyse digital evidence
- **Threat hunters** (usually L3) — proactively detect advanced threats using threat intelligence

> {As an entry-level SOC analyst, you're L1. Your job is to triage, prioritise, ticket, and escalate. You don't need to solve every incident — you need to recognise what matters and get it to the right person fast. That's the real skill at L1.}

---

## 5. Incident Response Plan

**Incident response plan** = a document outlining procedures for each step of incident response.

Plans are tailored per organisation (size, industry, culture, legal requirements).

### Common elements:
- **Incident response procedures** — step-by-step instructions
- **System information** — network diagrams, data flow diagrams, asset inventory, logging details
- **Supporting documents** — contact lists, forms, templates

Plans are tested through **tabletop exercises** and **simulations** to ensure familiarity and identify gaps.

---

## 6. Documentation

**Documentation** = any recorded content used for a specific purpose (digital, audio, handwritten, video).

No single industry standard — organisations set their own practices.

### Types of documentation in incident response:
- Playbooks
- Incident handler's journals
- Policies, standards, procedures
- Incident response plans
- Final reports

### Documentation tools:
- Word processors: Google Docs, OneNote, Evernote, Notepad++
- Ticketing systems: **Jira** (document and track incidents)
- Spreadsheets: Google Sheets
- Audio recorders, cameras, handwritten notes

**Effective documentation** = clear, consistent, accurate. Reduces uncertainty when tensions are high.

---

## 7. Detection Tools — IDS, IPS, EDR

### IDS — Intrusion Detection System
- Monitors system/network activity; generates alerts
- Does **NOT** stop or prevent activity — alerts only
- Analysts investigate and act
- Examples: Zeek, **Suricata**, Snort, Sagan

### IPS — Intrusion Prevention System
- All IDS capabilities + **actively stops** activity
- Can block traffic, modify access control lists on routers
- Many tools do both IDS and IPS (Suricata, Snort, Sagan)

### EDR — Endpoint Detection and Response
- Installed on endpoints (computers, phones, tablets)
- Collects and analyses endpoint activity data
- Performs **behavioural analysis** using ML/AI to detect threats
- Can **automatically block** suspicious processes without human intervention
- Examples: Open EDR, Bitdefender EDR, FortiEDR

### Detection Tool Comparison:

| Capability | IDS | IPS | EDR |
|---|---|---|---|
| Detects malicious activity | ✅ | ✅ | ✅ |
| Prevents intrusions | ❌ | ✅ | ✅ |
| Logs activity | ✅ | ✅ | ✅ |
| Generates alerts | ✅ | ✅ | ✅ |
| Behavioural analysis | ❌ | ❌ | ✅ |

### Four Detection Categories:

| Category | Meaning |
|---|---|
| **True positive** | Alert correctly detects a real attack |
| **True negative** | No alert; no malicious activity (correct) |
| **False positive** | Alert triggered by legitimate activity (wasted analyst time) |
| **False negative** | Attack happens but IDS misses it (dangerous — blind spot) |

> {False negatives are the most dangerous outcome. False positives waste time. Tuning detection rules to reduce false positives without creating false negatives is one of the core skills of a senior SOC analyst.}

---

## 8. SIEM — Process Deep Dive

**SIEM** = collects and analyses log data from multiple sources; provides real-time overview of network activity.

### Three-Step SIEM Process:

| Step | What happens |
|---|---|
| **1. Collect & Aggregate** | Ingests logs from firewalls, servers, IDS/IPS, applications, databases; centralises all data in one place |
| **2. Normalise** | Converts different log formats into a standard structured format; removes non-essential data; creates consistency for searching |
| **3. Analyse** | Applies detection rules to normalised data; generates alerts when activity matches a rule; includes **correlation** — comparing multiple events to identify threat patterns |

**Parsing** = during collection, maps raw log fields to standard values (e.g. source IP, username, timestamp).

### Common SIEM Tools:
AlienVault OSSIM, **Chronicle** (Google), Elastic, Exabeam, IBM QRadar, LogRhythm, **Splunk**

---

## 9. SOAR

**SOAR** = Security Orchestration, Automation, and Response — automates analysis and response to security events.

- SIEM: **collects, analyses, reports** → requires human review
- SOAR: **automates analysis and response** → reduces manual workload
- Can track and manage **cases** (multiple related incidents viewed in one place)

---

## Key Terms

| Term | Definition |
|---|---|
| Event | Observable occurrence on a network, system, or device |
| Security incident | Event that jeopardises CIA or violates security policies/law |
| NIST Incident Response Lifecycle | Preparation → Detection & Analysis → Containment, Eradication & Recovery → Post-Incident Activity |
| CSIRT | Computer Security Incident Response Team |
| SOC | Security Operations Center |
| Incident handler's journal | Documentation tool for recording incident details (5 W's) |
| Incident response plan | Procedures document for responding to security incidents |
| IDS | Intrusion Detection System — alerts only |
| IPS | Intrusion Prevention System — alerts + blocks |
| EDR | Endpoint Detection and Response — behavioural analysis + auto-block |
| True positive | Alert correctly identifies a real attack |
| False positive | Alert incorrectly flags legitimate activity |
| False negative | Real attack goes undetected |
| SIEM | Security Information and Event Management — collects, normalises, analyses logs |
| Normalisation | Converting log data into a standard structured format |
| Correlation | Comparing multiple events to identify threat patterns |
| SOAR | Security Orchestration, Automation, and Response — automates incident response |
| Tabletop exercise | Simulated incident discussion used to test and improve response plans |

---
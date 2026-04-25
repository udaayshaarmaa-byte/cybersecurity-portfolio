# Security Tools & Analyst Toolkit



---

## What Are Logs?

**Log** = a record of events that occur within an organization's systems.

Examples of security-related logs:
- Employees signing into computers
- Users accessing web-based services

> Logs are the **source of data** that security tools are designed to organize, filter, and analyze.
> Logs help security professionals identify vulnerabilities and potential security breaches.

---

## Core Security Tools

### 1. SIEM Tools (Security Information and Event Management)

**What it is:** An application that collects and analyzes log data to monitor critical activities in an organization.

**Pronunciation:** "sim" (used throughout the Google cert)

| Feature | Detail |
|---------|--------|
| Data collection | From multiple sources across the organization |
| Real-time monitoring | Identifies potential breaches as they happen |
| Alerts | Flags specific types of risks, threats, and vulnerabilities |
| Dashboards | Visually organizes data into categories for easy analysis |
| Hosting options | On-premise or cloud-hosted |

> Cloud-hosted SIEMs tend to be easier to set up, use, and maintain — better for less experienced teams.

**What analysts use SIEMs for:**
- Analyzing filtered events and patterns
- Performing incident analysis
- Proactively searching for threats (threat hunting)

#### Common SIEM Tools

| Tool | Type | Key Detail |
|------|------|-----------|
| **Splunk Enterprise** | Self-hosted | Retain, analyze, and search org log data — data analysis platform |
| **Google Chronicle** | Cloud-native | Fast delivery of new features; stores security data for search and analysis |

---

### 2. Network Protocol Analyzers (Packet Sniffers)

**What it is:** A tool designed to capture and analyze data traffic within a network.

- Keeps a record of all data a computer on the network encounters
- Also called: **packet sniffer**

| Tool | Notes |
|------|-------|
| **Wireshark** | GUI-based, widely used for network analysis |
| **tcpdump** | Command-line based packet analyzer |

---

### 3. Playbooks

**What it is:** A manual that provides details about any operational action — such as how to respond to a security incident.

- Guide analysts through steps **before, during, and after** an incident
- Vary from organization to organization but share the same purpose: ensuring proper protocols are followed
- Cover: security/compliance reviews, access management, incident response, and more

#### Two Key Forensic Playbooks

| Playbook | Purpose |
|----------|---------|
| **Chain of Custody** | Documents evidence possession and control during an incident lifecycle — who, what, where, and why evidence is held |
| **Protecting and Preserving Evidence** | Proper handling of fragile and volatile digital evidence |

**Chain of Custody key points:**
- Evidence is your responsibility while in your possession
- Must be kept safe and tracked at all times
- Every time evidence is moved → must be reported

**Protecting and Preserving Evidence key points:**
- Follows the **order of volatility** — sequence outlining which data must be preserved first to last
- **Volatile data** = data that may be lost if the device powers off (highest priority)
- Improper management of digital evidence can compromise it and make it inadmissible
- First priority: **preserve data by making copies** — conduct investigation on the copies, not the originals

---

## Entry-Level Analyst Toolkit — Summary

| Tool | Category | Primary Use |
|------|----------|-------------|
| Splunk Enterprise | SIEM | Log retention, analysis, search |
| Google Chronicle | SIEM (cloud-native) | Security data search and analysis |
| Wireshark | Packet sniffer | GUI network traffic capture and analysis |
| tcpdump | Packet sniffer | CLI network traffic capture |
| Playbooks | Process documentation | Incident response, forensics, access management |

> Every organization provides a different toolkit. What matters is being familiar with **industry standard tools** and demonstrating the ability to learn new ones quickly.

---

## Key Takeaway

> Security tools don't replace analyst judgment — they reduce noise so analysts can focus on what matters.
> SIEM tools cut down log review time from days to minutes.
> Playbooks ensure consistency and legal defensibility — especially critical in forensic investigations.

---

## Australian Market Context

| Concept | Australian Relevance |
|---------|---------------------|
| **SIEM tools (Splunk/Chronicle)** | Widely used in Australian SOC environments — familiarity is a hiring advantage |
| **Chain of custody playbooks** | Required for admissibility of digital evidence under Australian law |
| **Protecting and preserving evidence** | Aligns with ASD guidance on incident response handling |
| **ASD Essential Eight** | SIEM log monitoring directly supports Maturity Level 2+ detection requirements |
| **NDB Scheme** | SIEM alerts enable faster detection → faster breach notification compliance |

---



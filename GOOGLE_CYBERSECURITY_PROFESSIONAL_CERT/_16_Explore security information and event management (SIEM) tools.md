# SIEM Tools, Dashboards & Open-Source vs Proprietary


---

## 1. Open-Source vs Proprietary Tools

### Open-Source Tools
- Free to use, built collaboratively by the public
- Source code is **publicly available** → anyone can inspect, modify, improve it
- More customisable — teams can build new services on top of the same package
- **Common misconception:** open-source = less secure. Actually the opposite — wide exposure means vulnerabilities get spotted and fixed faster
- Training materials are also publicly available

### Proprietary Tools
- Developed and owned by a company; users **pay a fee** for usage and training
- Only the owner can access/modify the source code
- Users wait for vendor to push updates (and sometimes pay for them)
- Limited customisation
- Examples: **Splunk**, **Google SecOps (Chronicle)**

> {Open-source ≠ unsafe. Linux powers most of the internet. Suricata is used by enterprises worldwide. Don't let the "free" tag fool you into thinking it's less capable.}

---

## 2. Key Open-Source Tools

### Linux
- Open-source **operating system** — the interface between hardware and the user
- Highly customisable via **command-line interface (CLI)**
- Multiple versions exist for specific tasks
- Widely used in cybersecurity environments

### Suricata
- Open-source **network analysis and threat detection** tool
- Inspects network traffic → identifies suspicious behaviour → generates network data logs
- Detects activity across users, computers, and IP addresses
- Developed and maintained by the **Open Information Security Foundation (OISF)**
- Integrates with many SIEM tools and other security platforms
- Used in both public and private sectors

> {Suricata is going to come up a lot in SOC work — worth getting hands-on with it early. It does what a commercial IDS/IPS does, for free.}

---

## 3. Types of SIEM Deployment

| Type | Description | Best For |
|---|---|---|
| **Self-Hosted** | Org installs and manages on own physical infrastructure | Orgs needing physical control over confidential data |
| **Cloud-Hosted** | Managed by SIEM vendor, accessed via internet | Orgs that don't want to build/maintain own infra |
| **Cloud-Native** | Vendor-managed + built specifically to leverage cloud capabilities (availability, flexibility, scalability) | Cloud-first or hybrid environments |
| **Hybrid** | Combination of self-hosted + cloud-hosted | Best of both worlds — cloud benefits + physical data control |

---

## 4. Key SIEM Tools

### Splunk Enterprise
- **Self-hosted** SIEM
- Retains, analyses, and searches log data
- Provides real-time security information and alerts
- Ideal when physical control over data is required

### Splunk Cloud
- **Cloud-hosted** SIEM
- Collects, searches, and monitors log data
- Ideal for hybrid or cloud-only environments

### Google Chronicle
- **Cloud-native** SIEM
- Retains, analyses, and searches log data
- Provides log monitoring, data analysis, and data collection
- Designed to fully exploit cloud computing capabilities
- Can search/filter by: asset, domain name, user, IP address

> {Chronicle is Google's answer to the explosion of cloud data. Cloud-native means it scales with you — no infra headaches.}

---

## 5. Splunk Dashboards

| Dashboard | Purpose |
|---|---|
| **Security Posture** | Last 24hrs of notable security events; real-time threat monitoring for SOC |
| **Executive Summary** | Overall org health over time; high-level insights for stakeholders |
| **Incident Review** | Visual timeline of events leading up to an incident; highlights high-risk items |
| **Risk Analysis** | Risk per object (user/computer/IP); tracks abnormal behaviour e.g. after-hours logins |

---

## 6. Chronicle Dashboards

| Dashboard | Purpose |
|---|---|
| **Enterprise Insights** | Recent alerts; flags suspicious domains (IOCs) with confidence score + severity level |
| **Data Ingestion & Health** | Tracks log sources, event counts, success rates — ensures logs are flowing correctly |
| **IOC Matches** | Top threats by domain, IP, device IOCs over time; helps prioritise response |
| **Main Dashboard** | High-level summary of ingestion, alerts, and events over time |
| **Rule Detections** | Stats on alerts triggered by specific detection rules; helps manage recurring incidents |
| **User Sign-In Overview** | User access behaviour; flags unusual activity e.g. signing in from multiple locations simultaneously |

> {IOC = Indicator of Compromise. In a SOC shift, the IOC Matches and Rule Detections dashboards are what you'd check first when triaging.}

---

## Key Terms

| Term | Definition |
|---|---|
| Open-Source Tool | Publicly available software with accessible source code |
| Proprietary Tool | Vendor-owned software; source code is closed |
| Suricata | Open-source network threat detection tool (OISF) |
| Self-Hosted SIEM | Org manages its own SIEM infrastructure |
| Cloud-Hosted SIEM | SIEM managed by vendor, accessed via internet |
| Cloud-Native SIEM | Built specifically for cloud environments |
| Hybrid SIEM | Mix of self-hosted and cloud-hosted |
| IOC | Indicator of Compromise — evidence of a potential breach |
| Splunk Enterprise | Self-hosted SIEM from Splunk |
| Splunk Cloud | Cloud-hosted SIEM from Splunk |
| Chronicle | Cloud-native SIEM from Google |

    
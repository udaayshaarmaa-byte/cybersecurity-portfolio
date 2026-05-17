# Lab 5 | Incident Report | SIEM-Based Threat Detection
**Analyst:** Uday Sharma    
---

## 1.Summary

A retrospective SIEM analysis was conducted on Suricata IDS telemetry captured during Lab 4 (Port Scan Detection). Logs were ingested into Splunk and queried using SPL to identify threat patterns. Three distinct Suricata alert signatures were detected across 103 total alert events. The dominant finding was an nmap-based port scan originating from the internal Kali, which probed 1,004 unique destination ports on the Ubuntu. All findings were confirmed through automated SPL detection queries and visualised in a SOC monitoring dashboard.

---

## 2. Environment

| Component | Detail |
|-----------|--------|
| Attacker VM | Kali Linux — 192.168.56.102 |
| Target VM | Ubuntu — 192.168.56.103 |
| IDS | Suricata |
| SIEM | Splunk Enterprise Free |
| Log volume | 10,540 events |
| Network | VirtualBox Host-Only Adapter (NAT + Host-Only) |
| Lab date | 11–12 May 2026 |

---

## 3. Detection Methodology

Suricata eve.json logs from Lab 4 were exported and ingested into Splunk via the Add Data → Upload workflow. Sourcetype was set to `_json`. Three SPL queries were written to automate detection of threats observed manually during Lab 4.

**SPL Query 1 | Port Scan Detection:**
```
source="/home/uday/lab5-suricata.json" host="udayy" index="main" sourcetype="_json"
| stats dc(dest_port) as unique_ports values(dest_port) as ports_scanned by src_ip
| where unique_ports > 20
| sort -unique_ports
```

**SPL Query 2 | Suricata Alert Summary:**
```
source="/home/uday/lab5-suricata.json" host="udayy" index="main" sourcetype="_json"
| stats count by alert.signature
| sort -count
```

**SPL Query 3 | Threat Activity Timeline:**
```
source="/home/uday/lab5-suricata.json" host="udayy" index="main" sourcetype="_json"
| timechart count by event_type
```

---

## 4. Findings

### Finding 1 | Nmap Port Scan Detected
| Field | Detail |
|-------|--------|
| Alert Signature | ET SCAN Possible Nmap User-Agent Observed |
| Alert Count | 82 |
| Source IP | 192.168.56.102 (Kali) |
| Target IP | 192.168.56.103 (Ubuntu) |
| Unique Ports Scanned | 1,004 |
| Detection Method | SPL Query 1 |

**Analysis:** Kali initiated a TCP SYN scan across 1,004 ports on the Ubuntu host. Suricata identified the nmap User-Agent string embedded in probe packets and fired the ET SCAN signature 82 times.

---

### Finding 2 — ICMP Anomaly Detected
| Field | Detail |
|-------|--------|
| Alert Signature | SURICATA ICMPv4 unknown code |
| Alert Count | 18 |
| Source IP | 192.168.56.102 (Kali) |
| Target IP | 192.168.56.103 (Ubuntu) |
| Detection Method | SPL Query 2 |

**Analysis:** Suricata detected 18 ICMP packets with unrecognised code values during the scan sequence. This is characteristic of nmap's host discovery phase, where ICMP echo requests are sent prior to the TCP port scan to confirm the target is alive.

---

### Finding 3 — Applayer Protocol Anomaly
| Field | Detail |
|-------|--------|
| Alert Signature | SURICATA Applayer Detect protocol only one direction |
| Alert Count | 3 |
| Source IP | 192.168.56.102 (Kali) |
| Target IP | 192.168.56.103 (Ubuntu) |
| Detection Method | SPL Query 2 |

**Analysis:** Three connections were flagged where Suricata detected application-layer protocol data flowing only from the attacker with no response from the target. This occurs when nmap sends probe packets to closed or filtered ports that do not respond, causing an incomplete protocol handshake.


---

## 6. SIEM Dashboard

Dashboard name: **SOC Monitoring Dashboard**  
Platform: Splunk Enterprise  
| Panel | Type | Key Output |
|-------|------|------------|
| Port Scan Detection | Table | Kali: 1,004 unique ports |
| Suricata Alert Summary | Bar Chart | 3 signatures, 103 total alerts |
| Threat Activity Timeline | Line Chart | Spike confirmed at ~19:00 May 11 |

---


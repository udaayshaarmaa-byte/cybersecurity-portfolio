# Network Hardening & Security Tools — Notes


---

## 1. Network Hardening vs OS Hardening

| Focus | OS Hardening | Network Hardening |
|---|---|---|
| Scope | Individual device security | Network-wide security |
| Examples | Patch updates, password policy, secure config | Port filtering, network segmentation, encryption, log analysis |

---

## 2. Network Hardening Tasks

### Performed Regularly:
- **Firewall rules maintenance** — review and update allow/deny rules as the network evolves
- **Network log analysis** — examining logs to identify events of interest; done using SIEM or log analyser tools
- **Patch updates** — keep all network devices and software up to date
- **Server backups** — ensure recovery capability if systems are compromised or fail

### Performed Once (then updated as needed):
- **Port filtering** — block all ports not required for normal operations; only allow what's needed
- **Network access privileges** — define who can access which parts of the network
- **Encryption standards** — set and enforce encryption for all network communication
- **Network segmentation** — create isolated subnets per department or security zone
- **Wireless protocol updates** — use latest Wi-Fi security protocols; disable older ones (WEP, WPA)

---

## 3. Port Filtering

**Principle:** only ports required for normal operations should be open. All others blocked.

- Implemented on firewalls
- Reduces attack surface by eliminating unnecessary entry points
- Example: if HTTPS is the only web protocol used, block port 80 (HTTP) and only allow 443



## 4. Network Segmentation

- Divides the network into isolated **subnets** per department or security zone
- Issues in one subnet don't spread across the whole network
- Users only access the subnet relevant to their role
- Highly classified data sits in a **restricted zone** — separated from the rest of the network with stricter encryption and access controls

Example: university with separate faculty and student subnets — if the student subnet is compromised, the faculty subnet remains clean.

---

## 5. Encryption Standards

- All network communication should be encrypted using **current encryption standards**
- Restricted zones require **higher encryption standards** — harder to access even if perimeter is breached
- **Encryption standards** = rules/methods used to conceal outgoing data and decrypt incoming data

---

## 6. Defence-in-Depth — Layered Security Tools

Each tool adds a layer. More layers = harder to breach.

```
Internet
    ↓
[ Firewall ]          ← filters by port/IP; NGFW also inspects payload
    ↓
[ IDS ]               ← detects and alerts; sits behind firewall
    ↓
[ IPS ]               ← detects and blocks; inline between firewall and LAN
    ↓
Internal Network
    ↓
[ SIEM ]              ← aggregates logs from all above; single pane of glass
```

---

## 7. Security Tools — Comparison

### Firewall
- Allows or blocks traffic based on rules (port number, IP address)
- NGFW also inspects packet payloads
- Every system should have its own firewall, even behind a network firewall
- **Limitation:** only filters based on packet header information (basic firewalls)

### IDS — Intrusion Detection System
- Monitors system activity; **alerts** administrators about possible intrusions
- Sniffs packets and checks for signatures of known attacks + anomalies
- Placed **behind the firewall** — analyses already-filtered traffic (reduces false positives)
- **Limitation:** only detects known attacks/obvious anomalies; new attacks may slip through; does NOT stop traffic — only alerts

### IPS — Intrusion Prevention System
- Monitors activity AND **actively stops** threats — blocks sender or drops suspicious packets
- Placed **between firewall and internal network** — disrupts risky traffic before it reaches sensitive systems
- Reports anomalies to analysts and takes action simultaneously
- **Limitation:** inline appliance — if it fails, internet connection drops; risk of false positives blocking legitimate traffic

### Full Packet Capture Devices
- Record and analyse **all data** transmitted over the network
- Support investigation of IDS alerts with full traffic context

### SIEM — Security Information and Event Management
- Collects and analyses log data from: IDS, IPS, firewalls, VPNs, proxies, DNS logs
- Presents everything in a **single pane of glass** (centralised dashboard)
- Works in real time; prioritises vulnerabilities from high to low for analyst attention
- **Limitation:** only reports — does NOT take action to stop threats; requires analyst expertise to act on findings



---

## 8. Summary Table

| Tool | Detects | Stops Traffic? | Location in Network |
|---|---|---|---|
| **Firewall** | Port/IP violations | Yes — blocks packets | Perimeter (and per device) |
| **IDS** | Known attack signatures + anomalies | No — alerts only | Behind firewall, before LAN |
| **IPS** | Known signatures + anomalies | Yes — blocks/drops | Between firewall and LAN (inline) |
| **SIEM** | Aggregated events across all sources | No — reports only | Centralised; feeds from all tools |

---

## Key Terms

| Term | Definition |
|---|---|
| Network Hardening | Securing network infrastructure through configuration, filtering, segmentation, and encryption |
| Port Filtering | Firewall function blocking all non-essential ports |
| Network Segmentation | Dividing network into isolated subnets for security and access control |
| Encryption Standard | Rules for concealing and decrypting network data |
| IDS | Intrusion Detection System — monitors and alerts |
| IPS | Intrusion Prevention System — monitors and blocks |
| SIEM | Aggregates log data into a centralised dashboard for analysis |
| Single Pane of Glass | SIEM dashboard showing all security events in one place |
| Defence in Depth | Layered security approach — multiple tools/strategies combined |
| False Positive | Alert triggered by legitimate traffic incorrectly flagged as malicious |
| Full Packet Capture | Recording all network data for deep analysis and investigation |
| Network Log Analysis | Reviewing logs to identify security events of interest |
| SOC | Security Operations Centre — where analysts monitor and respond to events |

---



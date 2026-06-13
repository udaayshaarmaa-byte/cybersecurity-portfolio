# Network Monitoring, Traffic Analysis & Data Exfiltration

---

## 1. Network Traffic vs Network Data

| Term | Definition |
|---|---|
| **Network traffic** | The amount of data that moves across a network; also the *type* of data (e.g. HTTP, DNS) |
| **Network data** | The data transmitted between devices on a network |

Large organisations generate massive volumes of network traffic — knowing what's *normal* is the prerequisite to detecting what's *abnormal*.

---

## 2. Baseline — Foundation of Network Monitoring

**Baseline** = a reference point representing normal or expected behaviour for systems, devices, and networks.

Without a baseline, you have no standard to compare against — anomalies become invisible.

**Example:** A North American company has bulk traffic between 09:00–17:00. Large traffic volumes outside those hours = off-baseline = investigate.

---

## 3. What to Monitor — Three Key Areas

### Flow Analysis
- **Flow** = movement of network communications including packets, protocols, and ports
- Normal: protocols use their expected ports (e.g. HTTPS on port 443)
- Suspicious: **command and control (C2)** communications using unexpected port/protocol combinations (e.g. HTTPS over port 8088 instead of 443)
- Organisations need to know which ports should be open and watch for mismatches

**C2 (Command and Control)** = techniques used by attackers to maintain communications with compromised systems — a key indicator of an active intrusion.

### Packet Payload Information
- Packets contain source/destination IP addresses + **payload** (actual data being transmitted)
- Payload is often encrypted — requires decryption to read content
- Monitoring payload can reveal: sensitive data leaving the network = possible **data exfiltration**

### Temporal Patterns
- Network packets carry timestamps
- Unusual traffic *volume* or *timing* relative to the baseline = investigation trigger
- Example: bulk data transfer at 03:00 when the office is empty

---

## 4. Indicators of Compromise (IoC)

**IoC** = observable evidence suggesting signs of a potential security incident.

Examples of network-level IoCs:
- Large volumes of outbound traffic from a single host
- Large internal file transfers to unusual destinations
- Large external uploads at unusual times
- Unexpected file writes
- Multiple user logins from IPs outside the normal network range
- Protocol/port mismatches (C2 traffic)

---

## 5. Data Exfiltration — Attack Lifecycle

**Data exfiltration** = the unauthorised transmission of data from a system — used to steal usernames, passwords, intellectual property, PII, financial records.

### Attacker's perspective (step by step):

```
1. Initial access
   → Phishing email with malicious attachment or credential-harvesting link
   → Attacker gains foothold on a device

2. Lateral movement (pivoting)
   → Attacker explores the network
   → Searches file shares, intranet, code repositories for valuable assets
   → Expands access to other systems while avoiding detection

3. Data collection and packaging
   → Identifies high-value data (PII, proprietary code, financial records)
   → Compresses/reduces data size to evade security controls and reduce noise

4. Exfiltration
   → Sends data outside the network (e.g. emails it from the compromised account,
     uploads to attacker-controlled server, or uses C2 channel)
```

### Defender's response:

| Phase | Action |
|---|---|
| **Prevent access** | MFA, phishing training, email filtering |
| **Monitor for compromise** | Watch for logins from unusual IPs; unusual internal file transfers; off-hours traffic spikes |
| **Protect assets** | Asset inventory with classification; appropriate access controls per classification level |
| **Detect and stop exfiltration** | SIEM alerts on large outbound transfers, unexpected uploads; block attacker IPs via firewall rules |

---

## 6. Network Monitoring Tools

### IDS (Intrusion Detection System)
- Monitors packet payload for patterns associated with threats (malware, phishing)
- Alerts on deviations from configured rules
- Does not stop traffic — alerts only

### Network Protocol Analyser (Packet Sniffer)
- Captures and analyses data traffic on a network
- Used for **manual, detailed investigation** of network communications
- Produces **packet captures** (pcap files) for later analysis

| Tool | Use |
|---|---|
| **Wireshark** | GUI-based packet capture and analysis |
| **tcpdump** | Command-line packet capture; used in home lab |

---

## 7. SOC vs NOC

| | SOC | NOC |
|---|---|---|
| **Focus** | Security — detecting and responding to threats | Network performance and availability |
| **Goal** | Protect against attacks | Maintain uptime and performance |
| **Responds to** | Security incidents, IoCs | Network outages, degraded performance |

Both may coexist in large organisations.

---

## Key Terms

| Term | Definition |
|---|---|
| Network traffic | Amount and type of data moving across a network |
| Network data | Data transmitted between devices |
| Baseline | Reference point for expected/normal network behaviour |
| Flow analysis | Monitoring packets, protocols, and ports for anomalies |
| C2 (Command and Control) | Attacker technique for maintaining communications with compromised systems |
| Packet payload | The actual data content of a network packet |
| Temporal pattern | Time-based analysis of network traffic |
| IoC | Indicator of Compromise — observable evidence of a potential incident |
| Data exfiltration | Unauthorised transmission of data from a system |
| Lateral movement | Attacker expanding access across a network after initial compromise |
| Packet sniffer | Tool that captures and analyses network traffic |
| Packet capture (pcap) | Recorded network traffic file for analysis |
| NOC | Network Operations Center — monitors performance, not security |

---
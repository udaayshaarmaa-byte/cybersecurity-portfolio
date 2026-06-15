# Intrusion Detection Systems, Signatures & Suricata
---

## 1. Telemetry vs Logs

- **Telemetry** = the collection and transmission of data for analysis  describes the *data itself* (e.g. packet captures = network telemetry).
- **Logs** = record *events* that occur on systems.
- Both logs and telemetry are sources of **evidence** used to answer investigative questions.

---

## 2. Intrusion Detection Systems (IDS)

**IDS** = an application that monitors system activity and alerts on possible intrusions.

Depending on where it's deployed, an IDS is either **host-based** or **network-based**.

### Host-based IDS (HIDS)
- Installed as an **agent** on a single host/endpoint (laptop, server, etc.)
- Monitors **internal activity** on that host: unauthorized applications, file system changes, resource usage, user activity, inbound/outbound traffic
- Detects unusual behaviour → logs it → generates an alert

### Network-based IDS (NIDS)
- Installed at specific points in the network to inspect **network traffic** from multiple devices
- Works similarly to a **packet sniffer**
- Multiple NIDS sensors are often deployed across a network for adequate visibility
- Detects malicious traffic → logs it → generates an alert

| | HIDS | NIDS |
|---|---|---|
| **Scope** | Single endpoint | Entire network / traffic between devices |
| **Installed as** | Agent on the host | Sensor at a network chokepoint |
| **Best for** | Endpoint-level behaviour (file changes, local processes) | Traffic patterns, lateral movement, external connections |

> {Using HIDS + NIDS together gives a multi-layered, comprehensive view  each tool sees something the other can't.}

---

## 3. Detection Techniques

### Signature-based analysis
**Signature** = a pattern associated with malicious activity (binary sequences, bytes, IP addresses, specific content, etc.)

- IDS compares activity against a database of signatures
- Match → event logged + alert generated
- Related concept: **Pyramid of Pain**  prioritises types of IoCs (IPs, tools, TTPs, etc.) useful for building signatures

| Advantages | Disadvantages |
|---|---|
| Low false-positive rate  efficient at detecting *known* threats | Signatures can be evaded by attackers modifying their behaviour/code |
| | Requires constant updates as new exploits emerge |
| | Cannot detect unknown threats (new malware families, zero-days) |

### Anomaly-based analysis
Two phases:

| Phase | What happens |
|---|---|
| **Training** | Establish a **baseline** of normal/expected behaviour |
| **Detection** | Compare current activity against the baseline; deviations get logged + alerted |

| Advantages | Disadvantages |
|---|---|
| Can detect new/unknown/evolving threats | High false-positive rate  any deviation (even benign) gets flagged |
| | If an attacker is present during training, their activity becomes part of the "normal" baseline (pre-existing compromise goes undetected) |

> {Signature-based = good at catching what you already know about. Anomaly-based = good at catching what you don't  but noisier. Mature SOCs run both.}

---

## 4. NIDS Signature Syntax

A signature (rule) defines the **detection rules** an IDS uses, and consists of **three components**:

| Component | Description |
|---|---|
| **Action** | What to do if traffic matches  e.g. `alert`, `pass`, `drop`, `reject` |
| **Header** | Defines the traffic: protocol, source/destination IPs, source/destination ports, traffic direction |
| **Rule options** | Additional customisation parameters, enclosed in `()`, separated by `;` |

**Rule order matters**  changing the order of rule options changes the rule's meaning. Suricata's default processing order is: **pass → drop → reject → alert** (regardless of the order rules are written in the config file). This matters when a `drop` rule and an `alert` rule both match the same packet.

### Example header breakdown
```
TCP 10.120.170.17 any -> 133.113.202.181 80
```
- Protocol: **TCP**
- Source IP: `10.120.170.17`, Source port: `any`
- `->` indicates traffic **direction**
- Destination IP: `133.113.202.181`, Destination port: `80`

### Common rule options

| Option | Stands for | Purpose |
|---|---|---|
| `msg` | Message | Text shown when the alert fires |
| `sid` | Signature ID | Unique identifier for the signature |
| `rev` | Revision | Version number  increments when the signature is updated |
| `flow` | Flow | Matches direction/state of traffic (e.g. `established` = connection successfully made) |
| `content` | Content | Inspects packet payload for specific text/data (used to detect malicious payloads) |

### Worked example  HTTP custom rule
A signature that:
- **Action**: `alert`
- **Header**: protocol `http`, source `HOME_NET` any port → destination `EXTERNAL_NET` any port
- **Rule options**: `msg:"GET on wire"`, `flow:established`, `content:"GET"`

**Meaning**: Alert whenever an established HTTP connection from the home network to an external network contains the text `GET` (an HTTP request to retrieve data).

> Lines starting with `#` in a rules file are **comments**  ignored by Suricata, used to give context to humans reading the file.

---

## 5. Suricata

**Suricata** = an open-source IDS, IPS, and network analysis tool.

### Three modes of operation

| Mode | Function |
|---|---|
| **IDS** | Monitors network (NIDS) or host (HIDS) traffic/activity and alerts on suspicious activity |
| **IPS** | Detects **and blocks** malicious traffic (requires enabling IPS mode + extra config) |
| **NSM (Network Security Monitoring)** | Produces/saves network logs; analyses live traffic or existing pcap files; creates full/conditional packet captures  useful for forensics, IR, and signature testing |

### Rules / Signatures
- "Rule" and "signature" are **synonymous** in Suricata
- Same 3 components as above: **Action, Header, Rule options**
- Pre-written rules act as **templates**  customise them for your environment
- **Custom rules** reduce false positives and tailor detection to your org's infrastructure
- No one-size-fits-all  every org's IT environment differs, so rules must be tested and tuned

### Configuration
- Config file: **`suricata.yaml`** (YAML format)
- Configuration files live in `/etc/suricata/`
- Rules folder contains pre-written rule templates by protocol/service (e.g. `custom.rules`)

### Log files

| File | Format | Contents | Use case |
|---|---|---|---|
| **`eve.json`** | EVE JSON (Extensible Event Format + JSON) | Detailed events/alerts, includes `flow_id` to correlate logs to a network flow | Detailed analysis, SIEM ingestion, IR, threat hunting |
| **`fast.log`** | Plaintext (legacy) | Minimal info  basic IP/port details | Basic logging/alerting only  **not** suitable for IR or threat hunting |

### EVE JSON  two log types

| Log type | Contents | Example |
|---|---|---|
| **Alert logs** | Output of triggered signatures; security-relevant | `event_type: alert`, IPs, protocol, signature message + ID (e.g. malware detection) |
| **Network telemetry logs** | Records of network activity/flows; not always security-relevant | `event_type: http`  hostname, user agent (e.g. Mozilla 5.0), content type (e.g. HTML) |

> {flow_id is what lets you stitch an alert log together with its corresponding telemetry  that's how you go from "an alert fired" to "here's the full story of that connection."}

---

## Key Terms

| Term | Definition |
|---|---|
| Telemetry | Collection and transmission of data for analysis (describes the data itself) |
| IDS | Application that monitors activity and alerts on possible intrusions |
| HIDS | Host-based IDS  agent monitoring a single endpoint |
| NIDS | Network-based IDS  monitors traffic across the network |
| Endpoint / Host | Any device connected to a network (laptop, server, etc.) |
| Signature-based analysis | Detection method comparing activity to known malicious patterns |
| Anomaly-based analysis | Detection method comparing activity to a learned baseline of normal behaviour |
| Baseline | Established profile of normal/expected system behaviour |
| Pyramid of Pain | Framework prioritising IoC types by difficulty for attackers to change |
| Zero-day | Previously unknown exploit/vulnerability |
| Signature / Rule | Pattern/ruleset an IDS uses to detect specific activity (terms used interchangeably in Suricata) |
| Action | Signature component specifying response (alert, pass, drop, reject) |
| Header | Signature component defining traffic (IPs, ports, protocol, direction) |
| Rule options | Signature component for additional customisation (msg, sid, rev, flow, content, etc.) |
| Rule order | The sequence in which an IDS evaluates/applies rules; affects final verdict on conflicting matches |
| Suricata | Open-source IDS/IPS/NSM tool |
| suricata.yaml | Suricata's main configuration file (YAML format) |
| eve.json | Suricata's detailed JSON log file (alerts + telemetry), includes flow_id |
| fast.log | Suricata's minimal legacy log file |
| flow_id | Unique identifier correlating related logs/alerts to a single network flow |

---
# Detection Methods, IoC, IoA, Pyramid of Pain & Threat Intelligence

---

## 1. Detection and Analysis Phase

The second phase of the NIST Incident Response Lifecycle.

| Sub-phase | What happens |
|---|---|
| **Detection** | Prompt discovery of security events using IDS, SIEM, and other tools |
| **Analysis** | Investigation and validation of alerts — determining if a real incident occurred |

**Key challenge:** it's impossible to detect everything.
- Detection tools only catch what they're configured to monitor
- Misconfigured rules create **false positives** — alert rules too broad for the environment
- High alert volumes can also be legitimate — a newly discovered vulnerability being actively exploited at scale
- Some incidents are unavoidable — this is why the incident response **plan** is non-negotiable

> {A Tier 1 analyst can receive thousands of alerts per shift. The job isn't to investigate every one in depth — it's to triage, prioritise, and escalate correctly. Tuning alert rules to reduce false positives without creating false negatives is a senior skill, but understanding why it matters is fundamental.}

---

## 2. IoC vs IoA

| | IoC | IoA |
|---|---|---|
| **Full name** | Indicator of Compromise | Indicator of Attack |
| **Focus** | Evidence of what already happened | Behavioural evidence of an ongoing or unknown attack |
| **Answers** | Who did it and what did they do? | Why and how is this happening right now? |
| **Example** | Filename of malicious process; IP address contacted | A process making an unexpected network connection |
| **Timing** | After-the-fact | Real-time |

> {IoC = crime scene evidence. IoA = watching the crime happen in real time. Both matter — IoA gives you a chance to intervene before damage is done. IoC helps you understand what already happened.}

**Important:** IoCs are not confirmation of an incident. They can also result from human error or system malfunctions — always validate before escalating.

---

## 3. Pyramid of Pain

Created by security researcher **David J. Bianco** — captures the relationship between IoC types and the level of difficulty an attacker faces when those IoCs are blocked.

**Higher up the pyramid = more painful for the attacker = harder to evade.**

```
        ▲  TTPs (Tactics, Techniques, Procedures) — Tough
        │  Tools
        │  Host Artifacts
        │  Network Artifacts
        │  Domain Names
        ▼  Hash Values / IP Addresses — Easy (trivial to change)
```

### Full Breakdown:

| Level | IoC Type | Description | Pain for attacker if blocked |
|---|---|---|---|
| 1 (Bottom) | **Hash values** | Hashes of known malicious files; unique fingerprints of malware samples | Easy — attacker changes one byte, hash changes |
| 2 | **IP addresses** | Known malicious IPs | Easy — attacker switches to another IP |
| 3 | **Domain names** | Malicious domains used for C2 or phishing | Annoying — costs money and time to re-register |
| 4 | **Network artifacts** | Observable evidence in network protocols (e.g. User-Agent strings) | Uncomfortable — requires more technical adaptation |
| 5 | **Host artifacts** | Files, registry keys, or other evidence left on compromised hosts | Uncomfortable — requires rewriting malware components |
| 6 | **Tools** | Specific software used by the attacker (e.g. John the Ripper, Mimikatz) | Challenging — must find/build replacement tools |
| 7 (Top) | **TTPs** | The attacker's entire behaviour pattern — tactics, techniques, procedures | Tough — requires completely changing how they operate |

> {If you can detect and block at the TTP level, you're not just stopping this attack — you're stopping that threat actor's entire methodology. This is why MITRE ATT&CK maps TTPs — it's the highest-value intelligence for long-term defence.}

---

## 4. Detection Methods Beyond Automated Tools

### Threat Hunting
**Threat hunting** = the proactive, human-driven search for threats on a network not identified by automated detection tools.

- Combines human analytical skill with technology
- Especially effective against **fileless malware** (hides in memory, bypasses signature-based detection)
- Threat hunters look for anomalies that tools were not configured to detect

**Threat hunters use:**
- Threat intelligence
- Indicators of compromise (IoC)
- Indicators of attack (IoA)
- Machine learning
- Active network and host analysis

### Threat Intelligence
**Threat intelligence** = evidence-based information about existing or emerging threats, providing context for decision-making.

| Source | Content |
|---|---|
| **Industry reports** | Attacker TTPs documented by security firms |
| **Government advisories** | ACSC advisories, CISA alerts — attacker TTPs + IOC lists |
| **Threat data feeds** | Real-time streams of IoCs (IP addresses, domains, file hashes) — especially useful for APT tracking |

**TIP (Threat Intelligence Platform)** = application that collects, centralises, and analyses threat intelligence from multiple sources — helps prioritise which threats matter most to your environment.

> {Threat data feeds should add context to detections, not drive them entirely. An IP address on a threat list doesn't automatically mean you're being attacked — it means you should look more closely.}

### Cyber Deception / Honeypots
**Honeypot** = a decoy system or resource intentionally left vulnerable to attract attackers.

- Example: a fake file named "Client Credit Card Information - 2022" placed in a network share
- When an attacker accesses it → alert fires → security team is notified
- No legitimate user should ever touch a honeypot → any access = suspicious

Honeypots are **proactive** — they don't wait for attackers to hit real assets. They lure them in and expose their presence.

---

## 5. CI/CD Pipeline IoCs (Brief Overview)

While primarily a developer concern, SOC analysts monitoring CI/CD environments should recognise these IoCs:

| Category | IoC |
|---|---|
| **Unauthorised code changes** | Code commits from unexpected accounts; late-night changes; large unexplained deletions |
| **Suspicious deployments** | Deployments to unapproved systems; off-schedule deployments; unusual initiating accounts |
| **Compromised dependencies** | New CVEs found in build dependencies; unexpected new packages added |
| **Unusual pipeline execution** | Steps failing unexpectedly; pipelines taking far longer than baseline |
| **Secrets exposure** | Hardcoded credentials found in commits; access to secrets from unapproved pipeline stages |

SIEM integration with CI/CD logs enables automated anomaly detection against pipeline baselines.

---

## Key Terms

| Term | Definition |
|---|---|
| IoC | Indicator of Compromise — observable evidence of a past incident |
| IoA | Indicator of Attack — behavioural evidence of an ongoing attack |
| Pyramid of Pain | Framework ranking IoC types by difficulty for attacker to evade if blocked |
| TTP | Tactics, Techniques, and Procedures — attacker behaviour patterns (hardest to evade) |
| Threat hunting | Proactive human-driven search for threats not caught by automated tools |
| Threat intelligence | Evidence-based information about existing or emerging threats |
| TIP | Threat Intelligence Platform — centralises and analyses threat intelligence |
| Threat data feed | Real-time stream of IoCs (IPs, domains, hashes) |
| Honeypot | Decoy system designed to attract and expose attackers |
| APT | Advanced Persistent Threat — long-term unauthorised network access, often nation-state |
| False positive | Alert on legitimate activity — wastes analyst time |
| False negative | Real attack not detected — dangerous blind spot |
| MITRE ATT&CK | Knowledge base of adversary TTPs based on real-world observations |
| Fileless malware | Memory-resident malware that evades signature-based detection |

---
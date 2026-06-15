# Documentation, Triage, Chain of Custody, Playbooks & Containment
---

## 1. Why Documentation Matters

**Documentation** = any recorded content used for a specific purpose.

Three core benefits:

| Benefit | What it means | Example |
|---|---|---|
| **Transparency** | Creates an audit trail; supports legal proceedings, compliance, and insurance claims | Chain of custody forms tracking evidence handling |
| **Standardisation** | Establishes repeatable processes; enables knowledge transfer; supports onboarding | Incident response plans; security policies and procedures |
| **Clarity** | Gives team members a clear understanding of roles and actions required | Playbooks providing step-by-step instructions |

### Documentation best practices:
- **Know your audience**  a report for a SOC manager is different from one for a CEO; adjust technical depth accordingly
- **Be concise**  establish the purpose immediately; executive summaries at the top for fast scanning
- **Update regularly**  threats evolve, regulations change; outdated documentation creates risk, not safety

> {As a detection engineer, I've learned: without clear documentation on what a rule does, what it means when it fires, and how to validate it, a SOC team can never scale past 2 analysts. The documentation isn't the afterthought  it's what makes the alert actionable.}

---

## 2. Chain of Custody

**Chain of custody** = the process of documenting evidence possession and control during an incident lifecycle.

Used to establish proof of integrity, reliability, and accuracy of evidence  especially when legal proceedings may follow.

### How it works (example):
```
Aisha discovers compromised hard drive
→ Write-protects the drive (no data can be altered)
→ Calculates a cryptographic hash of the disk image (integrity baseline)
→ Transfers to Colin (forensics)  logged in chain of custody form
→ Colin transfers to Nav  logged
→ Nav transfers to Arman (manager)  logged
Each transfer: who, when, why, and where
```

If anyone tampers with the drive later → the hash changes → tampering is detected.

### Elements of a chain of custody form:
- **Description of evidence**  hostname, IP address, MAC address, location, serial number
- **Custody log**  names of people who handled it; date/time of transfer; purpose of transfer

**Broken chain of custody** = inconsistencies in the collection or logging of evidence. In court, this can undermine the admissibility and credibility of evidence  even if the evidence itself is valid.

> {Chain of custody is how forensic evidence survives the journey from incident to courtroom. A broken chain can let a malicious actor walk free even when the technical evidence is clear.}

---

## 3. Playbooks

**Playbook** = a manual providing details about operational actions for incident response.

- Provide structure and order when situations are unpredictable and chaotic
- Include checklists to prevent steps being missed under pressure
- Cover specific incident types: ransomware, data breach, malware, DDoS

### Three types of playbooks:

| Type | Description | Use case |
|---|---|---|
| **Non-automated** | Step-by-step manual actions performed by an analyst | Most common; DDoS flowchart example |
| **Automated** | Tasks triggered automatically (severity categorisation, evidence gathering) | SOAR/SIEM-configured automation; reduces time to resolution |
| **Semi-automated** | Analyst actions + automation combined | Analyst handles judgement calls; routine tasks are automated |

Playbooks are **living documents**  updated regularly, especially after incidents during post-incident activity review.

---

## 4. Triage

**Triage** = prioritising incidents according to their level of importance or urgency.

The security equivalent of hospital emergency triage  limited resources, critical decisions under pressure.

### Three-step triage process:

**Step 1  Receive and assess:**
- Verify the alert is a true positive (not a false positive)
- Gather: what triggered the alert, which systems/assets are involved, any existing context
- Questions to ask:
  - Is this a false positive?
  - Has this alert fired before? How was it resolved?
  - Is it linked to a known vulnerability?
  - What is the severity?

**Step 2  Assign priority:**
Three factors determine priority:

| Factor | Question to ask |
|---|---|
| **Functional impact** | How does this affect the business operations of the affected system? (e.g. ransomware = high  complete outage) |
| **Information impact** | What data is at risk? PII, financial records, IP? Who else is affected beyond the organisation? |
| **Recoverability** | Can we recover? If stolen data is already public, recovery isn't possible  spending resources there is wasteful |

**Step 3  Collect and analyse:**
- Gather evidence from multiple sources
- Conduct external research (CVE, MITRE ATT&CK, threat intelligence)
- Document the investigative process
- Escalate to L2/L3 if the severity warrants it

### Adding context to triage:
A single failed login = low concern.
Same alert with context: 500 failed logins in 5 minutes, from an overseas IP, at 03:00, against an admin account = escalate immediately.

> {Context transforms a data point into intelligence. Never assess an alert in isolation.}

---

## 5. Containment, Eradication & Recovery

The third phase of the NIST Incident Response Lifecycle.

These three steps are interrelated  containment enables eradication, eradication enables recovery.

### Containment
**Goal:** limit and prevent additional damage.

- Defined in the incident response plan for each incident type
- Example for malware on a single machine: **isolate the affected system from the network**  stops spread, limits blast radius
- Containment is the first step toward removing the threat

### Eradication
**Goal:** complete removal of all incident elements from affected systems.

- Actions: vulnerability testing, applying patches to address the exploited weakness
- Ensures the threat is fully purged before systems go back online

### Recovery
**Goal:** return affected systems to normal operations.

Recovery actions include:
- Reimaging affected systems (clean OS install)
- Resetting passwords
- Adjusting network configurations (firewall rules, ACLs)
- Restoring services that were disrupted

> {The lifecycle is cyclical  new discoveries during recovery can send the team back to detection or analysis. Multiple incidents can be active simultaneously and may be related. Document everything as you go the post-incident report depends on it.}

---

## 6. Business Continuity Planning (BCP)

**BCP** = a document outlining procedures to sustain business operations during and after a significant disruption.

Not the same as a **Disaster Recovery Plan** (DRP)  DRP focuses on restoring IT systems after major disasters (floods, hardware failure). BCP focuses on keeping the *business* operational.

### Site resilience (recovery strategy):

| Site type | Readiness | Cost |
|---|---|---|
| **Hot site** | Fully operational duplicate; immediate activation | Highest |
| **Warm site** | Configured but not live; quick to activate | Medium |
| **Cold site** | Basic infrastructure only; needs significant work before operational | Lowest |

**Why it matters:** Ransomware targeting healthcare can cut off access to patient records. Without a BCP, providers can't deliver care. At national scale, attacks on critical infrastructure can undermine public safety and national security.

---

## Key Terms

| Term | Definition |
|---|---|
| Transparency | Documentation creates an accessible audit trail for legal and compliance purposes |
| Standardisation | Repeatable processes documented to ensure consistent quality |
| Chain of custody | Documents evidence possession and control throughout an incident lifecycle |
| Broken chain of custody | Inconsistencies in evidence logging that undermine legal admissibility |
| Playbook | Operational manual providing step-by-step incident response instructions |
| Non-automated playbook | Manual step-by-step actions by an analyst |
| Automated playbook | SIEM/SOAR-triggered automated response actions |
| Semi-automated playbook | Combines analyst judgement with automated tasks |
| Triage | Prioritising alerts and incidents by urgency and impact |
| False positive | Alert incorrectly identifying legitimate activity as malicious |
| Functional impact | Effect of an incident on business operations |
| Information impact | Effect of an incident on data confidentiality, integrity, and availability |
| Recoverability | Whether and how completely systems can be restored after an incident |
| Containment | Limiting and preventing further damage after an incident is detected |
| Eradication | Complete removal of incident elements from affected systems |
| Recovery | Returning affected systems to normal operations |
| BCP | Business Continuity Plan — sustains operations during disruptions |
| Hot site | Fully operational duplicate facility; immediate failover |
| Warm site | Configured but not immediately live |
| Cold site | Basic infrastructure; requires significant setup before use |

---
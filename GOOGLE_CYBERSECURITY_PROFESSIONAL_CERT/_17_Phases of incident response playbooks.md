# Playbooks & Incident Response

---

## 1. What is a Playbook?

A **playbook** is a manual that provides details about any operational action — essentially a predefined, up-to-date list of steps to follow when responding to an incident.

- Ensures **consistency** — same process regardless of who is handling the case
- Comes with a **strategy** (what's expected of team members) and a **plan** (exactly how to execute each task)
- Some playbooks also list the specific individuals responsible for each step

> {Think of a playbook as the SOC's standard operating procedure. Without it, every analyst would handle incidents differently — that inconsistency is a risk in itself.}

### Types of Playbooks:
- Incident response
- Security alerts
- Team-specific
- Product-specific
- Vulnerability response
- Attack-specific (ransomware, vishing, BEC, etc.)

---

## 2. Playbooks are Living Documents

Playbooks are **regularly updated** — they're not set-and-forget. Updates happen when:

- A **failure or oversight** is found in existing procedures
- **Industry standards change** (laws, compliance regulations)
- **Threat actor tactics evolve**

> {A playbook that's 2 years old without updates is a liability. Part of SOC work is knowing when the playbook needs a revision.}

Playbooks are managed **collaboratively** — different team members contribute based on their expertise level.

---

## 3. Incident Response Playbook — 6 Phases

**Incident response** = an org's quick attempt to identify an attack, contain the damage, and correct the effects of a breach.

### Phase 1 — Preparation
- Document procedures, establish staffing plans, educate users
- Create incident response plans outlining roles and responsibilities
- Sets the foundation for everything that follows

### Phase 2 — Detection & Analysis
- Detect and analyse events using defined processes and technology
- Determine **whether** a breach occurred and assess its **magnitude**
- SIEM tools play a key role here — alerts feed into this phase

### Phase 3 — Containment
- **Stop further damage** and reduce immediate impact
- High priority — prevents ongoing risk to critical assets and data
- Actions taken here minimise the blast radius of the incident

### Phase 4 — Eradication & Recovery
- **Complete removal** of incident artifacts (malicious code, compromised accounts, etc.)
- Mitigate the vulnerabilities that were exploited
- Restore affected environment to a secure state — also called **IT restoration**

### Phase 5 — Post-Incident Activity
- Document the incident thoroughly
- Inform organisational leadership
- Apply **lessons learned** to improve future response
- May involve full root cause analysis depending on severity

### Phase 6 — Coordination
- Report incidents and share information throughout the process
- Based on the org's established standards
- Ensures **compliance** with legal/regulatory requirements
- Enables coordinated response and resolution across teams

> {Coordination matters in Australia specifically — mandatory data breach notification under the Privacy Act 1988 means there are legal timelines to hit. The playbook has to account for that.}

---

## 4. How SIEM + Playbooks Work Together

```
SIEM detects threat → generates alert → analyst receives alert
→ analyst consults playbook → structured response begins
```

- SIEM provides the **detection**
- Playbook provides the **response procedure**
- Together they create a structured, efficient, and consistent incident response process

---

## 5. Incident & Vulnerability Response Playbooks

These are the most common playbooks for entry-level analysts. Key points:

- Developed based on the org's **Business Continuity Plan (BCP)** — the established path for recovering and continuing operations after a disruption
- Risk formula: **Risk = Likelihood of threat × potential impact**
- Following playbook steps is critical for **legal compliance** and **forensic integrity**

> {Mishandling data during an incident — even accidentally — can destroy forensic evidence and make it unusable in court or investigations. The playbook keeps you from making costly mistakes under pressure.}

---

## Key Terms

| Term | Definition |
|---|---|
| Playbook | Manual providing predefined steps for operational/security actions |
| Incident Response | Org's process to identify, contain, and recover from a security breach |
| Living Document | A document regularly updated to reflect current standards and threats |
| Business Continuity Plan (BCP) | Plan for recovering operations after a disruption |
| Eradication | Complete removal of incident artifacts and malicious code |
| IT Restoration | Returning affected systems to a secure, operational state |
| Coordination | Reporting and sharing incident information per established standards |
| IOC | Indicator of Compromise — evidence of a potential security breach |

---

## Australian Market Context

- **Privacy Act 1988 & Notifiable Data Breaches (NDB) scheme** — Australian orgs must notify the OAIC and affected individuals within 30 days of a breach. Playbooks must include this notification step in the Coordination phase
- **ASD Essential Eight** alignment: Incident response playbooks map directly to the ASD's guidance on incident detection and response maturity — a mature playbook = higher Essential Eight compliance
- Many Australian government agencies follow **ACSC (Australian Cyber Security Centre)** incident response guidelines — knowing these alongside generic frameworks is a differentiator
- Entry-level SOC analysts in Australia are often tested on playbook knowledge during interviews — being able to name all 6 phases and explain each is baseline expected knowledge

---



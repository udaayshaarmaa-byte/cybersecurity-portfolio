# Course 2 – Module 1: The 8 CISSP Security Domains
---

## What Are the 8 Domains?

CISSP defines **8 security domains** that organize security work, identify gaps, and establish an organization's **security posture** — its ability to defend critical assets and react to change.

| # | Domain | Core Focus |
|---|--------|------------|
| 1 | Security & Risk Management | Goals, risk mitigation, compliance, ethics |
| 2 | Asset Security | Data lifecycle: storage, retention, destruction |
| 3 | Security Architecture & Engineering | Secure design, shared responsibility, zero trust |
| 4 | Communication & Network Security | Protecting data in transit — on-site, remote, cloud |
| 5 | Identity & Access Management (IAM) | Authentication, authorization, least privilege |
| 6 | Security Assessment & Testing | Pen testing, audits, control validation |
| 7 | Security Operations | Incident response, SIEM, forensics — your SOC work |
| 8 | Software Development Security | Secure SDLC, code reviews, penetration testing |

---

## Domain 1 — Security and Risk Management

The foundation of all security work. Defines **what you're protecting**, **why**, and **what rules govern** the protection.

| Area of Focus | What It Means in Practice |
|---|---|
| Security Goals & Objectives | Reduce risks to critical assets — PII, SPII, IP |
| Risk Mitigation | Procedures to quickly reduce impact of a breach or incident |
| Compliance | Internal policies + external regulations (e.g. GDPR, APRA CPS 234) |
| Business Continuity | Disaster recovery plans to keep the org running during incidents |
| Legal & Regulations | Follow jurisdiction-specific laws; ethics minimizes negligence & fraud |
| InfoSec Design Areas | Incident response, vuln mgmt, app security, cloud & infra security |

> 🇦🇺 **ASD Essential Eight:** Risk management underpins the entire Essential Eight. Each control (patching, MFA, app control) is a direct risk mitigation measure. When mapping labs, always reference the risk being mitigated.

---

## Domain 2 — Asset Security

Covers the **full lifecycle of data** — from creation to destruction.

- Covers **PII and SPII** at rest, in transit, and physically collected
- Requires policies for **data lifecycle management** — storage, retention, disposal
- Analysts may oversee **physical destruction of hard drives** to prevent data exposure
- Security impact analysis and recovery plans depend on **asset risk level**

> 🇦🇺 **ASD Essential Eight:** Regular Backups (Control 7) maps directly here. Maintaining secure, tested, and offline backups is a core asset security function.

---

## Domain 3 — Security Architecture and Engineering

Ensures the right **tools, systems, and processes** are in place. Key concept: **Shared Responsibility**.

| Principle | Description |
|---|---|
| Threat Modeling | Proactively identify and address threats during design |
| Least Privilege | Grant only the minimum access required — no more |
| Defense in Depth | Multiple layers so no single failure is catastrophic |
| Fail Securely | Systems default to a secure state when something breaks |
| Separation of Duties | No single person controls an entire critical process |
| Zero Trust | Never trust, always verify — even inside the network |
| Trust but Verify | Verify even trusted entities before granting access |
| Keep It Simple | Complex systems create more attack surface |

> 🇦🇺 **ASD Essential Eight:** Least Privilege maps to Restrict Administrative Privileges (Control 5). Zero Trust reinforces this. Defense in Depth is the philosophy behind the Essential Eight framework as a whole.

---

## Domain 4 — Communication and Network Security

Manages and secures **physical and wireless networks** across all environments.

- Protects data in transit — wired, wireless, cloud
- **Remote workers** face risks from insecure Bluetooth and public Wi-Fi
- Security teams can **restrict insecure channel access** at the organizational level
- Hybrid work environments make this domain increasingly complex

> 🇦🇺 **ASD Essential Eight:** Restricting untrusted channels supports Application Control (Control 1) and Restrict Admin Privileges (Control 5).

---

## Domain 5 — Identity and Access Management (IAM)

Ensures only the **right people access the right things**, governed by **Least Privilege**.

| IAM Component | Description | Example |
|---|---|---|
| Identification | User claims an identity | Username, access card, fingerprint |
| Authentication | Identity is verified | Password, PIN, biometric scan |
| Authorization | Access level is granted | Role-based access to specific systems |
| Accountability | Actions are monitored & logged | Login attempts, file access logs |

> 🇦🇺 **ASD Essential Eight:** Maps directly to Multi-Factor Authentication (Control 6) and Restrict Administrative Privileges (Control 5).

---

## Domain 6 — Security Assessment and Testing

Validates that **security controls actually work**.

- **Security control testing** — do controls actually achieve the stated goals?
- **Penetration testing** — ethical hackers simulate attacks to find weaknesses
- **Security audits** — monitor and reduce probability of data breaches
- **User permission audits** — validate access levels are correct and minimal

> 🇦🇺 **ASD Essential Eight:** Vulnerability scanning supports Patch Applications (Control 2) and Patch Operating Systems (Control 3).

---

## Domain 7 — Security Operations

**Your primary domain as a SOC analyst.**

### Key SOC Activities
- Training and awareness | Reporting and documentation
- Intrusion detection and prevention | SIEM tools
- Log management | Incident management | Playbooks
- Post-breach forensics | Lessons learned reviews

### Incident Response Flow

| # | Phase | Action |
|---|---|---|
| 1 | Detect | Incident identified — raise alert |
| 2 | Contain | Active attack — mitigate, prevent escalation |
| 3 | Collect | Threat neutralized — gather digital & physical evidence |
| 4 | Analyse | Forensic investigation — when, how, why? |
| 5 | Improve | Identify gaps — implement preventative measures |

> 🇦🇺 **ASD Essential Eight:** SIEM and log management support all detection capabilities. Post-breach forensics aligns with Maturity Level 3.

---

## Domain 8 — Software Development Security

Security must be **baked into every phase of the SDLC**.

| SDLC Phase | Security Activity | Who's Involved |
|---|---|---|
| Design | Secure design review — threat model the architecture | Architect, Security |
| Development | Secure code review — identify vulnerable patterns | Dev team, Security |
| Testing | Secure code review + QA testing | QA, Pen testers |
| Deployment | Penetration testing — simulate real-world attacks | Pen testers, Security |

> 🇦🇺 **ASD Essential Eight:** Secure coding supports Application Control (Control 1) and User Application Hardening (Control 8).

---

## ASD Essential Eight — Full Domain Mapping

| Essential Eight Control | Domain(s) | Why It Maps |
|---|---|---|
| 1. Application Control | D4, D7, D8 | Enforced at network, ops, and dev levels |
| 2. Patch Applications | D6 | Assessment identifies unpatched apps as vulnerabilities |
| 3. Patch Operating Systems | D6 | OS patching is a control validation activity |
| 4. Configure MS Office Macro Settings | D3 | System hardening and config management |
| 5. Restrict Admin Privileges | D3, D5 | Least privilege (D3) enforced via IAM (D5) |
| 6. Multi-Factor Authentication | D5 | MFA is an authentication control — IAM's core |
| 7. Regular Backups | D2 | Backup is part of asset retention and recovery |
| 8. User Application Hardening | D3, D4 | Secure design and network controls enforce this |

---

## Key Terms

| Term | Definition |
|---|---|
| Security Posture | Org's ability to manage defense of critical assets and react to change |
| PII | Personally Identifiable Information |
| SPII | Sensitive PII — financial, medical, or biometric data |
| IAM | Identity and Access Management |
| Least Privilege | Grant only the minimum access required to complete a task |
| Shared Responsibility | All individuals in an org take an active role in lowering risk |
| SDLC | Software Development Lifecycle |
| Penetration Testing | Simulated attacks by ethical hackers to find vulnerabilities |
| SIEM | Security Information and Event Management tool |
| Defense in Depth | Layered security so no single failure compromises the whole system |
| Zero Trust | Never assume trust — verify every user, device, and request |

---

## SOC Analyst Perspective

Domain 7 is your daily reality — SIEM, log review, incident triage, playbooks, forensics. But understanding all 8 gives you context. When writing incident reports, cite which domains are in play: an auth bypass touches Domain 5 (IAM) **and** Domain 7 (Ops). That framing shows maturity most entry-level candidates don't demonstrate.

---

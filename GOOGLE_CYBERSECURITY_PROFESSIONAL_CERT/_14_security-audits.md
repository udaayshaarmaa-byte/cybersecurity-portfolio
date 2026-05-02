# Security Audits
---
## 1. What Is a Security Audit?

A **security audit** is a review of an organization's security controls, policies, and procedures against a set of expectations.

Audits evaluate whether an organization is meeting:

| Criteria Type | Examples |
|---|---|
| **Internal** | Organizational policies, procedures, and best practices |
| **External** | Regulatory compliance, laws, federal regulations |

> **Key Purpose:** Audits ensure IT practices meet industry and organizational standards, identify failures, and develop a plan to correct them. They also help organizations avoid fines and penalties from governing agencies.

---

## 2. Types of Security Audits

### External Audits
- Conducted by an **independent third party**
- Assesses compliance with external regulations and standards
- Often required by law or regulation (e.g., financial institutions, healthcare)

### Internal Audits
- Conducted by an **internal team** — typically includes the compliance officer, security manager, and other security team members
- Used to improve security posture and identify gaps **before** external auditors do
- Entry-level analysts are most likely to **contribute to internal audits**

**Internal audits help organizations:**
- Identify organizational risk
- Assess the effectiveness of current controls
- Correct compliance issues proactively

---

## 3. Factors That Affect Audits

The type, scope, and frequency of audits an organization conducts depends on:

- **Industry type** — healthcare, finance, government all have different requirements
- **Organization size** — larger organizations have more assets and more complex audit requirements
- **Government regulation ties** — regulated industries face mandatory audit schedules
- **Geographical location** — different laws apply depending on where the business operates (e.g., GDPR in EU, Privacy Act in Australia)
- **Chosen compliance frameworks** — organizations that voluntarily adopt ISO 27001 or NIST CSF may structure audits around those

---

## 4. The Five Elements of an Internal Security Audit

```
1. Establish Scope & Goals
        ↓
2. Conduct Risk Assessment
        ↓
3. Complete Controls Assessment
        ↓
4. Assess Compliance
        ↓
5. Communicate Results to Stakeholders
```

---

## 5. Element 1 — Establish Scope & Goals

### Scope
Defines the **specific criteria** of the audit — what will be examined.

Scope includes identifying:
- People (roles, access levels)
- Assets (hardware, software, data)
- Policies and procedures
- Technologies currently in use

**Example scope:**
- Assess all user permissions
- Identify existing controls, policies, and procedures
- Account for all technology in use by the organization

### Goals
Define what the organization wants to **achieve** through the audit — the desired security posture outcome.

**Example goals:**
- Implement core NIST CSF functions
- Establish policies and procedures to ensure compliance
- Strengthen system controls

> **Analyst role:** Senior staff typically set scope and goals. Entry-level analysts review and understand them to inform their contributions to the remaining elements.

---

## 6. Element 2 — Conduct a Risk Assessment

A **risk assessment** identifies potential threats, risks, and vulnerabilities to the organization's assets.

**Purpose:** Determine what security measures need to be implemented or improved.

**What a risk assessment examines:**
- Budget constraints on security investment
- Effectiveness of current controls
- Internal processes and their weaknesses
- External compliance standards that apply

**Example findings from a risk assessment:**
- Inadequate controls to protect physical and digital assets
- Employee equipment not properly secured
- Access to private data on the internal network lacks robust controls

> **Analyst role:** Risk assessments are typically completed by managers or senior stakeholders. Entry-level analysts are asked to **analyze the findings** and determine what controls and compliance regulations should be put in place.

---

## 7. Element 3 — Complete a Controls Assessment

A controls assessment involves **closely reviewing existing assets**, evaluating potential risks, and determining whether current controls are effective.

### Three Categories of Controls

| Category | Description | Examples |
|---|---|---|
| **Administrative / Managerial** | Human component — policies and procedures governing how data is managed | Password policies, separation of duties, employee training |
| **Technical** | Hardware and software solutions | Firewalls, IDS/IPS, encryption, MFA, antivirus |
| **Physical** | Measures preventing unauthorized physical access | CCTV, locks, access badges, security guards |

### Controls Assessment Questions to Ask
- What is the audit meant to achieve?
- Which assets are most at risk?
- Are current controls sufficient to protect those assets?
- If not, what controls and compliance regulations need to be implemented?

---

## 8. Element 4 — Assess Compliance

Determine whether the organization is **adhering to all applicable compliance regulations**.

**Compliance regulations** = laws that organizations must follow to keep private data secure.

### Common Regulations by Context

| Regulation | Applies To |
|---|---|
| **GDPR** | Organizations handling data of EU citizens |
| **PCI DSS** | Organizations that accept, process, or store credit card payments |
| **HIPAA** | U.S. healthcare organizations handling patient data |
| **Privacy Act 1988** | Australian organizations handling personal information |
| **Australian Privacy Principles (APPs)** | Governs how Australian entities collect, store, and use personal data |
| **Notifiable Data Breaches (NDB) Scheme** | Requires Australian organizations to notify individuals of eligible data breaches |

**Example:**  
An organization operating in the EU that accepts credit card payments must comply with **both GDPR and PCI DSS**.

> **Australian Market Note:** If you're working in Australia, the Privacy Act 1988, APPs, and NDB Scheme are your primary compliance baseline — equivalent to what HIPAA or GDPR is in other jurisdictions. Always map audit findings to these where relevant.

---

## 9. Element 5 — Communicate Results to Stakeholders

The final step is delivering a **clear, actionable report** to stakeholders.

### What the Communication Should Include

| Section | Content |
|---|---|
| **Scope & Goals Summary** | Restate what the audit covered and what it aimed to achieve |
| **Existing Risks** | List identified risks and how urgently they need to be addressed |
| **Compliance Gaps** | Identify which regulations the organization is not currently meeting |
| **Recommendations** | Specific improvements to controls, policies, and procedures |

> **Communication principle:** Results should be clear enough for non-technical stakeholders (executives, legal teams, board members) to understand the risk and make informed decisions.

---

## 10. Audit Checklist — Summary

Before and during an internal audit, work through the following:

- [ ] **Scope defined** — assets, people, policies, technologies listed
- [ ] **Goals documented** — what the audit aims to achieve
- [ ] **Audit frequency established** — based on regulations and business risk
- [ ] **Risk assessment completed** — threats, risks, and vulnerabilities identified
- [ ] **Controls assessed** — administrative, technical, and physical controls reviewed
- [ ] **Compliance checked** — all applicable regulations identified and assessed
- [ ] **Mitigation plan created** — strategy to lower risk and address gaps
- [ ] **Results communicated** — report delivered to stakeholders with clear recommendations

---

## 11. Role of Frameworks in Audits

Frameworks help organizations **prepare for and structure** security audits.

| Framework | Audit Relevance |
|---|---|
| **NIST CSF v2.0** | Provides the Govern → Identify → Protect → Detect → Respond → Recover structure for evaluating security maturity |
| **ISO/IEC 27001** | Defines requirements for an ISMS — directly maps to audit criteria |
| **ASD Essential Eight** | Used as an audit baseline in Australian government and critical infrastructure assessments |

> Using established frameworks saves time during audits — controls and policies are already mapped to compliance requirements, reducing gaps.

---

## 12. Real-World Example — Password Audit

**Scenario:** An internal security team conducts a password audit.

| Audit Element | What Happened |
|---|---|
| Scope | All user accounts and password policies |
| Risk Assessment | Identified weak password practices across the organization |
| Controls Assessment | Existing password policy was not enforced or monitored |
| Compliance | Weak passwords violate minimum security standards |
| Communication | Findings reported to compliance team |
| Outcome | Compliance team enforced stricter password policies organization-wide |

> **Lesson:** Audits create accountability. A finding without communication and a mitigation plan has no impact.

---

## 13. ASD Essential Eight Mapping

| Audit Element | ASD Essential Eight Alignment |
|---|---|
| Controls Assessment — Technical | Patch Applications, Patch OS, Application Control, MFA |
| Controls Assessment — Administrative | Restrict Administrative Privileges |
| Controls Assessment — Physical | Supports overall hardening posture |
| Compliance Assessment | All Eight controls are baseline compliance for Australian government entities |
| Risk Assessment | Informs which Essential Eight Maturity Level the organization is at |

---

## 14. Key Takeaways

- A security audit reviews controls, policies, and procedures against internal and external expectations
- **Internal audits** are where entry-level analysts contribute — especially in controls assessment and analysis
- The five elements: **Scope & Goals → Risk Assessment → Controls Assessment → Compliance → Communication**
- Controls are classified as **administrative, technical, or physical**
- Compliance requirements vary by industry, geography, and chosen frameworks
- In Australia: **Privacy Act 1988, APPs, NDB Scheme** are your compliance anchors
- Audits are how all the frameworks, controls, and principles you've learned actually get **applied and verified**

---

## 15. Quick Reference — Terminology

| Term | Definition |
|---|---|
| Security Audit | Review of controls, policies, and procedures against a set of expectations |
| Internal Audit | Audit conducted by internal team to improve posture and fix compliance gaps |
| External Audit | Independent third-party audit assessing regulatory compliance |
| Scope | Specific criteria of the audit — what assets, people, and systems are being assessed |
| Goals | What the organization wants to achieve through the audit |
| Risk Assessment | Evaluation of threats, risks, and vulnerabilities affecting organizational assets |
| Controls Assessment | Review of existing controls to determine if they adequately protect assets |
| Mitigation Plan | Strategy to lower the level of risk identified during an audit |
| Compliance | Adherence to applicable laws, regulations, and standards |
| GDPR | General Data Protection Regulation — EU data privacy law |
| PCI DSS | Payment Card Industry Data Security Standard — applies to card payment processors |
| NDB Scheme | Notifiable Data Breaches — Australian mandatory breach notification requirement |

---
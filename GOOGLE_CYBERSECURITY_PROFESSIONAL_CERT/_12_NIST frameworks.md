# NIST Frameworks — CSF, RMF & SP 800-53

> **Author:** Uday Sharma | **Updated:** May 2026  
> **Source:** Google Cybersecurity Certificate — Course 1  
> **Purpose:** Understanding NIST frameworks used to manage cybersecurity risk across all organization types.

---

## 1. What Is NIST?

**NIST = National Institute of Standards and Technology**

- A U.S.-based organization that creates cybersecurity frameworks and guidelines
- Although U.S.-based, its guidance is used by security professionals **worldwide**
- Applies to: for-profit businesses, nonprofits, and government agencies

---

## 2. NIST Cybersecurity Framework (CSF)

### What It Is
- A **voluntary framework** consisting of standards, guidelines, and best practices
- Designed to help organizations **manage cybersecurity risk**
- Widely respected and relevant regardless of the organization or country
- Current version: **CSF v2.0** — adds a new Govern function and greater emphasis on **supply chain risk management**

### Six Core Functions (CSF v2.0)

```
         GOVERN (Overarching)
            |
IDENTIFY → PROTECT → DETECT → RESPOND → RECOVER
(Proactive)                              (Reactive)
```

| # | Function | Purpose |
|---|---|---|
| 0 | **Govern** | Establish and monitor cybersecurity risk management strategy, policies, and accountability across the organization |
| 1 | **Identify** | Manage cybersecurity risk and understand its effect on people and assets |
| 2 | **Protect** | Implement policies, procedures, training, and tools to mitigate threats |
| 3 | **Detect** | Identify potential security incidents and improve monitoring capabilities |
| 4 | **Respond** | Contain, neutralize, and analyze incidents — implement process improvements |
| 5 | **Recover** | Return affected systems to normal operation after an incident |

> **Key Insight:** Govern sits above all other functions — it's the foundation that ensures leadership accountability and organizational-wide cybersecurity strategy. The remaining five functions cover the **full incident lifecycle** — from before an incident happens (Identify, Protect) to during (Detect, Respond) to after (Recover).

---

## 3. The Six Functions — Deep Dive

### 3.0 Govern *(New in CSF v2.0)*
- Establishes the **cybersecurity risk management strategy, expectations, and policy** across the entire organization
- Ensures leadership and the board are accountable for cybersecurity decisions
- Covers: organizational context, risk management strategy, cybersecurity policy, roles & responsibilities, oversight
- Also emphasizes **supply chain risk management** — vetting third-party vendors, software, and hardware for security risks
- **Analyst task example:** Ensure security policies are documented, up to date, and aligned with business risk appetite
- Govern is **overarching** — it informs and supports all other five functions

> **Why Supply Chain?** CSF v2.0 added supply chain risk management because modern attacks increasingly target vendors and third parties (e.g., SolarWinds attack). If your supplier is compromised, so are you.

### 3.1 Identify
- Monitor systems and devices in the internal network
- Identify potential security issues **before** they become incidents
- Includes: asset management, risk assessment, understanding the attack surface
- **Analyst task example:** Review internal network for anomalous devices or unauthorized access

### 3.2 Protect
- Implement policies, procedures, training, and security tools
- Study historical attack data to improve defenses
- Includes: access control, employee training, data security, patch management
- **Analyst task example:** Study past attack patterns and update security policies to close gaps

### 3.3 Detect
- Identify potential security incidents in real time
- Improve **speed and efficiency** of detections
- Includes: setting up monitoring tools, configuring alert thresholds (low / medium / high risk)
- **Analyst task example:** Configure a SIEM or security tool to correctly flag and alert on suspicious behavior

### 3.4 Respond
- Contain and neutralize security incidents
- Collect and organize data to document what happened
- Suggest process improvements to prevent recurrence
- Includes: incident response plans, communication procedures, forensic analysis
- **Analyst task example:** Document an incident in detail — who, what, where, when, how — and recommend improvements

### 3.5 Recover
- Restore affected systems, data, and assets to normal operation
- Minimize downtime and business disruption
- Includes: restoring backups, rebuilding systems, post-incident reviews
- **Analyst task example:** Work with the team to restore financial or legal files affected by a breach

---

## 4. Real-World Incident Walkthrough (USB Attack)

> **Scenario:** A high-risk notification fires — a workstation has been compromised. An unknown device is plugged into it.

| CSF Function | Action Taken |
|---|---|
| **Govern** | USB port policy exists (or should exist) — supply chain risk policy covers personal device usage |
| **Identify** | Monitor systems → detect compromised workstation → find unknown USB device plugged in |
| **Protect** | Remotely block the unknown device → prevent further threat spread |
| **Detect** | Remove infected workstation → use tools to detect additional threat actor behavior |
| **Respond** | Investigate: who used the device, how the threat occurred, what was affected, where it originated. Root cause: employee charging infected phone via USB port |
| **Recover** | Restore any affected files/data → repair damage to the workstation |

> **Lesson:** This is a **supply chain / physical security incident**. The threat entered through a personal device, not the network. Physical access controls and endpoint policies (blocking USB ports) are key preventive controls here.

---

## 5. NIST SP 800-53

### What It Is
- **Special Publication 800-53** — an extension of NIST CSF specifically for the **U.S. federal government**
- Provides a **unified framework** for protecting information systems used by the federal government
- Includes systems provided by **private companies** operating on behalf of the federal government
- Security controls within SP 800-53 are designed to maintain the **CIA Triad**

### When It Matters to You
- Essential knowledge if you pursue roles with U.S. government contractors, federal agencies, or defence-related organizations
- In Australia: comparable framework is the **Australian Government Information Security Manual (ISM)** published by ASD — same concept, different jurisdiction

---

## 6. NIST CSF vs. SP 800-53

| Feature | NIST CSF | NIST SP 800-53 |
|---|---|---|
| **Scope** | All organizations worldwide | U.S. federal government + contractors |
| **Voluntary?** | Yes | Mandatory for federal agencies |
| **Focus** | Risk management framework (6 functions in v2.0) | Specific security controls catalog |
| **CIA Triad** | Supports all three principles | Directly designed to maintain CIA Triad |
| **Audience** | All security professionals | Federal IT and security teams |
| **Latest version** | CSF v2.0 (adds Govern + supply chain focus) | SP 800-53 Rev 5 |

---

## 7. Proactive vs. Reactive Functions

| Type | Functions | Focus |
|---|---|---|
| **Governance** | Govern | Set strategy, policy, accountability, supply chain risk |
| **Proactive** | Identify, Protect | Prevent incidents before they happen |
| **Reactive** | Detect, Respond, Recover | Minimize damage once an incident occurs |

> **Analyst Mindset:** You need both. No organization can prevent 100% of attacks. The question is: **how fast can you detect, respond, and recover?** This is what separates mature security programs from weak ones.

---

## 8. ASD Essential Eight Mapping

| NIST CSF Function | ASD Essential Eight Alignment |
|---|---|
| **Govern** | All Eight controls — governance ensures policies exist for each control; supply chain risk maps to vendor vetting practices |
| **Identify** | Application Control (know what's running), Patch management (know what's vulnerable) |
| **Protect** | MFA, Restrict Administrative Privileges, Application Control, Patch Applications/OS |
| **Detect** | User Application Hardening, logging and monitoring (underpins detection) |
| **Respond** | Incident response procedures (supported by all Essential Eight controls) |
| **Recover** | **Regular Backups** — direct Essential Eight control (Maturity Level 1–3) |

> **Portfolio Note:** When writing SOC-style incident reports in your labs, structure them using the six NIST CSF v2.0 functions as headers. It signals framework fluency and maps directly to how real SOC teams document incidents.

---

## 9. Key Takeaways

- NIST CSF is **voluntary**, globally respected, and applies to any organization
- **CSF v2.0** adds a **Govern** function and increased focus on **supply chain risk management**
- The six functions — **Govern, Identify, Protect, Detect, Respond, Recover** — cover the complete security lifecycle
- Security incidents **will** happen — an organization's strength lies in how fast it recovers
- NIST SP 800-53 extends the CSF specifically for **U.S. federal systems** and contractors
- All NIST frameworks tie back to maintaining the **CIA Triad**
- In Australia, the equivalent to SP 800-53 is the **ASD Information Security Manual (ISM)**

---

## 10. Quick Reference — Terminology

| Term | Definition |
|---|---|
| NIST | National Institute of Standards and Technology — U.S. standards body |
| CSF | Cybersecurity Framework — voluntary risk management framework; v2.0 has 6 core functions |
| CSF v2.0 | Latest version of CSF — adds Govern function and supply chain risk management emphasis |
| SP 800-53 | NIST Special Publication — security controls for U.S. federal information systems |
| Govern | CSF v2.0 function: set strategy, policy, accountability, and manage supply chain risk |
| Identify | CSF function: manage risk and understand assets/people affected |
| Protect | CSF function: implement controls, policies, and training |
| Detect | CSF function: monitor and identify potential incidents |
| Respond | CSF function: contain, neutralize, and document incidents |
| Recover | CSF function: restore systems and data to normal operation |
| Supply Chain Risk | Risk introduced through third-party vendors, software, or hardware — emphasized in CSF v2.0 |
| ISM | Australian Government Information Security Manual — ASD's equivalent to SP 800-53 |

---

*These notes are part of Uday Sharma's cybersecurity learning portfolio — Google Cybersecurity Certificate, Course 1.*

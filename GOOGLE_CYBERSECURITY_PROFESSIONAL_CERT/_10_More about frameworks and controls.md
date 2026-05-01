# Security Frameworks & Controls


---

## 1. What Are Security Frameworks?

Security frameworks are **guidelines used for building plans** to help mitigate risks, threats, and vulnerabilities to data and privacy.

### Why Frameworks Exist
- Help organizations **comply with laws and regulations** (e.g., HIPAA, GDPR)
- Provide a **starting point** for building internal security policies and processes
- Cover both **virtual** (network, data) and **physical** (building access, CCTV) security
- Help organizations **educate employees** — because people are the biggest threat to security

> **Key Insight:** Frameworks are typically **voluntary**, but organizations are strongly encouraged to adopt them. Non-compliance often leads to financial penalties and reputational damage.

---

## 2. Key Frameworks

### 2.1 NIST Risk Management Framework (RMF)
A structured process for integrating security and risk management across an organization's lifecycle.  
→ Covered separately in NIST module notes.

### 2.2 NIST Cybersecurity Framework (CSF)
Five core functions: **Identify → Protect → Detect → Respond → Recover**  
→ Covered separately in NIST module notes.

### 2.3 Cyber Threat Framework (CTF)
- Developed by the **U.S. government** (Office of the Director of National Intelligence)
- Provides a **common language** for describing and communicating cyber threat activity
- Helps analysts **share threat intelligence** efficiently across organizations and agencies
- Improves response to evolving threat actor **tactics and techniques**

### 2.4 ISO/IEC 27001
- Internationally recognized standard from the **International Organization for Standardization (ISO)** and **International Electrotechnical Commission (IEC)**
- Part of the **ISO 27000 family** of standards
- Applies to organizations of **all sizes and sectors**
- Outlines requirements for an **Information Security Management System (ISMS)**
- Does **not mandate specific controls** — but provides a collection of controls organizations can adopt
- Covers: financial information, intellectual property, employee data, third-party data

---

## 3. What Are Security Controls?

Security controls are **safeguards designed to reduce specific security risks**.

Controls work **alongside frameworks** — the framework sets the plan, controls are the actual measures that execute it.

### Control Goals
| Goal | Description |
|---|---|
| **Prevent** | Stop a security incident before it happens |
| **Detect** | Identify that an incident is occurring or has occurred |
| **Correct** | Fix the issue and restore normal operations after an incident |

---

## 4. Types of Controls

### 4.1 Physical Controls
Protect the **physical environment** from unauthorized access.

| Example | Purpose |
|---|---|
| Gates, fences, locks | Perimeter access restriction |
| Security guards | Human monitoring and response |
| CCTV, surveillance cameras, motion detectors | Physical monitoring and evidence collection |
| Access cards / badges | Identity-based entry to office spaces |

### 4.2 Technical Controls
Use **technology** to enforce security policies.

| Example | Purpose |
|---|---|
| Firewalls | Filter network traffic based on rules |
| Multi-Factor Authentication (MFA) | Verify identity using multiple factors |
| Antivirus software | Detect and remove malicious software |
| Encryption | Protect data confidentiality |

### 4.3 Administrative Controls
**Policies and procedures** that govern how people interact with systems and data.

| Example | Purpose |
|---|---|
| Separation of duties | Prevent a single person from having too much access/power |
| Authorization policies | Define who can access what resources |
| Asset classification | Categorize data by sensitivity to apply appropriate controls |
| Employee training | Reduce human error and social engineering susceptibility |

---

## 5. Three Critical Technical Controls (Deep Dive)

### 5.1 Encryption
- Process of converting data from **plaintext → ciphertext**
- Ciphertext is unreadable to humans and computers until decrypted
- Used to ensure **confidentiality** of sensitive data (e.g., customer accounts, SSNs)
- Core component of the **CIA Triad — Confidentiality**

```
Plaintext  →  [Encryption Algorithm]  →  Ciphertext
Ciphertext →  [Decryption + Key]      →  Plaintext
```

### 5.2 Authentication
- Process of **verifying who someone or something is**
- Levels of authentication:

| Level | Example |
|---|---|
| Basic | Username + Password |
| MFA | Password + OTP / security code |
| Biometrics | Fingerprint, face scan, eye scan, palm scan |

**Biometrics Risk — Vishing:**
- **Vishing** = Voice phishing; exploits electronic voice communication
- Can be used to **impersonate someone's voice** to steal identity and commit fraud
- Highlight: Even biometrics can be socially engineered

### 5.3 Authorization
- Process of **granting access to specific resources** after identity is verified
- Authentication asks: *Who are you?*
- Authorization asks: *What are you allowed to do?*
- Example: A federal entry-level analyst may be authenticated into a system but only **authorized** to view certain classified datasets

> **Authentication ≠ Authorization.**  
> You can be authenticated (identity confirmed) but still denied access (not authorized).

---

## 6. Framework + Controls: How They Work Together

```
FRAMEWORK                          CONTROLS
(The Plan)                         (The Execution)
─────────────────                  ─────────────────
ISO 27001 / NIST CSF  ──────────►  MFA, Encryption, Firewalls
HIPAA Compliance      ──────────►  Access cards, Audit logs, MFA
Employee Safety Plan  ──────────►  CCTV, Security guards, Badges
```

**Real-world example:**  
A hospital uses **HIPAA** (regulation) → adopts **NIST CSF** (framework) → implements **MFA + encryption + audit logging** (controls) → patients' data is protected.

---

## 7. ASD Essential Eight Mapping

| Framework/Control | Essential Eight Alignment |
|---|---|
| MFA | **Multi-Factor Authentication** (direct match — Maturity Level 1–3) |
| Authorization / Least Privilege | **Restrict Administrative Privileges** |
| Application whitelisting | **Application Control** |
| Antivirus / Patching | **Patch Applications / Patch Operating Systems** |
| Encryption | **Encrypt Sensitive Data** (supports all levels) |
| Audit logs + monitoring | **User Application Hardening + logging** |

> **Australia Note:** The ASD Essential Eight is Australia's government-recommended baseline. When you document controls in your portfolio, always map them to Essential Eight where possible — it shows employer-ready thinking for the Australian job market.

---

## 8. Social Engineering & the Human Factor

Frameworks specifically address **human vulnerabilities** because people are the biggest threat vector.

| Attack Type | Description | Relevant Control |
|---|---|---|
| **Phishing** | Fake emails tricking users into revealing credentials | Employee training, Email filtering |
| **Vishing** | Voice-based impersonation to extract sensitive info | MFA, Identity verification procedures |
| **Trespassing** | Unauthorized physical access | Access badges, Security guards, CCTV |
| **Fake employee accounts** | Identity fraud to gain system access | Authorization policies, Separation of duties |

---

## 9. Key Takeaways

- **Frameworks** = the plan and guidelines (strategic layer)
- **Controls** = the actual safeguards in place (tactical layer)
- Controls are **physical, technical, or administrative**
- Controls aim to **prevent, detect, or correct** security issues
- Every control maps back to protecting the **CIA Triad** (Confidentiality, Integrity, Availability)
- In Australia, always align controls with the **ASD Essential Eight**

---

## 10. Quick Reference — Terminology

| Term | Definition |
|---|---|
| Framework | Guidelines for building security plans |
| Control | Safeguard that reduces a specific risk |
| Encryption | Converting plaintext to ciphertext |
| Authentication | Verifying identity |
| Authorization | Granting access to resources |
| MFA | Multi-factor authentication — requires 2+ verification factors |
| Biometrics | Physical characteristics used for identity verification |
| Vishing | Voice-based phishing attack |
| ISMS | Information Security Management System (ISO 27001 core concept) |
| CTF | Cyber Threat Framework — common language for threat communication |
| ISO/IEC 27001 | International standard for information security management |

---*

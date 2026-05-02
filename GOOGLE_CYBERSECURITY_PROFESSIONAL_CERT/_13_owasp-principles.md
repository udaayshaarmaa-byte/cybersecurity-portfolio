# OWASP Security Principles
---

## 1. What Is OWASP?

**OWASP = Open Worldwide Application Security Project**  
*(Previously: Open Web Application Security Project)*

- A nonprofit foundation that publishes security guidelines, tools, and best practices
- Freely available to everyone — widely used by developers and security professionals globally
- Best known for the **OWASP Top 10** (most critical web application security risks)
- The principles below are embedded in everyday analyst work — log analysis, SIEM monitoring, vulnerability scanning, and more

---

## 2. The Ten OWASP Security Principles

### 2.1 Minimize Attack Surface Area

**Attack surface** = all potential vulnerabilities a threat actor could exploit.  
**Attack vectors** = the specific pathways attackers use to penetrate defenses.

Common attack vectors:
- Phishing emails
- Weak passwords
- Unpatched software
- Exposed APIs or open ports

**How to minimize it:**
- Disable unused software features
- Restrict access to sensitive assets
- Enforce complex password requirements
- Close unnecessary network ports
- Remove or decommission unused systems

> **Analyst mindset:** Every feature, service, or account that exists is a potential entry point. Less surface = less risk.

---

### 2.2 Principle of Least Privilege

Users should have the **minimum access required** to perform their job — nothing more.

**Why it matters:**
- Limits the blast radius of a compromised account
- Reduces insider threat risk
- Prevents accidental or deliberate misuse of access

**Example:**  
As an entry-level analyst, you may have read access to log data but no ability to change user permissions. If your credentials are stolen, the attacker can only access what you could — limiting their ability to execute an attack.

| Role | Access Granted | Access Denied |
|---|---|---|
| Entry-level analyst | View logs, SIEM alerts | Modify user permissions |
| HR staff | Employee records | Financial systems |
| Developer | Code repository | Production database |

> **Ties to:** Separation of Duties, Defense in Depth, CIA Triad (Confidentiality)

---

### 2.3 Defense in Depth

An organization should have **multiple, layered security controls** that address risks in different ways. No single control is enough.

**The idea:** A threat actor must bypass multiple independent defenses to reach the target.

```
Internet → Firewall → IDS/IPS → MFA → Role-based Access → Encryption → Data
           Layer 1    Layer 2   Layer 3      Layer 4          Layer 5
```

**Examples of controls at each layer:**

| Layer | Control |
|---|---|
| Perimeter | Firewall, DDoS protection |
| Network | Intrusion Detection System (IDS), VPN |
| Endpoint | Antivirus, EDR, patch management |
| Application | MFA, input validation, WAF |
| Data | Encryption, access controls, backups |
| Human | Security awareness training |

> **ASD Essential Eight alignment:** The Essential Eight is itself a defense-in-depth strategy — eight independent controls that collectively raise the cost of an attack.

---

### 2.4 Separation of Duties

**Critical actions should require multiple people** — no single person should have enough privilege to carry out a harmful or fraudulent action alone.

**Classic example:**  
The person who *prepares* paychecks should not also be the person who *approves* them.

**Security examples:**
- A developer should not be able to deploy code to production without a second reviewer
- An admin who creates accounts should not also have the ability to audit those accounts
- Access to sensitive data should require approval from a second team

> **Why it matters:** Prevents insider fraud, limits the damage of a single compromised account, and creates accountability trails.

---

### 2.5 Keep Security Simple

Avoid unnecessarily complex security solutions. **Complexity is the enemy of security.**

- Complex systems are harder to understand, maintain, and audit
- Overly complicated controls lead to misconfigurations
- Hard-to-use security tools get bypassed or ignored by users
- Simple, well-understood controls are more reliably enforced

> **Real-world example:** A complex custom-built authentication system is riskier than using a well-tested standard like OAuth 2.0 — even if the custom system seems more sophisticated.

---

### 2.6 Fix Security Issues Correctly

When a security incident occurs, the goal is not just to patch the symptom — it's to **fix the root cause**.

**The process:**
1. Identify the **root cause** of the vulnerability
2. **Contain** the impact — stop the bleeding
3. **Remediate** — apply the actual fix
4. **Test** — verify the fix works and hasn't introduced new vulnerabilities
5. **Document** — record what happened, what was done, and what changed

**Example:**  
Weak WiFi password → breach risk.  
Wrong fix: Change the password.  
Right fix: Implement a strong password policy, enforce WPA3, add network monitoring.

> **Analyst task:** After every incident, write a post-incident report that captures root cause and remediation steps. This is a core SOC skill.

---

### 2.7 Establish Secure Defaults

The **default state** of any system or application should be its **most secure state**.

- Users should have to deliberately take action to make something less secure
- Security should not rely on users making the right configuration choice

**Examples:**
- Default: MFA enabled → User must opt-out (not opt-in)
- Default: Firewall blocks all → Specific rules required to allow traffic
- Default: Least privilege access → Elevated access requires a request

> **Contrast:** Many legacy systems shipped with security OFF by default — requiring admins to harden them. Secure defaults flip this model.

---

### 2.8 Fail Securely

When a security control **fails or stops working**, it should default to its **most secure state** — not open everything up.

**Example:**
- Firewall fails → should **block all connections**, not allow all traffic
- Authentication service goes down → should **deny access**, not bypass login
- Encryption module fails → should **stop transmitting data**, not send in plaintext

> **Why it matters:** In an outage or attack scenario, a failing-open system becomes an instant vulnerability. Failing secure limits damage during failure.

---

### 2.9 Don't Trust Services

Organizations frequently work with **third-party partners** — and those partners may have weaker security policies.

**Never assume a partner's system is secure.**

**Example:**  
If a third-party vendor tracks airline reward points, the airline should **independently verify** the balance before displaying it to customers. Blindly trusting external data could expose customers to fraud.

**Practical controls:**
- Validate all data received from third parties
- Apply the principle of least privilege to third-party integrations
- Review vendor security posture regularly
- Use contracts that enforce minimum security standards (e.g., SOC 2 compliance)

> **CSF v2.0 link:** Supply chain risk management — introduced in NIST CSF v2.0 — directly addresses this principle at the governance level.

---

### 2.10 Avoid Security by Obscurity

**Security should never rely on keeping implementation details secret.**

Hiding source code, endpoints, or configurations is not a security control — it's a delay tactic.

**What security SHOULD rely on:**
- Strong password policies
- Defense in depth
- Business transaction limits
- Solid network architecture
- Fraud and audit controls

**Example:**  
A mobile app that hides its API keys inside the app binary is not secure — reverse engineering tools can extract them in minutes. The app should use proper authentication, not rely on "hidden" credentials.

> **Key principle:** Assume attackers can see your code, your architecture, and your configs. Your security must hold up even under that assumption.

---

## 3. All Ten Principles — Quick Reference

| # | Principle | One-Line Summary |
|---|---|---|
| 1 | Minimize Attack Surface | Reduce the number of ways an attacker can get in |
| 2 | Least Privilege | Give users only the access they need |
| 3 | Defense in Depth | Layer multiple independent security controls |
| 4 | Separation of Duties | No single person should be able to cause harm alone |
| 5 | Keep It Simple | Complex security breaks down — simplicity is stronger |
| 6 | Fix Issues Correctly | Find and fix the root cause, not just the symptom |
| 7 | Secure Defaults | Systems should be secure out of the box |
| 8 | Fail Securely | When controls fail, they should lock down — not open up |
| 9 | Don't Trust Services | Never assume third-party systems are secure |
| 10 | Avoid Security by Obscurity | Hiding details is not a security strategy |

---

## 4. Daily Analyst Application

| Analyst Task | Principles Applied |
|---|---|
| Reviewing SIEM alerts | Defense in Depth, Detect (NIST CSF) |
| Analyzing logs | Least Privilege (your access), Fix Issues Correctly |
| Running a vulnerability scan | Minimize Attack Surface, Fix Issues Correctly |
| Reviewing user permissions | Least Privilege, Separation of Duties |
| Evaluating a third-party tool | Don't Trust Services, Secure Defaults |
| Writing an incident report | Fix Issues Correctly, Respond (NIST CSF) |

---

## 5. ASD Essential Eight Mapping

| OWASP Principle | ASD Essential Eight Alignment |
|---|---|
| Minimize Attack Surface | Application Control, User Application Hardening |
| Least Privilege | Restrict Administrative Privileges |
| Defense in Depth | All Eight controls together form a defense-in-depth strategy |
| Separation of Duties | Restrict Administrative Privileges |
| Fix Issues Correctly | Patch Applications, Patch Operating Systems |
| Secure Defaults | Application Control, User Application Hardening |
| Don't Trust Services | Supply chain risk — supported by Application Control and patch policies |
| Fail Securely | Supported by MFA (fails to deny) and Application Control |

---

## 6. Key Takeaways

- OWASP principles are **not theoretical** — they are applied in every analyst task
- The ten principles work **alongside** the CIA Triad and NIST frameworks
- **Least Privilege + Separation of Duties** together significantly reduce insider threat risk
- **Defense in Depth** is the overarching strategy — assume one control will fail
- **Fail Securely and Secure Defaults** are especially important in system design and configuration
- **Don't Trust Services** is increasingly critical as organizations rely more on third-party vendors and cloud services
- **Avoid Security by Obscurity** — assume attackers know your system; build security that holds up anyway

---

## 7. Quick Reference — Terminology

| Term | Definition |
|---|---|
| OWASP | Open Worldwide Application Security Project — nonprofit publishing security standards and guidelines |
| Attack Surface | All potential vulnerabilities a threat actor could exploit in a system |
| Attack Vector | A specific pathway an attacker uses to penetrate security defenses |
| Defense in Depth | Layered security approach using multiple independent controls |
| Least Privilege | Granting users only the minimum access needed for their role |
| Separation of Duties | Splitting critical actions across multiple people to prevent fraud |
| Secure Defaults | Systems should be configured securely out of the box |
| Fail Securely | When a control fails, it defaults to the most restrictive/secure state |
| Security by Obscurity | Relying on hiding details as a security measure — considered ineffective |
| Root Cause | The underlying reason a vulnerability or incident occurred |

---

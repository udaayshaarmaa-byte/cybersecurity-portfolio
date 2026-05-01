# The CIA Triad

> **Author:** Uday Sharma | **Updated:** May 2026  
> **Source:** Google Cybersecurity Certificate — Course 1  
> **Purpose:** Core security model used to inform risk decisions, system design, and security policies.

---

## 1. What Is the CIA Triad?

The CIA Triad is a **foundational security model** that helps organizations consider risk when setting up systems and security policies.

Every security decision — from designing a network to writing an access policy — should be evaluated against all three principles.

```
        Confidentiality
           /\
          /  \
         /    \
        /______\
  Integrity    Availability
```

> **Security Posture** = An organization's ability to manage its defense of critical assets and data, and react to change. The CIA Triad is the backbone of a strong security posture.

---

## 2. Confidentiality

**Definition:** Only authorized users can access specific assets or data.

- Data should be available on a **"need to know" basis**
- Unauthorized access = confidentiality breach

### Key Control: Principle of Least Privilege
- Users are given access **only to what they need** to complete their job
- Limits the blast radius if an account is compromised
- Example: An accounting employee can access corporate accounts but NOT development project data

### Common Threats to Confidentiality
| Threat | Description |
|---|---|
| Phishing | Tricks users into revealing credentials |
| Insider threat | Authorized user abuses their access |
| Data exfiltration | Attacker steals and transfers data externally |
| Credential stuffing | Using leaked passwords to access accounts |

### Controls That Protect Confidentiality
- Encryption (data at rest and in transit)
- MFA
- Role-based access control (RBAC)
- Principle of Least Privilege
- Data classification policies

---

## 3. Integrity

**Definition:** Data is verifiably correct, authentic, and reliable.

- If data can be **tampered with**, it cannot be trusted
- Integrity applies to data **in storage, in transit, and in use**

### Key Mechanisms
| Mechanism | How It Protects Integrity |
|---|---|
| **Cryptography** | Uses mathematical techniques to transform data so unauthorized parties cannot read or tamper with it |
| **Encryption** | Converts readable data to encoded format — prevents tampering of messages, files, configs |
| **Hashing** | Generates a unique fixed-length value for data — any change to the data changes the hash |
| **Digital signatures** | Verify the sender's identity and confirm data hasn't been altered |

### Real-World Example — Banking
If a customer's spending habits or locations change dramatically, the bank **disables account access** and verifies the account owner before restoring it. This protects the integrity of financial records from unauthorized modification.

### Common Threats to Integrity
| Threat | Description |
|---|---|
| Man-in-the-Middle (MitM) | Attacker intercepts and alters data in transit |
| SQL Injection | Attacker manipulates database queries to corrupt data |
| Malware | Malicious code modifies or deletes system files |
| Insider tampering | Authorized user deliberately alters records |

---

## 4. Availability

**Definition:** Data and systems are accessible to authorized users when needed.

- Inaccessible data = useless data
- Ensuring uptime of **systems, networks, and applications** is a core analyst responsibility

### Real-World Example — Banking
Banks invest heavily in ensuring customers can access account information at any time via the web. Even during a suspected breach, they use **validation processes** to minimize damage while keeping services running.

### Common Threats to Availability
| Threat | Description |
|---|---|
| DDoS (Distributed Denial of Service) | Floods a system with traffic to make it unavailable |
| Ransomware | Encrypts data and locks users out until ransom is paid |
| Hardware failure | Physical damage or failure causes outage |
| Misconfiguration | Incorrectly configured systems block legitimate access |

### Controls That Protect Availability
- Redundancy and failover systems
- Regular backups (offline + offsite)
- DDoS mitigation services
- Disaster Recovery Plans (DRP)
- System monitoring and alerting

---

## 5. The CIA Triad in Practice

### Banking Example (All Three Principles)

| Principle | How the Bank Applies It |
|---|---|
| **Confidentiality** | Keeps personal and financial data accessible only to account holders and authorized staff |
| **Integrity** | Flags unusual spending patterns and disables access until the legitimate user is verified |
| **Availability** | Ensures 24/7 online access to account information with validation processes to minimize breach impact |

### Remote Work Example

| Scenario | CIA Mapping |
|---|---|
| Employee accesses internal network remotely | **Availability** — data is accessible when needed |
| Employee can only see data relevant to their role | **Confidentiality** — least privilege applied |
| Files on the internal network cannot be altered by unauthorized parties | **Integrity** — access controls + encryption |

---

## 6. CIA Triad vs. Common Attacks

| Attack | CIA Component Targeted |
|---|---|
| Data theft / exfiltration | Confidentiality |
| Phishing (credential harvest) | Confidentiality |
| Man-in-the-Middle | Integrity |
| SQL Injection | Integrity |
| DDoS | Availability |
| Ransomware | Availability + Confidentiality |
| Insider data tampering | Integrity + Confidentiality |

> **Note:** Many attacks target **multiple CIA components simultaneously.** Ransomware, for example, destroys availability AND threatens confidentiality if data is exfiltrated before encryption.

---

## 7. ASD Essential Eight Mapping

| CIA Principle | ASD Essential Eight Alignment |
|---|---|
| **Confidentiality** | Restrict Administrative Privileges, MFA, Application Control |
| **Integrity** | Patch Applications, Patch OS, Application Control (prevents tampering) |
| **Availability** | Regular Backups (direct match — Essential Eight Maturity Levels 1–3) |

> **Australia Portfolio Note:** When documenting any security incident or lab, always state which CIA principle was violated and which Essential Eight control would have mitigated it. This is the kind of structured thinking Australian employers look for.

---

## 8. Key Takeaways

- **Confidentiality** → Only the right people access the right data (Least Privilege)
- **Integrity** → Data is trustworthy and hasn't been tampered with (Cryptography, Hashing)
- **Availability** → Authorized users can always access what they need (Redundancy, Backups)
- All three must be **balanced** — over-securing for confidentiality can hurt availability
- The CIA Triad directly supports an organization's **security posture**
- As an analyst, every system, policy, or control you evaluate should be tested against all three principles

---

## 9. Quick Reference — Terminology

| Term | Definition |
|---|---|
| CIA Triad | Confidentiality, Integrity, Availability — core security model |
| Security Posture | Organization's ability to defend assets and react to threats |
| Principle of Least Privilege | Users only get access needed for their role |
| Cryptography | Mathematical techniques to secure data from tampering or unauthorized reading |
| Encryption | Converting plaintext to ciphertext to protect data |
| Hashing | Generating a unique value for data to verify it hasn't changed |
| DDoS | Distributed Denial of Service — floods a system to make it unavailable |
| Ransomware | Malware that encrypts data and demands payment to restore access |
| MitM | Man-in-the-Middle — attacker intercepts and potentially alters data in transit |

---

*These notes are part of Uday Sharma's cybersecurity learning portfolio — Google Cybersecurity Certificate, Course 1.*

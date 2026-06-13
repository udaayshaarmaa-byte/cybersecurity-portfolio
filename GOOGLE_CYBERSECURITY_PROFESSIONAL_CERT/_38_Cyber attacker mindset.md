# Attack Surfaces, Threat Actors, Attacker Mindset & Brute Force
---

## 1. Attack Surface

**Attack surface** = all the potential vulnerabilities that a threat actor could exploit.

Analysing the attack surface is usually the **first step** for any security team. The smaller the attack surface, the easier it is to protect.

### Two Types of Attack Surface:

| Type | What it includes | Example threats |
|---|---|---|
| **Physical** | People and their devices — both inside and outside the org | Unattended laptop with sensitive data visible; disgruntled employee leaking info |
| **Digital** | Everything beyond the organisation's firewall — anything connecting to the org online | Cloud data accessed from anywhere; remote workers; third-party services |

**Cloud computing has expanded the digital attack surface** — data stored in the cloud is accessible from anywhere, which increases the number of potential entry points.

### Security Hardening:
**Security hardening** = the process of strengthening a system to reduce its vulnerabilities and attack surface — minimising points of entry.

Examples: access controls, organisation policies, patch management, network segmentation.

---

## 2. Attack Vectors

**Attack vectors** = the pathways attackers use to penetrate security defences — the exploitable features of an attack surface.

| Attack Vector | Description |
|---|---|
| **Direct access** | Physical access to a device or system |
| **Removable media** | USB drives, external hard drives |
| **Social media** | Employees accidentally or intentionally leaking sensitive information |
| **Email** | Personal and business accounts — phishing delivery mechanism |
| **Wireless networks** | On-premises Wi-Fi with weak security |
| **Cloud services** | Third-party hosted data and applications |
| **Supply chain** | Third-party vendors providing a backdoor into systems |

Attack vectors are used by both **malicious actors** and **unintentional insiders** (e.g. employee posting sensitive news on social media).

---

## 3. Threat Actors

**Threat actor** = any person or group who presents a security risk — includes insiders, outsiders, intentional, and accidental.

### Five Categories of Threat Actor:

| Category | Description |
|---|---|
| **Competitors** | Rival companies who might benefit from leaked information |
| **State actors** | Government intelligence agencies |
| **Criminal syndicates** | Organised crime groups motivated by financial gain |
| **Insider threats** | Current or former employees — accidental or deliberate |
| **Shadow IT** | Individuals using unapproved tech (e.g. personal email for work) |

### Three Types of Hackers:

| Type | Description |
|---|---|
| **Unauthorised (malicious/unethical)** | Commits crimes using programming skills; includes "script kiddies" who use pre-written tools |
| **Authorised (ethical)** | Internal security teams, bug bounty hunters, ethical pen testers |
| **Semi-authorised (hacktivist)** | Violates ethical standards but not purely malicious; often politically motivated |

### Advanced Persistent Threats (APTs):
**APT** = a threat actor maintaining unauthorised access to a system for an extended period — primarily associated with nation-state actors.

- Goal: surveillance and intelligence gathering (not always immediate disruption)
- Targets government, defence, financial, and telecom services
- Often target private companies first as a stepping stone to larger targets
- Stealthy — can remain undetected for months or years

---

## 4. Attacker Mindset

**Attacker mindset** = analysing systems from the perspective of an attacker to proactively identify vulnerabilities.

Think of it as a controlled experiment — cause problems in a safe environment to understand what could go wrong.

### Four-Step Process:
1. **Identify the target** — specific data, system, person, group, or the organisation itself
2. **Determine how the target can be accessed** — what information is publicly available to an attacker?
3. **Evaluate attack vectors** — which pathways can be exploited to reach the target?
4. **Find tools and methods** — what would an attacker use to carry this out?

### Two Simulation Types:

| Simulation | Role | Also known as |
|---|---|---|
| **Proactive** | Acts as attacker — exploits vulnerabilities and tests defences | Red team exercise |
| **Reactive** | Acts as defender — scans for vulnerabilities and assesses risk | Blue team exercise |

---

## 5. Defending Attack Vectors

| Defence | How it helps |
|---|---|
| **User education** | Teach employees to recognise phishing, social engineering, and safe data handling |
| **Principle of least privilege** | Reduces internal attack surface by limiting access to what's required |
| **Right security controls and tools** | Anti-virus, EDR, MFA, firewalls — reduce impact of human error |
| **Diverse security team** | Different perspectives = better attacker mindset; catches blind spots |

---

## 6. Brute Force Attacks

**Brute force attack** = trial-and-error process of discovering private information — systematically tries combinations until one works.

### Types of Brute Force Attacks:

| Type | Method |
|---|---|
| **Simple brute force** | Tries every possible username/password combination |
| **Dictionary attack** | Uses a list of commonly used credentials |
| **Reverse brute force** | Starts with one credential; tries it across multiple systems |
| **Credential stuffing** | Uses stolen credentials from previous breaches on other platforms |
| **Pass the hash** | Reuses stolen, unsalted hashed credentials to create a new authenticated session |

### Common Brute Force Tools:
- **Aircrack-ng** — Wi-Fi network testing
- **Hashcat** — password hash cracking
- **John the Ripper** — password cracking
- **Ophcrack** — Windows password recovery
- **THC Hydra** — multi-protocol attack tool *(you used this in Lab 6 against SSH)*

### Brute Force Prevention:

| Control | How it helps |
|---|---|
| **Hashing + salting** | Unique salted hashes make pre-computed attacks (rainbow tables) ineffective |
| **MFA** | Even with a cracked password, second factor blocks access |
| **CAPTCHA** | Distinguishes humans from automated tools |
| **Password policy** | Complexity + lockout rules increase time-to-crack; NIST SP 800-63B guidance |

---

## Key Terms

| Term | Definition |
|---|---|
| Attack surface | All potential vulnerabilities a threat actor could exploit |
| Physical attack surface | People and devices — inside and outside the org |
| Digital attack surface | Everything beyond the org's firewall connected online |
| Security hardening | Strengthening systems to reduce vulnerabilities and attack surface |
| Attack vector | Pathway attackers use to penetrate security defences |
| Threat actor | Any person or group presenting a security risk |
| Script kiddie | Low-skill attacker using pre-written tools |
| Hacktivist | Semi-authorised hacker with political motivations |
| APT | Advanced Persistent Threat — sustained unauthorised access, often nation-state |
| Attacker mindset | Analysing systems from an attacker's perspective |
| Red team | Offensive simulation — acts as attacker |
| Blue team | Defensive simulation — responds to attacks |
| Credential stuffing | Using stolen credentials from one breach on other platforms |
| Pass the hash | Reusing stolen hashed credentials to create a new session |
| Brute force | Trial-and-error method of discovering private information |

---
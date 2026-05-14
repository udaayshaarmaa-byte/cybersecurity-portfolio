# OS Hardening & Brute Force Attacks — Note
--

## 1. Why OS Hardening Matters

The **OS (Operating System)** = interface between computer hardware and the user; first program loaded at boot.

One insecure OS can compromise an **entire network** — hardening every endpoint is essential.

---

## 2. OS Hardening Tasks

### Regular / Ongoing Tasks:

#### Patch Updates (Patch Installation)
- A **patch** = software/OS update that addresses a known security vulnerability
- Once a vendor publishes a patch, attackers immediately know where the vulnerability is in **unpatched systems** — so organisations must patch quickly
- After patching, update the **baseline configuration**

**Baseline configuration (baseline image)** = documented set of specifications for a system, used as a reference for future builds and to detect unauthorised changes. If unusual activity is suspected, compare current config to baseline to identify what changed.

#### Hardware & Software Disposal
- Properly **wipe and dispose** of old hardware
- **Delete unused software** — unused apps may have known vulnerabilities that expand the attack surface

#### Access Privileges & Password Policy Reviews
- Regularly audit who has access to what
- Enforce strong password policies (minimum length, complexity requirements, lockout after failed attempts)

### One-Time / Initial Setup Tasks:
- Configure device settings to meet a secure encryption standard
- Establish baseline image immediately after initial secure configuration

---

## 3. Password Policies & MFA

### Strong Password Policy includes:
- Minimum character count (e.g. 8+)
- Requires uppercase, number, and symbol
- Account lockout after a defined number of failed login attempts
- Rules around password reuse and rotation frequency

### MFA (Multi-Factor Authentication)
A user must verify identity using **two or more** of:

| Factor | Examples |
|---|---|
| **Something you know** | Password, PIN |
| **Something you have** | ID card, hardware token, OTP on phone |
| **Something you are** | Fingerprint, facial recognition |

**2FA** = same concept but exactly two factors.


---

## 4. Brute Force Attacks

A **brute force attack** = trial-and-error process of discovering private information (typically passwords).

### Types:

| Type | Method |
|---|---|
| **Simple Brute Force** | Systematically tries every possible username/password combination |
| **Dictionary Attack** | Uses a list of commonly used passwords and previously breached credentials |

Brute force can be done manually or via automated tools — tools make it fast at scale.

---

## 5. Vulnerability Assessment Tools

Before an attack occurs, analysts can proactively test for vulnerabilities using:

### Virtual Machines (VMs)
- Software versions of physical computers
- Run suspicious code in **isolation** — malicious code can't affect the host system
- Can be deleted and replaced with a clean image after testing
- Allow reverting to a previous state
- Used for: malware analysis, testing tools, simulating environments

**Risk:** small chance that malware can escape virtualisation and reach the host machine.

### Sandboxes
- Isolated testing environments — separate from the production network
- Used for: testing patches, identifying bugs, evaluating suspicious files, simulating attack scenarios
- Can be physical machines (air-gapped) or software/cloud-based VMs

**Risk:** sophisticated malware can detect sandbox/VM environments and behave harmlessly — analysts must account for this.



---

## 6. Brute Force Prevention Measures

| Measure | How it helps |
|---|---|
| **Hashing** | Converts password to a one-way hash value — original text cannot be recovered even if the hash is stolen |
| **Salting** | Adds random characters to a password before hashing — increases complexity; prevents rainbow table attacks |
| **MFA / 2FA** | Requires additional verification — stolen password alone is not enough to gain access |
| **CAPTCHA / reCAPTCHA** | Distinguishes humans from bots — blocks automated brute force tools |
| **Password Policies** | Enforces complexity, rotation, no reuse, and lockout rules across the org |

**CAPTCHA** = Completely Automated Public Turing test to tell Computers and Humans Apart

**reCAPTCHA** = Google's free CAPTCHA service

---

## Key Terms

| Term | Definition |
|---|---|
| OS Hardening | Set of procedures to maintain and improve OS security |
| Patch Update | Software fix for a known security vulnerability |
| Baseline Configuration | Documented secure system state used as a reference |
| Brute Force Attack | Trial-and-error password guessing — manual or automated |
| Dictionary Attack | Brute force using known/common passwords and breached credential lists |
| VM (Virtual Machine) | Software computer used for isolated testing |
| Sandbox | Isolated environment for safely running suspicious code or simulations |
| Hashing | One-way conversion of data to a fixed-length value |
| Salting | Adding random data to a password before hashing to increase complexity |
| MFA | Multi-Factor Authentication — two or more identity verification factors |
| 2FA | Two-Factor Authentication — exactly two verification factors |
| CAPTCHA | Human-verification test to block automated bots |

---


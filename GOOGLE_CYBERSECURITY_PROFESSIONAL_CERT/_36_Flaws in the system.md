# Vulnerability Management, CVE, OWASP, OSINT & Defence in Depth
---

## 1. Vulnerability Management

**Vulnerability** = a weakness that can be exploited by a threat
**Exploit** = a way of taking advantage of a vulnerability
**Exposure** = a mistake that can be exploited by a threat (e.g. leaving a document near an open window)

**Vulnerability management** = the process of finding and patching vulnerabilities  a cyclic, ongoing process.

### Four-Step Cycle:
```
1. Identify vulnerabilities
2. Consider potential exploits of those vulnerabilities
3. Prepare defences against threats
4. Evaluate those defences
→ Repeat
```

### Zero-Day Exploit:
**Zero-day** = an exploit that was previously unknown  happens in real time with zero days to fix it.
- Cannot be planned for in advance
- Represents the most dangerous category of threat
- Example: unexpected new spyware infecting a popular website

---

## 2. CVE List

**CVE (Common Vulnerabilities and Exposures) list** = an openly accessible dictionary of known vulnerabilities and exposures.

- Created by **MITRE Corporation** in **1999**
- MITRE = non-profit R&D centres sponsored by the US government
- Purpose: provide a standard way of identifying and categorising known vulnerabilities
- Reported by: independent researchers, technology vendors, ethical hackers, and the public

### CVE Criteria (must meet all four):
1. Independent of other issues can be fixed without fixing something else
2. Recognised as a potential security risk by the reporter
3. Submitted with supporting evidence
4. Affects only one codebase (one program's source code)

Once assigned a **CVE ID**, vulnerabilities are reviewed by other databases.

---

## 3. CVSS Common Vulnerability Scoring System

**CVSS** = a measurement system that scores the severity of a vulnerability (used by NIST National Vulnerabilities Database).

| Score Range | Risk Level | Action |
|---|---|---|
| 0.0 – 3.9 | Low | No immediate attention required |
| 4.0 – 6.9 | Medium | Monitor and plan remediation |
| 7.0 – 8.9 | High | Address promptly |
| 9.0 – 10.0 | Critical | Address immediately |

Base scores = fixed at time of evaluation; don't change over time.

Security teams use CVSS to **prioritise patching**  critical scores need same-day response.

---

## 4. OWASP Top 10

**OWASP (Open Worldwide Application Security Project)** = non-profit foundation improving software security; publishes the Top 10 most targeted web vulnerabilities.

Updated every few years. Mainly applies to **new or custom-built software**.

### Current OWASP Top 10 Categories:

| # | Vulnerability | Description |
|---|---|---|
| 1 | **Broken Access Control** | Access restrictions failing → unauthorised data access, modification, or deletion |
| 2 | **Cryptographic Failures** | Weak or missing encryption (e.g. MD5 hashing for passwords) → data exposure |
| 3 | **Injection** | Malicious code inserted into a vulnerable app (e.g. SQL injection in login forms) |
| 4 | **Insecure Design** | Missing or poorly implemented security controls in the application's architecture |
| 5 | **Security Misconfiguration** | Default or incorrect settings on systems, servers, or cloud services |
| 6 | **Vulnerable & Outdated Components** | Using open-source libraries with known, unpatched vulnerabilities |
| 7 | **Identification & Authentication Failures** | Weak authentication allowing unauthorised access |
| 8 | **Software & Data Integrity Failures** | Updates/patches not reviewed → supply chain attacks (e.g. SolarWinds 2020) |
| 9 | **Security Logging & Monitoring Failures** | Insufficient logs → incidents go undetected |
| 10 | **Server-Side Request Forgery (SSRF)** | Attacker manipulates server to fetch unauthorised data |

> {OWASP Top 10 helps you build secure apps. CVE list helps you fix existing vulnerable ones. Different purposes, both essential.}

**Supply chain attack** = attacker compromises one system to infect all downstream third parties. SolarWinds (2020) is the canonical example.

---

## 5. OSINT Open Source Intelligence

**OSINT** = collection and analysis of information from publicly available sources to generate usable intelligence.

**Information** = raw data/facts
**Intelligence** = analysis of information to produce actionable insights for decision-making

OSINT uses in security:
- Detect potential data exposures
- Identify emerging threats and vulnerabilities
- Evaluate existing defences
- Build profiles of potential attackers
- Monitor hacker forums for discussions about new CVEs affecting your systems

### Key OSINT Tools:

| Tool | Purpose |
|---|---|
| **VirusTotal** | Analyse suspicious files, domains, URLs, and IPs for malicious content |
| **MITRE ATT&CK** | Knowledge base of adversary tactics and techniques (real-world observations) |
| **OSINT Framework** | Web interface aggregating OSINT tools by source/platform |
| **Have I Been Pwned** | Search for email addresses in known breach databases |

---

## 6. CI/CD Pipeline Security (Brief Overview)

**CI/CD** = Continuous Integration / Continuous Delivery automates the software build, test, and deployment process.

### Common CI/CD Vulnerabilities:

| Vulnerability | Risk |
|---|---|
| Insecure dependencies | Third-party libraries with known CVEs get built in automatically |
| Misconfigured permissions | Weak RBAC → attackers can modify code or pipeline config |
| No automated security testing | Vulnerabilities reach production undetected |
| Exposed secrets | Hardcoded API keys/passwords in code → breach |
| Unsecured build environments | Compromised build server → malicious code injected into releases |

### Key CI/CD Security Controls:
- DevSecOps mindset security built into every stage
- RBAC + MFA on pipeline access
- SAST (Static Application Security Testing) and DAST (Dynamic Application Security Testing)
- Secrets management tools (HashiCorp Vault, AWS Secrets Manager)
- Dependency scanning tools (Dependabot, Snyk)

> {CI/CD is increasingly common in Australian organisations. Even as a SOC analyst, understanding that the software you're monitoring may have been deployed via an automated pipeline and that pipeline itself can be an attack vector is valuable context.}

---

## 7. Defence in Depth (Castle Approach)

**Defence in depth** = a layered security model where multiple independent controls reduce risk if one layer fails, another stops the attack.

Also called the **castle approach** medieval castles used multiple independent barriers (moat, walls, watch towers) that each posed unique challenges to attackers.

### Five Layers of Defence in Depth:

| Layer | Focus | Example Controls |
|---|---|---|
| **1 Perimeter** | User authentication filter external access | Usernames, passwords, SSO |
| **2 Network** | Authorisation control network-level access | Firewalls, VPNs, network segmentation |
| **3 Endpoint** | Protect individual devices on the network | Anti-virus, EDR, patch management |
| **4 Application** | Security built into software interfaces | MFA, input validation, HTTPS, OAuth |
| **5 Data** | Protect the actual critical data | Asset classification, encryption, access controls |

Information passes through all five layers whenever exchanged over a network. Every layer reduces the risk that a breach at one layer causes total compromise.

> {Defence in depth means no single control is a silver bullet. This is why the ASD Essential Eight has eight controls they're designed as complementary layers, not standalone fixes.}

---

## Key Terms

| Term | Definition |
|---|---|
| Vulnerability | Weakness that can be exploited by a threat |
| Exploit | Method of taking advantage of a vulnerability |
| Exposure | Mistake that can be exploited by a threat |
| Zero-day | Previously unknown exploit no time to prepare |
| Vulnerability management | Cyclic process of finding and patching vulnerabilities |
| CVE | Common Vulnerabilities and Exposures standardised vulnerability dictionary |
| MITRE | Non-profit R&D; created the CVE list |
| CNA | CVE Numbering Authority reviews and assigns CVE IDs |
| CVSS | Common Vulnerability Scoring System 0–10 severity scale |
| OWASP | Open Worldwide Application Security Project |
| OWASP Top 10 | List of most targeted web application vulnerabilities |
| Injection | Inserting malicious code into a vulnerable application |
| Supply chain attack | Compromising one system to infect downstream third parties |
| OSINT | Open Source Intelligence analysis of publicly available information |
| VirusTotal | Online tool for malicious file/URL/IP analysis |
| MITRE ATT&CK | Adversary tactics and techniques knowledge base |
| Have I Been Pwned | Tool to check email addresses against breach databases |
| CI/CD | Continuous Integration/Deployment automated software pipeline |
| DevSecOps | Security embedded throughout the development lifecycle |
| Defence in depth | Layered security model multiple independent controls |
| Castle approach | Alternative name for defence in depth |

---
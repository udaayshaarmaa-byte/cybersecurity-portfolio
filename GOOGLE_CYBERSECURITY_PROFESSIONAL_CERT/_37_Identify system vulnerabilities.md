# Vulnerability Assessments, Scanning, Patching & Penetration Testing

## 1. Vulnerability Assessment

**Vulnerability assessment** = the internal review process of an organisation's security systems — finds weaknesses before attackers do.

Goals:
- Identify weak points
- Prevent attacks
- Verify security controls meet regulatory standards

### Four-Step Process:

| Step | Name | What happens |
|---|---|---|
| 1 | **Identification** | Scanning tools + manual testing used to map the current security state — "taking a photo" of the system |
| 2 | **Vulnerability Analysis** | Each identified vulnerability is tested to find its source — "digital detective" work |
| 3 | **Risk Assessment** | Score assigned based on: severity of impact if exploited + likelihood of exploitation → prioritises what to fix first |
| 4 | **Remediation** | Vulnerabilities addressed based on severity score — joint effort between security and IT teams |

Remediation examples: enforcing new procedures, updating OS, applying patches, changing configurations.

> {Vulnerabilities found always outnumber people available to fix them. Risk assessment is how you decide what to fix today vs. what can wait.}

---

## 2. Vulnerability Scanners

**Vulnerability scanner** = software that automatically compares known vulnerabilities against technologies on the network; finds misconfigurations and programming flaws.

Scanners analyse all five layers of **defence in depth**:
- Perimeter (authentication systems)
- Network (firewalls)
- Endpoint (laptops, servers)
- Application (software interfaces)
- Data (stored/in-transit/in-use data)

At the end of each scan, vulnerabilities are flagged and added to the scanner's reference database — each scan improves accuracy.

**Scanners are non-intrusive** — they don't exploit vulnerabilities, they identify them. (Rare exception: scans can occasionally crash unstable systems.)

### Types of Vulnerability Scans:

| Scan Type | Description | Finds |
|---|---|---|
| **External** | Tests perimeter from outside the network | Exposed ports, vulnerable public-facing servers |
| **Internal** | Tests from inside the organisation | Application weaknesses, internal misconfigs |
| **Authenticated** | Logs in with a real user/admin account | Broken access controls, privilege escalation paths |
| **Unauthenticated** | No credentials — simulates an external attacker | Publicly accessible resources that shouldn't be |
| **Limited** | Targets specific devices | Firewall misconfigurations, specific system flaws |
| **Comprehensive** | All devices on the network | Full OS, user database, and config review |

**Pro tip:** Run **discovery scanning** first — maps all devices, systems, and open ports before limited or comprehensive scans begin.

---

## 3. Patch Management & Updates

**Patch update** = a software/OS update that addresses security vulnerabilities within a program or product.

**Patching is remediation** — it closes the "unlocked doors" in a system.

### Two Update Strategies:

| Strategy | Advantage | Disadvantage |
|---|---|---|
| **Manual** | More control; avoids unstable patches | Critical updates can be forgotten or delayed |
| **Automatic** | Simplest; keeps systems current | Untested patches can cause instability |

**CISA recommends** automatic updates whenever available.

### End-of-Life (EOL) Software:
- Software no longer supported by its manufacturer
- No patches available → **unfixable security risk**
- CISA recommends discontinuing EOL software
- Reality: replacement costs are high, so many orgs still run EOL systems (especially IoT devices)

**WannaCry (2017)** — real-world consequence of unpatched systems: affected 150+ countries, ~$4 billion in damage; a patch fixing the vulnerability was available months before the attack.

> {EOL software + unpatched systems are the two most consistent findings in post-breach reviews. Understanding this is why "Patch Applications" and "Patch OS" are both standalone ASD Essential Eight controls.}

---

## 4. Penetration Testing

**Penetration test (pen test)** = a simulated attack that identifies vulnerabilities by exploiting them — determines actual consequences if a system is breached.

Pen testing = **ethical hacking** (authorised attack).

Difference from vulnerability assessment:
- Vulnerability assessment: **finds** weaknesses
- Pen test: **exploits** weaknesses to determine real-world impact

Organisations regulated by **PCI DSS, HIPAA, or GDPR** must routinely perform pen tests for compliance.

### Three Team Approaches:

| Team | Focus |
|---|---|   
| **Red team** | Simulates attacks — offensive; identifies vulnerabilities in systems/networks/apps |
| **Blue team** | Defends — validates existing security systems and incident response |
| **Purple team** | Collaborative — red + blue work together to improve overall security posture |

### Three Testing Strategies:

| Strategy | Access level | Also known as |
|---|---|---|
| **Open-box (White-box)** | Full internal access — same as an internal developer | Internal, full knowledge, clear-box |
| **Closed-box (Black-box)** | No internal access — simulates an external attacker | External, zero knowledge |
| **Partial knowledge (Grey-box)** | Limited access — simulates e.g. a customer service rep | Grey-box |

**Closed-box** produces the most realistic simulation of a real-world attack.

### Bug Bounty Programs:
Organisations offer financial rewards to freelance pen testers for responsibly disclosing vulnerabilities — good way to grow skills and build a portfolio.

---

## Key Terms

| Term | Definition |
|---|---|
| Vulnerability assessment | Internal review of an org's security systems to find and fix weaknesses |
| Vulnerability scanner | Software that identifies misconfigurations and known vulnerabilities |
| Discovery scanning | Pre-scan step to map devices, systems, and open ports |
| Patch update | Software fix addressing a security vulnerability |
| EOL software | End-of-Life — no longer supported or patched by the vendor |
| Penetration test | Authorised simulated attack to find and exploit vulnerabilities |
| Ethical hacking | Authorised hacking used to improve security |
| Red team | Offensive pen testing — simulates attacker |
| Blue team | Defensive security — validates defences |
| Purple team | Collaborative red + blue exercise |
| Open-box testing | Full internal access (white-box) |
| Closed-box testing | No access (black-box) — most realistic simulation |
| Partial knowledge testing | Limited access (grey-box) |
| Bug bounty | Programme rewarding freelancers for responsibly disclosing vulnerabilities |
| WannaCry | 2017 ransomware attack demonstrating cost of unpatched systems |

---

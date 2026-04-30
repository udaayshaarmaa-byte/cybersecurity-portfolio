# Cybersecurity Fundamentals: Assets, Risk Management, and RMF

---

## 1. Assets

An asset is anything of value to an organization.

### Digital Assets:
- Personally Identifiable Information (PII)
  - SSNs / national IDs
  - Dates of birth
  - Bank details
  - Addresses
- Intellectual property

### Physical Assets:
- Servers
- Workstations
- Payment systems
- Office infrastructure

---

## 2. Core Concepts

### Threat
Any event or circumstance that can harm assets.

Examples:
- Social engineering (phishing)
- Insider threats
- Advanced Persistent Threats (APTs)

---

### Risk
The likelihood that a threat will exploit a vulnerability and impact:

- Confidentiality
- Integrity
- Availability

---

### Vulnerability
A weakness that can be exploited by a threat.

Examples:
- Outdated systems
- Weak authentication
- Unpatched software
- Poor logging and monitoring

---

### Key Relationship
Risk exists only when:
Threat + Vulnerability → Risk

---

## 3. Risk Levels

- Low: Minimal impact (public data)
- Medium: Moderate financial or reputational impact
- High: Severe legal, financial, or operational damage (PII, IP)

---

## 4. Risk Management Strategies

- Acceptance: Accept risk to maintain operations
- Avoidance: Eliminate the risk completely
- Transference: Shift risk to third parties
- Mitigation: Reduce likelihood or impact

---

## 5. Types of Risks

- External: Threat actors outside the organization
- Internal: Employees, vendors, partners
- Legacy Systems: Outdated, unpatched systems
- Multiparty: Third-party/vendor exposure
- Compliance Risk: Unpatched or non-compliant software

---

## 6. Common Vulnerabilities

- ProxyLogon (Microsoft Exchange exploit)
- ZeroLogon (authentication bypass)
- Log4Shell (remote code execution via Java logging)
- PetitPotam (NTLM relay technique)
- Server-Side Request Forgery (SSRF)
- Logging and monitoring failures

---

## 7. Ransomware

A malware attack where:
- Data is encrypted
- Access is denied
- Payment is demanded for decryption

Impact:
- Operational shutdown
- Data loss or exposure
- Financial damage

---

## 8. Layers of the Web

- Surface Web: Publicly accessible content
- Deep Web: Restricted access systems (e.g., intranet)
- Dark Web: Anonymous networks used for illicit activity

---

## 9. Organizational Impact of Security Failures

### Financial Impact
- Downtime
- Recovery costs
- Regulatory fines

### Identity Theft
- Exposure of sensitive data
- Sale of PII on dark web

### Reputational Damage
- Loss of trust
- Customer churn
- Long-term brand damage

---

## 10. NIST Risk Management Framework (RMF)

A structured approach to managing risk.

### Steps:

1. Prepare  
   Identify risks and required controls  

2. Categorize  
   Classify systems based on CIA impact  

3. Select  
   Choose and document security controls  

4. Implement  
   Apply controls to systems  

5. Assess  
   Evaluate effectiveness of controls  

6. Authorize  
   Approve system operation and accept risk  

7. Monitor  
   Continuously observe and improve systems  

---

## 11. Vulnerability Management

Process of:
- Identifying weaknesses
- Applying patches
- Monitoring systems continuously

Key principle:
Unpatched vulnerability = active risk

---

## 12. Industry Standards and Resources

- NIST (Risk frameworks and vulnerability databases)
- OWASP Top 10 (Web application risks)
- CISA Known Exploited Vulnerabilities Catalog

---

## 13. Role of a Security Analyst

- Monitor systems and logs
- Identify threats and vulnerabilities
- Support risk mitigation
- Educate users (e.g., phishing awareness)
- Enforce access controls
- Document and report incidents

---

## Final Principle

Security is continuous.

Effective defense requires:
- Constant monitoring
- Timely patching
- Structured risk management
- Organization-wide awareness
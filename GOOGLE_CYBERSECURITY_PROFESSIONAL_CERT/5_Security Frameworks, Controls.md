* \# Security Frameworks, Controls \& Compliance



Security framework - Guidelines for building plans to mitigate risks and threats to data and privacy. Provides a structured approach to implementing a security lifecycle.



Security lifecycle - A constantly evolving set of policies and standards that define how an org manages risk, follows guidelines, and meets regulatory compliance (laws).



Security control - A safeguard designed to reduce a specific security risk. Controls are the tools/actions that implement a framework's guidelines.



Compliance - The process of adhering to internal standards and external regulations.



Key distinction: Frameworks set the strategy and goals; controls are the specific mechanisms that carry out those goals.



Why Frameworks Exist??

Security frameworks serve 5 core purposes:

1. Protect personally identifiable information (PII)
2. Secure financial information
3. Identify security weaknesses
4. Manage organizational risk
5. Align security with business goals





Core Components of a Security Framework

1. Identify \& document security goals-Find where the org is out of compliance with GDPR
2. Set guidelines to achieve security goals-Develop policies for handling individual user data requests
3. Implement strong security processes-Design procedures to verify and fulfil data update/delete requests
4. Monitor \& communicate results-Report GDPR-relevant network issues to the compliance officer



GDPR

* Full name: General Data Protection Regulation
* Jurisdiction: European Union
* Purpose: Grants EU citizens more control over their personal data
* Analyst role: Identify compliance gaps → build policies → design verification procedures → monitor and report
* Key rule: If a breach occurs, affected EU citizens must be notified within 72 hours



&#x20;Frameworks vs Controls 

Framework  →  sets the GOAL (reduce data breach risk)

Control    →  is the MECHANISM (privacy training + software tracking tool)

example::

Policy requires all employees to complete privacy training to reduce data breach risk.

The control is the software tool that automatically assigns and tracks training completion.



CIA Triad

A foundational model that informs how organizations consider risk when setting up systems and security policies. The three pillars are used to establish controls that mitigate threats, risks, and vulnerabilities.



C-Confidentiality → Only authorized users can access specific assets or data(Strict access controls, role-based permissions)



I-Integrity → Data is correct, authentic, and reliable — not tampered with(Encryption, hashing, checksums)



A-Availability → Authorized users can access data when they need it(Redundancy, uptime monitoring, backups)



Asset

An asset is any item perceived as having value to an organization.

Value = cost + risk exposure → higher value = stricter controls required



|Asset type|Example|Security level|
|-|-|-|
|High-value|App storing SSNs or bank account data|Strict controls required|
|Low-value|Website serving public news content|Lighter security acceptable|







NIST Cybersecurity Framework (NIST CSF)

* What it is: Voluntary framework of standards, guidelines, and best practices to manage cybersecurity risk
* Created by: U.S. National Institute of Standards and Technology (NIST)
* Scope: Used globally, not just in the U.S.
* Purpose: Baseline for managing both short-term and long-term risk
* Related framework: NIST RMF (Risk Management Framework)
* The more aligned an organization is with NIST CSF, the lower its overall risk.





Threat Actors — Key Insight



Countermeasure: Apply the principle of least privilege (links to CIA — Availability pillar)

* Restrict staff to only the data and systems their role requires
* Enforced via organizational guidelines and access control frameworks

Additional insight:

* Threat actors operate globally
* Diverse security teams help identify varied attacker intentions and methods



&#x20;Global Compliance Standards

NIST CSF \& RMF

* Jurisdiction: U.S. (used worldwide)
* Voluntary frameworks for managing cybersecurity risk
* CSF = Cybersecurity Framework · RMF = Risk Management Framework



FERC-NERC



* Jurisdiction: U.S. / North America
* Applies to orgs working with electricity or the power grid
* Must prepare for, mitigate, and report security incidents
* Must adhere to Critical Infrastructure Protection (CIP) Reliability Standards



FedRAMP



* Jurisdiction: U.S. federal government
* Standardizes security assessment, authorization, and monitoring of cloud services
* Ensures consistency across government and third-party cloud providers



CIS (Center for Internet Security)



* Jurisdiction: International nonprofit
* Provides a set of controls to safeguard systems and networks against attacks
* Also provides actionable controls to follow when a security incident occurs



GDPR (General Data Protection Regulation)



* Jurisdiction: European Union
* Protects EU residents' data and right to privacy — inside and outside EU territory
* Key rule: Orgs must notify affected EU citizens of a breach within 72 hours
* Applies to any org handling EU citizen data, regardless of where the org is located



PCI DSS (Payment Card Industry Data Security Standard)



* Jurisdiction: International
* Ensures orgs storing, accepting, or transmitting credit card data do so securely
* Objective: Reduce credit card fraud



HIPAA (Health Insurance Portability and Accountability Act)



* Jurisdiction: U.S. federal law (1996)
* Protects patients' health information (PHI)
* Prohibits sharing patient data without consent
* Three rules: Privacy · Security · Breach notification
* Related framework: HITRUST — helps institutions meet HIPAA compliance
* PHI covers: Past, present, or future physical/mental health condition, plan of care, or payments for care



ISO (International Organization for Standardization)



* Jurisdiction: International
* Establishes global standards for technology, manufacturing, and management
* Helps orgs improve processes across staff retention, planning, waste, and services



SOC 1 \& SOC 2 (System and Organizations Controls)



* Jurisdiction: U.S. (AICPA — American Institute of Certified Public Accountants)
* Series of audit reports assessing user access policies across org levels:



Associate · Supervisor · Manager · Executive · Vendor





Covers: Confidentiality, privacy, integrity, availability, security, and data safety

Risk: Control failures in these areas can lead to fraud






















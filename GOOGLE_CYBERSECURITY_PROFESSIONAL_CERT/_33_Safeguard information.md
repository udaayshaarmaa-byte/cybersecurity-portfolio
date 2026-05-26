# Security Controls, Least Privilege, Data Governance & Privacy

## 1. Security Controls

**Security controls** = safeguards designed to reduce specific security risks; protect assets before, during, and after an event.

### Three Types:

| Type | Description | Examples |
|---|---|---|
| **Technical** | Technologies used to protect assets | Encryption, authentication systems, firewalls, IDS/IPS |
| **Operational** | Day-to-day security practices performed by people | Awareness training, incident response, access reviews |
| **Managerial** | How the other two reduce risk  governance layer | Policies, standards, procedures |

---

## 2. Information Privacy vs Information Security

| Concept | Definition |
|---|---|
| **Information Privacy** | Protection from unauthorised access and distribution of data; the right to control how personal info is shared |
| **Information Security (InfoSec)** | Keeping data in all states away from unauthorised users |

**Key distinction:**
- **Privacy** = giving people control over their personal information and how it's used
- **Security** = protecting those choices and keeping the data safe from threats

Both are needed to maintain customer trust and brand reputation. Security controls are the *technologies* used to regulate information privacy.


---

## 3. Principle of Least Privilege (PoLP)

**Principle of Least Privilege** = a user is only granted the minimum level of access and authorisation required to complete a task or function.

Supports the CIA triad  limits breach impact by restricting what each user can touch.

### Benefits:
- Limits access to sensitive information
- Reduces chances of accidental data modification, tampering, or loss
- Supports system monitoring and administration
- Reduces likelihood of successful attack

### Types of User Accounts:

| Account Type | Description |
|---|---|
| **Guest accounts** | External users  customers, contractors, business partners |
| **User accounts** | Staff  based on job duties |
| **Service accounts** | Applications/software interacting with other software |
| **Privileged accounts** | Elevated permissions or admin access |


---

## 4. Auditing Account Privileges

Accounts must be **regularly audited**  correct setup at creation is not enough.

| Audit Type | Purpose |
|---|---|
| **Usage audit** | Reviews which resources each account accesses and what users do with them; identifies unused permissions |
| **Privilege audit** | Checks if user roles still match their current access level; addresses **privilege creep** |
| **Account change audit** | Reviews logs for suspicious account changes (e.g. repeated password change attempts) |

**Privilege creep** = users accumulate more access than needed over time as roles change; a privilege audit catches and corrects this.

**Separation of duties** = related concept; divides tasks among different users to prevent any single person from having complete control over a critical function.

---

## 5. Data Lifecycle

Data protection policies must cover data across its **entire lifecycle**:

```
Collect → Store → Use → Archive → Destroy
```

Security controls must be applied at **every stage**  not just when data is actively being used.

---

## 6. Data Governance

**Data governance** = a set of processes defining how an organisation manages information; includes policies for keeping data private, accurate, available, and secure throughout its lifecycle.

### Key Roles:

| Role | Responsibility |
|---|---|
| **Data owner** | Decides who can access, edit, use, or destroy their information |
| **Data custodian** | Responsible for safe handling, transport, and storage of information (can be a person, org, or system) |
| **Data steward** | Maintains and implements data governance policies |


---

## 7. Legally Protected Data Types

| Type | Definition | Key Regulation |
|---|---|---|
| **PII** (Personally Identifiable Information) | Any info used to infer or contact an individual | General data privacy laws globally |
| **SPII** (Sensitive PII) | PII requiring stricter handling  bank account numbers, login credentials | Need-to-know access only |
| **PHI** (Protected Health Information) | Information about a person's past, present, or future health | HIPAA (US), GDPR (EU) |

---

## 8. Key Privacy Regulations

| Regulation | Jurisdiction | Scope |
|---|---|---|
| **GDPR** (General Data Protection Regulation) | EU | Applies to any business handling EU citizens' data, anywhere in the world; gives data owners total control |
| **PCI DSS** (Payment Card Industry Data Security Standard) | Global (financial industry) | Secures credit/debit card transactions against theft and fraud |
| **HIPAA** (Health Insurance Portability and Accountability Act) | US | Protects patient health information; prohibits disclosure without consent |

---

## 9. Security Audits vs Security Assessments

| | Security Audit | Security Assessment |
|---|---|---|
| **What it is** | Review of security controls, policies, and procedures against a set of expectations | Check of how resilient current security implementations are against threats |
| **Frequency** | ~Once per year | Every 3–6 months |
| **Who conducts it** | Internal and/or external third parties | Typically internal employees |
| **Purpose** | Validates compliance with standards/regulations | Identifies gaps before an audit or incident |

---

## Key Terms

| Term | Definition |
|---|---|
| Security Control | Safeguard designed to reduce a specific security risk |
| Technical Control | Technology-based safeguard (encryption, firewalls) |
| Operational Control | People-driven day-to-day security practice |
| Managerial Control | Governance layer policies, standards, procedures |
| Information Privacy | Right to control how personal data is accessed and shared |
| InfoSec | Keeping data in all states away from unauthorised users |
| Least Privilege (PoLP) | Users get only the minimum access needed for their task |
| Privilege Creep | Accumulation of unnecessary access over time |
| Separation of Duties | Divides tasks to prevent one person having total control |
| Data Lifecycle | Collect → Store → Use → Archive → Destroy |
| Data Governance | Processes for managing information throughout its lifecycle |
| Data Owner | Decides who can access/edit/use/destroy their data |
| Data Custodian | Responsible for safe handling, storage, and transport of data |
| Data Steward | Implements and maintains data governance policies |
| PII | Personally Identifiable Information |
| SPII | Sensitive PII — stricter access controls |
| PHI | Protected Health Information |
| GDPR | EU data protection regulation — applies globally |
| PCI DSS | Payment card security standard |
| HIPAA | US health data protection law |
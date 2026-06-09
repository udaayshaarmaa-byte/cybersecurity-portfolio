# AAA Framework, IAM, Authentication, Authorization & Accounting
---

## 1. Access Controls Overview

**Access controls** = security controls that manage access, authorisation, and accountability of information.

Well-implemented access controls:
- Maintain CIA (Confidentiality, Integrity, Availability)
- Get users the information they need quickly
- Limit damage when credentials are compromised

### AAA Framework  Three Functions:

| Function | Question it answers | Purpose |
|---|---|---|
| **Authentication** | Who are you? | Verify identity |
| **Authorisation** | What are you allowed to do? | Determine access rights |
| **Accounting** | What did you do? | Monitor and log activity |

---

## 2. Authentication

**Authentication** = verifying the identity of a user, device, or system.

### Three Factors of Authentication:

| Factor | Type | Examples |
|---|---|---|
| **Knowledge** | Something you know | Password, security question answer |
| **Ownership** | Something you have | OTP via SMS, hardware token, authenticator app |
| **Characteristic** | Something you are | Fingerprint, facial scan (biometrics) |

**MFA (Multi-Factor Authentication)** = requires two or more factors  makes impersonation significantly harder.

**2FA** = exactly two factors.

---

## 3. Single Sign-On (SSO)

**SSO** = technology that combines several different logins into one  authenticates a user once for access to multiple systems.

### Why organisations use SSO:
- Reduces password fatigue (tendency to reuse passwords across services)
- Fewer access points for attackers
- Lower admin costs
- Improved user experience

### How SSO works:
- Uses trusted third-party identity providers
- Exchanges encrypted **access tokens** between identity provider and service provider
- Protocols used:
  - **LDAP** (Lightweight Directory Access Protocol)  on-premises
  - **SAML** (Security Assertion Markup Language)  cloud/off-premises
  - Often used together

### SSO limitation:
Single credential failure (lost/stolen password) exposes access to all connected systems → solved by combining with MFA.

> {SSO + MFA together = convenient AND secure. Neither alone is enough. This is the standard in Australian enterprise environments.}

---

## 4. Authorisation

**Authorisation** = determining what an authenticated user is allowed to do.

Governed by two principles:
- **Least Privilege**  minimum access needed for the task
- **Separation of Duties**  responsibilities divided to prevent any one person having full control over a critical function

Both apply to people, systems, networks, databases, and processes not just human users.

### Authorisation Technologies:

| Technology | How it works | Security level |
|---|---|---|
| **HTTP Basic Auth** | Sends username/password with every request | Insecure  transmits credentials openly over network |
| **HTTPS** | Encrypted; doesn't expose credentials in transit | Secure  current standard |
| **OAuth** | Open-standard protocol; uses API tokens instead of passwords | Secure  tokens are encrypted, limited scope |

**OAuth** = open-standard authorisation protocol that shares designated access between applications using **API tokens**.

**API token** = a small block of encrypted code containing user identity, permissions, and expiry  never exposes the underlying password.

> {OAuth is why "Sign in with Google" is safer than creating a new account with a new password. The API token is scoped and encrypted  even if another platform is breached, your Google password stays safe.}

---

## 5. IAM  Identity and Access Management

**IAM** = a collection of processes and technologies that helps organisations manage digital identities in their environment.

IAM and AAA both:
- Authenticate users
- Determine access privileges
- Track activities

Goal: **right user → right resource → right time → right reason**

### User Provisioning:
**Provisioning** = creating and maintaining a user's digital identity (accounts, access rights, roles).
**Deprovisioning** = removing access rights when no longer needed  critical for preventing stale accounts.

### Three Authorisation Frameworks:

| Framework | Who decides access? | Strictness | Used in |
|---|---|---|---|
| **MAC** (Mandatory Access Control) | Central authority / system admin need-to-know basis | Strictest | Law enforcement, military, government |
| **DAC** (Discretionary Access Control) | Data owner decides | Flexible | Google Drive folder sharing |
| **RBAC** (Role-Based Access Control) | User's organisational role | Moderate | Most enterprise environments |

---

## 6. Accounting  Sessions, Logs & Monitoring

**Accounting** = monitoring the access logs of a system to track who accessed what and when.

**Access logs contain:** who accessed the system, when, and what resources they used.

Use cases for access logs:
- Identify trends (e.g. repeated failed logins)
- Detect unauthorised access
- Uncover data breaches
- First step in most security incident investigations

### Sessions:

**Session** = a sequence of HTTP requests and responses associated with the same user (from login to logout or timeout).

When a session starts, two things happen:
1. **Session ID** created  unique token identifying the user and device; active until browser closes or session times out
2. **Session cookie** exchanged  token that validates the session and controls its duration

Cookies allow websites to remember who you are without re-transmitting usernames and passwords on every request.

### Session Hijacking:

**Session hijacking** = attacker steals a legitimate user's session ID/cookie and impersonates them.

Consequences:
- Financial theft
- Data theft
- If SSO cookie is stolen → attacker gains access to all connected systems

> {Session hijacking is why just having HTTPS isn't enough. Cookie theft can happen even over HTTPS through XSS attacks. This is why monitoring session logs for impossible logins (same session ID, different geos) is a real SOC detection task.}

---

## 7. Full Framework Summary

```
AAA / IAM Framework:

Authentication → Who are you?
  - Knowledge (password)
  - Ownership (OTP)
  - Characteristic (biometrics)
  - Technologies: SSO, MFA, LDAP, SAML

Authorisation → What can you do?
  - Principles: Least Privilege, Separation of Duties
  - Technologies: HTTP Basic Auth, HTTPS, OAuth, API tokens
  - Frameworks: MAC, DAC, RBAC

Accounting → What did you do?
  - Tools: Access logs, session tracking, session IDs, cookies
  - Threat: Session hijacking
```

---

## Key Terms

| Term | Definition |
|---|---|
| AAA | Authentication, Authorisation, Accounting framework |
| IAM | Identity and Access Management |
| Authentication | Verifying identity |
| Authorisation | Determining access rights |
| Accounting | Monitoring and logging access activity |
| Knowledge factor | Something you know (password) |
| Ownership factor | Something you have (OTP, token) |
| Characteristic factor | Something you are (biometrics) |
| MFA / 2FA | Multi/Two-Factor Authentication |
| SSO | Single Sign-On  one login for multiple systems |
| Password fatigue | Tendency to reuse passwords across services |
| LDAP | Lightweight Directory Access Protocol  on-premises SSO |
| SAML | Security Assertion Markup Language  cloud SSO |
| OAuth | Open-standard authorisation using API tokens |
| API token | Encrypted token containing identity + permissions |
| Least Privilege | Minimum access needed for the task |
| Separation of Duties | Divide responsibilities to prevent misuse |
| MAC | Mandatory Access Control  central authority, strictest |
| DAC | Discretionary Access Control  data owner decides |
| RBAC | Role-Based Access Control  access by organisational role |
| User Provisioning | Creating and configuring user digital identities |
| Deprovisioning | Removing access rights when no longer needed |
| Session | Sequence of requests/responses from login to logout |
| Session ID | Unique token identifying user and device during session |
| Session Cookie | Token validating a session and its duration |
| Session Hijacking | Attacker steals session ID to impersonate a user |

---
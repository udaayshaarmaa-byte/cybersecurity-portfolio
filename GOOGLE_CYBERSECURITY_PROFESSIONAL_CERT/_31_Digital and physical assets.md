# Data States, InfoSec & Cloud Security Challenges

---

## 1. Data  The Most Valuable Asset

**Data** = information that is translated, processed, or stored by a computer.

Most modern organisational value is in information  and most information exists as data. Protecting data is central to all security work.

---

## 2. Three States of Data

Protecting data depends on **where it is and what it's doing**.

| State | Definition | Example |
|---|---|---|
| **Data in use** | Being actively accessed by one or more users | Checking your email inbox after logging in |
| **Data in transit** | Travelling from one point to another | Clicking send on an email  message in transit |
| **Data at rest** | Not currently being accessed; stored on a device | Closing your laptop and walking away  data sitting on the drive |

### Cloud complication for "data at rest":
Smartphones and devices now store data in the cloud  data on a device physically at rest may still be actively syncing or accessible remotely. "At rest" is no longer purely a physical state.

---

## 3. Information Security (InfoSec)

**InfoSec** = the practice of keeping data in **all three states** away from unauthorised users.

**Consequences of weak InfoSec:**
- Identity theft
- Financial loss
- Reputational damage to the organisation, partners, and customers

---

## 4. Cloud-Based Services

The shift to cloud has changed how data is managed and secured  and introduced new risks.

### Three Service Models (recap with security lens):

| Model | What the client gets | Client security responsibility |
|---|---|---|
| **SaaS** (Software as a Service) | Front-end applications via web browser | Data handling, user access management |
| **PaaS** (Platform as a Service) | Development tools and environments; back-end managed by CSP | Applications they build; resource configuration |
| **IaaS** (Infrastructure as a Service) | Remote access to servers, storage, networking | Everything above the infrastructure layer |

**Examples of major CSPs:** Google Cloud Platform, Microsoft Azure, AWS

> {The further up the stack (SaaS → PaaS → IaaS), the more the CSP manages. The further down (IaaS), the more the customer is responsible for. This is the core of the shared responsibility model.}

---

## 5. Shared Responsibility Model (Revisited)

In cloud environments, security responsibilities are split:

**CSP is responsible for:** physical infrastructure, hypervisors, networking, hardware

**Client is responsible for:**
- **Identity and access management (IAM)**
- **Resource configuration**
- **Data handling**

**Common failure point:** clients use out-of-the-box CSP configurations without adapting them to their specific security requirements → misconfiguration → breach.

---

## 6. Cloud Security Challenges

| Challenge | Detail |
|---|---|
| **Misconfiguration** | Biggest concern — clients configure their own cloud environment; default settings often don't meet security objectives |
| **Cloud-native breaches** | More likely due to misconfigured services than traditional infrastructure attacks |
| **Monitoring access** | Visibility can be limited depending on the service level and CSP |
| **Regulatory compliance** | Industries governed by HIPAA, PCI DSS, GDPR must meet specific requirements — cloud environments complicate compliance |

**Cloud security** = growing subfield of cybersecurity focused specifically on protecting data, applications, and infrastructure in the cloud. Ranked among the most in-demand cybersecurity skills globally.

---

## Key Terms

| Term | Definition |
|---|---|
| Data | Information translated, processed, or stored by a computer |
| Data in use | Data actively being accessed by a user |
| Data in transit | Data travelling between points on a network |
| Data at rest | Data stored on a device and not currently accessed |
| InfoSec | Information Security — keeping data in all states away from unauthorised users |
| SaaS | Software as a Service — front-end apps via browser |
| PaaS | Platform as a Service — dev tools and environments |
| IaaS | Infrastructure as a Service — remote access to back-end infrastructure |
| Shared Responsibility Model | CSP secures infrastructure; client secures what they put in it |
| Cloud-native breach | Breach caused by misconfigured cloud services |
| Misconfiguration | Incorrectly configured cloud settings — leading cause of cloud breaches |

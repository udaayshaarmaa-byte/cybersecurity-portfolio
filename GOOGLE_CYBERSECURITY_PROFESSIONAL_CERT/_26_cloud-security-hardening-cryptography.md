# Cloud Security, Hardening & Cryptography

---

## 1. Cloud Security Considerations

Cloud computing = on-demand access to a shared pool of configurable computing resources, released with minimal management effort.

Like any IT infrastructure, cloud needs securing — but it introduces **unique challenges**.

### Key Security Challenges:

| Challenge | Detail |
|---|---|
| **IAM (Identity Access Management)** | Loosely configured user roles = unauthorised access to critical cloud operations |
| **Configuration** | Every cloud service needs precise config; misconfiguration is a frequent source of breaches especially during cloud migrations |
| **Expanded attack surface** | Each additional service/application adds entry points; must compensate with increased security |
| **Zero-day attacks** | Previously unknown exploits; CSPs are often faster to respond than traditional IT orgs they can patch hypervisors and migrate workloads before customers are impacted |
| **Visibility limitations** | Orgs can monitor their own data via flow logs and packet mirroring, but cannot monitor traffic on the CSP's servers directly |
| **Rapid change** | CSPs update infrastructure frequently; orgs must adapt configurations and processes to match  security settings can break during updates |

> {The shift to cloud means you lose some control but gain scale and speed. The risk is assuming the CSP handles everything it doesn't. Misconfiguration is the #1 cloud security failure.}

---

## 2. Shared Responsibility Model

**Core principle:** security is split between the CSP and the customer.

| Responsibility | CSP | Customer (Organisation) |
|---|---|---|
| Physical data centres | ✅ | ❌ |
| Hypervisors | ✅ | ❌ |
| Host operating systems | ✅ | ❌ |
| Cloud infrastructure availability | ✅ | ❌ |
| Service configuration | ❌ | ✅ |
| Data stored in the cloud | ❌ | ✅ |
| Access control / IAM | ❌ | ✅ |
| Application security | ❌ | ✅ |

**Common mistake:** organisations assume the CSP is responsible for security they actually own. The CSP secures the cloud *infrastructure*; the org secures what it *puts in* the cloud.

---

## 3. Cloud Security Hardening Techniques

### IAM Identity Access Management
- Manages digital identities and authorises how users interact with cloud resources
- Misconfigured user roles = unauthorised access to critical operations
- Principle: least privilege  users only get access to what they need for their role

### Hypervisors
A **hypervisor** = software that abstracts hardware from the OS environment; enables virtualisation.

| Type | Runs on | Examples | Used by |
|---|---|---|---|
| **Type 1** | Bare metal (hardware directly) | VMware ESXi | CSPs (most common in cloud) |
| **Type 2** | Host OS (software layer) | VirtualBox | End users, home labs |

> {Your VirtualBox setup at home is a Type 2 hypervisor. CSPs use Type 1 for performance and security.}

**VM Escape** = exploit where a malicious actor breaks out of a VM and gains access to the hypervisor potentially reaching the host machine and other VMs. CSPs are responsible for patching against this.

### Baselining
- Establishes a **fixed reference point** for how the cloud environment should be configured
- Used to detect and investigate changes
- Examples of baseline controls:
  - Restricting access to the admin portal
  - Enabling password management
  - Enabling file encryption
  - Enabling threat detection for databases

### Cryptography
**Encryption** = scrambles data into **ciphertext**  unreadable without the encryption key.

- Modern encryption relies on **key secrecy**, not algorithm secrecy
- Protects **data in transit** and **data at rest**
- Applied to secure sensitive data stored and processed in the cloud

### Cryptographic Erasure (Crypto-Shredding)
- Traditional data destruction is less effective in cloud environments
- **Crypto-shredding** = destroying the encryption keys rather than the data itself
- Without the key, the data is permanently undecipherable
- All copies of the key must be destroyed  any surviving copy is a risk

> {Deleting a file in the cloud doesn't mean it's gone  it just means the pointer is removed. Destroying the encryption key is the only way to guarantee the data is unrecoverable.}

---

## 4. Key Management

Keeping encryption keys secure is the foundation of modern cryptography.

| Tool | Function |
|---|---|
| **TPM (Trusted Platform Module)** | Computer chip that securely stores passwords, certificates, and encryption keys |
| **CloudHSM (Cloud Hardware Security Module)** | Dedicated device for secure cryptographic key storage and operations (encryption/decryption) |

**Customer key management:**
- CSPs typically don't share their own encryption keys with customers
- Most CSPs allow customers to provide their own keys  the customer is then responsible for keeping those keys secure
- If customer-owned keys are compromised or destroyed, the CSP has very limited ability to help

**Audits:** customers can request CSP security audits and reports; they cannot access CSP systems directly. For US federal contractors: **FedRAMP** provides a list of verified CSPs.

---

## 5. Visibility Tools in the Cloud

| Tool | Purpose |
|---|---|
| **Flow logs** | Record metadata about network traffic (source, destination, protocol, volume) |
| **Packet mirroring** | Copies network packets for inspection  equivalent to packet sniffing in cloud environments |
| **Third-party audits** | CSPs commission independent audits to verify their security posture and identify vulnerabilities |

---

## Key Terms

| Term | Definition |
|---|---|
| Cloud Computing | On-demand access to shared, configurable computing resources |
| IAM | Identity Access Management  manages digital identities and cloud resource authorisation |
| Shared Responsibility Model | CSP secures the infrastructure; customer secures what they put in it |
| Hypervisor | Software that abstracts hardware to enable virtualisation |
| Type 1 Hypervisor | Runs directly on hardware (bare metal)  used by CSPs |
| Type 2 Hypervisor | Runs on a host OS  used by end users (e.g. VirtualBox) |
| VM Escape | Exploit where malware breaks out of a VM to access the hypervisor/host |
| Baseline | Fixed reference configuration used to detect unauthorised changes |
| Encryption | Converting data into ciphertext using an algorithm and key |
| Ciphertext | Scrambled, unreadable form of data |
| Cryptographic Erasure | Destroying encryption keys to render data permanently unreadable |
| Crypto-Shredding | Synonym for cryptographic erasure |
| TPM | Trusted Platform Module secure chip for key/credential storage |
| CloudHSM | Hardware security module for cryptographic operations in the cloud |
| Zero-Day Attack | Exploit targeting an unknown/unpatched vulnerability |
| Flow Logs | Cloud network traffic metadata records |
| Packet Mirroring | Cloud equivalent of packet sniffing copies traffic for inspection |

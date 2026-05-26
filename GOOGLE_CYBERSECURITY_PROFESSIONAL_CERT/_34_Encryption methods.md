# Cryptography, Encryption, PKI & Hashing

---

## 1. Cryptography Fundamentals

**Cryptography** = the process of transforming information into a form that unintended readers can't understand.

**Two-step process:**
1. **Encryption** — converts plaintext into ciphertext (unreadable)
2. **Decryption** — converts ciphertext back into plaintext (readable)

**Cipher** = an algorithm that encrypts information
**Cryptographic key** = a mechanism that decrypts ciphertext

### Caesar's Cipher (historical example):
- Shifts letters in the alphabet forward by a fixed number of spaces
- Shift of 3: A→D, B→E, "hello"→"khoor"
- **Flaws:** only 26 possible shifts (easily brute-forced); relies on a single key (if stolen, data is exposed)
- Led to development of more complex modern algorithms

**Brute force attack** = trial-and-error process of discovering private information (trying all possible keys)

---

## 2. Symmetric vs Asymmetric Encryption

| Feature | Symmetric | Asymmetric |
|---|---|---|
| Keys used | One shared secret key | Public + private key pair |
| Speed | Faster | Slower |
| Security | Less secure (key sharing risk) | More secure |
| Key length | Shorter | Longer (two keys generated) |
| Best for | Bulk data, ongoing sessions | Initial connection, high-value data |
| Example algorithms | AES, 3DES | RSA, DSA |

### Symmetric:
- Same key encrypts and decrypts
- Both sender and receiver must know the secret key
- Vulnerable: if the key is lost or stolen, the data is exposed

### Asymmetric:
- **Public key** = anyone can use it to encrypt data to send to you (like a mail slot  you can put things in but can't take them out)
- **Private key** = only you hold it; used to decrypt received data (opens the full box)
- Public key can be shared freely; private key never leaves the owner

---

## 3. Encryption Algorithms

### Symmetric Algorithms:

| Algorithm | Key length | Notes |
|---|---|---|
| **3DES** (Triple DES) | 168-bit effective (3 × 56-bit) | Based on original DES (1970s); being phased out; still in use for backwards compatibility |
| **AES** | 128, 192, or 256-bit | Most secure symmetric algorithm today; 128-bit would take modern computers billions of years to brute-force |

### Asymmetric Algorithms:

| Algorithm | Key length | Notes |
|---|---|---|
| **RSA** | 1,024 / 2,048 / 4,096-bit | One of the first asymmetric algorithms; used to protect highly sensitive data |
| **DSA** | 2,048-bit | NIST standard; complements RSA in PKI |

**Key length principle:** longer key = more secure but slower to compute. Balance between security and performance.

**Kerckhoff's Principle:** a cryptographic system should be secure even if everything about the system (except the private key) is public knowledge. Security must not depend on algorithm secrecy only on key secrecy.


---

## 4. Public Key Infrastructure (PKI)

**PKI** = an encryption framework that secures the exchange of information online.

PKI is a **two-step process:**

### Step 1  Encrypted information exchange:
Uses asymmetric encryption, symmetric encryption, or both depending on priority:
- **Asymmetric** when security is the priority (establishing a connection)
- **Symmetric** when speed is the priority (ongoing session data)

Example: mobile chat apps use asymmetric to establish the connection, then switch to symmetric for the actual conversation.

### Step 2  Trust establishment via digital certificates:
**Problem:** how do computers know the public key they've received is from who they think it is?

**Solution:** digital certificates issued by a Certificate Authority (CA).

**Digital certificate** = a file that verifies the identity of a public key holder  like a digital ID badge.

### How a digital certificate is created:
```
1. Business registers domain
2. Hosting company sends company info + public key to a Certificate Authority (CA)
3. CA verifies the company's identity
4. CA encrypts the company data with its own private key
5. CA issues a digital certificate containing:
   - Encrypted company data
   - CA's digital signature (proves authenticity)
6. Certificate is used online to establish trust
```

**Certificate Authority (CA)** = a trusted third party that issues and verifies digital certificates.

---

## 5. Generating Keys

**OpenSSL** = open-source command-line tool used to generate public and private keys; used by computers to verify digital certificates in PKI.

**Heartbleed bug (2014):** vulnerability in OpenSSL that exposed sensitive data in memory of websites and applications — patched the same year; highlights why keeping security tools up to date is critical.

---

## 6. Hash Functions

**Hash function** = an algorithm that produces a unique code (hash value / digest) that **cannot be decrypted**.

Unlike encryption:
- **One-way process** — no decryption key generated
- Input of any size → fixed-size output (hash value)
- Even a single character change in input → completely different hash

**Primary use:** verifying **data integrity** (has a file been tampered with?)

**Non-repudiation** = the concept that the authenticity of information can't be denied; hash functions make this possible.

### Practical use in Linux:
```bash
sha256sum newfile.txt
```
Generates the SHA-256 hash of a file — can be compared against known malicious file hashes in databases like **VirusTotal**.

---

## 7. Hashing Algorithms

| Algorithm | Hash length | Status |
|---|---|---|
| **MD5** | 128-bit (32 chars) | Vulnerable to hash collisions; avoid for new implementations |
| **SHA-1** | 160-bit | Considered weak; being phased out |
| **SHA-224** | 224-bit | Collision-resistant |
| **SHA-256** | 256-bit | Current standard — widely used |
| **SHA-384** | 384-bit | Collision-resistant |
| **SHA-512** | 512-bit | Collision-resistant; highest in SHA family |

**SHA family** = Secure Hashing Algorithms; approved by NIST.

### Hash Collision:
- Occurs when two different inputs produce the same hash value
- MD5 is vulnerable to this — makes it unsuitable for security-critical use
- Longer hash values = less collision risk

### Rainbow Table Attack:
- Attackers pre-compute hash values for common/weak passwords
- Compare stolen hashed password database against the table
- **Defence: salting**

### Salting:
- Add a random string of characters to data **before** hashing
- Each password gets a unique salt → even identical passwords produce different hashes
- Makes rainbow table attacks ineffective

```
"password" + random_salt → hash (unique per user even with same password)
```

---

## 8. How Encryption and Hashing Work Together

```
PKI (asymmetric) → establishes trust, secures key exchange
Symmetric encryption → protects bulk data in transit (speed)
Hashing → verifies file/data integrity (non-repudiation)
Salting → strengthens password storage against rainbow tables
```

---

## Key Terms

| Term | Definition |
|---|---|
| Cryptography | Process of transforming information to protect it from unintended readers |
| Plaintext | Original readable data |
| Ciphertext | Encrypted, unreadable data |
| Cipher | Algorithm that encrypts information |
| Cryptographic key | Mechanism that decrypts ciphertext |
| Symmetric encryption | Single shared secret key for both encryption and decryption |
| Asymmetric encryption | Public key encrypts; private key decrypts |
| AES | Advanced Encryption Standard — most secure symmetric algorithm |
| 3DES | Triple DES — older symmetric algorithm; being phased out |
| RSA | Rivest Shamir Adleman — asymmetric algorithm for high-sensitivity data |
| DSA | Digital Signature Algorithm — asymmetric; used in PKI |
| PKI | Public Key Infrastructure — framework securing online information exchange |
| Digital Certificate | File verifying identity of a public key holder |
| CA | Certificate Authority — trusted third party issuing digital certificates |
| OpenSSL | Open-source tool for generating keys and verifying certificates |
| Hash function | One-way algorithm producing a fixed-size digest; cannot be decrypted |
| Hash value / digest | Unique output of a hash function |
| Data integrity | Accuracy and consistency of information |
| Non-repudiation | Authenticity of information cannot be denied |
| MD5 | Early hash algorithm — 128-bit; vulnerable to hash collisions |
| SHA-256 | Current standard hash algorithm — 256-bit; collision-resistant |
| Hash collision | Two different inputs producing the same hash value |
| Rainbow table | Pre-computed database of hash values for common passwords |
| Salting | Adding random characters to data before hashing; defeats rainbow tables |
| Kerckhoff's Principle | Security must rely on key secrecy, not algorithm secrecy |
| Brute force attack | Trial-and-error process of discovering private information |
| VirusTotal | Online tool for comparing hash values against known malicious files |
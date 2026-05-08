## 1. What is a Network Protocol?

A **network protocol** = a set of rules used by two or more devices on a network to describe the order of delivery and the structure of data.

- Acts as a common language for devices to communicate across the globe
- Comes packaged with data packets as instructions for the receiving device
- Each protocol has security implications — some are exploitable

---

## 2. Three Categories of Network Protocols

### Category 1 — Communication Protocols
Govern the exchange of information; define how and when data is transmitted.

| Protocol | Layer | Port | Purpose |
|---|---|---|---|
| **TCP** | Transport | — | Forms connections; reliable data streaming; uses 3-way handshake (SYN → SYN/ACK → ACK) |
| **UDP** | Transport | — | Connectionless; fast; no reliability tracking; used for DNS requests, streaming, gaming |
| **HTTP** | Application | 80 | Client-server web communication; **insecure** — being replaced by HTTPS |
| **DNS** | Application | 53 (UDP default; TCP for large replies) | Translates domain names to IP addresses |

### Category 2 — Management Protocols
Used for monitoring and managing network activity, error reporting, and performance.

| Protocol | Layer | Purpose |
|---|---|---|
| **SNMP** | Application | Monitors/manages network devices; can reset passwords, change configs, report bandwidth usage |
| **ICMP** | Internet | Reports transmission errors between devices; used by `ping` to test connectivity and latency |
| **DHCP** | Application | Assigns unique IP addresses to devices; provides DNS server and default gateway info |

DHCP ports: **UDP port 67** (server) / **UDP port 68** (client)

### Category 3 — Security Protocols
Ensure data is sent and received securely using encryption.

| Protocol | Layer | Port | Purpose |
|---|---|---|---|
| **HTTPS** | Application | 443 | Secure web communication; uses SSL/TLS encryption |
| **SFTP** | Application | 22 (via SSH) | Secure file transfer; uses AES and other encryption; used with cloud storage |
| **SSH** | Application | 22 | Encrypted remote system access; replaces Telnet |

> {Security protocols encrypt the data payload but do NOT hide source/destination IP addresses. A packet capture still reveals who is talking to whom — just not what they're saying.}

---

## 3. Additional Protocols Reference

| Protocol | Layer | Port(s) | Notes |
|---|---|---|---|
| **ARP** | Network Access (Layer 2) | No port (Layer 2) | Maps IP addresses to MAC addresses; no port number |
| **NAT** | Internet + Transport | — | Translates private IPs to public IP for internet communication |
| **Telnet** | Application | TCP 23 | Remote access; **sends all data in cleartext — insecure; replaced by SSH** |
| **POP3** | Application | TCP/UDP 110 (unencrypted), 995 (SSL/TLS) | Downloads email to local device; may delete from server after download; no multi-device sync |
| **IMAP** | Application | TCP 143 (unencrypted), 993 (TLS) | Email stays on server; supports multi-device sync; partial read before full download |
| **SMTP** | Application | TCP/UDP 25 (unencrypted), 587 (TLS) | Sends/routes email; works with MTA software; port 25 commonly abused for spam |

---

## 4. How Protocols Work Together — Real Example

Visiting `www.yummyrecipesforme.org`:

```
1. TCP        → establishes connection with web server (3-way handshake)
2. ARP        → resolves MAC address of next router along the path
3. DNS        → translates domain name to IP address (port 53)
4. HTTPS      → securely requests and receives the webpage (port 443, SSL/TLS encrypted)
```

> {Four protocols firing just to load one webpage. In a SOC context, anomalies in any of these — e.g. DNS request to an unusual domain, ARP requests flooding the network — are potential threat indicators.}

---

## 5. NAT & Private IP Ranges

**NAT (Network Address Translation)** = router replaces a device's private IP with the network's public IP for outbound traffic, and reverses this for inbound responses.

**Private IP ranges (RFC 1918 — memorise these):**
- `10.0.0.0 – 10.255.255.255`
- `172.16.0.0 – 172.31.255.255`
- `192.168.0.0 – 192.168.255.255`

These never appear as source IPs on the public internet — if you see them in external traffic logs, something is wrong.

---

## 6. Wireless Security Protocols — Evolution

Wi-Fi = **IEEE 802.11** standards family (maintained by the Institute of Electrical and Electronics Engineers)

| Protocol | Year | Key Feature | Vulnerability |
|---|---|---|---|
| **WEP** | 1999 | First wireless security standard | Broken encryption — considered high-risk; avoid |
| **WPA** | 2003 | Introduced TKIP; larger key sizes; message integrity check | KRACK attack — attacker intercepts handshake, resets encryption key to zeros |
| **WPA2** | 2004 | Uses AES + CCMP; current security standard | Still vulnerable to KRACK |
| **WPA3** | 2018 | Uses SAE; 128-bit (192-bit in enterprise); KRACK-resistant | Most secure current option |

### WPA2 Personal vs Enterprise:

| | Personal | Enterprise |
|---|---|---|
| Setup | Simple; single global passphrase | Complex; centralised; individual access control |
| Best for | Home networks | Business environments |
| Key visibility | Users share the passphrase | Users never see encryption keys |

> {WPA2 Enterprise is far more secure for orgs because admins can revoke individual user access instantly — you can't do that with a shared passphrase.}

### KRACK Attack (Key Reinstallation Attack):
- Attacker inserts themselves into the WPA/WPA2 authentication handshake
- Replaces the dynamic encryption key with a new key (often all zeros)
- Result: transmission is effectively unencrypted
- **WPA3 fix:** uses SAE (Simultaneous Authentication of Equals) — prevents key reinstallation

---

## 7. Port Number Reference — Must Memorise

| Port | Protocol | Notes |
|---|---|---|
| 20/21 | FTP | File transfer (unencrypted) |
| 22 | SSH / SFTP | Encrypted remote access and file transfer |
| 23 | Telnet | Remote access — cleartext, insecure |
| 25 | SMTP | Email sending — unencrypted; spam abuse |
| 53 | DNS | Domain name resolution (UDP default) |
| 67/68 | DHCP | IP address assignment |
| 80 | HTTP | Web — unencrypted |
| 110 | POP3 | Email retrieval — unencrypted |
| 143 | IMAP | Email retrieval — unencrypted |
| 443 | HTTPS | Web — encrypted (SSL/TLS) |
| 587 | SMTP (TLS) | Email sending — encrypted |
| 993 | IMAP (TLS) | Email retrieval — encrypted |
| 995 | POP3 (TLS) | Email retrieval — encrypted |

---

## Key Terms

| Term | Definition |
|---|---|
| Network Protocol | Rules governing how devices communicate on a network |
| TCP | Reliable, connection-oriented transport protocol; 3-way handshake |
| UDP | Connectionless, fast transport protocol |
| DNS | Translates domain names to IP addresses |
| HTTPS | Encrypted web communication using SSL/TLS |
| ARP | Maps IP addresses to MAC addresses |
| NAT | Translates private IPs to public IP for internet traffic |
| DHCP | Automatically assigns IP addresses on a network |
| SNMP | Manages and monitors network devices |
| ICMP | Reports network errors; used by `ping` |
| SMTP | Sends and routes email |
| POP3 | Downloads email locally; limited multi-device support |
| IMAP | Email stays on server; multi-device sync |
| SSH | Encrypted remote access; replaces Telnet |
| Telnet | Remote access — cleartext, insecure; avoid |
| WEP | Oldest wireless protocol; broken — avoid |
| WPA/WPA2/WPA3 | Wireless security protocols; WPA3 is most secure |
| KRACK | Key reinstallation attack against WPA/WPA2 |
| SAE | WPA3's handshake method; KRACK-resistant |
| IEEE 802.11 | Family of Wi-Fi standards |

---

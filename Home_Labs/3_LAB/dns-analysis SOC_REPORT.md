# Lab 3 — DNS Traffic Analysis with Wireshark

**Home Lab Series 
**Analyst:** Uday Shaarma  
**Environment:** Ubuntu VM (10.0.2.15) → NAT → DNS Server (192.168.31.1) → Internet  
**Tools:** Wireshark, nslookup, dig | Ubuntu 
---

## Objective

Capture and analyse DNS traffic between Ubuntu VM and a real DNS server using Wireshark. Understand how DNS queries and responses work at the packet level, identify key DNS record types, and recognise anomaly patterns indicative of malicious behaviour such as DNS tunnelling.

---

## Lab Setup

| Component | Detail |
|-----------|--------|
| VM | Ubuntu 26.04 (VirtualBox) |
| Network Adapter | NAT (enp0s3) |
| Source IP | 10.0.2.15 (Ubuntu VM) |
| DNS Server IP | 192.168.31.1 (NAT gateway) |
| Wireshark Filter | `dns` (display filter) |
| Capture Interface | enp0s3 |

---

## DNS Query/Response Cycle

Every DNS interaction follows a two-step pattern:

```
Ubuntu (10.0.2.15)  ──[Query]──►  DNS Server (192.168.31.1)
Ubuntu (10.0.2.15)  ◄──[Response]──  DNS Server (192.168.31.1)
```

- Query packet: QR flag = 0
- Response packet: QR flag = 1
- Transaction ID matches query to its response

> {This is simpler than DHCP's DORA — DNS is just ask and answer. No lease, no acknowledgement needed.}

---

## Observations — Packet by Packet

### 1. google.com — A and AAAA Records

```
Packet 1: Ubuntu → DNS    Standard query A google.com
Packet 2: DNS → Ubuntu    Standard query response A 142.250.192.238
Packet 3: Ubuntu → DNS    Standard query AAAA google.com
Packet 4: DNS → Ubuntu    Standard query response AAAA 2404:6800:4002:823::200e
```

**What I observed:** Ubuntu sends both an A (IPv4) and AAAA (IPv6) query simultaneously. Both return valid answers — google.com supports dual-stack.


---

### 2. github.com — A Record and SOA Response

```
Packet 1: Ubuntu → DNS    Standard query A github.com
Packet 2: DNS → Ubuntu    Standard query response A 20.207.73.82
Packet 3: Ubuntu → DNS    Standard query AAAA github.com
Packet 4: DNS → Ubuntu    Standard query response AAAA SOA ns-1707.awsdns-21.co.uk
```

**What I observed:** github.com has an IPv4 address (20.207.73.82) but no IPv6. When AAAA was queried, the DNS server returned a SOA (Start of Authority) record instead  meaning "I'm authoritative for this domain and no IPv6 record exists."

**#** Any AAAA traffic directed TO github.com from inside a network would be suspicious since the domain has no IPv6.

> {SOA = the DNS server saying "I own this domain and I'm telling you no IPv6 here." It's a definitive negative answer, not a timeout.}

---

### 3. gmail.com — MX Records

```
Packet 1: Ubuntu → DNS    Standard query MX gmail.com
Packet 2: DNS → Ubuntu    Standard query response MX (multiple records)
```

**Mail servers returned (with priority):**

| Priority | Mail Server |
|----------|-------------|
| 5 | gmail-smtp-in.l.google.com |
| 10 | alt1.gmail-smtp-in.l.google.com |
| 20 | alt2.gmail-smtp-in.l.google.com |
| 30 | alt3.gmail-smtp-in.l.google.com |
| 40 | alt4.gmail-smtp-in.l.google.com |

**What I observed:** Lower priority number = higher preference. Mail delivery attempts gmail-smtp-in first, then falls back to alt1 → alt4.

---

### 4. google.com — TXT Records

```
Packet 1: Ubuntu → DNS    Standard query TXT google.com
Packet 2: DNS → Ubuntu    Standard query response TXT (1002 bytes — multiple TXT records)
```

**What I observed:** Response was 1002 bytes significantly larger than all other query responses. TXT records contained SPF, DKIM keys, and domain verification strings.

**#** TXT records are the primary vector for DNS tunnelling. Attackers encode stolen data inside TXT record responses to exfiltrate it through DNS, which is rarely blocked by firewalls. A 1002-byte TXT response from an unknown domain would be a major red flag.

> {This is why the Sigma rule targets TXT records specifically. Legitimate TXT lookups like SPF/DKIM checks happen occasionally — hundreds per minute from an unknown domain means something is being exfiltrated.}

---

### 5. amazon.com — A Record with Load Balancing

```
Packet 1: Ubuntu → DNS    Standard query A amazon.com
Packet 2: DNS → Ubuntu    Standard query response A (3 IP addresses)
```

**dig output:**
```
amazon.com    886    IN    A    98.87.170.71
amazon.com    886    IN    A    98.87.170.74
amazon.com    886    IN    A    98.82.161.185
```

**What I observed:** Three IPs returned for one domain load balancing across distributed infrastructure. TTL of 886 seconds is normal for stable infrastructure.



---

### 6. ipv6.google.com — AAAA with CNAME Chain

```
Packet 1: Ubuntu → DNS    Standard query AAAA ipv6.google.com
Packet 2: DNS → Ubuntu    Standard query response AAAA CNAME + AAAA record
```

**dig output:**
```
ipv6.google.com      203    IN    CNAME    ipv6.l.google.com
ipv6.l.google.com    225    IN    AAAA     2404:6800:4002:82a::200e
```

**What I observed:** Not a direct AAAA response the DNS server first returned a CNAME (alias) pointing ipv6.google.com to ipv6.l.google.com, then resolved that to the IPv6 address. Two-step resolution.

**#** CNAME chaining is used by attackers to redirect C2 traffic through multiple domains, making it harder to identify and block the real server. Multiple CNAME hops to unknown domains = red flag.

> {CNAME is basically a domain alias. google.com uses it for internal infrastructure management. Attackers use it to hide behind legitimate-looking domain chains.}

---

### 7. connectivity-check.ubuntu.com — Background Traffic

```
Packet 32: Ubuntu → DNS    Standard query AAAA connectivity-check.ubuntu.com
Packet 33: DNS → Ubuntu    Standard query response AAAA 2620:2d:4002:1::196
```

**What I observed:** I didn't trigger this query. Ubuntu automatically runs connectivity checks in the background. This appeared in my capture without any terminal commands.

**#** In a real environment, analysts need to establish which DNS traffic is OS-generated versus user or application-generated. Background traffic creates noise that can mask malicious activity.


---

## DNS Record Types — Summary

| Record | Purpose | SOC Relevance |
|--------|---------|---------------|
| A | Maps domain → IPv4 | Baseline traffic — most common |
| AAAA | Maps domain → IPv6 | Monitor for IPv6 exfiltration |
| MX | Mail server for domain | Phishing/spam infrastructure recon |
| CNAME | Alias → another domain | C2 domain aliasing |
| TXT | Arbitrary text data | HIGH — DNS tunnelling vector |
| SOA | Authoritative nameserver info | Negative answer — record doesn't exist |
| NS | Nameserver for domain | DNS hijacking detection |

---

---


---


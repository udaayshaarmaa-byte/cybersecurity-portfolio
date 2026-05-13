# DoS & DDoS Attacks | Notes


---

## 1. Denial of Service (DoS)

A **DoS attack** = floods a network or server with traffic to disrupt normal operations.

**Goal:** overwhelm a network device until it crashes or can no longer respond to legitimate users.

**Impact:**
- Business operations halted → costs money and time
- Crashed network leaves org vulnerable to further attacks

---

## 2. Distributed Denial of Service (DDoS)

A **DDoS attack** = a DoS attack using **multiple devices or servers** from different locations to flood the target simultaneously.

- Multiple sources = harder to block a single IP
- Combined traffic volume is more likely to overwhelm the target
- Attackers often use botnets (networks of compromised machines) to launch DDoS


---

## 3. Three Common Network-Level DoS Attacks

### Attack 1 — SYN Flood Attack
**Protocol abused:** TCP (Transport Layer)

**How TCP handshake normally works:**
```
Client → SYN          → Server
Client ← SYN/ACK      ← Server (port left open)
Client → ACK           → Server (connection established)
```

**How the attack works:**
- Attacker floods the server with SYN requests but never sends the final ACK
- Server leaves ports open waiting for ACK packets that never arrive
- When SYN requests exceed available ports → server is overwhelmed → crashes

---

### Attack 2 — ICMP Flood Attack
**Protocol abused:** ICMP (Internet Layer)

**How it works:**
- Attacker repeatedly sends ICMP packets to a network server
- Server is forced to send an ICMP reply to every one
- Consumes all available bandwidth for both incoming and outgoing traffic → server crashes

**ICMP recap:** Internet Control Message Protocol — used by devices to report transmission errors and status updates (also used by `ping`)

---

### Attack 3 — Ping of Death
**Protocol abused:** ICMP (Internet Layer)

**How it works:**
- Attacker sends a single **oversized ICMP packet** larger than **64 KB** (the maximum valid size)
- Vulnerable server tries to process the malformed packet → system overloads → crashes
- One packet can be enough — volume is not required

**Analogy from lecture:** dropping a large rock on an anthill — each ant can only carry so much; one large impact collapses the whole colony.

---

## 4. Quick Comparison

| Attack | Protocol | Mechanism | Volume needed? |
|---|---|---|---|
| **SYN Flood** | TCP | Exploits 3-way handshake; exhausts server ports | Yes — many SYN packets |
| **ICMP Flood** | ICMP | Forces continuous ICMP replies; saturates bandwidth | Yes — many packets |
| **Ping of Death** | ICMP | Single oversized packet exceeds 64 KB limit | No — one packet enough |

---

## Key Terms

| Term | Definition |
|---|---|
| DoS | Denial of Service — floods a single target to disrupt operations |
| DDoS | Distributed DoS — same attack from multiple sources simultaneously |
| SYN Flood | Exploits TCP handshake; exhausts server ports with incomplete connections |
| ICMP Flood | Overwhelms server by forcing constant ICMP replies |
| Ping of Death | Single oversized ICMP packet (>64 KB) crashes the target |
| Botnet | Network of compromised machines used to launch DDoS attacks |
| Bandwidth | Amount of data a network can handle per second — primary target of flood attacks |

---

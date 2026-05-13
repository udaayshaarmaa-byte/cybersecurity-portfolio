# Packet Sniffing & IP Spoofing Notes
---

## 1. Packet Sniffing

**Packet sniffing** = using software tools to observe and capture data as it moves across a network.

**Legitimate use:** security analysts use it to investigate incidents and debug network issues (tools like Wireshark, tcpdump).

**Malicious use:** threat actors intercept packets to steal data from the body (names, passwords, financial info, credit card numbers).

### How attackers gain access:
- Insert themselves between two communicating devices
- Set a NIC (Network Interface Card) to **promiscuous mode** — accepts ALL traffic on the network, not just packets addressed to that device
- Capture and store data for later use or use IP/MAC addresses to launch further attacks

### Two Types of Packet Sniffing:

| Type | What happens | Analogy |
|---|---|---|
| **Passive** | Packets are read in transit — no modification | Postal worker reading your mail without delivering it differently |
| **Active** | Packets are manipulated in transit — data altered or redirected | Neighbour intercepts your mail, reads it, changes the letter, then delivers it |

---

## 2. Preventing Packet Sniffing

| Defence | How it helps |
|---|---|
| **VPN** | Encrypts data in transit — attacker can intercept but cannot decode |
| **HTTPS (SSL/TLS)** | Encrypts application-layer data — eavesdropping yields nothing readable |
| **Avoid unprotected Wi-Fi** | Public Wi-Fi has no encryption — anyone on the network can see all traffic; use VPN if you must connect |

---

## 3. IP Spoofing

**IP spoofing** = attacker changes the **source IP address** of a data packet to impersonate an authorised system — bypasses firewall rules that block untrusted external traffic.

**Setup:** attacker first sniffs the network → learns real IP and MAC addresses of authorised devices → uses those addresses to impersonate them.

---

## 4. IP Spoofing Attack Types

### On-Path Attack (Meddler-in-the-Middle)
- Attacker places themselves between two trusted devices (e.g. browser and web server)
- Intercepts or **alters data in transit** — can collect usernames, passwords, session tokens
- Can also intercept a **DNS lookup** and spoof the DNS response → redirect a legitimate domain to a malicious IP
- **Defence:** encrypt data in transit using TLS — even if intercepted, data is unreadable

### Replay Attack
- Attacker intercepts a valid data packet and either:
  - **Delays** it → causes connection issues between target devices
  - **Repeats** it later → impersonates the original authorised sender
- Example: capturing an authentication token and replaying it to log in as the victim
- **Defence:** session tokens with expiry times; timestamps; TLS

### Smurf Attack
- Combines **IP spoofing + DDoS**
- Attacker sniffs an authorised user's IP address
- Sends spoofed ICMP packets to the network **broadcast address** using the victim's IP as the source
- Every device on the network replies to the victim's IP → victim is overwhelmed with ICMP echo responses → server/network crashes
- **Defence:** NGFW with anomaly detection; block directed broadcast at the router level

---

## 5. Quick Comparison — All Interception Attacks

| Attack | Technique used | Primary goal | Defence |
|---|---|---|---|
| **Passive Sniffing** | NIC in promiscuous mode | Steal data silently | VPN, HTTPS |
| **Active Sniffing** | Packet manipulation | Alter or redirect traffic | VPN, HTTPS, encryption |
| **On-Path (MitM)** | Intercept trusted connection | Steal credentials, redirect DNS | TLS encryption |
| **Replay Attack** | Capture + retransmit valid packet | Impersonate authorised user | Token expiry, TLS, timestamps |
| **Smurf Attack** | IP spoof + ICMP broadcast flood | DDoS via amplification | NGFW, block directed broadcast |
| **DoS via IP Spoof** | Flood target with fake-source packets | Crash server | Firewall rules rejecting spoofed IPs |

---

## 6. Firewall Defence Against IP Spoofing

**Key firewall rule:** reject all **inbound internet traffic** where the source IP matches the **internal private network's IP range**.

Logic: if a packet arrives from the internet claiming to be from `192.168.x.x`, it's spoofed — all real devices with those IPs are already inside the LAN.
---

## 7. Defence-in-Depth Principle

No single defence stops everything. Layer multiple strategies:

```
Encryption (TLS/VPN) → makes intercepted data unreadable
Firewall rules       → blocks spoofed IPs at the perimeter
NGFW anomaly detection → catches unusual traffic patterns (smurf, flood)
Secure protocols     → HTTPS, SSH instead of HTTP, Telnet
Network segmentation → limits blast radius if attack succeeds
```

---

## Key Terms

| Term | Definition |
|---|---|
| Packet Sniffing | Capturing and inspecting data packets on a network |
| Passive Sniffing | Read-only interception — no packet modification |
| Active Sniffing | Intercept and modify packets in transit |
| NIC | Network Interface Card — hardware connecting a device to a network |
| Promiscuous Mode | NIC setting that accepts all network traffic, not just addressed packets |
| IP Spoofing | Changing source IP of a packet to impersonate an authorised device |
| On-Path Attack | Attacker inserts between two trusted devices; intercepts/alters traffic |
| Replay Attack | Capture and re-send a valid packet to impersonate the original sender |
| Smurf Attack | IP spoof + ICMP broadcast flood = DDoS via amplification |
| Defence-in-Depth | Layered security strategy — no single point of failure |

---
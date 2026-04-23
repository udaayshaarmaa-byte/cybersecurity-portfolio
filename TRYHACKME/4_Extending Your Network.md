# Port Forwarding, Firewalls, VPNs, Routers & Switches


---

## 1. Port Forwarding

- Without port forwarding, a server (e.g. web server on 192.168.1.10:80) is only accessible to devices **within the same local network** (intranet)
- Port forwarding exposes that service to the **public internet** via the router's public IP
- Example: Internal server at 192.168.1.10:80 becomes reachable via public IP 82.62.51.70:80
- **Configured at the router** of a network
- Port forwarding **opens specific ports** — it does NOT control whether traffic is allowed through (that's the firewall's job)

> Key distinction: Port forwarding = opens ports. Firewall = controls traffic through those ports.

---

## 2. Firewalls

A firewall is a network device that determines what traffic is **allowed to enter and exit** a network. Think of it as border security — administrators configure rules based on:

- **Source** — where is the traffic coming from?
- **Destination** — where is it going?
- **Port** — what port is it destined for?
- **Protocol** — is it TCP, UDP, or both?

Firewalls perform **packet inspection** to answer these questions. They come in hardware form (enterprise networks) and software form (e.g. Snort).

### Firewall Types

| Type | How it Works | Key Characteristics |
|---|---|---|
| **Stateful** | Inspects the **entire connection**, not just individual packets | Dynamic decision-making; consumes more resources; can allow early handshake parts that later fail; blocks the **entire device** if a bad connection is detected |
| **Stateless** | Uses **static rules** to evaluate **individual packets** | Lightweight, fewer resources; only as smart as its rules — if no rule matches, useless; great for handling large traffic volumes (e.g. DDoS) |

---

## 3. VPN (Virtual Private Network)

A VPN creates an encrypted **tunnel** between devices across the internet, allowing them to communicate as if on the same private network.

### How it works
- Devices on separate physical networks join a **virtual private network (Network #3)**
- They remain part of their original networks but also share the VPN tunnel
- Traffic through the tunnel is encrypted — not visible to ISPs or intermediaries

### VPN Benefits

| Benefit | Description |
|---|---|
| **Geographic connection** | Links offices/networks in different locations — shared resources (servers, infrastructure) accessible remotely |
| **Privacy** | Encrypts data so it can only be understood by sender and receiver — protects against sniffing, especially on public WiFi |
| **Anonymity** | Hides traffic from ISPs and intermediaries — though only as private as the VPN provider's own logging policies |

> Note: TryHackMe uses a VPN to let you interact with vulnerable machines without exposing them to the public internet.

### VPN Technologies

| Technology | Description |
|---|---|
| **PPP** | Handles authentication and encryption using private key + public certificate (similar to SSH). Non-routable — cannot leave a network on its own |
| **PPTP** (Point-to-Point Tunneling Protocol) | Allows PPP data to travel and leave a network. Easy to set up, widely supported — but **weakly encrypted** |
| **IPSec** (Internet Protocol Security) | Encrypts data using the existing IP framework. Harder to set up — but **strong encryption** and widely supported |

---

## 4. Routers

- A router's job is to **connect networks** and pass data between them
- Operates at **Layer 3 (Network Layer)** of the OSI model
- Uses **routing** — the process of creating a path between networks for data to travel
- Can be configured via web interface or console (port forwarding, firewall rules, etc.)

### Route Selection Factors
When multiple paths exist between networks, routers choose based on:
- **Shortest path**
- **Most reliable path**
- **Fastest medium** (e.g. fibre vs copper)

> Routers are dedicated devices — they do NOT perform switch functions.

---

## 5. Switches

A switch connects **multiple devices** within a network (3 to 63 devices) using Ethernet cables. Switches operate at **Layer 2 or Layer 3** — but not both simultaneously on the same switch.

### Layer 2 Switch
- Operates at the **Data Link layer**
- Forwards **frames** to devices using **MAC addresses**
- Sole job: send frames to the correct device
- Cannot perform routing

### Layer 3 Switch
- More sophisticated — can perform some **router functions**
- Sends frames using **MAC addresses** (like Layer 2)
- Also **routes packets** between devices using **IP addresses**
- Supports **VLANs**

### VLAN (Virtual Local Area Network)
- Virtually splits devices on the **same physical switch** into separate networks
- Each VLAN has its own IP subnet (e.g. 192.168.1.1 for Sales, 192.168.2.1 for Accounting)
- Devices in different VLANs **cannot communicate with each other** by default — even on the same switch
- All VLANs can still share an internet connection via the router
- Provides **network segmentation and security**

---

## Quick Comparison: Router vs Switch

| | **Router** | **Switch (L2)** | **Switch (L3)** |
|---|---|---|---|
| OSI Layer | Layer 3 | Layer 2 | Layer 3 |
| Uses | IP addresses | MAC addresses | Both |
| Function | Connects networks | Connects devices in a network | Connects + routes between VLANs |
| Supports VLANs | No (natively) | No | Yes |

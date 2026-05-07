# Network Architecture & Cloud Networking
---

## 1. What is a Network?

A **network** = a group of connected devices that communicate with each other over wired or wireless connections.

Devices identify each other using two unique addresses:
- **IP address** — logical address, used for routing across networks
- **MAC address** — physical address, burned into the hardware, used within a local network

---

## 2. Types of Networks

| Type | Scope | Example |
|---|---|---|
| **LAN** (Local Area Network) | Small area — office, home, school | Your phone connecting to home Wi-Fi |
| **WAN** (Wide Area Network) | Large geographic area — city, country, globe | The internet; employee in Sydney communicating with one in Dublin |

> {The internet is essentially one massive WAN. LAN is what you control locally — WAN is everything beyond your router.}

---

## 3. Network Devices

### Hub
- Broadcasts data to **every device** on the network — no targeting
- Like a radio tower — everyone tuned in receives the signal
- **Security risk:** vulnerable to eavesdropping (all devices see all traffic)
- Rarely used in modern networks — mostly limited home/office setups

### Switch
- Sends data **only to the intended destination** device
- Maintains a **MAC address table** — matches device MAC addresses to port numbers
- More secure and more efficient than a hub
- Part of the **data link layer** in the TCP/IP model
- Preferred device in most modern networks

### Router
- Connects **multiple networks** together
- Reads the **IP address** in the packet header → forwards to the next router on the path
- Part of the **network layer** in the TCP/IP model
- Can include a built-in firewall to block malicious traffic
- Data path: Computer → Router → Modem → Internet → Recipient's Modem → Recipient's Router → Device

### Modem
- Connects your router to the ISP → brings internet access to the LAN
- Converts digital signals from the internet into a format compatible with your local connection
- ISPs use telephone lines, coaxial cables, or fibre optic cables

### Wireless Access Point (WAP)
- Sends and receives data over **radio waves** — creates a wireless network
- Devices connect via Wi-Fi (a set of wireless communication standards)
- WAP → Router/Switch → final destination

### Firewall
- Monitors and filters incoming and outgoing network traffic
- Configured by the organisation with security rules
- Sits between the **internal trusted network** and the **external untrusted internet**
- First line of defence — but not the only one

### Server
- Provides information and services to other devices (**clients**)
- **Client-server model:** client sends request → server processes and responds
- Examples: DNS servers, file servers, mail servers

> {Hubs = dumb, loud, insecure. Switches = smart, targeted, secure. Know this distinction cold — it comes up in SOC interviews and network analysis constantly.}

---

## 4. Network Diagrams

- Visual maps showing all devices on a network and how they connect
- Use representative icons for devices, dotted lines for connections
- Security analysts use them to **understand network architecture** and identify weak points
- Essential tool for designing and refining security strategies

---

## 5. Cloud Computing

**Traditional (on-premise):** all network devices physically housed at the company's location

**Cloud computing:** using remote servers, applications, and network services hosted on the internet — no physical hardware on-site

A **Cloud Service Provider (CSP)** = company that owns massive data centres globally and sells compute, storage, and networking services

### Three CSP Service Models:

| Model | What it provides | Example |
|---|---|---|
| **SaaS** (Software as a Service) | Software operated by CSP, used remotely | Gmail, Microsoft 365 |
| **IaaS** (Infrastructure as a Service) | Virtual compute, storage, containers | AWS EC2, Azure VMs |
| **PaaS** (Platform as a Service) | Dev tools to build custom cloud apps | Google App Engine |

---

## 6. Cloud Network Types

| Type | Description |
|---|---|
| **Cloud Network** | Servers/computers in remote data centres, accessed via internet |
| **Hybrid Cloud** | CSP services + org's own on-premise infrastructure |
| **Multi-Cloud** | Using more than one CSP simultaneously |

Most organisations use **hybrid** to reduce costs while keeping control over sensitive data.

---

## 7. Software-Defined Networks (SDN)

- Virtual equivalents of physical network devices (switches, routers, firewalls)
- Hosted on CSP servers, configured programmatically via API or web console
- Most modern physical hardware also supports SDN and network virtualisation

> {SDN means your firewall rules, routing tables, and switch configs can be changed with a few API calls instead of physically touching hardware. For security, this means faster response to threats — but also new attack vectors if the API is compromised.}

---

## 8. Why Cloud? — Key Benefits

| Benefit | Explanation |
|---|---|
| **Reliability** | Services available consistently with minimal downtime |
| **Cost** | No upfront hardware costs; pay only for what you use |
| **Scalability** | Scale up or down instantly — elastic utility model |

Security tools (WAF, IDS/IPS, L3/L4 firewalls) can be spun up quickly through CSP console when threats emerge.

---

## 9. Cloud Security Shift

Traditional security = **network-based** (where is the traffic coming from?)

Cloud security = **identity-based** on top of network-based (who is making the request, not just where from?)

> {This is a big shift. In cloud environments, an attacker with stolen credentials can look like a legitimate user. Identity verification becomes as important as IP filtering — this is why IAM (Identity and Access Management) is so critical in cloud SOC work.}

---

## Key Terms

| Term | Definition |
|---|---|
| LAN | Local Area Network — small geographic area |
| WAN | Wide Area Network — large geographic area |
| IP Address | Logical network identifier used for routing |
| MAC Address | Physical hardware identifier used within LAN |
| Hub | Broadcasts to all devices — insecure |
| Switch | Sends to intended device only — secure, efficient |
| Router | Connects multiple networks; routes via IP address |
| Modem | Connects router to ISP/internet |
| Firewall | Monitors and filters network traffic |
| CSP | Cloud Service Provider |
| SaaS | Software as a Service |
| IaaS | Infrastructure as a Service |
| PaaS | Platform as a Service |
| SDN | Software-Defined Network — virtualised network devices |
| Hybrid Cloud | On-premise + cloud combined |
| WAP | Wireless Access Point |

---

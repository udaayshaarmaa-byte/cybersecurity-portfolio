# Lab 2 — DHCP Traffic Analysis with Wireshark

**Author:** Uday Sharma
**Lab Environment:** VirtualBox — Kali Linux VM (NAT adapter)
**Tool Used:** Wireshark (capture interface: eth0)


---

## Overview

In this lab, I captured and analysed a full DHCP lease cycle using Wireshark on Kali Linux. The goal was to observe the DORA handshake (Discover, Offer, Request, ACK) at the packet level, understand what each packet contains, and document findings in a SOC-style report format.

> **Lab note:** Both VMs (Kali Linux and Ubuntu) use VirtualBox NAT, which isolates each VM into its own private network. This means cross VM DHCP capture is not possible in this setup  each VM only sees its own NAT traffic. As a result, I triggered and captured the DHCP handshake on Kali itself using `dhclient`. The learning outcome is identical  the DORA sequence, packet structure, and analysis are the same regardless of which machine generates the traffic. This will be corrected in Lab 3 by switching to Internal Network mode.

---

## Incident Report

| Field | Details |
|---|---|
| **Date / Time** | May 2026, 12:26 AEST |
| **Analyst** | Uday Sharma (SOC Analyst — Training) |
| **Severity** | Low |
| **Environment** | Isolated lab — VirtualBox NAT |
| **Tool** | Wireshark 4.x — interface eth0 |
| **Trigger** | Manual DHCP release and renewal via dhclient |

---

## Technical Observations

| Field | Value |
|---|---|
| **Client MAC address** | `08:00:27:8a:35:d2` |
| **Assigned IP address** | `10.0.2.15` |
| **Subnet mask** | `255.255.255.0` |
| **DHCP server IP** | `10.0.2.2` |
| **Default gateway** | `10.0.2.2` |
| **DNS server (Option 6)** | `192.168.31.1` |
| **Lease duration (Option 51)** | 86400 seconds — 24 hours |
| **Transaction ID** | `0xbf002647` |
| **Total packets captured** | 5 (1 Release + 4 DORA) |

---

## Packet-by-Packet Analysis

### Packet 1 — DHCP Release
- **Source:** `10.0.2.15` → **Destination:** `10.0.2.2`
- **Transaction ID:** `0xfdcea568` (separate session release of old lease)
- The client gracefully relinquished its current IP before requesting a new one.
- In a real environment, a Release followed immediately by a Discover from the same MAC is normal behaviour. A Release from one MAC followed by a Discover from a *different* MAC for the same IP could indicate MAC spoofing a useful SIEM detection point.

---

### Packet 2 — DHCP Discover
- **Source:** `0.0.0.0` → **Destination:** `255.255.255.255`
- **Transaction ID:** `0xbf002647`
- Client has no IP yet, so source is `0.0.0.0`.
- Sent as broadcast because the client does not know which DHCP server exists on the network.
- Contains the client's MAC address so the server knows who to respond to.

---

### Packet 3 — DHCP Offer
- **Source:** `10.0.2.2` → **Destination:** `255.255.255.255`
- **Transaction ID:** `0xbf002647`
- Server responds with an IP offer: `10.0.2.15`
- Key options included:
  - Option 1 — Subnet Mask: `255.255.255.0`
  - Option 3 — Router: `10.0.2.2`
  - Option 6 — DNS Server: `192.168.31.1`
  - Option 51 — Lease Time: 86400 seconds
  - Option 54 — DHCP Server ID: `10.0.2.2`
- Still broadcast because the client has no IP yet to receive a unicast reply.

---

### Packet 4 — DHCP Request
- **Source:** `0.0.0.0` → **Destination:** `255.255.255.255`
- **Transaction ID:** `0xbf002647`
- Client formally accepts the offered IP.
- Option 50 (Requested IP): `10.0.2.15`
- Option 54 (Server ID): `10.0.2.2`  client specifies which server it chose.
- Still broadcast  this also notifies any other DHCP servers that their offers were declined.

---

### Packet 5 — DHCP ACK
- **Source:** `10.0.2.2` → **Destination:** `255.255.255.255`
- **Transaction ID:** `0xbf002647`
- Server confirms the lease. IP assignment is now official.
- All lease parameters confirmed: IP, subnet, gateway, DNS, lease time.
- At this point the client can communicate on the network.

> 
---

## Protocol Analysis

| Check | Result |
|---|---|
| All 4 DORA packets present | Yes |
| Consistent Transaction ID across DORA | Yes — `0xbf002647` |
| Single DHCP server responded | Yes — no competing Offers observed |
| Rogue DHCP indicators | None |
| Broadcast → Unicast transition | Observed as expected after IP assignment |
| Normal / Anomalous | **Normal** |

---

## Key Concepts Reinforced

**Why does Discover use `0.0.0.0` as source?**
The client has no IP address at the point of sending a Discover. `0.0.0.0` is the placeholder meaning "I have no identity yet." The server identifies the client by MAC address instead.

**Why is Discover broadcast but ACK is also broadcast here?**
In VirtualBox NAT, the ACK is sent to `255.255.255.255` rather than directly to the client IP. In a real network environment, the ACK is typically unicast directly to the assigned IP once the client has it. This is a VirtualBox NAT behavioural quirk and not representative of production network behaviour.

**Why does the Release have a different Transaction ID?**
Each DHCP session generates a fresh random Transaction ID. The Release (`0xfdcea568`) was a separate session from the DORA handshake (`0xbf002647`). The Transaction ID links packets within a single session only.

---




## Evidence

- Wireshark capture file: `lab2-dhcp-capture.pcap`
- Screenshot: Wireshark packet list showing all 5 packets (Release + DORA)


---


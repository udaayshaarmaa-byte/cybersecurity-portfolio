## 1. IP Addresses

An **IP address** = a unique string of characters that identifies the location of a device on the internet.

### Two Types:

| Type | Description |
|---|---|
| **Public IP** | Assigned by ISP; tied to geographic location; visible to the internet; shared by all devices on the same network |
| **Private IP** | Only visible to devices on the same local network; not exposed to the internet |

> {Like a house address — public IP is the street address everyone can see, private IP is which room you're in inside the house.}

---

## 2. IPv4 vs IPv6

| Feature | IPv4 | IPv6 |
|---|---|---|
| Format | 4 decimal numbers separated by periods | 8 hexadecimal groups separated by colons |
| Example | `198.51.100.0` | `2002:0db8::ff21:0023:1234` |
| Size | 4 bytes | 16 bytes |
| Total addresses | ~4.3 billion | 340 undecillion (340 followed by 36 zeros) |
| Header complexity | More complex (13 fields) | Simpler — drops IHL, Identification, Flags fields |
| Unique field | — | Flow Label (flags packets needing special handling) |

**IPv4 exhaustion** = the problem that drove IPv6 development — the internet grew far beyond what 4.3 billion addresses could support.

**IPv6 security improvements:**
- More efficient routing
- Eliminates private address collisions (two devices accidentally using the same IP on a LAN)

> {IPv6 adoption is still incomplete globally, so you'll see both in the wild. Being able to read both formats is practical for log analysis.}

---

## 3. MAC Addresses

A **MAC address** = unique alphanumeric identifier assigned to each **physical** device on a network.

- Used for communication **within** a local network (Layer 2)
- Switches read the destination MAC address → look up the MAC address table → forward packet to the correct port
- **MAC address table** = the switch's address book mapping MAC addresses to port numbers
- **ARP** (Address Resolution Protocol) maps IP addresses → MAC addresses when needed

---

## 4. IPv4 Packet Structure

A data packet for TCP = **IP packet**
A data packet for UDP = **datagram**

An IPv4 packet has two sections:

```
[ HEADER (20–60 bytes) ] [ DATA (up to 65,515 bytes) ]
```

Maximum total IPv4 packet size = **65,535 bytes**

---

## 5. IPv4 Header Fields (13 Fields)

| Field | Purpose |
|---|---|
| **Version (VER)** | Identifies the IP version (IPv4 or IPv6) |
| **IP Header Length (HLEN/IHL)** | Shows where the header ends and data begins |
| **Type of Service (ToS)** | Tells routers how to prioritise this packet |
| **Total Length** | Full size of the packet (header + data) |
| **Identification** | Unique ID for reassembling fragmented packets |
| **Flags** | Indicates if the packet is fragmented and if more fragments follow |
| **Fragmentation Offset** | Tells routers where this fragment fits in the original packet |
| **Time to Live (TTL)** | Counter that decrements at each router hop; packet discarded when it hits 0; prevents infinite routing loops |
| **Protocol** | Specifies which protocol handles the data portion (e.g. TCP, UDP) |
| **Header Checksum** | Detects corruption in the header; corrupted packets are discarded |
| **Source IP Address** | IP address of the sending device |
| **Destination IP Address** | IP address of the receiving device |
| **Options** | Optional security settings; only present if HLEN > 5 |

> {TTL is practically useful in SOC work — traceroute abuses TTL intentionally to map network paths. Attackers do the same for reconnaissance. Seeing unusual TTL values in logs can be a red flag.}

---

## 6. Network Layer Operations (OSI Layer 3)

- Organises **addressing and delivery** of packets from source to destination
- Packets routed from router to router using the **destination IP in the header**
- Routing tables store IP address info along the packet's path for future routing decisions
- Routers read the IP header → decide next hop → forward accordingly

---

## Key Terms

| Term | Definition |
|---|---|
| IP Address | Unique identifier for a device's location on the internet |
| IPv4 | 4-byte address format; ~4.3 billion addresses |
| IPv6 | 16-byte address format; 340 undecillion addresses |
| Public IP | Externally visible IP assigned by ISP |
| Private IP | Internal-only IP, not visible outside the LAN |
| MAC Address | Physical hardware identifier used within a LAN |
| ARP | Maps IP addresses to MAC addresses |
| TTL | Time to Live — limits how many hops a packet can take |
| Fragmentation | Splitting a large packet into smaller pieces for transmission |
| Header Checksum | Validates packet header integrity |
| Datagram | IP packet used with UDP connections |
| Routing Table | Router's record of paths to destination networks |

---


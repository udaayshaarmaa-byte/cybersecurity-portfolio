## 1. Data Packets

A **data packet** = the basic unit of information that travels between devices on a network.

Structure of a packet (think of it like a physical letter):

| Part | Contains |
|---|---|
| **Header** | Destination IP address, destination MAC address, protocol number |
| **Body** | The actual message/data being transmitted |
| **Footer** | Signals to the receiving device that the packet is complete |

### Network Performance Metrics:
- **Bandwidth** = amount of data a device receives per second (quantity of data ÷ time in seconds)
- **Speed** = rate at which data packets are received or downloaded
- Irregular bandwidth or speed → potential indicator of an attack

**Packet sniffing** = capturing and inspecting data packets across a network (a core analyst skill)

---

## 2. Ports

A **port** = software-based location in an OS that organises sending/receiving of data between devices.

- Divides network traffic into segments based on the service being performed
- Devices use port numbers to prioritise and process incoming data correctly

| Port | Service |
|---|---|
| **25** | Email (SMTP) |
| **20** | Large file transfers (FTP) |
| **443** | Secure internet communication (HTTPS) |

> {Ports are like apartment numbers in a building — the router finds the building (IP address), the port tells it which apartment (service) to deliver to.}

---

## 3. TCP/IP Model — 4 Layers

The **TCP/IP model** = framework for visualising how data is organised and transmitted across a network. Used by security professionals to identify where attacks or disruptions occur.

### TCP — Transmission Control Protocol
- Allows two devices to form a connection and stream data
- Ensures packets reach their destination
- Retransmits lost or corrupt data
- **Reliable** — tracks all data sent

### IP — Internet Protocol
- Routes and addresses data packets as they travel between devices
- Every private network has an IP address

---

### Layer 1 — Network Access Layer *(also called Data Link Layer)*
- Creation and transmission of data packets
- Physical hardware: hubs, modems, cables, wiring, switches
- **ARP (Address Resolution Protocol)** lives here — maps IP addresses to MAC addresses for local network communication

### Layer 2 — Internet Layer *(also called Network Layer)*
- Attaches IP addresses to packets (sender + receiver locations)
- Determines routing — does the packet stay on the LAN or go to a remote network?
- Key protocols:
  - **IP** — routes packets to correct destination
  - **ICMP** — shares error info and status updates; used for detecting/troubleshooting network errors (dropped packets, connectivity issues)

### Layer 3 — Transport Layer
- Delivers data between two systems
- Controls flow of traffic, error control, connection status
- Key protocols:
  - **TCP** — connection-oriented, reliable, tracks all data
  - **UDP** — connectionless, no reliability tracking, used for real-time/performance-sensitive apps (video streaming, gaming)

### Layer 4 — Application Layer
- Determines how data packets interact with receiving devices
- Directly involves the end user
- Key protocols:

| Protocol | Function |
|---|---|
| **HTTP/HTTPS** | Web browsing |
| **SMTP** | Email sending/receiving |
| **SSH** | Secure remote access |
| **FTP** | File transfers |
| **DNS** | Translates domain names to IP addresses |

---

## 4. OSI Model — 7 Layers

The **OSI model** = more detailed framework; security professionals use it to pinpoint exactly where threats or disruptions occur.

> {TCP/IP is 4 layers — simpler, widely used. OSI is 7 layers — more granular, used for precise troubleshooting. Know both; use OSI when you need to get specific about where in the stack something went wrong.}

| Layer | Name | Key Function |
|---|---|---|
| **7** | Application | User-facing protocols (HTTP, DNS, SMTP, SSH, FTP) |
| **6** | Presentation | Data translation, encryption, compression (SSL lives here) |
| **5** | Session | Establishes, manages, and terminates sessions; authentication; checkpoints for interrupted transfers |
| **4** | Transport | Data delivery between devices; segmentation; TCP & UDP |
| **3** | Network | Routing via IP addresses; routers operate here |
| **2** | Data Link | Organises data within a single network; switches and NICs; MAC addresses |
| **1** | Physical | Physical hardware — cables, hubs, modems; converts data to 0s and 1s |

---

## 5. TCP/IP vs OSI — Mapping

| OSI Layer | TCP/IP Layer |
|---|---|
| 7 — Application | Application |
| 6 — Presentation | Application |
| 5 — Session | Application |
| 4 — Transport | Transport |
| 3 — Network | Internet |
| 2 — Data Link | Network Access |
| 1 — Physical | Network Access |

TCP/IP collapses layers 5, 6, 7 into one Application layer and layers 1, 2 into one Network Access layer.

---

## 6. TCP vs UDP — Quick Comparison

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Reliability | High — tracks and retransmits lost data | Low — no tracking |
| Speed | Slower | Faster |
| Use case | Web browsing, email, file transfer | Video streaming, DNS, gaming |

---

## Key Terms

| Term | Definition |
|---|---|
| Data Packet | Basic unit of information transmitted across a network |
| Bandwidth | Amount of data received per second |
| Port | Software location that organises data by service type |
| TCP | Reliable, connection-oriented transport protocol |
| UDP | Fast, connectionless transport protocol |
| IP | Routes and addresses packets across networks |
| ARP | Maps IP addresses to MAC addresses on local network |
| ICMP | Reports packet errors and network connectivity issues |
| DNS | Translates domain names to IP addresses |
| SSL | Encrypts data at the Presentation layer (OSI Layer 6) |
| Packet Sniffing | Capturing and inspecting packets on a network |

---

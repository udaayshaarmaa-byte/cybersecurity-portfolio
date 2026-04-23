# Packets, TCP, UDP & Ports
  
**Topic:** Packets & Frames, TCP/IP, UDP, Ports & Protocols

---

## 1. Packets vs Frames

| | **Packet** | **Frame** |
|---|---|---|
| **OSI Layer** | Layer 3 — Network | Layer 2 — Data Link |
| **Contains** | IP header + payload | Encapsulates the packet + MAC addresses |
| **Relates to** | IP addresses | MAC addresses |

- **Encapsulation** = wrapping data with additional headers as it moves down OSI layers
- **Decapsulation** = stripping those headers as data moves up on the receiving end
- Analogy: the **frame is the envelope**, the **packet is the letter inside**
- Data is broken into small packets to prevent bottlenecking — e.g. an image loads as multiple pieces that are reassembled on your device

### IP Packet Headers (notable)

| Header | Description |
|---|---|
| **Time to Live (TTL)** | Expiry timer — stops lost packets from clogging the network |
| **Checksum** | Integrity check — if data changes in transit, the value won't match → packet marked corrupt |
| **Source Address** | IP of the sending device |
| **Destination Address** | IP of the receiving device |

---

## 2. TCP (Transmission Control Protocol)

### What is TCP?
- A **connection-based**, reliable transport protocol
- Part of the **TCP/IP model** — a 4-layer summarised version of OSI:
  - Application → Transport → Internet → Network Interface
- Guarantees data delivery via the **Three-Way Handshake**
- Uses **encapsulation/decapsulation** same as OSI model

### TCP Advantages vs Disadvantages

| **Advantages** | **Disadvantages** |
|---|---|
| Guarantees data integrity | Requires reliable connection — if one chunk is lost, the whole chunk must be re-sent |
| Synchronises devices to prevent out-of-order data flooding | Slow connection bottlenecks the other device (connection stays reserved) |
| Performs extra processes to ensure reliability | Significantly slower than UDP due to higher computing overhead |

### TCP Packet Headers

| Header | Description |
|---|---|
| **Source Port** | Randomly chosen port (0–65535) opened by the sender |
| **Destination Port** | Port of the target application/service (e.g. port 80 for web) — not random |
| **Source IP** | IP address of the sending device |
| **Destination IP** | IP address of the receiving device |
| **Sequence Number** | Random number assigned to the first piece of data sent |
| **Acknowledgement Number** | Sequence number + 1 — confirms receipt and orders the next piece |
| **Checksum** | Mathematical integrity check — mismatched output = corrupt data |
| **Data** | The actual payload bytes being transmitted |
| **Flag** | Controls handshake behaviour (SYN, ACK, FIN, RST, etc.) |

### Three-Way Handshake

| Step | Message | Who Sends | Description |
|---|---|---|---|
| 1 | **SYN** | Client | Initiates connection, sends Initial Sequence Number (ISN) |
| 2 | **SYN/ACK** | Server | Acknowledges client's ISN, sends its own ISN |
| 3 | **ACK** | Client | Acknowledges server's ISN — connection established |
| 4 | **DATA** | Either | Actual data transfer begins |
| 5 | **FIN** | Either | Cleanly closes the connection |
| # | **RST** | Either | Abruptly terminates — last resort, indicates a fault or low resources |

### Sequence Number Example

| Device | Initial Sequence Number (ISN) | Final Sequence Number |
|---|---|---|
| Client (Sender) | 0 | 0 + 1 = 1 |
| Client (Sender) | 1 | 1 + 1 = 2 |
| Client (Sender) | 2 | 2 + 1 = 3 |

> Each piece of data increments by 1 — both devices must agree on the sequence to reconstruct data in the correct order.

### Closing a TCP Connection
- TCP closes once all data is confirmed received
- Best practice: close connections ASAP to free up system resources
- Device sends a **FIN** packet → other device must **ACK** it

---

## 3. UDP (User Datagram Protocol)

### What is UDP?
- A **stateless**, connectionless protocol
- No Three-Way Handshake — no synchronisation between devices
- No guarantee data is received — **fire and forget**
- Used where speed > reliability: video streaming, voice chat, online gaming

### UDP Advantages vs Disadvantages

| **Advantages** | **Disadvantages** |
|---|---|
| Much faster than TCP | No confirmation data was received |
| Application controls packet send rate (flexible for developers) | Flexible to developers but unpredictable |
| Does not reserve a continuous connection on a device | Unstable connections = terrible user experience |

### UDP Packet Headers

| Header | Description |
|---|---|
| **Time to Live (TTL)** | Expiry timer — prevents packet from clogging the network |
| **Source Address** | IP of the sending device |
| **Destination Address** | IP of the receiving device |
| **Source Port** | Randomly chosen port (0–65535) opened by the sender |
| **Destination Port** | Target application's port (e.g. port 80) — not random |
| **Data** | The payload bytes being transmitted |

> UDP has **fewer headers** than TCP — no sequence numbers, no acknowledgement, no checksum.

---

## 4. Ports & Protocols

### What are Ports?
- Ports are numerical values (**0–65535**) that act as exchange points for data
- Enforce which application handles which data — like a harbour enforcing which ships dock where
- Ports **0–1024** = **common/well-known ports**
- Non-standard ports can be used (e.g. web server on 8080 instead of 80) — but the app must be told explicitly using `:port` syntax

### Common Protocols & Port Numbers

| Protocol | Port | Description |
|---|---|---|
| **FTP** (File Transfer Protocol) | 21 | File sharing via client-server model |
| **SSH** (Secure Shell) | 22 | Secure remote login via text-based interface |
| **HTTP** (HyperText Transfer Protocol) | 80 | Powers the web — browsers use this for text, images, video |
| **HTTPS** (HTTP Secure) | 443 | Same as HTTP but encrypted |
| **SMB** (Server Message Block) | 445 | File + device sharing (e.g. printers) on a network |
| **RDP** (Remote Desktop Protocol) | 3389 | Secure remote login via visual desktop interface |

> **SOC Note:** Unusual traffic on well-known ports (e.g. SSH on port 22 from an unexpected IP) or known malware using non-standard ports is a common detection trigger.

---

## Key Comparisons: TCP vs UDP

| | **TCP** | **UDP** |
|---|---|---|
| Connection | Connection-based | Connectionless (stateless) |
| Reliability | Guaranteed delivery | No guarantee |
| Speed | Slower | Faster |
| Handshake | Three-Way Handshake | None |
| Use Case | File transfers, web browsing, email | Streaming, VoIP, gaming |
| Headers | More (sequence, ACK, checksum, flags) | Fewer (TTL, src/dst, data) |

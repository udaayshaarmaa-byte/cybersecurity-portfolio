# Incident Report | Lab 4: Port Scan Detection

**Analyst:** Uday Sharma

---

# 1. Lab Overview

This home lab simulates a basic reconnaissance attack scenario in which an attacker machine running Kali Linux performed an Nmap scan against a defender machine running Ubuntu Linux. Network traffic was captured using Wireshark while alerts and intrusion detection were monitored through Suricata.

---

# 2. Environment

| Component | Details |
|---|---|
| Attacker VM | Kali Linux |
| Defender VM | Ubuntu Linux |
| IDS | Suricata 8.0.3 |
| Packet Sniffer | Wireshark |
| Scanning Tool | Nmap |
| Network Type | VirtualBox Host-Only Adapter |

---

# 3. Incident Summary

A simulated port scan attack was conducted against an Ubuntu virtual machine (`192.168.56.103`) from a Kali Linux attacker machine (`192.168.56.102`) over a VirtualBox Host-Only network.

From the defender perspective, traffic patterns consistent with an Nmap SYN scan were observed during the investigation.

Suricata generated multiple alerts during the scan activity, including alerts associated with possible Nmap reconnaissance behavior. Wireshark packet captures confirmed SYN-based reconnaissance activity, HTTP service fingerprinting, and TCP connection analysis.

---

# 4. Findings – Attacker Perspective

| Observation | Details |
|---|---|
| Open Port | 80/tcp |
| Service | HTTP |
| Software Identified | Apache httpd 2.4.66 |
| Operating System | Ubuntu |
| Firewall Observation | UFW blocked all tested ports except 80/tcp |

---

# 5. Findings – Defender Perspective

## TRAFFIC ANALYSIS — Wireshark
Hundreds of TCP SYN packets sent from 192.168.56.102 to 192.168.56.103 in rapid succession,
targeting sequential port numbers.

SYN → RST, ACK (Ubuntu immediately rejected — UFW blocking)

SYN → SYN, ACK → RST (Kali confirmed port open then reset — never completed
handshake)

Full TCP three-way handshake completed on port 80, followed by HTTP application-layer traffic.
SYN → SYN,ACK → ACK (complete connection established)
HTTP GET / HTTP/1.0 sent by nmap  Ubuntu responded HTTP/1.1 200 OK (text/html)

Echo requests/replies visible in Wireshark nmap -A performs host discovery ping before scanning.

## IDS ANALYSIS-SURICATA
Suricata's fast.log was initially empty because the IDS was not restarted after running suricata-update. Alerts only appeared after restarting Suricata.
ET SCAN Possible Nmap User-Agent Observed-Web Application Attack-Priority(1)
SURICATA ICMPv4 unknown code -Generic Protocol Command Decode-Priority(3)
SURICATA Applayer Detect protocol only one direction-Generic Protocol Command Decode-Priority(3)

# SOC Incident Report — INC-2026-001

| Field | Details |
|---|---|
| **Incident ID** | INC-2026-001 |
| **Date** | 2026-04-29 |
| **Severity** | MEDIUM |
| **Status** | ✅ Resolved |
| **Analyst** | Uday Sharma |
| **Source Host** | 192.168.56.103 — Ubuntu 22.04 |
| **Target Host** | 192.168.56.102 — Kali Linux |
| **Protocol** | ICMP / ARP |

---

## Summary

During Lab 01, ICMP echo requests (ping sweeps) were exchanged between Kali Linux (192.168.56.102) and Ubuntu (192.168.56.103) across an isolated VirtualBox Host-Only network. ARP resolution was observed prior to all ICMP activity confirming standard Layer 2/3 behaviour. Firewall rules were applied on both hosts — Ubuntu using `iptables` and Kali using `nftables` — to block inbound ICMP. Wireshark packet capture confirmed successful enforcement via one-sided ICMP traffic with zero reply packets. All rules were subsequently removed and connectivity restored.

> ⚠️ ARP broadcast followed by ICMP sweep is a standard network reconnaissance pattern used in real attacks. This lab demonstrates both the attack pattern and the defensive response at the packet level.

---

## Network Environment

| Host | OS | NAT IP | Host-Only IP | Role |
|---|---|---|---|---|
| Kali | Kali Linux 2026.1 | 10.0.2.15 | 192.168.56.102 | Attacker / Analyst |
| Ubuntu | Ubuntu 22.04 LTS | 10.0.2.15 | 192.168.56.103 | Defender / Target |

---

## Timeline of Events

| Phase | Event | Details |
|---|---|---|
| Session Start | Lab environment initialised | Both VMs booted · Host-Only network confirmed active (192.168.56.0/24) |
| Phase 1 | IP discovery — `ip a` on both VMs | Kali: eth0=10.0.2.15, eth1=192.168.56.102 · Ubuntu: enp0s3=10.0.2.15, enp0s8=192.168.56.103 |
| Phase 2 | Ping sweep — both directions | Kali → Ubuntu: 0% packet loss ✅ · Ubuntu → Kali: 0% packet loss ✅ |
| Phase 3 | ARP table observed on both hosts | Ubuntu ARP showed: gateway (56.1), DHCP server (56.100), Kali MAC (08:00:27:7f:53:c9) |
| Phase 4 | Firewall block applied on Ubuntu | `iptables -I INPUT -p icmp --icmp-type 8 -j DROP` · Kali ping to Ubuntu: 100% loss ✅ |
| Phase 5 | Firewall block applied on Kali | nftables rule added to `/etc/nftables.conf` · Ubuntu ping to Kali: 100% loss ✅ |
| Phase 6 | Wireshark packet capture on eth1 | ICMP request/reply captured · Firewall block confirmed via zero reply packets · "no response found" flagged |
| Phase 7 | All rules removed — connectivity restored | Both hosts confirmed 0% packet loss · Capture saved · Report filed |

---

## Evidence

| ID | Description | Tool | Severity |
|---|---|---|---|
| E-001 | `ip a` output — both VMs showing NAT and Host-Only IPs | `ip a` | INFO |
| E-002 | Successful ping both directions — 0% packet loss | `ping` | INFO |
| E-003 | ARP table — Ubuntu showing Kali MAC and VirtualBox gateway | `arp -a` | MEDIUM |
| E-004 | Wireshark ICMP request/reply sequence — normal traffic | Wireshark | MEDIUM |
| E-005 | Wireshark one-sided ICMP — "no response found" post firewall block | Wireshark | MEDIUM |
| E-006 | iptables rule active on Ubuntu — ICMP DROP confirmed | `iptables -L` | LOW |

---

## Technical Findings

**F1 — ARP precedes ICMP**
ARP resolution preceded all ICMP activity — Wireshark confirmed the ARP handshake completed before any ping packet was transmitted. Standard Layer 2/3 behaviour but confirms active host discovery occurs before sweep.

**F2 — Passive network discovery via ARP**
Ubuntu ARP table revealed three Host-Only network participants beyond the target: VirtualBox gateway (192.168.56.1), DHCP server (192.168.56.100), and Kali (192.168.56.102). This passive network discovery requires no active scanning.

**F3 — Different firewall systems across distros**
Ubuntu and Kali use different firewall systems — `iptables` on Ubuntu vs `nftables` on Kali. Commands are not interchangeable between systems. Numeric ICMP type codes (type 8) proved more reliable than named types (echo-request) across both systems.

**F4 — One-sided ICMP as firewall signature**
Wireshark confirmed firewall enforcement via one-sided ICMP — outbound requests visible, zero reply packets returned. Wireshark automatically flagged each unanswered request as "no response found" — a definitive firewall block signature.

**F5 — Clean firewall rule lifecycle**
Both hosts confirmed 0% packet loss after rule removal — demonstrating clean firewall rule lifecycle: apply → verify → remove → restore. This is the standard change management process for firewall rules in production environments.

---

## ASD Essential Eight Mapping

| Control | Maturity Level | Relevance |
|---|---|---|
| Application Control | ML1 | iptables and nftables blocking ICMP — controlling which protocols reach each host |
| Network Segmentation | ML1 | Host-Only adapter isolates all lab traffic — mimics real network zone separation |
| Incident Response | ML2 | Wireshark used for live packet capture, traffic analysis and post-incident evidence |

---

## Sign-off

| Role | Name |
|---|---|
| Analyst | Uday Sharma · Junior SOC Analyst |
| Reviewed By | Pending · Senior Analyst |

---

*cybersecurity-portfolio · udaayshaarmaa-byte · Lab 01*

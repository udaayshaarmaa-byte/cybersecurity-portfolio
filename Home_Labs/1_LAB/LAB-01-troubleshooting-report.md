# Troubleshooting Report — Lab 01
## What Failed, What Worked & Why

| Field | Details |
|---|---|
| **Report** | LAB-01-TROUBLESHOOTING |
| **Date** | 2026-04-29 |
| **Analyst** | Uday Sharma |
| **Lab** | ARP, Ping, Firewall & Wireshark |

---

## P-01 — Kali eth1 Had No IP Address

**Problem**
After both VMs were booted, Ubuntu successfully pinged Kali but Kali could not be pinged from Ubuntu. Running `ip a` on Kali revealed that eth1 (Host-Only adapter) had no IP address assigned — only a MAC address. VirtualBox did not automatically assign a DHCP IP to Kali's eth1 interface.

| Status | Command | Reason |
|---|---|---|
| ❌ Failed | `sudo ip addr add 192.168.56.102/24 dev eth1` | Assigned IP to RAM only — dropped as soon as network activity occurred |
| ❌ Failed | `sudo dhclient eth1` | Kali's DHCP client did not receive an IP from VirtualBox DHCP on Host-Only network |
| ✅ Worked | Static config in `/etc/network/interfaces` + `sudo systemctl restart networking` | IP written to config file — loaded on boot and network restart, survives all activity |

**Root Cause**
Kali Linux pre-built VirtualBox image does not configure secondary network adapters automatically. eth1 requires manual static IP configuration via `/etc/network/interfaces` to be persistent.

---

## P-02 — Blocking ICMP on Ubuntu

**Problem**
Multiple commands were attempted to block inbound ICMP on Ubuntu. UFW and named iptables types both failed before the correct numeric type code was found.

| Status | Command | Reason |
|---|---|---|
| ❌ Failed | `sudo ufw deny proto icmp from any to any` | UFW on Ubuntu 22.04 does not support `proto icmp` syntax in CLI — returns "unsupported protocol" |
| ❌ Failed | `sudo iptables -A INPUT -p icmp --icmp-type echo-request -j DROP` | Named ICMP type not consistently recognised · `-A` appends to bottom of chain, may never be reached |
| ✅ Worked | `sudo iptables -I INPUT -p icmp --icmp-type 8 -j DROP` | Numeric type 8 universally recognised · `-I` inserts at top of chain — processed first |

**Root Cause**
UFW does not support direct ICMP blocking via CLI on Ubuntu 22.04. Named ICMP types in iptables are version-dependent. Numeric ICMP type codes are portable and reliable across all iptables versions.

---

## P-03 — Blocking ICMP on Kali

**Problem**
Kali Linux uses nftables as its default firewall backend, not iptables. Multiple nftables syntax attempts failed due to zsh shell conflicts and missing table structure before the correct approach was found.

| Status | Command | Reason |
|---|---|---|
| ❌ Failed | `sudo iptables -I INPUT -p icmp --icmp-type 8 -j DROP` | Kali uses nftables not iptables — returns "no chain/target/match by that name" |
| ❌ Failed | `sudo nft add rule ip filter input icmp type echo-request drop` | No existing nftables table named "filter" — returns "no such file or directory" |
| ❌ Failed | `sudo nft add chain ip filter input { type filter hook input priority 0 \; }` | zsh interprets curly brackets as special characters — returns "parse error near the bracket" |
| ✅ Worked | Edit `/etc/nftables.conf` directly — add `icmp type echo-request drop` inside existing input chain, then `sudo nft -f /etc/nftables.conf` | Config file already had filter table and input chain defined · Bypasses all zsh shell conflicts |

**Root Cause**
Kali Linux uses nftables (not iptables) as default firewall. zsh shell conflicts with inline nftables syntax. Editing `/etc/nftables.conf` directly is the most reliable approach on Kali — avoids shell escaping issues entirely.

---

## Key Learnings

**L1 — Always use numeric ICMP type codes**
`--icmp-type 8` instead of `--icmp-type echo-request`. Named types are version-dependent and unreliable across different Linux distributions and iptables builds.

**L2 — Use -I not -A for firewall rules**
`-I` inserts at the top of the chain and is processed first. `-A` appends to the bottom and may never be reached if other rules match first.

**L3 — Kali uses nftables, Ubuntu uses iptables**
Never assume the same firewall commands work across distributions. Always check which backend is active: `sudo nft list ruleset` for nftables, `sudo iptables -L` for iptables.

**L4 — Temporary vs persistent network config**
`ip addr add` assigns IPs to RAM only — they disappear under network activity. Always write static IPs to `/etc/network/interfaces` for persistence across reboots and network restarts.

**L5 — zsh conflicts with inline nftables syntax**
Curly brackets are special characters in zsh. When nft CLI commands fail due to shell parsing, editing the config file directly with `sudo nano /etc/nftables.conf` is the most reliable workaround.

**L6 — Diagnose before assuming**
Initial assumption was Kali's firewall blocking ping from Ubuntu. Running `ip a` revealed the real issue was a missing IP on eth1. Always verify network config before jumping to firewall conclusions.

---

*cybersecurity-portfolio · udaayshaarmaa-byte · Lab 01*

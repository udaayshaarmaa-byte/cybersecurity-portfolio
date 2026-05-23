# Lab 06 | Brute Force Attack Detection & Response
**Author:** Uday Sharma    
---

## Executive Summary

On 23 May 2026, a simulated brute force attack was launched against an SSH service running on an Ubuntu 26.04 LTS virtual machine (192.168.56.103) from a Kali Linux attack machine (192.168.56.102). The attacker performed reconnaissance using Nmap to identify the SSH service, then used Hydra to systematically attempt 9 passwords against the target user account. The attack was successfully detected via Splunk SIEM monitoring live auth.log ingestion. Automated containment was achieved through fail2ban, which identified the brute force pattern and banned the attacking IP without manual intervention. The attack was fully contained within the detection window.

---

## Environment

| Component | Details |
|---|---|
| Attacker | Kali Linux — 192.168.56.102 |
| Target | Ubuntu  — 192.168.56.103 |
| SIEM | Splunk |
| Log Source | /var/log/auth.log via live monitoring |
| Detection Tool | Splunk SPL queries + fail2ban |
| Network | VirtualBox Host-Only Adapter |

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID | Description |
|---|---|---|---|
| Reconnaissance | Active Scanning | T1595 | Nmap service and version scan against port 22 |
| Credential Access | Brute Force: Password Guessing | T1110 | Hydra SSH password brute force |
| Initial Access | Valid Accounts | T1078 | Successful credential compromise (harrypotter) |

---

## Phase 1 | Reconnaissance

Attacker performed service discovery using Nmap prior to the brute force attack.

**Commands executed from Kali (192.168.56.102):**

```bash
nmap -sV -p 22 192.168.56.103
nmap -A -p 22 192.168.56.103
```

**Findings:**

```
PORT    STATE  SERVICE  VERSION
22/tcp  open   ssh      OpenSSH 10.2p1 Ubuntu 2ubuntu3.2 (Ubuntu Linux; protocol 2.0)
OS: Linux
Network Distance: 1 hop
```

The attacker confirmed SSH was running on port 22, identified the exact OpenSSH version, and confirmed the target OS as Ubuntu Linux.

---

## Phase 2 | Brute Force Attack

Hydra was used to systematically attempt passwords against the `uday` account via SSH.

**Command executed:**

```bash
hydra -l uday -P /home/kali/lab6_wordlist.txt ssh://192.168.56.103 -t 1 -W 3 -V
```

**Result:**

```
[22][ssh] host: 192.168.56.103   login: uday   password: harrypotter
1 of 1 target successfully completed, 1 valid password found
```

9 password attempts were made before the correct credential was identified. The attack succeeded because:
- Password authentication was enabled on the SSH service
- No account lockout policy was in place prior to fail2ban deployment
- The password was present in a common wordlist

---

## Phase 3 | Detection

### 3.1 Log Source

Auth.log was ingested into Splunk via live file monitoring configured on the Ubuntu VM:

```
Monitor path: /var/log/auth.log
Index: main
Sourcetype: linux_secure
Ingestion method: Splunk local file monitor (real-time)
```

Every SSH authentication event written by sshd to auth.log was indexed in Splunk within seconds of occurrence.

### 3.2 Splunk Detection Queries

**Query 1 | Failed login events:**

```
index=main sourcetype=linux_secure "Failed password"
| table _time, _raw
| sort -_time
```

Result: 22 failed password events detected from 192.168.56.102 targeting user `uday`.

**Query 2 | Brute force threshold detection:**

```
index=main sourcetype=linux_secure "Failed password"
| rex field=_raw "for (?P<user>\S+) from (?P<src_ip>\S+)"
| bucket _time span=5m
| stats count by src_ip, user, _time
| where count > 5
```

Result: Single row returned | `192.168.56.102` targeting `uday` with count of **9** within a 5-minute window. Threshold of 5 crossed, confirming brute force pattern.

**Query 3 | Successful authentication confirmation:**

```
index=main sourcetype=linux_secure "Accepted password"
```

Result: 2 accepted password events confirmed | credential compromise verified in logs.


## Phase 4 | Containment & Response

### 4.1 Automated Response | fail2ban

fail2ban was installed and configured on the Ubuntu VM to provide automated IP banning upon detection of brute force patterns.

```bash
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

**fail2ban status after second Hydra attack:**

```
Status for the jail: sshd
|- Filter
|  |- Currently failed: 0
|  |- Total failed: 5
|  `- Journal matches: _SYSTEMD_UNIT=ssh.service + _COMM=sshd
`- Actions
   |- Currently banned: 1
   |- Total banned: 1
   `- Banned IP list: 192.168.56.102
```

fail2ban detected the brute force pattern and automatically banned `192.168.56.102` without manual intervention. A second Hydra run confirmed the ban was effective | 0 valid passwords found, attack blocked.
# Incident Report Lab 7:Brute Force Against Active Directory Domain Controller

**Date of Incident:** June 20, 2026
**Analyst:** Uday Sharma
**Environment:** Home SOC Lab Active Directory (corp.local)

---

## 1. Incident Summary

On June 20, 2026, a simulated brute force attack was launched against the SMB service (port 445) running on a Windows Server 2019 Active Directory Domain Controller (DC01, 192.168.56.106) from a Kali Linux attacker machine (192.168.56.102). The attacker first performed service reconnaissance using Nmap to identify open ports, then used netexec (nxc) to brute force the credentials of the domain account `jdoe` over SMB. After six failed authentication attempts, the seventh attempt succeeded, granting the attacker valid domain credentials. The attack was detected via Windows Event Viewer (Security log) on DC01, correlating Event ID 4625 (failed logon) and Event ID 4624 (successful logon).

---

## 2. Timeline

| Machine | Start | End | Timezone |
|---|---|---|---|
| Attacker (Kali, 192.168.56.102) | 04:16:57 AM | 04:17:09 AM | EDT (UTC-4) |
| Target (DC01, 192.168.56.106)  logged events | 1:05:05 PM | 1:05:05 PM | PDT (UTC-7, per system config) |

**Observation Clock Drift:** Based on DC01's configured timezone (Pacific Daylight Time, UTC-7), the attack window observed on Kali (04:16:57–04:17:09 AM EDT) should have translated to approximately 01:16:57–01:17:09 AM PDT on DC01. Instead, DC01 logged the corresponding events at 1:05:05 PM  a discrepancy of nearly 12 hours beyond the expected 3-hour timezone offset. This indicates the DC01 system clock is not properly synchronized (NTP drift), separate from the timezone configuration itself.

---

## 3. Environment Details

| Component | Details |
|---|---|
| Attacker | Kali Linux | 192.168.56.102 |
| Target | Windows Server 2019 (DC01, domain controller for corp.local) | 192.168.56.106 |
| Target Account | jdoe (member of IT-Admins security group) |
| Detection Tool | Windows Event Viewer Security log |
| Network | VirtualBox Host-Only Adapter (isolated lab network) |
| Service Attacked | SMB (port 445 / microsoft-ds) |
| Attack Tool | netexec (nxc) |
---

## 4. MITRE ATT&CK Mapping

| Tactic | Technique | ID | Description |
|---|---|---|---|
| Reconnaissance | Active Scanning | T1595 | Nmap service scan against ports 445, 3389, 5985 to identify open SMB, RDP, and WinRM services |
| Credential Access | Brute Force: Password Guessing | T1110.001 | netexec used to attempt 7 passwords against the jdoe account over SMB |
| Initial Access | Valid Accounts: Domain Accounts | T1078.002 | Successful credential compromise  attacker obtained valid domain credentials for jdoe (P@ssword@1234) |

---

## 5. Phase 1 Reconnaissance

The attacker performed service discovery using Nmap prior to the brute force attack, to identify which authentication services were reachable on the target.

**Command executed (from Kali, 192.168.56.102):**
```
nmap -p 3389,445,5985 192.168.56.106
```

**Result:**

| Port | State | Service |
|---|---|---|
| 445/tcp | open | microsoft-ds (SMB) |
| 3389/tcp | filtered | ms-wbt-server (RDP) |
| 5985/tcp | open | wsman (WinRM) |

SMB (445) was selected as the attack vector since it was confirmed open and unfiltered, unlike RDP (3389), which returned a filtered state and was not viable for direct authentication attempts.

---

## 6. Phase 2 Brute Force Attack

netexec was used to execute a password brute force against the domain account `jdoe` over SMB.

**Command executed:**
```
nxc smb 192.168.56.106 -u jdoe -p /home/kali/passlist.txt
```

**Wordlist used (7 entries):** password, Password1, admin123, Welcome1, Corp@123, Summer2026, P@ssword@1234

**Result:**

| # | Password Attempted | Result |
|---|---|---|
| 1 | password | STATUS_LOGON_FAILURE |
| 2 | Password1 | STATUS_LOGON_FAILURE |
| 3 | admin123 | STATUS_LOGON_FAILURE |
| 4 | Welcome1 | STATUS_LOGON_FAILURE |
| 5 | Corp@123 | STATUS_LOGON_FAILURE |
| 6 | Summer2026 | STATUS_LOGON_FAILURE |
| 7 | P@ssword@1234 | **SUCCESS** |


---

## 7. Phase 3 Detection

Detection was performed using Windows Event Viewer on DC01, filtering the Security log for relevant Event IDs.

### 7.1 Event ID 4625 Failed Logon (x6)

Filtered: `Log: Security; Event ID: 4625`

| Field | Value |
|---|---|
| Account Name | jdoe |
| Account Domain | corp.local |
| Logon Type | 3 (Network) |
| Source Network Address | 192.168.56.102 |
| Source Port | 57134 (varied per attempt) |
| Authentication Package | NTLM |
| Failure Reason | Unknown user name or bad password |
| Status / Sub Status | 0xC000006D / 0xC000006A |
| Logged Time | 6/20/2026 1:05:05 PM |

Six consecutive 4625 events were observed for the `jdoe` account, all originating from the same source IP (192.168.56.102), within the same logged timestamp cluster — consistent with an automated brute force attempt rather than isolated manual login failures.

### 7.2 Event ID 4624 — Successful Logon

Filtered: `Log: Security; Event ID: 4624`

Two 4624 events were logged in the same window. One was excluded as unrelated (an ANONYMOUS LOGON / NT AUTHORITY session, generated by netexec's initial null-session fingerprinting probe not the credentialed attack). The relevant successful logon is detailed below:

| Field | Value |
|---|---|
| Account Name | jdoe |
| Account Domain | CORP |
| Logon Type | 3 (Network) |
| Elevated Token | Yes |
| Source Network Address | 192.168.56.102 |
| Source Port | 57238 |
| Authentication Package | NTLM (NTLM V2) |
| Logged Time | 6/20/2026 1:05:05 PM |

The successful logon shares the same source IP, account, and logon type as the preceding failures, confirming it is the culmination of the same attack the seventh and final password attempt succeeding after six failures. The **Elevated Token: Yes** field is significant: jdoe is a member of the IT-Admins security group, meaning this compromise grants the attacker privileged access rather than standard user access, increasing the severity of the incident.

### 7.3 Evidence Exported

- `lab7_4625_failed_logon_jdoe.evtx`
- `lab7_4624_successful_logon_jdoe.evtx`

---

# LAB-AD-001 — Active Directory Penetration Test
**Date:** 2026-06-01  
**Tester:** BrndnSmo  
**Environment:** Home Lab VLAN 40  
**Domain:** lab.local  

---

## Summary

Full penetration test of an internal Active Directory environment. Starting with zero credentials and zero knowledge, a complete attack chain was executed from initial reconnaissance to cracking a privileged service account password in under 10 seconds.

---

## Attack Chain

```
[1] Host Discovery (nmap ping sweep)
        ↓
[2] Port Scanning & Service Enumeration (nmap -sV -sC -A)
        ↓
[3] SMB Enumeration (enum4linux)
        ↓
[4] Authenticated LDAP Enumeration (ldapsearch)
        ↓
[5] Kerberoasting (impacket-GetUserSPNs)
        ↓
[6] Offline Password Cracking (hashcat)
        ↓
[7] SQLService Credentials Obtained ✅
        ↓
[NEXT] Privilege Escalation → Domain Admin
```

---

## Targets

| Host | IP | OS | Role |
|---|---|---|---|
| LAB-DC01 | 10.10.40.10 | Windows Server 2022 | Domain Controller |
| LAB-WS01 | 10.10.40.20 | Windows 10 | Workstation |
| LAB-KALI01 | 10.10.40.60 | Kali Linux | Attacker |

---

## Findings Overview

| ID | Title | Severity |
|---|---|---|
| FIND-001 | SMB Signing Not Required on Workstation | 🔴 High |
| FIND-002 | Full Domain User Enumeration via LDAP | 🟡 Medium |
| FIND-003 | Kerberoastable Service Account | 🔴 Critical |
| FIND-004 | SQLService Password Cracked in 9 Seconds | 🔴 Critical |
| FIND-005 | Overprivileged Service Account | 🔴 Critical |
| FIND-006 | Weak Passwords on Domain User Accounts | 🔴 High |

---

## Credentials Obtained

| Account | Method | Privilege |
|---|---|---|
| jdoe | Known credential | Standard Domain User |
| SQLService | Kerberoasting + hashcat | Group Policy Creator Owners |

---

## Files

- [Full Pentest Report](./AD-Lab-Pentest-Report-001.md)
- [Commands Reference](./Commands-Reference.md)
- [Screenshots](./screenshots/)

---

## Tools Used

| Tool | Purpose |
|---|---|
| nmap | Reconnaissance and port scanning |
| enum4linux | SMB enumeration |
| ldapsearch | LDAP domain enumeration |
| impacket-GetUserSPNs | Kerberoasting |
| hashcat | Password cracking |

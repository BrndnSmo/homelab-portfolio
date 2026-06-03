# Home Lab Cybersecurity Portfolio
**Author:** BrndnSmo  
**Focus:** Active Directory Attack & Defense | Penetration Testing | SOC Operations  

---

## About This Lab

This repository documents hands-on penetration testing and security research conducted in a self-built enterprise-style home lab. Every finding, attack chain, and technique here was performed in an isolated lab environment built from scratch.

The lab simulates a real enterprise network with:
- OPNsense firewall with VLAN segmentation
- Active Directory domain (Windows Server 2022)
- Domain-joined workstations (Windows 10)
- Wazuh SIEM for security monitoring
- Dedicated Kali Linux attack machine

---

## Lab Infrastructure

| Component | Details |
|---|---|
| Firewall | OPNsense on Goodtico N100 Mini PC |
| Switch | Netgear GS308E (VLAN-managed) |
| Hypervisor | Proxmox VE on Dell Optiplex 3060 |
| Storage | Ugreen DXP2800 NAS — RAID1 |
| Attack Machine | Kali Linux (VLAN 40) |
| Domain Controller | Windows Server 2022 |
| Workstation | Windows 10 |
| SIEM | Wazuh |

---

## Network Architecture

```
Internet
    │
[OPNsense Firewall]
    │
[Netgear GS308E Switch]
    ├── VLAN 10 — Trusted Devices
    ├── VLAN 20 — Guest Devices
    ├── VLAN 30 — IoT Devices
    ├── VLAN 40 — Cybersecurity Lab ← All attacks contained here
    └── VLAN 99 — Management
```

---

## Penetration Test Reports

| ID | Date | Target | Techniques | Status |
|---|---|---|---|---|
| [LAB-AD-001](./penetration-tests/LAB-AD-001/) | 2026-06-01 | Active Directory Environment | Recon, LDAP Enum, Kerberoasting, Password Cracking | ✅ Complete |

---

## Techniques Practiced

| Technique | Category | Report |
|---|---|---|
| Network Reconnaissance (nmap) | Recon | LAB-AD-001 |
| SMB Enumeration (enum4linux) | Enumeration | LAB-AD-001 |
| LDAP Domain Enumeration | Enumeration | LAB-AD-001 |
| Kerberoasting | Credential Attack | LAB-AD-001 |
| Offline Password Cracking (hashcat) | Credential Attack | LAB-AD-001 |
| NTLM Relay Attack | Credential Attack | LAB-AD-002 |
| BloodHound AD Enumeration | Enumeration | LAB-AD-002 |
| AS-REP Roasting | Credential Attack | LAB-AD-002 |
| Pass the Hash | Lateral Movement | LAB-AD-002 |
| DCSync | Privilege Escalation | LAB-AD-002 |
| Domain Admin Compromise | Full Compromise | LAB-AD-002 |

---

## Certifications In Progress

- [ ] CompTIA Security+
- [ ] eJPT (Junior Penetration Tester)
- [ ] OSCP (Offensive Security Certified Professional)

---

> All activity in this repository was performed in an isolated home lab environment on systems I own and operate. No unauthorized systems were accessed.

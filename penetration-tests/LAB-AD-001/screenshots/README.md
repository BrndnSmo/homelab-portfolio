# Screenshots — LAB-AD-001
**Evidence from both attack sessions**

---

## Session 001 — 2026-06-01

| File | What It Shows |
|---|---|
| `nmap ping sweep results` | Host discovery — all 5 live hosts on VLAN 40 identified |
| `nmap scan of ws01` | Full port scan of LAB-WS01 — SMB signing not required finding |
| `nmap scan of DC01_A` | Full port scan of LAB-DC01 — Kerberos, LDAP, SMB exposed |
| `nmap scan of DC01_B` | DC01 scan continued — SMB signing required confirmed |
| `enum4linux results` | SMB enumeration — null sessions blocked, domain name confirmed |
| `ldapserarch user list` | Authenticated LDAP query — full domain user list extracted |
| `ntpdate sync` | Clock skew fix — required before Kerberos attacks |
| `Kerberoasting hash output` | SQLService TGS hash extracted via Kerberoasting |
| `Kerberoasting hash output_B` | Full hash output confirmation |
| `hashcat cracked password_A` | hashcat cracking session started |
| `hashcat cracked password_B` | Cracking in progress — rockyou.txt dictionary attack |
| `hashcat cracked password_C` | Status: Cracked — MYpassword123# — 9 seconds |

---

## Session 002 — 2026-06-02

| File | What It Shows |
|---|---|
| `Neo4j Start` | Neo4j database service started successfully |
| `Bloodhound json files` | bloodhound-python collection complete — 7 JSON files |
| `bloodhound zip files for import` | Data packaged for BloodHound import |
| `Bloodhound results` | BloodHound CE dashboard after data import |
| `Attack Path` | SQLSERVICE → MemberOf → DOMAIN ADMINS attack path |
| `Evil-WinRM Domain Access` | Interactive shell on DC — Domain Admin confirmed |
| `Full dump_A` | DCSync attack — domain credentials being extracted |
| `Full dump_B` | DCSync complete — all hashes including Administrator dumped |

---

*All testing performed on owned lab infrastructure — VLAN 40 isolated network*

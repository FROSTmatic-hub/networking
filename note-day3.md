# Day 3 — SMB & Windows service enumeration 
**Author:** Shaafi (FROSTmatic-hub)  
**Objective:** Enumerate SMB/NetBIOS/RPC on the Windows 10 lab VM; identify shares, permissions, user accounts, and potential misconfigurations.

---

## Lab setup
- Host: my laptop (home network)  
- Attacker: Kali VM — IP: `192.168.31.216` (bridged)  
- Target: Windows 10 VM — IP: `192.168.31.159` (bridged)  
- Network note: Bridged mode — scans target single VM IP only.

---


## Commands executed
```bash
nmap -p 139,445 --script smb-os-discovery, smb-protocols, smb-enum-shares, smb-vuln-ms17-010 192.168.31.159
enum4linux -a 192.168.31.159
smbclient -L //192.168.31.159 -N
smbclient -L //192.168.31.159 -U 





```
## Observations
- Ports: 139/tcp and 445/tcp are open.
- `smb-protocols` : NT LM 0.12 (SMBv1) 
- `smb-os-discovery` : OS: Windows 10 Pro 10240 (Windows 10 Pro 6.3)
- `enum4linux` : Result saved in `images/day3/day3_enum4linux.png`
- `smbclient -L //192.168.1.101 -N` : resulted in failure tried again with `-U` for user and password of WIN 10 VM
- Tried scanning with `smb-enum-shares, smb-vuln-ms17-010` resulted in error saved in `networking/outputs/day3_failed_smb.txt`
- Tried another scan with `smb-*` saved the result in `networking/outputs/day3_smb_scans.txt`

## Lessons learned
- Practiced targeted SMB enumeration using Nmap NSE scripts, enum4linux, smbclient
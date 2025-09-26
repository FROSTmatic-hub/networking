# Day 2 — Host Discovery & Nmap Scanning 
**Author:** Shaafi (FROSTmatic-hub)  
**Objective:** Identify the Windows 10 lab host, discover open ports/services, and attempt OS fingerprinting.

---

## Lab setup
- Host: Windows Laptop (connected to Wi-Fi router)  
- Attacker: Kali Linux VM — IP: 192.168.31.213 (Bridged to router LAN)  
- Target: Windows 10 VM — IP: 192.168.31.159 (Bridged to router LAN)  
- Network mode: Bridged Adapter (VMs get IPs directly from router DHCP)  



---

## Commands executed
```bash
# Host discovery (ping sweep)
nmap -sn 192.168.31.159

# SYN scan (top ports)
nmap -sS 192.168.31.159

# Service/version detection and save output
nmap -sV -oN day2_scan.txt 192.168.31.159

# Aggressive scan (OS detection + scripts)
nmap -A 192.168.31.159

```
## Observations
nmap -sn: Nmap scan report for DESKTOP-TD9BS8A.lan (192.168.31.159) | Host is up (0.00041s latency).
nmap -sS: open ports found [135/tcp, 139/tcp, 445/tcp, 5357/tcp] | With Win 10 Firewall settings set to off.
nmap -sV: View output from images/
nmap -A: OS details: Microsoft Windows 10 1507 - 1607

# Lessons learned & next steps
Practiced host discovery and scanning with nmap flags: -sn, -sS, -sV, -A.
Learned to save scan outputs for documentation.
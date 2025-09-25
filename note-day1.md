# Day 1 — Networking refresher & ARP discovery
**Date:** 2025-09-25  
**Author:** Shaafi (FROSTmatic-hub)  
**Objective:** Confirm basic connectivity and view ARP table to map IP ↔ MAC in a local lab VM.

## Lab setup
- Attacker: Kali Linux (VM)  
- Target: Windows 10 (VM)  
- Network mode: Host-only (192.168.56.0/24) — isolated lab

## Commands executed
```bash
ip a
ping -c 4 192.168.56.101
arp -a

# Observations
ping succeeded, confirming basic network-level connectivity (ICMP allowed).

arp -a output shows mapping: 192.168.56.101 → 08:00:27:12:34:56 (example MAC). This confirms layer-2 discovery and local ARP resolution.

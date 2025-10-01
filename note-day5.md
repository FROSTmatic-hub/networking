# Day 5 — PoC Report: Local Privilege Escalation

**Author:** Shaafi (FROSTmatic-hub)  
**Lab:** Local Win10/Win11 VM (owned lab VM)  
**Snapshot before PoC:** `day5_before_poc` (taken)

---

## Objective (PoC)
Attempt to demonstrate a safe, non-destructive proof-of-concept (PoC) for local privilege escalation based on findings from Day 4 (winPEAS enumeration). The goal was to identify a feasible escalation vector and document evidence and remediation. Exploit steps that enable real-world weaponization are *not* included here, this writeup instead documents the reconnaissance and PoC outcomes for responsible reporting and portfolio use.

---

## Summary (one-line)
User `win11\frost` has `SeImpersonatePrivilege` enabled (high-value). A SYSTEM scheduled task (`MicrosoftEdgeUpdateTaskMachineCore{GUID}`) was discovered and can be triggered, but the EdgeUpdate binary & folder are correctly protected (no write/modify by Users). `C:\Users\frost\Downloads` is writable and available as a staging area.

---

## Evidence collected (commands + outputs)

### 1) User privilege confirmation
```powershell
whoami /priv
#Output saved to outputs/day5_whoami_priv.txt
#SeImpersonatePrivilege - Enabled
#SeDebugPrivilege - Enabled
```
### 2) Scheduled Task discovered (SYSTEM)
```powershell
schtasks /query /fo LIST /v | findstr /i "TaskName Run As User"
#FiTaskName: \MicrosoftEdgeUpdateTaskMachineCore{8F235A54-E7A2-4B40-8DE2-E8EBD2ED5320}
#Run As User: SYSTEM
#Task To Run: C:\Program Files (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe /c
schtasks /run /TN "\MicrosoftEdgeUpdateTaskMachineCore{8F235A54-E7A2-4B40-8DE2-E8EBD2ED5320}"
#Result: SUCCESS (task triggered and executed)
#Evidence saved to outputs/day5_schtasks_edgeupdate.txt, images/day5/day5_schtasks_run.png
```

### 3) 4) File/folder ACL checks (evidence)
```powershell
icacls "C:\Program Files (x86)\Microsoft\EdgeUpdate"
icacls "C:\Program Files (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe"
icacls "C:\Users\frost\Downloads"
#EdgeUpdate folder & MicrosoftEdgeUpdate.exe → BUILTIN\Users: (RX) → read/execute only, no write/modify. (Saved in outputs/day5_icacls_edgeupdate.txt)
#C:\Users\frost\Downloads → writable by the current user (Saved in outputs/day5_download_write_test.txt)
```
## PoC Outcome
1) #### Unquoted Service Path
- Status: Not found: Service sweep returned services executed via `svchost` or correctly quoted `PathNames`. No classic unquoted-path target present.
2) #### Scheduled Task (EdgeUpdate)
- Status: Found and runnable as `SYSTEM`, but not exploitable on this VM because binary and folder are locked down. Documented as a high-value observation and remediation target.
3) #### Token impersonation (SeImpersonatePrivilege)
- Status: `SeImpersonatePrivilege` is enabled for `win11\frost`. This is a condition that can enable token-impersonation based local privilege escalation when paired with a suitable IPC endpoint / service that performs impersonation.
- Action taken: enumeration only (no exploit performed in this environment).
- Next-step (ethical): practice the sequence on a sanctioned training VM (TryHackMe or VulnHub) that’s explicitly designed for demonstrating token-impersonation techniques. 

## Ethics & safety note
All actions described above were performed on lab VMs owned by me. No exploitation of external or third-party systems was performed. Any future exploit testing will be done only in authorized, isolated training environments or on owned lab machines and will include snapshots and cleanup.




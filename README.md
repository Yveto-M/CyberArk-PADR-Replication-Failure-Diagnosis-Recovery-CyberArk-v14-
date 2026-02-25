# CyberArk PADR Replication Failure Diagnosis Recovery-CyberArk-v14


![PADR Full Replication Completed Successfully](<img width="963" height="403" alt="Screenshot 2026-02-25 141701" src="https://github.com/user-attachments/assets/9da850b3-34f3-46a1-a980-64de27fc4c74" />)


---

## What Happened
The PADR service on the DR Vault was failing to replicate from the Primary Vault and 
repeatedly triggering unintended failover. Five layered issues were diagnosed and resolved 
entirely via PowerShell and the CyberArk REST API — no UI required.

---

## Root Causes & Fixes

| # | Root Cause | Fix |
|---|---|---|
| 1 | `Replicate` user was type `EPVUser` — Vault rejects DR connections from this type | Deleted and recreated as `DRUser` via REST API |
| 2 | `BackupAllSafes` permission missing from new user | Applied via PUT API with `vaultAuthorization` |
| 3 | `user.ini` credential file was stale/mismatched after password change | Regenerated using `CreateCredFile.exe /NotSecure` |
| 4 | `FailoverMode=Yes` persisted in `padr.ini` after unintended failover | Reset to `No` via PowerShell string replace |
| 5 | DR Vault's `PrivateArk Server` service kept auto-starting | Stopped and set to `Manual` startup |

---

## Confirmed Resolution

PADR0093I Full Replication Completed Successfully.
PADR0099I Metadata Replication is running successfully.
---

## Skills Demonstrated
`CyberArk REST API` · `PADR Log Analysis` · `PowerShell` · 
`CreateCredFile.exe` · `DR Architecture` · `PAM Fault Isolation`

---
*Part of an enterprise-grade CyberArk v14 home lab built for IAM Engineer portfolio development.*

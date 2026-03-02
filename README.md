# Threat Intelligence Mapping & Enterprise Ransomware Playbooks

**Author:** Farouq Hassan
**Focus Areas:**

* MITRE ATT&CK Navigator (Impact-Scored)
* Threat Actor Evidence Mapping
* Ransomware IR Playbooks
* Supply-Chain Compromise Response
* Executive & Regulatory Communications

---

# Part 1 — APT29 (NOBELIUM) Impact-Scored ATT&CK Mapping

📄 Source: 

---

## Objective

Build a structured ATT&CK Navigator layer with:

* OSINT-backed technique mapping
* Evidence references `[S#]`
* Impact-based scoring model:

  * High = 90
  * Medium = 60
  * Low = 30

---

## Impact Scoring Model

| Score | Meaning                           |
| ----- | --------------------------------- |
| 90    | High operational/strategic impact |
| 60    | Medium operational impact         |
| 30    | Lower operational impact          |

---

## High-Impact Techniques (Score: 90)

| Technique | Description              | Evidence                                     |
| --------- | ------------------------ | -------------------------------------------- |
| T1195.002 | Supply Chain Compromise  | SolarWinds Orion trojanized updates [S1][S4] |
| T1550.001 | Access Token Abuse       | Identity/token abuse in cloud/AD [S1]        |
| T1003.001 | LSASS Credential Dumping | Credential access enabler [S5]               |

---

## Medium-Impact Techniques (Score: 60)

* T1566.002 — Spearphishing Link (USAID campaign) [S2][S3]
* T1204.002 — User Execution
* T1059.001 — PowerShell
* T1053.005 — Scheduled Task
* T1071.001 — Web-based C2 (SUNBURST)
* T1027 — Obfuscation
* T1041 — Exfiltration over C2
* T1114 — Email Collection

---

## Low-Impact Techniques (Score: 30)

* T1087 — Account Discovery
* T1005 — Local Data Collection

---

## Full ATT&CK Navigator JSON (Verbatim)

The complete JSON layer is stored in:

📄 

(Used for direct import into MITRE ATT&CK Navigator)

This includes:

* Technique IDs
* Color-coded severity
* Evidence comments
* Platform filtering
* Metadata sources (CISA, Microsoft, Google Cloud, MITRE)

---

## Intelligence Sources Referenced

From metadata section :

* CISA AA20-352A (SolarWinds)
* Microsoft (USAID / Constant Contact campaign)
* Google Cloud / Mandiant SUNBURST analysis
* MITRE ATT&CK Group page (APT29)
* Microsoft FoggyWeb blog

---

# Part 2 — CityWorks Utilities Ransomware IR Playbook

📄 Source: 

---

## Trigger Criteria

Playbook activates when:

* Mass file modifications
* Ransom instructions appear
* Abnormal privileged authentication
* Backup failures + file integrity issues

---

## Scope Definition

Incident is in scope when:

* Encryption confirmed
* Data extortion suspected
* Active lateral movement detected

---

# Decision Tree — Pre-Impact vs Ongoing Impact

## Initial Signals (Pre-Impact)

Indicators:

* Limited file changes
* Isolated workstation alerts
* No mass encryption

Actions:

* Restrict affected accounts
* Isolate endpoints (switch-level)
* Preserve memory + logs

---

## Ongoing Impact

Indicators:

* Widespread encryption
* Ransom notes present
* Backup failures

Actions:

* Enforce segmentation
* Disable compromised accounts
* Suspend backup jobs
* Secure domain controller logs

---

# Containment Strategy Matrix

| Option                    | Speed  | Impact                  | Evidence Preservation |
| ------------------------- | ------ | ----------------------- | --------------------- |
| Endpoint Isolation        | Medium | Localized disruption    | High                  |
| Account Controls          | Fast   | Low–Medium              | High                  |
| Lateral Comms Restriction | Medium | Moderate service impact | Medium                |

---

## Selected Containment Path

✔ Immediate account controls + targeted endpoint isolation

Reason:

* Fast
* Reversible
* Limits spread
* Maintains municipal operations

---

# Recovery Preconditions

Before restore:

* Encryption halted
* Clean offline backups verified
* Credentials reset
* Systems validated

Recovery Order:

1. Identity services
2. File services
3. Line-of-business apps
4. User endpoints

---

# Communications Templates

## Executive Update

Incident confirmed at 04:00 UTC affecting file services and limited workstations. Containment actions initiated. Core services partially available. Incident Commander: Alex Morgan (CISO).

---

## Staff Advisory

Do not power off devices. Do not attempt self-remediation. Report ransom messages immediately.

---

# Closure Criteria

* No malicious indicators for 72 hours
* Systems restored from clean backups
* Evidence archived
* Post-incident review within 10 business days

---

# Part 3 — Bazaarjo 24-Hour Incident Response Playbook

📄 Source: 

---

## Trigger

NCSC notification:

> Active sale of Bazaarjo data on external marketplace.

---

# 0–4 Hours: Immediate Containment

* Activate IR team
* Assign Incident Commander + legal liaison
* Isolate production systems
* Revoke exposed credentials
* Suspend data pipelines
* Block IOCs
* Preserve volatile data
* Engage legal counsel

---

# 4–24 Hours: Evidence & Scoping

* Collect logs (30–60 days):

  * Application logs
  * Database logs
  * Authentication logs
* Acquire forensic images
* Review CI/CD logs
* Validate data samples with NCSC

---

# Communication Plan

* CISO informs CEO + Board
* Legal handles regulator coordination
* Hourly security updates internally
* External statements jointly approved

---

# Draft Communications

### NCSC (3-line response)

Bazaarjo has activated IR process, containing systems, preserving evidence, and will provide scope within 24 hours.

### Public Statement

Investigating potential incident; immediate security steps taken; affected parties will be contacted.

---

# Business Risk Trade-Off

Immediate containment may disrupt operations and revenue, but delay risks:

* Wider data exposure
* Regulatory penalties
* Loss of trust

---

# Reflection — Root Cause

Primary failure:

> Lack of secure software supply-chain validation and runtime artifact integrity controls.

Specifically:

* Missing artifact validation
* Inadequate runtime monitoring
* Insufficient CI/CD integrity controls

---

# Top 3 Evidence Sources

1. Authentication & IAM logs
2. CI/CD + artifact repository logs
3. Database access logs

---

# Skills Demonstrated in Session 15

* Impact-based ATT&CK scoring
* ATT&CK Navigator layer creation
* OSINT-backed technique mapping
* Ransomware IR design
* Supply-chain breach response
* Executive communication drafting
* Regulatory-aware IR handling
* Evidence prioritization
* Business risk trade-off evaluation

---

# Security Maturity Themes Across Session 15

| Area           | Improvement Theme                       |
| -------------- | --------------------------------------- |
| Identity       | Token protection + credential hardening |
| CI/CD          | Artifact integrity validation           |
| Logging        | Centralized, retention-aware logging    |
| Containment    | Reversible controls first               |
| Communications | Structured executive reporting          |
| Recovery       | Evidence-first restoration              |

# SOC Analyst L1 — Consolidated Investigation Report

**Report Type:** Consolidated SOC Investigation Report  
**Analyst Level:** Security Operations Center — Level 1  
**Investigation Scope:** Simulated Security Investigations  
**Cases Reviewed:** 001, 002, 003, 004  
**Environment:** Simulated Training Environment  
**Status:** Completed — Documentation and Analysis

---

## 1. Executive Summary

This report consolidates four simulated security investigations conducted as part of practical SOC Analyst Level 1 training.

The investigations cover several security scenarios:

- Multiple failed authentication attempts against user accounts.
- IP reputation analysis using threat intelligence sources.
- Windows authentication analysis involving failed and successful logons.
- Local account creation and potential privilege escalation activity.

The investigations identified suspicious patterns that may be associated with brute-force attempts, unauthorized access, account creation, and privilege escalation.

The findings demonstrate the importance of correlating authentication events, reviewing endpoint activity, and using threat intelligence to support security alert investigations.

All findings are based on simulated training exercises. They do not represent confirmed real-world security incidents or verified compromises.

## 2. Scope and Methodology

### 2.1 Investigation Scope

This report covers four independent simulated SOC investigations:

| Case ID | Investigation | Main Focus |
|---|---|---|
| 001 | Multiple Failed Logins | Authentication failures and suspicious login patterns |
| 002 | IP Reputation Analysis | Threat intelligence and IP reputation enrichment |
| 003 | Windows Authentication Analysis | Windows logon events and suspicious process activity |
| 004 | Account Creation and Privilege Assignment | Account creation and potential privilege escalation |

### 2.2 Analysis Methodology

The investigations followed a structured SOC L1 analysis approach:

1. **Alert Review:** Identify the reported security activity and understand the available evidence.
2. **Evidence Analysis:** Examine authentication records, Windows Security Event Logs, and process activity.
3. **Threat Intelligence Enrichment:** Review external IP reputation information where applicable.
4. **MITRE ATT&CK Mapping:** Identify potential relationships between observed activity and known adversary techniques.
5. **Risk Assessment:** Evaluate the suspicious activity, its potential impact, and the limitations of the available evidence.
6. **Documentation and Escalation:** Record findings, recommend further investigation, and identify cases requiring SOC L2 review.

### 2.3 Tools and Data Sources

The following tools and sources were used during the simulated exercises:

- Windows Security Event Logs
- VirusTotal
- AbuseIPDB
- MITRE ATT&CK
- Simulated SIEM alerts and training datasets

- ## 3. Investigation Findings

### 3.1 Case 001 — Multiple Failed Logins

**Investigation Focus:** Suspicious authentication activity.

**Key Findings:**
- A total of 82 failed authentication attempts were observed.
- Four user accounts were targeted: `jgarcia`, `mlopez`, `agarcia`, and `jperez`.
- The attempts originated from the same IP address: `185.220.101.45`.
- The activity occurred between 09:14 and 09:21.

**Analysis:**

The repeated authentication failures against multiple accounts from a single source IP may indicate password spraying or brute-force activity.

No successful authentication was identified in the available exercise data.

**Assessment:** Suspicious authentication activity requiring further investigation.

---

### 3.2 Case 002 — IP Reputation Analysis

**Investigation Focus:** Threat intelligence enrichment.

**Key Findings:**
- IP address analyzed: `185.220.101.45`.
- VirusTotal reported 16 detections.
- AbuseIPDB reported a 100% confidence score and 6,897 reports at the time of the exercise lookup.
- The available training notes associated the IP with suspicious activity, including brute-force attempts and other reported abuse categories.

**Analysis:**

The reputation information provides additional context for investigating the IP address identified in Case 001.

However, reputation scores and external reports do not independently prove malicious activity.

**Assessment:** High-risk reputation indicators supporting further investigation of the authentication activity.

---

### 3.3 Case 003 — Windows Authentication Analysis

**Investigation Focus:** Windows authentication and suspicious process activity.

**Key Findings:**
- Four failed logon events (4625) were recorded for the `admin` account.
- A successful logon event (4624) followed from the same source IP address.
- The source IP was `185.220.101.45`.
- Process creation events (4688) recorded commands including `cmd.exe`, `whoami.exe`, and `ipconfig.exe`.
- Additional activity involved account and group enumeration, creation of `backup_admin`, and subsequent authentication using that account.

**Analysis:**

The sequence of failed and successful logons, followed by command execution, represents suspicious activity that requires further investigation.

The available evidence does not establish whether the activity was authorized or whether the system was compromised.

**Assessment:** High-priority suspicious activity recommended for SOC L2 review.

---

### 3.4 Case 004 — Account Creation and Privilege Assignment

**Investigation Focus:** Local account creation and potential privilege escalation.

**Key Findings:**
- Commands were executed to enumerate local accounts and groups.
- A new account named `backup_admin` was created.
- Event ID 4720 recorded the account creation.
- Event ID 4728 recorded the addition of `backup_admin` to a group identified in the exercise as `Administrators`.
- A successful logon using `backup_admin` was subsequently recorded.
- A command prompt was executed after authentication.

**Analysis:**

The sequence may indicate unauthorized account creation and privilege escalation.

The group membership event requires validation against the original Windows logs, including confirmation of the group type and the appropriate event ID.

**Assessment:** High-priority suspicious activity recommended for SOC L2 review.

## 4. Overall Risk Assessment

The four investigations identified different types of suspicious activity, with varying levels of potential security impact.

| Case ID | Main Security Concern | Recommended Priority |
|---|---|---|
| 001 | Multiple failed authentication attempts against several accounts | Medium |
| 002 | Suspicious IP reputation indicators | Medium |
| 003 | Failed and successful logons followed by suspicious process activity | High |
| 004 | Account creation and potential administrative privilege assignment | High |

### 4.1 Risk Analysis

**Authentication Activity (Cases 001 and 002)**

The repeated authentication failures against multiple accounts, combined with the suspicious IP reputation indicators, justify further investigation.

The available evidence suggests possible brute-force or password-spraying activity. However, no successful authentication was identified in Case 001.

**Windows Authentication and Account Activity (Cases 003 and 004)**

The activity documented in Cases 003 and 004 raises greater concern because it includes successful authentication, command execution, account creation, and potential administrative privilege assignment.

These activities could indicate unauthorized access and attempts to maintain privileged access.

### 4.2 Overall Assessment

Cases 003 and 004 should receive the highest investigation priority due to their potential impact on system security.

Cases 001 and 002 provide relevant indicators of suspicious authentication activity and IP reputation, but the available evidence does not confirm a successful compromise.

All priorities are preliminary assessments based on the simulated evidence and may change if additional information becomes available.

# SOC Investigation 003 — Windows Authentication Analysis

## 1. Overview

| Field | Details |
|---|---|
| Case ID | SOC-2026-003 |
| Alert | Suspicious Authentication Activity |
| Severity | High (as assigned by the simulated SIEM alert) |
| Host | SRV-FILE-01 |
| Account | admin |
| Source IP | 185.220.101.45 |
| Status | Suspicious activity — escalation recommended |
| Environment | Simulated training exercise |

## 2. Objective

Investigate suspicious authentication activity on the Windows host `SRV-FILE-01` by correlating failed logons, a successful logon, and subsequent process creation events.

## 3. Evidence Collected

### Authentication events

Four failed logon events were recorded for the `admin` account:

| Time | Event ID | Result | Source IP |
|---|---:|---|---|
| 10:31:04 | 4625 | Failed logon | 185.220.101.45 |
| 10:31:08 | 4625 | Failed logon | 185.220.101.45 |
| 10:31:12 | 4625 | Failed logon | 185.220.101.45 |
| 10:31:17 | 4625 | Failed logon | 185.220.101.45 |
| 10:31:22 | 4624 | Successful logon | 185.220.101.45 |

The events identify the target host as `SRV-FILE-01` and the logon type as `10`, which is associated with RemoteInteractive logons, commonly Remote Desktop.

### Process creation events

After the successful logon, the SIEM recorded the following process creation events:

| Time | Event ID | Process | Parent process |
|---|---:|---|---|
| 10:31:41 | 4688 | `cmd.exe` | `winlogon.exe` |
| 10:31:45 | 4688 | `whoami.exe` | `cmd.exe` |
| 10:31:49 | 4688 | `ipconfig.exe` | `cmd.exe` |

Event ID 4688 records process creation. The commands shown can be used for legitimate administration, but their execution immediately after suspicious authentication warrants further investigation.

### Account discovery and account creation events

The simulated SIEM exercise recorded additional commands following the initial process activity:

| **Time** | **Event ID** | **Activity** |
| -------- | ------------ | ------------ |
| 10:32:03 | 4688 | `net.exe` executed with the `net user` command |
| 10:32:11 | 4688 | `net.exe` executed with the `net localgroup administrators` command |
| 10:32:24 | 4688 | `net.exe` executed with a command to create the `backup_admin` account |
| 10:32:25 | 4720 | A user account named `backup_admin` was created |

These events indicate account and group discovery activity followed by the creation of a new account. In the context of the preceding suspicious authentication events, this sequence warrants investigation for possible unauthorized account creation.

**Security note:** The original exercise includes a password in the account-creation command. It has intentionally been omitted from this public report.
## 4. Analysis

### Failed and successful authentication

Four failed logons followed by a successful logon from the same source IP suggest a possible password-guessing or other unauthorized access attempt.

The sequence raises concern because the successful authentication occurred only five seconds after the final recorded failure. However, these events alone do not establish who controlled the source IP or whether the account was definitively compromised.

### Post-authentication activity

- `cmd.exe`: Opens the Windows command shell.
- `whoami.exe`: Displays the identity associated with the current process.
- `ipconfig.exe`: Displays network configuration information.

In this context, these commands are consistent with possible initial system discovery following access. They are not inherently malicious, so the surrounding activity and authorization context must be reviewed.

## 5. MITRE ATT&CK Mapping

| Observed behavior | Potential technique | Evidence |
|---|---|---|
| Possible password guessing | T1110 — Brute Force | Four failed logons followed by a successful logon |
| Windows command execution | T1059.003 — Windows Command Shell | Event ID 4688: `cmd.exe` |
| User identity discovery | T1033 — System Owner/User Discovery | Event ID 4688: `whoami.exe` |
| Network configuration discovery | T1016 — System Network Configuration Discovery | Event ID 4688: `ipconfig.exe` |

These mappings are preliminary hypotheses based on the observed behavior, not proof that a specific attack technique was used.

## 6. Recommended L1 Actions

1. Preserve the relevant Windows Security logs and SIEM alert details.
2. Review surrounding authentication events for additional accounts, source addresses, and successful logons.
3. Verify whether the `admin` logon was expected and authorized.
4. Investigate subsequent process activity and any changes to accounts, groups, services, or scheduled tasks.
5. Enrich the source IP using approved threat-intelligence sources and correlate the results with the logs.
6. Escalate promptly to SOC L2 because the combination of failed logons, successful authentication, and subsequent command execution is suspicious.
7. Recommend containment measures through the organization's incident-response procedure. Any account restriction, IP block, or host isolation should follow the applicable authorization process.

## 7. Conclusion

The simulated alert contains a suspicious sequence of four failed logons, one successful logon to the `admin` account, and subsequent execution of system discovery commands on `SRV-FILE-01`.

The evidence supports a **high level of suspicion and escalation to SOC L2**. Further investigation is required to determine whether the access was unauthorized, establish its scope, and identify any additional activity.

## 8. Limitations

- This is a simulated training exercise, not a confirmed real-world incident.
- The supplied records do not include all Windows event fields or the complete host timeline.
- The legitimacy of the `admin` account activity has not been independently verified.
- The observed commands can also be used for legitimate administrative purposes.

## Disclaimer

This report is part of an educational SOC Analyst L1 portfolio. All findings are based on simulated training data and are not claims about a real organization or incident.

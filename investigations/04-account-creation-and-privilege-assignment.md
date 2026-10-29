# SOC Investigation 004 — Account Creation and Privilege Assignment

## 1. Investigation Objective

The objective of this investigation is to analyze suspicious account creation and privilege assignment activity on a Windows system.

The investigation focuses on identifying:
- Commands used to enumerate local accounts and groups.
- Creation of a new local user account.
- Assignment of the new account to the Administrators group.
- Subsequent authentication activity involving the newly created account.

The goal is to determine whether the observed activity may indicate unauthorized account creation or privilege escalation.

## 2. Event Summary

The simulated investigation includes the following security events:

| Event ID | Activity | Description |
|---|---|---|
| 4688 | Process Creation | Execution of commands to enumerate local users and groups. |
| 4688 | Process Creation | Execution of a command to create a new local user account named `backup_admin`. |
| 4720 | User Account Created | Creation of the `backup_admin` account. |
| 4728 | Member Added to Security Group | Addition of `backup_admin` to a group identified in the exercise as `Administrators`. |
| 4624 | Successful Logon | Successful authentication using the `backup_admin` account. |
| 4688 | Process Creation | Execution of `cmd.exe` after the successful logon. |

**Affected host:** Windows system (hostname not specified in the exercise).

**Account involved:** `backup_admin`

**Source:** Simulated Windows security event investigation exercises 4 and 5.

## 3. Activity Analysis

The simulated events show a sequence of account discovery, account creation, and privilege assignment activity.

### 3.1 Account and Group Discovery

The following commands were executed:

- `net user`
- `net localgroup administrators`

These commands can be used to enumerate local user accounts and identify members of the local Administrators group.

### 3.2 Account Creation

A process creation event (4688) recorded the execution of a command to create a new account named `backup_admin`.

A subsequent event (4720) recorded the creation of this account.

This activity may indicate an attempt to establish an additional account on the system.

### 3.3 Privilege Assignment

Event 4728 recorded the addition of `backup_admin` to a group identified in the exercise as `Administrators`.

If this account was successfully added to an administrative group, it would gain elevated privileges.

### 3.4 Subsequent Authentication

A successful logon event (4624) was recorded for `backup_admin`, followed by the execution of `cmd.exe` (Event ID 4688).

This indicates that the newly created account was subsequently used to authenticate to the system.

## 4. Security Assessment

The observed sequence raises concerns about possible unauthorized account creation and privilege escalation.

Key observations:

- Local account and group enumeration was performed.
- A new account named `backup_admin` was created.
- An event recorded the addition of this account to a group identified as `Administrators`.
- The newly created account was subsequently used for a successful logon.
- A command prompt was executed after authentication.

### Potential Security Impact

If the activity was not authorized, the newly created account could provide persistent access to the system with elevated privileges.

This could allow an unauthorized user to perform administrative actions and potentially compromise the affected host.

### Assessment Limitations

The available evidence comes from a simulated exercise. The following details have not been independently verified:

- Whether the account creation was authorized.
- Whether `backup_admin` actually received local administrator privileges.
- Whether the successful logon was performed by an attacker.
- Whether the activity affected any other systems.

The group membership event (4728) should be validated against the original Windows logs. For a built-in local group, Event ID 4732 would normally be expected instead.

## 5. MITRE ATT&CK Mapping

The observed activities may be associated with the following MITRE ATT&CK techniques:

| Technique ID | Technique | Observed Activity |
|---|---|---|
| T1136.001 | Create Account: Local Account | Creation of the `backup_admin` account. |
| T1087.001 | Account Discovery: Local Account | Execution of `net user`. |
| T1069.001 | Permission Groups Discovery: Local Groups | Execution of `net localgroup administrators`. |
| T1059.003 | Windows Command Shell | Execution of commands through `cmd.exe`. |

These mappings are based on the commands and events described in the simulated exercise. They represent potential technique associations, not confirmation of malicious activity.

## 6. Conclusion and Recommendations

### Conclusion

The simulated investigation identified a sequence of activities involving local account discovery, creation of a new account named `backup_admin`, attempted or reported administrative group assignment, and subsequent successful authentication using that account.

This sequence is suspicious and may indicate unauthorized account creation and privilege escalation.

However, the available evidence is insufficient to confirm a security compromise. Further validation is required.

### Recommended Actions

1. Verify whether the creation of `backup_admin` was authorized.
2. Review the original Windows Security logs to confirm the group membership event and its Event ID.
3. Verify whether `backup_admin` belongs to the local Administrators group.
4. Review the successful logon event (4624), including its logon type, source IP address, and timestamp.
5. Investigate the commands executed after authentication.
6. If unauthorized activity is confirmed, disable the account, review other privileged accounts, and follow the organization's incident response procedures.

### Escalation Recommendation

**Recommended priority: High**

Escalate the investigation to SOC Level 2 for further validation because the observed sequence includes account creation, possible privilege assignment, and successful authentication.

### Investigation Scope and Limitations

This case is based on simulated training exercises. The original event records and complete system context have not been independently verified. The findings should therefore be treated as investigative indicators rather than confirmation of a real security incident.

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

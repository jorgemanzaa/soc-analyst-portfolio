# SOC Investigation 001 — Multiple Failed Logins

## 1. Overview

- **Case ID:** SOC-2026-001
- **Investigation type:** Authentication analysis
- **Role:** SOC Analyst L1 — training exercise
- **Severity:** Medium — based on the simulated alert
- **Status:** Investigation and escalation recommended
- **Environment:** Simulated SIEM alert

## 2. Alert Summary

The SIEM generated an alert for multiple failed authentication attempts against a user account.

- **Source IP:** `185.220.101.45`
- **Initially affected user:** `jgarcia`
- **Initial failed attempts:** 20
- **Initial time window:** 09:14–09:21

Further simulated SIEM results showed failed authentication attempts against four accounts from the same source IP.

| User | Failed attempts |
|---|---:|
| jgarcia | 20 |
| mlopez | 18 |
| agarcia | 23 |
| jperez | 21 |
| **Total** | **82** |

## 3. Initial Assessment

The first alert could indicate repeated password guessing against a single account. However, the initial evidence alone does not establish whether the activity is malicious.

The additional evidence shows repeated failed authentication attempts against multiple accounts from the same IP address within the same time window.

This pattern raises suspicion of password spraying or another brute-force-related activity.

## 4. Evidence and Investigation

The following observations support further investigation:

- Repeated authentication failures.
- Four different user accounts targeted.
- A common source IP across the simulated events.
- A concentrated period of activity.

The next investigation steps would include checking for successful logins, reviewing authentication logs for other affected accounts, and determining whether the source IP appears in other alerts.

## 5. Threat Intelligence

The simulated investigation was extended using VirusTotal and AbuseIPDB.

The recorded results indicated a suspicious reputation for the source IP, including multiple abuse reports and threat detections.

External IP reputation is contextual evidence. It does not independently prove that the observed authentication attempts were malicious.

## 6. Recommended SOC L1 Actions

1. Review related authentication events and identify any successful logins.
2. Enrich the source IP using threat intelligence sources and record the lookup date.
3. Check whether additional accounts or hosts are affected.
4. Document the evidence, timestamps, affected accounts and working hypothesis.
5. Escalate to SOC L2 if the suspicious pattern persists or the investigation identifies stronger evidence of compromise.
6. Recommend blocking the source IP according to the organisation's incident response procedures and authorisation requirements.

## 7. MITRE ATT&CK — Preliminary Mapping

- **T1110 — Brute Force:** A possible match for the repeated authentication failures. The exact sub-technique cannot be established from the supplied evidence alone.

This mapping is a working hypothesis, not confirmation of a specific attack technique.

## 8. Conclusion

The simulated evidence shows 82 failed authentication attempts against four user accounts from a common source IP during a short period.

This behaviour is suspicious and consistent with possible password spraying or brute-force activity. Additional log correlation is required to determine whether any authentication succeeded and whether an account was compromised.

**Recommended disposition:** Continue investigation and escalate according to the SOC playbook if corroborating evidence is found.

## 9. Limitations

This case is based on simulated training data. The full raw authentication logs, authentication protocol, target system details and successful-login results were not provided for this initial scenario.

All conclusions are limited to the available evidence.

---

*This report is part of an educational SOC Analyst L1 portfolio. No real system was investigated or accessed.*

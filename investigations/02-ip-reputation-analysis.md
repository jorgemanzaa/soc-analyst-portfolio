# SOC Investigation 002 — IP Reputation Analysis

## 1. Overview

- **Case ID:** SOC-2026-002
- **Investigation type:** Indicator of Compromise (IOC) enrichment
- **Role:** SOC Analyst L1 — training exercise
- **Status:** Investigation documented; escalation recommended
- **Environment:** Simulated security investigation

## 2. Objective

Investigate the reputation of the source IP address observed in the previous authentication alert and assess whether external threat intelligence supports further investigation.

## 3. Indicator Under Investigation

- **IP address:** `185.220.101.45`
- **Sources consulted:** VirusTotal and AbuseIPDB

## 4. VirusTotal Findings

The results recorded during the exercise included:

- **Country:** Germany
- **ASN:** 60729
- **Recorded detections:** 16
- **Associated domain reported:** `feralhosting.com`
- **Additional observation:** A phishing-related classification was recorded in the notes.

These findings provide context for assessing the IP address. The exact meaning of each result should be verified against the source report and the date of consultation.

## 5. AbuseIPDB Findings

The results recorded during the exercise included:

- **Abuse Confidence Score:** 100%
- **Total reports:** 6,897
- **Last reported:** Approximately one hour before the lookup, according to the notes
- **Country:** Germany
- **Reported usage type:** University/College/School
- **Reported categories:** Web application attack, hacking, bad web bot, SSH, brute force and DDoS.

These are historical lookup results from the exercise, not verified current values.

## 6. Analysis

The recorded reputation results indicate that the IP address had a highly suspicious reputation at the time of the exercise.

When correlated with the previous simulated alert — 82 failed authentication attempts against four accounts from the same IP — the findings increase concern about possible password spraying or brute-force activity.

However, IP reputation alone does not establish that the specific authentication attempts were malicious. Additional evidence is required to confirm the nature and impact of the activity.

## 7. Recommended SOC L1 Actions

1. Record the sources consulted, lookup date and relevant findings.
2. Correlate the IP address with authentication logs and other SIEM alerts.
3. Check for successful logins, other affected accounts and related hosts.
4. Preserve the evidence and document the working hypothesis.
5. Escalate to SOC L2 when supported by the investigation and the applicable playbook.
6. Recommend restricting the source IP if appropriate under the organisation's response procedures.

## 8. MITRE ATT&CK Context

**Potential technique to investigate:** T1110 — Brute Force.

This is a hypothesis based on the authentication pattern in the related exercise. IP reputation data by itself does not establish that this technique occurred.

## 9. Conclusion

The external intelligence results recorded in this exercise indicate a suspicious IP reputation. Combined with repeated authentication failures across multiple accounts, they support further investigation of possible password spraying or brute-force activity.

**Assessment:** High suspicion; the activity should be correlated with internal logs before drawing a definitive conclusion.

## 10. Limitations

- The investigation uses training notes rather than preserved original intelligence reports.
- The lookup date and original report details were not retained as evidence in this case.
- Reputation scores and classifications can change over time.
- No single external reputation result proves that a particular event was malicious.

---

*This report is part of an educational SOC Analyst L1 portfolio. The investigation is based on simulated training notes and does not represent a confirmed real-world incident.*


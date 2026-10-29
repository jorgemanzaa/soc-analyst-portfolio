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
- **

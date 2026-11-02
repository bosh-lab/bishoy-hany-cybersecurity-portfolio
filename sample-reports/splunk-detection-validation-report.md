# Splunk SIEM Detection Validation — Portfolio Lab Report

> **Report type:** Controlled home-lab validation  
> **Environment:** Personal Splunk SIEM lab  
> **Purpose:** Demonstrate defensive detection engineering and technical reporting  
> **Important:** This is a portfolio exercise using simulated activity. It is not a report of a real client incident or a production security assessment.

## 1. Executive Summary

A home-lab SIEM was built with Splunk Enterprise to collect Windows Security/System/Application events, Sysmon telemetry, Linux syslog, and Apache access logs. Six scheduled detection alerts were developed, mapped to MITRE ATT&CK techniques, and validated by generating the corresponding activity inside the lab.

The project also includes a SOC-style dashboard for reviewing authentication activity, suspicious PowerShell execution, account/privilege changes, web attack indicators, and log-source activity.

## 2. Scope and Data Sources

The validation covered only the documented personal lab:

- Windows Security, System, and Application event logs.
- Sysmon operational events.
- Linux syslog.
- Apache access and error logs.
- Splunk saved searches, scheduled alerts, and Dashboard Studio panels.

No client environment, third-party production system, or real user account was tested.

## 3. Detection Coverage

| # | Detection | ATT&CK mapping | Lab validation activity |
| --- | --- | --- | --- |
| 1 | Multiple Failed Logins | T1110 — Brute Force | Generated repeated incorrect Windows logon attempts. |
| 2 | Brute Force Success | T1110 — Brute Force | Generated failed logons followed by a successful logon. |
| 3 | Suspicious PowerShell | T1059.001 — PowerShell | Executed a controlled encoded PowerShell command in the lab. |
| 4 | Privilege Escalation / Account Changes | T1136.001, T1098 | Created a test user and added it to a local administrators group. |
| 5 | Web Attack (SQLi / Traversal) | T1190 — Exploit Public-Facing Application | Sent test SQL injection and directory-traversal request patterns to the lab Apache service. |
| 6 | Web Scanner Spike | T1595 — Active Scanning | Generated repeated HTTP 404 requests from a lab client. |

The exact SPL searches are available in the project's `detections/` directory. Alert schedules and search windows are documented in the main project README.

## 4. Dashboard Deliverable

The **SIEM Security Monitoring Overview** Dashboard Studio dashboard includes:

- Alert-firing and failed-logon summary panels.
- Authentication activity over time.
- Top 404 scanner activity.
- Suspicious PowerShell execution details.
- Account and privilege-change activity.
- Web attack payload observations.
- Event volume by source/sourcetype.

Dashboard JSON exports are available in the project's `dashboard/` directory, with screenshots in `screenshots/`.

## 5. Tuning and Validation Notes

The lab validation identified several practical tuning considerations:

- Event ID 4672 was removed from the privilege-related detection because routine SYSTEM activity caused excessive noise.
- The brute-force-success correlation can also match a normal typo followed by a correct login. A production implementation should consider stricter thresholds and logon-type/context filters.
- The alert schedule runs every five minutes over a fifteen-minute search window. As a result, the same event may contribute to more than one alert firing unless throttling or schedule/window alignment is configured.
- Sysmon XML fields were not automatically extracted in the initial setup; the searches use `rex` field extraction.

## 6. Findings and Limitations

**Result:** All six detection scenarios were exercised through controlled simulations in the personal lab, and the corresponding alert searches and dashboard panels were documented.

This result demonstrates lab functionality only. It does not establish detection accuracy against real-world attacks, coverage of every attack technique, or readiness for production deployment.

Other limitations:

- The test environment is small and does not represent a full enterprise network.
- Detection thresholds have not been tuned against representative production noise.
- Active Directory telemetry was outside the project scope.
- Linux SSH brute-force detection was not included in this version.
- No external threat-intelligence enrichment or automated response was implemented.

## 7. Recommendations for a Production Engagement

A real client engagement would require a separate discovery and authorization process. Depending on the agreed scope, next steps could include:

1. Confirm log sources, retention, access permissions, and data sensitivity.
2. Review field extraction, timestamps, sourcetypes, and index routing.
3. Establish baseline event volume and normal administrative activity.
4. Tune alert thresholds using client-approved historical data.
5. Define severity, ownership, escalation paths, and notification requirements.
6. Validate detections in an approved test window and document false positives.
7. Provide handover notes and a list of residual coverage gaps.

No production changes should be made without explicit approval and a rollback plan.

## 8. Related Project Files

- [Main Splunk SIEM Detection Lab](../splunk-siem-detection-lab/README.md)
- [Detection searches](../splunk-siem-detection-lab/detections/)
- [Dashboard exports](../splunk-siem-detection-lab/dashboard/)
- [USB Registry Investigation Report](../USB-Registry-Investigation/report/investigation-report.md)

## 9. Author

**Bishoy Hany**  
Cybersecurity SOC Analyst Trainee | Splunk SIEM | Digital Forensics

- [GitHub portfolio](https://github.com/bosh-lab/bishoy-hany-cybersecurity-portfolio)
- [LinkedIn](https://www.linkedin.com/in/bishoy-hany-519baa373/)

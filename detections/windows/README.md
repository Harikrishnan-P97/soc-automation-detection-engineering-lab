# Windows Event Log Detections

This directory contains detections developed using Windows Security Event Logs collected from the monitored Windows endpoint within the SOC Automation & Detection Engineering Lab.

Windows Event Logs provide visibility into authentication activity, account management operations, system events, and user behavior. These events are commonly used by Security Operations Centers (SOCs) to identify unauthorized access attempts, account misuse, and suspicious authentication activity.

---

## Telemetry Source

**Log Source:** Windows Security Event Log

**Collection Method:**

* Windows Security Logs
* Splunk Universal Forwarder
* Splunk Enterprise

---

## Detection Coverage

| Detection             | Event ID | MITRE ATT&CK           |
| --------------------- | -------- | ---------------------- |
| Failed User Login     | 4625     | T1110 - Brute Force    |
| Successful User Login | 4624     | T1078 - Valid Accounts |

---

## Why These Detections Matter

Authentication activity is often one of the earliest indicators of malicious behavior within an environment.

Monitoring successful and failed logon events can help identify:

* Password guessing attacks
* Brute-force attempts
* Unauthorized remote access
* Credential misuse
* Suspicious account activity
* Initial access attempts

These detections were integrated into the SOC automation pipeline and can be investigated through Grafana dashboards and analyst workflows.

---

## Log Collection Workflow

```text
Windows Endpoint
      ↓
Security Event Logs
      ↓
Splunk Universal Forwarder
      ↓
Splunk Enterprise
      ↓
Detection Rules
      ↓
n8n Alert Pipeline
      ↓
Grafana SOC Dashboard
```

---

## Validation

All detections were validated using controlled authentication activity within the lab environment, including both successful and failed interactive and Remote Desktop Protocol (RDP) logon events.

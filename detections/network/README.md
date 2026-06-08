# Network Detections

This directory contains detections focused on identifying suspicious authentication activity and potentially malicious network communications within the SOC Automation & Detection Engineering Lab.

These detections leverage Windows authentication telemetry and Sysmon network connection events to identify behaviors commonly associated with credential attacks, command-and-control (C2) activity, and unauthorized access attempts.

---

## Detection Coverage

| Detection                                  | Data Source                 | MITRE ATT&CK                       |
| ------------------------------------------ | --------------------------- | ---------------------------------- |
| Possible Brute Force Attack                | Windows Security Event Logs | T1110 - Brute Force                |
| Network Connection from Suspicious Process | Sysmon Event ID 3           | T1071 - Application Layer Protocol |

---

## Telemetry Sources

### Windows Security Event Logs

Used to identify repeated authentication failures that may indicate password spraying or brute-force attacks.

Relevant Event IDs:

* 4625 – Failed Login

### Sysmon Network Connection Events

Used to identify network communications initiated by suspicious processes.

Relevant Event IDs:

* Sysmon Event ID 3 – Network Connection

---

## Why These Detections Matter

Network-based detections provide visibility into attacker activity after initial access.

These detections help identify:

* Brute-force attacks
* Password guessing activity
* Unauthorized access attempts
* Suspicious outbound communications
* Potential command-and-control traffic
* Post-compromise activity

---

## Investigation Workflow

```text
Attack Activity
      ↓
Windows / Sysmon Telemetry
      ↓
Splunk Detection Rule
      ↓
Alert Generation
      ↓
n8n Automation Pipeline
      ↓
Grafana SOC Dashboard
      ↓
Analyst Investigation
```

---

## Validation

All detections were validated using controlled attack simulations performed within the SOC lab environment.

Validation scenarios included:

* Multiple failed login attempts
* Remote Desktop authentication failures
* Suspicious PowerShell network connections
* External network communications from administrative tools
* Simulated command-and-control style traffic

# Sysmon Detection Rules

This directory contains endpoint detection rules built using Microsoft Sysmon telemetry and Splunk SPL.

The detections focus on identifying attacker behavior after initial access, including credential theft, PowerShell abuse, reconnaissance activity, suspicious process relationships, and potential data exfiltration.

These detections were developed and tested within the SOC Automation & Detection Engineering Lab using:

- Sysmon
- Splunk Enterprise
- Windows 10 Endpoint
- Custom SPL Detection Rules

---

## Detection Coverage

### Credential Access

- Credential Dumping Detection

MITRE ATT&CK:
- T1003 – OS Credential Dumping

---

### Execution

- Suspicious PowerShell Detection

MITRE ATT&CK:
- T1059.001 – PowerShell

---

### Defense Evasion / Execution

- Suspicious Parent-Child Process Detection

MITRE ATT&CK:
- T1055
- T1204

---

### Discovery

- Post-Exploitation Reconnaissance Detection

MITRE ATT&CK:
- T1087 – Account Discovery
- T1016 – System Network Configuration Discovery
- T1082 – System Information Discovery

---

### Exfiltration

- Data Exfiltration Detection

MITRE ATT&CK:
- T1041 – Exfiltration Over C2 Channel

---

## Data Source

Microsoft Sysmon Operational Logs

Event IDs commonly used:

- Event ID 1 – Process Creation
- Event ID 3 – Network Connection
- Event ID 11 – File Creation

---

## Lab Validation

All detections were validated in the SOC lab environment using simulated attacker activity and corresponding Splunk alerts.
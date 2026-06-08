# Incident Response Workflow

## Overview

The SOC lab simulates a complete alert investigation and response lifecycle by integrating detection, enrichment, analyst actions, and automated response workflows.

Alerts generated from Splunk detections are processed through n8n SOAR workflows, enriched with threat intelligence, visualized in Grafana dashboards, and optionally trigger automated response actions such as host isolation.

This workflow demonstrates how security teams handle alerts from initial detection through final resolution.

---

## Response Lifecycle

```text
Detection
    ↓
Alert Intake
    ↓
Alert Enrichment
    ↓
SOC Queue
    ↓
Analyst Investigation
    ↓
Response Actions
    ↓
Alert Closure
    ↓
Reporting & Metrics
```

---

## Phase 1 – Detection

Security events are collected from multiple telemetry sources:

* Windows Event Logs
* Sysmon
* Suricata IDS
* ModSecurity WAF
* pfSense Firewall
* Web Application Logs

Splunk correlation searches continuously analyze incoming telemetry and generate alerts for suspicious activity.

### Example Alerts

* Credential Dumping
* Suspicious PowerShell
* Failed Login Attempts
* Brute Force Detection
* SQL Injection
* XSS Attempts
* Command Injection
* Data Exfiltration

---

## Phase 2 – Alert Intake

When a detection rule triggers:

1. Splunk sends alert data to n8n via webhook.
2. Alert fields are normalized.
3. Alert metadata is generated.
4. Unique SOC Alert IDs are assigned.
5. Alerts are stored in SOC tracking tables.

### Key Workflow

**SOC - Alert Intake**

### Generated Fields

* alert_id
* severity
* risk_score
* status
* assigned_analyst
* created_time
* source
* mitre_tactic
* mitre_technique

---

## Phase 3 – Alert Enrichment

New alerts are automatically enriched with additional threat intelligence.

### VirusTotal Enrichment

The enrichment workflow retrieves:

* File reputation
* Hash intelligence
* Detection counts
* Community verdicts

### Benefits

* Reduces analyst workload
* Provides additional context
* Improves investigation speed

### Workflow

**SOC - VirusTotal Enrichment API**

---

## Phase 4 – Alert Queue

Processed alerts are sent to Grafana dashboards where analysts can review active incidents.

### Dashboard Capabilities

* Alert prioritization
* Severity filtering
* Risk score filtering
* Alert searching
* Investigation workflows

### Dashboard

**SOC Alert Dashboard**

---

## Phase 5 – Investigation

Analysts open alerts for detailed investigation.

The investigation dashboard provides:

### Alert Overview

* Alert details
* Severity
* Risk score
* Detection source

### Asset Context

* Host information
* User information
* IP addresses

### Threat Context

* MITRE ATT&CK mapping
* VirusTotal intelligence
* Related indicators

### Investigation Timeline

* Analyst notes
* Status changes
* Escalations
* Response actions

### Dashboard

**SOC Alert Investigation Dashboard**

---

## Phase 6 – Response Actions

Analysts can execute response actions directly from Grafana.

### Available Actions

* Investigate
* Escalate
* Mark False Positive
* Close Alert
* Isolate Host
* Unisolate Host

Actions are processed through:

**SOC - Alert Action API**

---

## Host Isolation Workflow

For high-severity endpoint alerts:

1. Analyst selects **Isolate Host**.
2. Grafana sends request to n8n.
3. n8n calls the LimaCharlie API.
4. Host is isolated.
5. Timeline is updated.
6. Slack notification is generated.

### Workflow

**SOC - Host Isolation Action**

### Benefits

* Rapid containment
* Reduced attacker movement
* Automated response execution

---

## Phase 7 – Notification and Escalation

Critical alerts automatically generate notifications.

### Notification Channels

* Slack

### Included Information

* Alert ID
* Severity
* Host
* User
* Alert Name
* Risk Score

This allows analysts to respond quickly to critical incidents.

---

## Phase 8 – Alert Closure

Once investigation is complete:

### Possible Outcomes

* True Positive
* False Positive
* Escalated
* Resolved

The final status is recorded in SOC tracking tables.

Timeline entries are preserved for future review.

---

## Phase 9 – Reporting and Metrics

The platform continuously tracks operational metrics.

### Metrics Collected

* Total Alerts
* Open Alerts
* Escalated Alerts
* Resolved Alerts
* Time To Resolve (TTR)
* Escalation Delay
* Analyst Activity

### Reporting Workflow

**SOC - Daily Summary Bot**

---

## Workflow Components

| Component   | Purpose                            |
| ----------- | ---------------------------------- |
| Splunk      | Detection and alert generation     |
| n8n         | Alert orchestration and automation |
| VirusTotal  | Threat intelligence enrichment     |
| Grafana     | Investigation dashboards           |
| LimaCharlie | Endpoint response actions          |
| Slack       | Alert notifications                |
| Data Tables | Alert lifecycle storage            |

---

## End-to-End Example

### Credential Dumping Scenario

1. Sysmon logs Mimikatz execution.
2. Splunk detection triggers.
3. Alert is sent to n8n.
4. Alert receives a unique SOC ID.
5. VirusTotal enrichment is performed.
6. Alert appears in Grafana.
7. Analyst investigates the alert.
8. Host isolation is executed through LimaCharlie.
9. Slack notification is sent.
10. Alert is resolved and closed.

This workflow demonstrates how detection, investigation, enrichment, and response are integrated into a complete SOC process.

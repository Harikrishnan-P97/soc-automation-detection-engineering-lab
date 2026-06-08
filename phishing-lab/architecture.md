# Phishing Lab Architecture

## Overview

This document describes the architecture of the phishing simulation environment used within the SOC Automation and Detection Engineering Lab.

The environment was designed to emulate a realistic phishing attack lifecycle while generating telemetry that can be collected, analyzed, detected, investigated, and responded to through a centralized SOC workflow.

The lab combines phishing infrastructure, endpoint monitoring, SIEM detection engineering, workflow automation, and incident response capabilities to provide end-to-end visibility across the attack chain.

---

## Objectives

The architecture was built to achieve the following goals:

* Simulate realistic phishing campaigns
* Generate endpoint and network telemetry
* Validate custom detection engineering content
* Test alert ingestion and enrichment workflows
* Support analyst investigation activities
* Automate response actions
* Map attacker behavior to MITRE ATT&CK techniques
* Create repeatable attack scenarios for SOC testing

---

## Lab Components

### Attacker System

The attacker infrastructure is hosted on an Ubuntu virtual machine.

This system is responsible for:

* Hosting phishing infrastructure
* Managing phishing campaigns
* Delivering phishing emails
* Operating command-and-control services
* Receiving exfiltrated data

Primary tools include:

* Gophish
* Sliver C2
* Netcat
* Python HTTP services

---

### Victim System

The victim endpoint is a Windows 11 virtual machine configured to emulate a corporate workstation.

The system contains:

* Thunderbird Mail Client
* Sysmon
* Splunk Universal Forwarder
* LimaCharlie EDR Sensor

The victim system serves as the target of phishing campaigns and generates telemetry throughout the attack lifecycle.

---

### Email Delivery Layer

Email delivery is performed through Gophish.

The phishing platform is responsible for:

* Creating phishing campaigns
* Sending phishing emails
* Tracking email delivery
* Recording user interactions
* Monitoring payload downloads

This layer simulates the delivery phase of the Cyber Kill Chain.

---

### Command and Control Layer

Sliver is used as the command-and-control framework.

After payload execution, Sliver provides:

* Remote command execution
* Session management
* File transfer capabilities
* Post-exploitation operations
* Data collection activities

This layer simulates adversary access after successful compromise.

---

### Endpoint Telemetry Layer

Sysmon generates detailed endpoint visibility for:

* Process creation
* Network connections
* File operations
* Parent-child process relationships
* Command-line activity

This telemetry forms the foundation for detection engineering within the lab.

---

### Log Collection Layer

Splunk Universal Forwarder collects endpoint telemetry and forwards it to Splunk.

Collected data includes:

* Windows Event Logs
* Sysmon Events
* Authentication Events
* Process Execution Events
* Network Connection Events

This layer centralizes telemetry for analysis and alert generation.

---

### Detection Layer

Splunk Enterprise hosts the detection engineering platform.

Custom detections are used to identify:

* Credential dumping
* Suspicious PowerShell execution
* Parent-child process anomalies
* Reconnaissance activity
* Data exfiltration activity
* Authentication abuse
* Brute-force attempts

Detection outputs are normalized into a common alert structure for downstream automation.

---

### Automation Layer

n8n serves as the SOAR and workflow automation platform.

The automation layer performs:

* Alert ingestion
* Alert normalization
* Alert enrichment
* Timeline generation
* Alert state management
* Analyst action processing

This enables automated handling of security events throughout the investigation lifecycle.

---

### Investigation Layer

Grafana provides the analyst-facing investigation interface.

Custom dashboards support:

* Alert triage
* Alert queue monitoring
* Investigation workflows
* Alert timelines
* Asset context
* Threat context
* Analyst activity tracking

This layer simulates a SOC analyst investigation workflow.

---

### Response Layer

LimaCharlie provides endpoint response capabilities.

Response actions include:

* Host isolation
* Host unisolation
* Endpoint containment

Response actions can be initiated directly from investigation workflows.

---

### Notification Layer

Slack is used for operational alerting.

Critical alerts are forwarded automatically to Slack to provide:

* Rapid notification
* Alert visibility
* Incident awareness
* SOC workflow integration

---

## Data Flow

The overall telemetry flow within the environment follows this sequence:

1. Phishing email is delivered to the victim.
2. User interacts with the phishing content.
3. Payload execution occurs on the endpoint.
4. Sysmon generates telemetry.
5. Splunk Universal Forwarder collects events.
6. Events are forwarded to Splunk.
7. Detection rules generate alerts.
8. Alerts are sent to n8n.
9. n8n enriches and processes alerts.
10. Grafana dashboards display investigation data.
11. Critical alerts trigger Slack notifications.
12. Analysts perform response actions through LimaCharlie.

---

## Security Monitoring Coverage

The architecture provides visibility across multiple phases of the attack lifecycle:

| Phase               | Visibility Source     |
| ------------------- | --------------------- |
| Delivery            | Gophish               |
| Initial Access      | Windows Events        |
| Execution           | Sysmon                |
| Discovery           | Sysmon                |
| Credential Access   | Sysmon                |
| Command and Control | Sysmon Network Events |
| Exfiltration        | Sysmon + Splunk       |
| Detection           | Splunk                |
| Investigation       | Grafana               |
| Response            | LimaCharlie           |

---

## Summary

This phishing lab architecture was designed to simulate a complete attack lifecycle while providing comprehensive telemetry, detection, investigation, automation, and response capabilities. The environment serves as a practical platform for validating detection engineering concepts, SOC workflows, and incident response processes within a controlled lab environment.

# Lab Overview

## Introduction

This project is a Security Operations Center (SOC) Automation and Detection Engineering Lab designed to simulate the technologies, workflows, and processes commonly found in modern security operations environments.

The lab combines attack simulation, telemetry collection, detection engineering, threat intelligence enrichment, alert management, dashboard visualization, and automated incident response into a single integrated platform.

Rather than focusing on a single tool, the objective of the lab is to understand how security telemetry flows through an environment, how attacks are detected, and how analysts investigate and respond to security incidents.

---

## Project Objectives

The primary goals of the lab are:

* Build a realistic SOC environment using open-source and community editions of security tools.
* Generate meaningful security telemetry through attack simulation.
* Develop custom detection rules using Splunk SPL.
* Map detections to the MITRE ATT&CK framework.
* Create automated alert enrichment and response workflows.
* Visualize security operations through Grafana dashboards.
* Simulate analyst investigation and incident response processes.
* Gain practical experience across the detection and response lifecycle.

---

## Lab Architecture

The environment consists of multiple integrated security platforms that collectively simulate a modern SOC.

### Infrastructure Layer

* VirtualBox
* pfSense Firewall
* Ubuntu Attack Server
* Windows 11 Victim Endpoint
* DVWA (Damn Vulnerable Web Application)

### Telemetry Collection Layer

* Windows Event Logs
* Sysmon
* Sysmon-ng
* Splunk Universal Forwarder

### Security Monitoring Layer

* Splunk Enterprise
* Suricata IDS
* ModSecurity WAF
* OWASP Core Rule Set (CRS)

### Detection Engineering Layer

* Custom Splunk Detection Rules
* MITRE ATT&CK Mapping
* Risk-Based Alerting

### Automation Layer

* n8n Workflow Automation
* VirusTotal Threat Intelligence Enrichment
* Alert Lifecycle Management
* Investigation Timeline Tracking
* Host Isolation Workflows

### Visualization Layer

* Grafana Dashboards
* Alert Investigation Dashboard
* Analyst Activity Monitoring

### Response Layer

* LimaCharlie EDR
* Slack Notifications
* Automated Host Isolation

### Attack Simulation Layer

* Gophish
* Sliver C2 Framework
* Phishing Campaign Infrastructure

---

## Security Telemetry Sources

The lab collects and analyzes telemetry from multiple sources.

| Source             | Description                                        |
| ------------------ | -------------------------------------------------- |
| Windows Event Logs | Authentication and operating system events         |
| Sysmon             | Process, network, registry, and endpoint telemetry |
| Sysmon-ng          | Extended event collection and forwarding           |
| ModSecurity        | Web application firewall alerts                    |
| OWASP CRS          | Attack detection rules for common web attacks      |
| Suricata           | Network intrusion detection events                 |
| pfSense            | Firewall and network security logs                 |
| LimaCharlie        | Endpoint detection and response telemetry          |
| Splunk             | Centralized log collection and analytics           |

---

## Detection Engineering

The lab includes custom detections covering endpoint, authentication, network, and web application attack scenarios.

### Windows Authentication Detections

* Failed User Login
* Successful User Login
* Brute Force Detection

### Sysmon Detections

* Credential Dumping Tool Execution
* Suspicious PowerShell Activity
* Suspicious Parent-Child Process Relationships
* Post Exploitation Reconnaissance
* Data Exfiltration Activity
* Suspicious Network Connections

### Web Application Detections

* SQL Injection
* Cross-Site Scripting (XSS)
* Command Injection

### Network Detections

* Authentication Brute Force Activity
* Suspicious Outbound Connections

Each detection includes MITRE ATT&CK mappings, severity ratings, risk scores, and alert enrichment fields to support analyst investigations.

---

## SOC Automation

n8n serves as the automation and orchestration platform within the lab.

Implemented workflows include:

* SOC ID Generation
* Alert Intake Processing
* VirusTotal Enrichment
* Alert Dashboard APIs
* Investigation Timeline APIs
* Analyst Activity Tracking
* Alert Action Processing
* Daily Summary Reporting
* Host Isolation Actions

These workflows simulate SOAR-style operations by automating repetitive tasks and improving analyst efficiency.

---

## Investigation Workflow

Alerts generated within Splunk are processed through automation workflows and presented to analysts through Grafana dashboards.

The investigation lifecycle includes:

1. Alert Generation
2. Alert Normalization
3. Threat Intelligence Enrichment
4. Analyst Investigation
5. Timeline Documentation
6. Escalation or Closure
7. Incident Response Actions
8. Reporting and Metrics Collection

This process mirrors common workflows used by SOC analysts in production environments.

---

## Incident Response Capabilities

The lab includes response workflows that allow analysts to simulate containment actions.

Examples include:

* Host Isolation
* Alert Escalation
* False Positive Classification
* Investigation Tracking
* Critical Alert Notifications

Response actions are executed through LimaCharlie and integrated into the analyst workflow through n8n and Grafana.

---

## Phishing Simulation Environment

A dedicated phishing simulation environment was developed to generate realistic attack telemetry and validate detections.

The environment includes:

### Attacker Infrastructure

* Ubuntu Attack Server
* Gophish
* Sliver C2

### Victim Infrastructure

* Windows 11
* Thunderbird Mail Client
* Sysmon
* Splunk Universal Forwarder
* LimaCharlie Sensor

The phishing lab enables simulation of:

* Phishing Email Delivery
* Initial Access
* Command Execution
* Post-Exploitation Activity
* Data Exfiltration
* Detection Validation
* Incident Response Workflows

---

## Repository Structure

- [architecture/](architecture/)
- [dashboards/](dashboards/)
- [detections/](detections/)
- [docs/](docs/)
- [phishing-lab/](phishing-lab/)
- [screenshots/](screenshots/)
- [workflows/](workflows/)

| Folder       | Description                                 |
| ------------ | ------------------------------------------- |
| architecture | Architecture and workflow diagrams          |
| dashboards   | Grafana dashboard exports and documentation |
| detections   | Detection engineering documentation         |
| docs         | Supporting project documentation            |
| phishing-lab | Phishing simulation documentation           |
| screenshots  | Validation evidence and screenshots         |
| workflows    | n8n workflow exports and documentation      |

---

## Technologies Used

### Security Monitoring

* Splunk Enterprise
* Sysmon
* Sysmon-ng
* Suricata
* ModSecurity
* OWASP CRS

### Detection Engineering

* Splunk SPL
* MITRE ATT&CK

### Automation

* n8n
* APIs
* Webhooks

### Visualization

* Grafana

### Threat Intelligence

* VirusTotal

### Response

* LimaCharlie
* Slack

### Offensive Security

* Gophish
* Sliver
* DVWA

### Infrastructure

* VirtualBox
* Ubuntu
* Windows 11
* pfSense

---

## Conclusion

This SOC Automation and Detection Engineering Lab provides a practical environment for understanding how modern security operations function end-to-end. By combining attack simulation, telemetry collection, detection engineering, automation, investigation workflows, and incident response capabilities, the lab serves as a platform for developing hands-on experience across both blue-team and purple-team security disciplines.

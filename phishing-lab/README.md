# Phishing Attack Simulation Lab

## Overview

This project simulates a complete phishing attack lifecycle within a controlled SOC lab environment, demonstrating how phishing activity can be delivered, detected, investigated, and responded to using a combination of endpoint telemetry, security monitoring, automation workflows, and EDR response actions.

The lab was built to move beyond theoretical concepts and provide hands-on experience with attack simulation, detection engineering, incident investigation, and SOC automation. Every stage of the attack generates telemetry that is collected, analyzed, enriched, and presented through custom dashboards and workflows.

The environment combines offensive tooling, defensive monitoring, automation, and response capabilities into a single end-to-end attack simulation platform.

---

## Objectives

The primary objectives of this lab are:

* Simulate a realistic phishing campaign
* Generate endpoint and network telemetry
* Develop and validate custom detection rules
* Correlate security events into actionable alerts
* Automate alert enrichment and management
* Investigate alerts through SOC dashboards
* Demonstrate automated response capabilities
* Map attacker activity to MITRE ATT&CK techniques
* Create a repeatable environment for future detection testing

---

## Lab Architecture

The phishing simulation is integrated into a larger SOC automation and detection engineering environment.

### Attacker Infrastructure

The attacker environment consists of an Ubuntu-based attack server hosting:

* Gophish
* Sliver Command & Control (C2)
* Phishing landing pages
* Payload hosting infrastructure

The attacker system is responsible for campaign creation, payload delivery, command execution, and simulated post-exploitation activity.

### Victim Endpoint

The victim workstation is a Windows 11 system configured with:

* Sysmon
* Splunk Universal Forwarder
* Thunderbird Mail Client
* LimaCharlie EDR Sensor

The endpoint serves as the target of the phishing campaign and generates the telemetry used throughout the detection and investigation workflows.

### Security Monitoring Stack

Security telemetry is processed through:

* Splunk Enterprise
* Grafana
* n8n
* Slack
* LimaCharlie EDR

Together these components provide log collection, alerting, enrichment, investigation workflows, dashboarding, and response automation.

### Network Infrastructure

The environment is hosted in VirtualBox and includes:

* pfSense Firewall
* Ubuntu Attack Server
* Windows 11 Victim Endpoint
* Security Monitoring Infrastructure

---

## Attack Scenario

The simulation follows a complete phishing attack chain from delivery to detection.

### Phase 1 — Phishing Campaign Creation

A phishing campaign is created using Gophish.

The campaign includes:

* Target user information
* Email template
* Landing page
* Malicious ZIP payload

Campaign activity is monitored through the Gophish dashboard.

---

### Phase 2 — Email Delivery

The phishing email is delivered to the victim mailbox.

The victim accesses the email through Thunderbird and interacts with the phishing content.

This stage simulates a realistic phishing delivery mechanism commonly observed in enterprise environments.

---

### Phase 3 — User Interaction

The victim:

1. Opens the email
2. Clicks the phishing link
3. Downloads the malicious archive
4. Extracts the ZIP contents
5. Executes the payload

Successful execution provides the attacker with initial access to the endpoint.

---

### Phase 4 — Command and Control

After execution, the payload establishes communication with the Sliver C2 server.

Telemetry generated during this phase includes:

* Process creation events
* Parent-child process relationships
* Network connections
* Command execution activity

Sysmon captures these events and forwards them to Splunk for analysis.

---

### Phase 5 — Post-Exploitation Activity

Following successful access, multiple reconnaissance activities are executed.

Examples include:

* whoami
* hostname
* ipconfig
* tasklist
* systeminfo
* net user

These activities generate endpoint telemetry commonly associated with attacker discovery behavior.

---

### Phase 6 — Data Exfiltration Simulation

Data exfiltration is simulated using command-line utilities and outbound network connections.

Detection logic monitors:

* Suspicious transfer tools
* Command execution patterns
* Outbound network activity
* File transfer behavior

Relevant alerts are generated and forwarded into the SOC workflow pipeline.

---

## Detection Coverage

The phishing simulation generates telemetry that triggers multiple custom detections.

### Windows Authentication

* Failed User Login
* Successful User Login

### Endpoint Detection (Sysmon)

* Credential Dumping Tool Execution
* Suspicious PowerShell Flags
* Suspicious Parent-Child Processes
* Post-Exploitation Reconnaissance Activity
* Data Exfiltration Activity

### Network Detection

* Possible Brute Force Attack
* Suspicious Network Connections

### Web Application Detection

* SQL Injection Detection
* Cross-Site Scripting (XSS) Detection
* Command Injection Detection

### Web Application Firewall

* OWASP Core Rule Set (CRS)
* ModSecurity Audit Events
* Attack Prevention and Request Blocking

---

## Investigation Workflow

Alerts generated by Splunk are automatically processed through custom n8n workflows.

The workflow performs:

* Alert ingestion
* Alert normalization
* Alert enrichment
* Alert correlation
* Timeline generation
* Dashboard population

Alert data is then presented through Grafana dashboards designed to support SOC investigations.

Investigation capabilities include:

* Alert triage
* Asset context review
* Threat context review
* Timeline analysis
* Analyst note tracking
* Escalation workflows

---

## Automated Response

The lab includes automated response actions integrated with LimaCharlie EDR.

Available actions include:

* Investigate
* Escalate
* Close Alert
* Mark False Positive
* Host Isolation
* Host Unisolation

Response actions can be executed directly from the SOC workflow pipeline and validated through LimaCharlie.

---

## MITRE ATT&CK Coverage

The phishing scenario generates activity across multiple ATT&CK tactics.

### Initial Access

* T1078 – Valid Accounts
* T1190 – Exploit Public-Facing Application

### Execution

* T1059 – Command and Scripting Interpreter
* T1059.001 – PowerShell

### Discovery

* T1082 – System Information Discovery

### Credential Access

* T1003 – OS Credential Dumping
* T1110 – Brute Force

### Command and Control

* T1071 – Application Layer Protocol

### Exfiltration

* T1041 – Exfiltration Over C2 Channel

---

## Skills Demonstrated

This project demonstrates practical experience with:

* Detection Engineering
* Security Monitoring
* SOC Operations
* Threat Detection
* Incident Investigation
* SIEM Engineering
* EDR Operations
* Security Automation
* SOAR Concepts
* Log Analysis
* Dashboard Development
* Threat Hunting
* MITRE ATT&CK Mapping
* Phishing Analysis
* Incident Response

---

## Key Takeaways

This lab demonstrates how phishing attacks can be monitored throughout the entire attack lifecycle, from initial email delivery to post-exploitation activity and response actions.

Rather than focusing solely on attack simulation, the project emphasizes the defensive side of cybersecurity by showcasing how telemetry is collected, transformed into detections, enriched through automation, investigated through dashboards, and acted upon through automated response workflows.

The environment also serves as a repeatable platform for future detection engineering, threat hunting, SOC automation, and incident response experiments.

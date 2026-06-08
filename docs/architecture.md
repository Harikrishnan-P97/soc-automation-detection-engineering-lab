# Architecture

## Overview

The SOC Automation and Detection Engineering Lab is built as a multi-layered environment designed to simulate the core functions of a modern Security Operations Center (SOC).

The architecture combines attack simulation, telemetry collection, centralized monitoring, detection engineering, automation, dashboard visualization, and incident response into a single integrated platform.

The design emphasizes visibility across the entire attack lifecycle while providing opportunities to develop detection engineering, investigation, and automation workflows.

---

## Architectural Goals

The environment was designed with the following objectives:

* Generate realistic attack telemetry.
* Centralize log collection and analysis.
* Build custom detections across multiple data sources.
* Automate repetitive SOC tasks.
* Support analyst investigations.
* Simulate incident response actions.
* Validate detections through attack simulations.
* Create an end-to-end SOC workflow.

---

## Infrastructure Layer

The infrastructure layer provides the foundation for all systems within the lab.

### Virtualization Platform

VirtualBox is used to host the lab environment and provide isolation between systems.

### Network Segmentation

pfSense serves as the central firewall and routing platform.

Responsibilities include:

* Network segmentation
* Traffic routing
* Firewall policy enforcement
* Network visibility
* Log generation

---

## Attack Simulation Layer

The attack simulation layer generates realistic security events that can be detected and investigated.

### Ubuntu Attack Server

The attacker system hosts offensive security tooling used to simulate adversary activity.

Capabilities include:

* Phishing campaign delivery
* Command and control operations
* Post-exploitation activities
* Data exfiltration simulations

### Gophish

Gophish is used to create and manage phishing campaigns.

Functions include:

* Email template creation
* Campaign management
* Landing pages
* Victim interaction tracking

### Sliver

Sliver provides command and control capabilities following successful compromise.

Functions include:

* Session management
* Remote command execution
* Post-exploitation simulation
* Data collection

### DVWA

The Damn Vulnerable Web Application (DVWA) provides a controlled environment for testing and validating web application attack detections.

Attack scenarios include:

* SQL Injection
* Cross-Site Scripting (XSS)
* Command Injection
* Other common web attacks

---

## Endpoint Layer

The Windows 11 endpoint represents the primary monitored asset within the environment.

### Installed Components

* Sysmon
* Sysmon-ng
* Splunk Universal Forwarder
* LimaCharlie Sensor
* Thunderbird Mail Client

### Responsibilities

The endpoint serves as:

* Phishing target
* Telemetry source
* Detection validation platform
* Incident response target

---

## Telemetry Collection Layer

Telemetry is generated across multiple security controls and monitoring systems.

### Windows Event Logs

Provide authentication and operating system activity.

Examples include:

* Successful logins
* Failed logins
* Account activity

### Sysmon

Provides detailed endpoint telemetry.

Examples include:

* Process creation
* Network connections
* File activity
* Registry modifications

### Sysmon-ng

Extends telemetry collection and forwarding capabilities.

### Suricata

Provides network intrusion detection visibility.

Examples include:

* Port scanning
* Network reconnaissance
* Suspicious traffic patterns

### ModSecurity

Provides web application firewall visibility.

Examples include:

* SQL Injection attempts
* XSS attempts
* Command injection attempts

### OWASP CRS

Provides the detection logic used by ModSecurity to identify common web attacks.

### pfSense Logs

Provide firewall and network-level telemetry.

### LimaCharlie Telemetry

Provides endpoint detection and response visibility.

---

## Security Monitoring Layer

### Splunk Enterprise

Splunk serves as the central security analytics platform.

Responsibilities include:

* Log aggregation
* Data normalization
* Correlation
* Detection execution
* Alert generation
* Investigation support

All major telemetry sources ultimately feed into Splunk for analysis.

---

## Detection Engineering Layer

Custom detections were developed using Splunk SPL.

Detection categories include:

### Authentication

* Failed User Login
* Successful User Login
* Brute Force Detection

### Endpoint

* Credential Dumping
* Suspicious PowerShell
* Parent-Child Process Anomalies
* Post Exploitation Reconnaissance
* Data Exfiltration

### Network

* Suspicious Outbound Connections

### Web Application

* SQL Injection
* XSS
* Command Injection

Each detection includes:

* Severity
* Risk Score
* MITRE ATT&CK Mapping
* Alert Metadata

---

## Automation Layer

n8n functions as the SOAR platform within the lab.

### Core Functions

* Alert ingestion
* Alert normalization
* Alert enrichment
* Alert tracking
* Analyst activity logging
* Timeline management
* Host isolation workflows
* Daily reporting

The automation layer reduces manual analyst effort and provides a centralized workflow engine.

---

## Visualization Layer

### Grafana

Grafana provides operational visibility for analysts.

Implemented dashboards include:

* SOC Alert Dashboard
* Alert Investigation Dashboard

Capabilities include:

* Alert triage
* Investigation workflows
* Timeline visibility
* Analyst activity tracking
* Operational metrics

---

## Response Layer

### LimaCharlie

LimaCharlie provides endpoint response capabilities.

Implemented actions include:

* Host isolation
* Host unisolation

### Slack

Slack provides analyst notifications.

Examples include:

* Critical alerts
* Isolation events
* SOC notifications

---

## Architectural Benefits

The architecture provides:

* End-to-end attack visibility
* Multi-source telemetry collection
* Detection validation capabilities
* Automated SOC workflows
* Integrated investigation processes
* Incident response simulation
* Practical detection engineering experience

---

## Conclusion

The architecture was designed to replicate the major functions of a modern SOC while remaining practical to deploy within a home lab environment. By integrating attack simulation, telemetry collection, detection engineering, automation, visualization, and response capabilities, the environment provides a realistic platform for developing hands-on blue-team and purple-team skills.

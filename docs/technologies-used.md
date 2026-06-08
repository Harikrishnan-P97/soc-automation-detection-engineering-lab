# Technologies Used

This project integrates multiple security, monitoring, automation, and infrastructure technologies to simulate a modern Security Operations Center (SOC) environment.

## SIEM & Log Analysis

### Splunk Enterprise

* Centralized log collection and analysis
* Detection engineering and correlation searches
* Alert generation and investigation
* Windows, Sysmon, Suricata, and WAF log ingestion

### Splunk Universal Forwarder

* Endpoint log forwarding
* Windows Event Log collection
* Sysmon telemetry forwarding

---

## Monitoring & Visualization

### Grafana

* SOC alert monitoring dashboards
* Alert investigation dashboards
* KPI and metrics visualization
* Analyst activity tracking

---

## Security Orchestration & Automation

### n8n

* Alert intake and normalization
* Alert enrichment workflows
* Alert lifecycle management
* Investigation timeline management
* Host isolation automation
* Dashboard API integrations
* Daily SOC summary generation

### VirusTotal API

* Threat intelligence enrichment
* File hash reputation checks
* IOC enrichment

---

## Endpoint Security

### Sysmon

* Process creation monitoring
* Network connection monitoring
* Command-line visibility
* Endpoint telemetry generation

### LimaCharlie

* Endpoint Detection and Response (EDR)
* Host isolation actions
* Endpoint visibility and response capabilities

### Windows 11

* Victim workstation
* Endpoint telemetry source
* Detection engineering target

---

## Network Security

### pfSense

* Virtual firewall
* Network segmentation
* Traffic routing

### Suricata

* Network Intrusion Detection System (NIDS)
* Network telemetry generation
* Detection of suspicious network activity

---

## Web Application Security

### DVWA (Damn Vulnerable Web Application)

* Web application attack simulation
* Security testing platform
* SQL Injection, XSS, and Command Injection testing

### ModSecurity

* Web Application Firewall (WAF)
* HTTP request inspection
* Attack detection and logging

### OWASP Core Rule Set (CRS)

* Standardized WAF detection rules
* Protection against common web attacks
* ModSecurity rule framework

---

## Attack Simulation

### Gophish

* Phishing campaign management
* Email template creation
* Campaign tracking and reporting

### Sliver

* Command and Control (C2) framework
* Post-exploitation simulation
* Red team activity generation

### Thunderbird

* Victim email client
* Phishing email delivery testing

### Ubuntu Linux

* Attacker workstation
* Red team infrastructure host
* Gophish and Sliver deployment platform

---

## Infrastructure & Virtualization

### VirtualBox

* Lab virtualization platform
* Multi-system environment management

### Slack

* Critical alert notifications
* SOC response communications

---

## Documentation & Version Control

### GitHub

* Source code management
* Project documentation
* Workflow and dashboard exports
* Detection engineering repository

---

## Technology Summary

| Category            | Technologies                 |
| ------------------- | ---------------------------- |
| SIEM                | Splunk Enterprise            |
| Log Collection      | Splunk Universal Forwarder   |
| Dashboarding        | Grafana                      |
| SOAR                | n8n                          |
| Threat Intelligence | VirusTotal                   |
| Endpoint Monitoring | Sysmon                       |
| EDR                 | LimaCharlie                  |
| Network Security    | pfSense, Suricata            |
| Web Security        | ModSecurity, OWASP CRS, DVWA |
| Phishing Simulation | Gophish, Thunderbird         |
| Command & Control   | Sliver                       |
| Operating Systems   | Windows 11, Ubuntu Linux     |
| Virtualization      | VirtualBox                   |
| Notifications       | Slack                        |
| Version Control     | GitHub                       |

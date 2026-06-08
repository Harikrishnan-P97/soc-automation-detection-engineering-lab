# Telemetry Pipeline

## Overview

The SOC Automation and Detection Engineering Lab is built around a centralized telemetry pipeline that collects, processes, enriches, and visualizes security events generated throughout the environment.

The pipeline enables security data from endpoints, network devices, web applications, and security controls to be transformed into actionable alerts and investigation workflows.

This document describes how telemetry flows through the lab from initial event generation to analyst response.

---

## Telemetry Flow

The telemetry pipeline follows the process below:

```text
Attack Activity
      ↓
Telemetry Sources
      ↓
Log Collection
      ↓
Splunk Ingestion
      ↓
Detection Rules
      ↓
Alert Generation
      ↓
n8n Automation
      ↓
Threat Intelligence Enrichment
      ↓
Grafana Dashboards
      ↓
Analyst Investigation
      ↓
Response Actions
```

---

## Telemetry Sources

The lab collects telemetry from multiple security data sources.

### Windows Event Logs

Windows Event Logs provide authentication and operating system activity.

Examples include:

* Successful logins
* Failed logins
* User account activity
* Authentication failures

### Sysmon

Sysmon provides detailed endpoint visibility.

Collected events include:

* Process creation
* Network connections
* Registry modifications
* File creation events
* Command-line execution

### Suricata

Suricata generates network security telemetry.

Examples include:

* Port scanning activity
* Suspicious connections
* Intrusion detection events

### ModSecurity

ModSecurity generates web application security telemetry.

Examples include:

* SQL Injection attempts
* XSS attempts
* Command Injection attempts
* Web attack signatures

### pfSense

pfSense provides network and firewall telemetry.

Examples include:

* Firewall events
* Network connections
* Traffic filtering activity

### LimaCharlie

LimaCharlie provides endpoint detection and response telemetry.

Examples include:

* Endpoint events
* Sensor activity
* Response actions

---

## Log Collection

Telemetry generated throughout the environment is forwarded to Splunk for centralized analysis.

### Splunk Universal Forwarder

Installed on the Windows endpoint.

Responsibilities include:

* Collecting Windows Event Logs
* Collecting Sysmon events
* Forwarding telemetry to Splunk

### Sysmon-ng

Provides additional event collection and forwarding capabilities for endpoint telemetry.

---

## Centralized Analysis

### Splunk Enterprise

Splunk serves as the primary analytics platform.

Responsibilities include:

* Data ingestion
* Data normalization
* Event correlation
* Detection execution
* Alert generation

All security telemetry is centralized within Splunk to provide a single source of truth for investigations.

---

## Detection Pipeline

Custom SPL detections continuously analyze incoming telemetry.

### Authentication Detections

Monitor:

* Successful logins
* Failed logins
* Brute force activity

### Endpoint Detections

Monitor:

* Credential dumping tools
* Suspicious PowerShell activity
* Parent-child process anomalies
* Post-exploitation reconnaissance
* Data exfiltration activity

### Web Application Detections

Monitor:

* SQL Injection
* XSS
* Command Injection

### Network Detections

Monitor:

* Suspicious outbound connections
* Authentication abuse

---

## Alert Generation

When a detection rule is triggered, Splunk generates a structured alert containing:

* Alert Name
* Severity
* Risk Score
* Source Host
* User
* MITRE ATT&CK Mapping
* Alert Type
* Supporting Evidence

These alerts are forwarded to the automation layer for processing.

---

## Automation Pipeline

### Alert Intake Workflow

The Alert Intake workflow acts as the entry point for all detections.

Responsibilities include:

* Alert normalization
* Alert validation
* Metadata processing
* Alert lifecycle initialization

### Alert ID Generation

A dedicated workflow generates unique SOC alert identifiers.

Example:

```text
SOC-000001
SOC-000002
SOC-000003
```

### Threat Intelligence Enrichment

The VirusTotal enrichment workflow performs:

* IP reputation lookups
* Domain reputation checks
* File hash analysis

Enrichment results are attached to alerts before analyst review.

---

## Alert Management Pipeline

Alert data is stored and managed through dedicated n8n workflows.

Functions include:

* Alert tracking
* Alert updates
* Analyst actions
* Timeline management
* Investigation history

This creates a centralized source of investigation data independent of Splunk.

---

## Dashboard Integration

### Grafana SOC Dashboard

The dashboard receives alert data through n8n APIs.

Capabilities include:

* Alert queue visibility
* Severity tracking
* Filtering and search
* Operational metrics

### Investigation Dashboard

Provides detailed investigation context.

Examples include:

* Asset information
* Threat context
* Timeline history
* Analyst notes
* Response actions

---

## Analyst Investigation Workflow

Analysts interact with enriched alerts through Grafana.

Typical activities include:

1. Reviewing alert details.
2. Validating evidence.
3. Performing investigations.
4. Updating timelines.
5. Escalating alerts.
6. Closing incidents.
7. Initiating response actions.

All actions are recorded through workflow APIs.

---

## Response Pipeline

When response actions are required, Grafana interacts with n8n workflows.

Supported actions include:

* Investigate
* Escalate
* Close Alert
* Mark False Positive
* Isolate Host

### LimaCharlie Integration

Host isolation requests are sent to LimaCharlie.

The endpoint is then isolated from the network while maintaining management connectivity.

---

## Notification Pipeline

Critical alerts trigger automated notifications.

Notifications include:

* Alert ID
* Severity
* Host
* User
* Alert Summary

Notifications are delivered through Slack to simulate SOC communication workflows.

---

## Benefits of the Pipeline

The telemetry pipeline provides:

* Centralized visibility
* Multi-source correlation
* Automated enrichment
* Structured investigations
* Reduced analyst workload
* Faster incident response
* Improved alert context

By connecting telemetry generation, detection engineering, automation, and response capabilities, the pipeline simulates how modern SOC environments transform raw security events into actionable investigations.

---

## Conclusion

The telemetry pipeline serves as the backbone of the SOC lab. Security events generated across endpoints, network devices, web applications, and attack simulations are collected, analyzed, enriched, and transformed into investigation workflows that support analyst decision-making and incident response activities.

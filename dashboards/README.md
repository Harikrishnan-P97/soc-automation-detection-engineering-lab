# Grafana Dashboards

Grafana serves as the primary analyst interface within the SOC Automation & Detection Engineering Lab. It provides visibility into alerts, investigations, analyst activity, response actions, and SOC performance metrics through interactive dashboards integrated with Splunk and n8n automation workflows.

## Dashboards Included

### SOC Alert Dashboard

The SOC Alert Dashboard functions as the central monitoring and triage console for security analysts.

Key capabilities include:

* Real-time alert queue management
* Alert severity and status monitoring
* Alert filtering and search functionality
* MITRE ATT&CK categorization
* SLA monitoring and response metrics
* Analyst workload visibility
* Alert trend analysis
* Investigation workflow initiation
* Integrated analyst action buttons

Supported analyst actions:

* Investigate Alert
* Escalate Alert
* Close Alert
* Mark False Positive
* Isolate Host

The dashboard is designed to simulate the day-to-day workflow of a SOC analyst responsible for monitoring, triaging, and responding to security alerts.

### SOC Alert Investigation Dashboard

The SOC Alert Investigation Dashboard provides detailed context and investigation capabilities for individual alerts.

Key capabilities include:

* Alert overview and metadata
* Asset context enrichment
* Threat intelligence context
* Investigation workflow tracking
* Alert timeline visualization
* Analyst activity history
* Escalation tracking
* Resolution metrics
* Case ownership visibility

The dashboard enables analysts to transition from alert triage to investigation and response within a unified workflow.

## Dashboard Architecture

The dashboards retrieve alert and investigation data from custom n8n APIs and present enriched information generated through the SOC automation pipeline.

Data sources include:

* Splunk detections
* n8n Alert Dashboard API
* Alert Activity API
* Alert Timeline API
* VirusTotal enrichment workflows
* Analyst action workflows

## Dashboard Exports

This directory contains Grafana dashboard exports that can be imported into another Grafana instance for reference or educational purposes.

Available exports:

- [SOC-Alert-Dashboard](/exports/SOC%20Alert%20Dashboard.json)
- [SOC-Alert-Investigation-Dashboard](/exports/SOC%20-%20Alert%20Investigation.json)

## Screenshots

Dashboard screenshots and demonstration recordings are available within:

- [Grafana](/screenshots/grafana/)

## Purpose

These dashboards were built to simulate realistic Security Operations Center workflows and provide analysts with a centralized interface for monitoring, investigating, escalating, and responding to security alerts generated throughout the SOC lab environment.

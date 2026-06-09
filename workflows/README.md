# n8n SOAR Workflows

n8n serves as the automation and orchestration layer of the SOC Automation & Detection Engineering Lab.

The workflows contained in this directory automate alert processing, enrichment, investigation tracking, analyst actions, and incident response activities, simulating many capabilities commonly associated with Security Orchestration, Automation, and Response (SOAR) platforms.

## Implemented Workflows

| Workflow                      | Purpose                                         |
| ----------------------------- | ----------------------------------------------- |
| SOC-ID-Generator              | Generates unique SOC alert identifiers          |
| SOC-Alert-Intake              | Processes and normalizes incoming Splunk alerts |
| SOC-VirusTotal-Enrichment-API | Enriches alerts using VirusTotal intelligence   |
| SOC-Host-Isolation-Action     | Isolates hosts through LimaCharlie integration  |
| SOC-Alert-Activity-API        | Tracks analyst activity and alert updates       |
| SOC-Alerts-Timeline-API       | Maintains investigation timelines               |
| SOC-Alert-Action-API          | Processes analyst actions from Grafana          |
| SOC-Alert-Dashboard           | Provides alert data for Grafana dashboards      |
| SOC-Alert-Dashboard-Filtered  | Supports filtering and dashboard searches       |
| SOC-Daily-Summary-Bot         | Generates automated SOC activity summaries      |

## Core Capabilities

The automation layer provides:

* Automated alert ingestion
* Alert normalization
* Severity assignment
* Threat intelligence enrichment
* VirusTotal integration
* Investigation timeline tracking
* Analyst activity tracking
* Host isolation workflows
* Slack notifications
* Alert lifecycle management
* Dashboard API integration

## Workflow Architecture

The workflow chain follows the general process below:

```text
Splunk Detection
        ↓
SOC Alert Intake
        ↓
Alert Normalization
        ↓
Threat Intelligence Enrichment
        ↓
Dashboard APIs
        ↓
Grafana Investigation Workflow
        ↓
Response Actions
        ↓
Host Isolation / Alert Closure
```

## Workflow Exports

Workflow exports are available within:

- [exports](exports/)

These exports can be imported into another n8n instance for educational and research purposes.

## Purpose

These workflows were built to simulate SOC analyst operations and demonstrate practical automation engineering concepts including enrichment, orchestration, alert management, investigation tracking, and incident response automation.

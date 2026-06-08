# Documentation

This directory contains supporting documentation for the SOC Automation & Detection Engineering Lab.

The documents in this section provide additional context around the lab architecture, telemetry collection pipeline, incident response workflows, technologies used, and key lessons learned during development.

## Documents

### Lab Overview

**File:** `lab-overview.md`

Provides a high-level overview of the complete SOC lab environment, including infrastructure components, security tooling, attack simulations, detection engineering, alert management, and response workflows.

### Architecture

**File:** `architecture.md`

Explains the overall architecture of the SOC lab, including:

* Splunk SIEM
* Grafana dashboards
* n8n automation platform
* LimaCharlie EDR
* pfSense firewall
* Suricata IDS
* ModSecurity WAF
* Windows endpoint telemetry
* Attack simulation infrastructure

### Telemetry Pipeline

**File:** `telemetry-pipeline.md`

Describes how telemetry flows through the environment, from data generation on endpoints and network devices to ingestion, detection, enrichment, visualization, and response actions.

### Incident Response Workflow

**File:** `incident-response-workflow.md`

Documents the end-to-end alert lifecycle, including:

* Alert generation
* Alert ingestion
* Threat enrichment
* Analyst investigation
* Escalation workflows
* Host isolation
* Alert closure

### Technologies Used

**File:** `technologies-used.md`

Provides a detailed breakdown of the technologies, platforms, and tools used throughout the project.

### Lessons Learned

**File:** `lessons-learned.md`

Summarizes key technical lessons, design decisions, implementation challenges, and improvements identified while building the lab.

---

## Recommended Reading Order

For first-time visitors, the following order is recommended:

1. Lab Overview
2. Architecture
3. Technologies Used
4. Telemetry Pipeline
5. Incident Response Workflow
6. Lessons Learned

---

## Related Documentation

* `/detections` — Detection engineering and Splunk correlation searches
* `/workflows` — n8n SOAR workflows and automation
* `/dashboards` — Grafana dashboards and exports
* `/phishing-lab` — Phishing simulation environment and attack chain documentation

Together, these documents provide a complete overview of the SOC Automation & Detection Engineering Lab, including monitoring, detection, investigation, automation, and incident response capabilities.

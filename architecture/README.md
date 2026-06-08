# Architecture Diagrams

This directory contains the primary architecture diagrams used throughout the SOC Automation & Detection Engineering Lab.

These diagrams provide a visual representation of the lab infrastructure, telemetry flow, alert processing pipeline, investigation workflow, and automated response capabilities.

## Contents

### Architecture Diagram

**File:** `Architecture-diagram.png`

This diagram provides a high-level overview of the complete SOC lab environment, including:

* Attacker infrastructure
* Windows endpoint
* pfSense firewall
* Suricata IDS
* ModSecurity WAF
* DVWA web application
* Splunk SIEM
* Grafana dashboards
* n8n automation platform
* VirusTotal enrichment
* Slack notifications
* LimaCharlie EDR

The diagram illustrates how security telemetry is generated, collected, processed, and transformed into actionable alerts.

---

### Telemetry Pipeline and Investigation Workflow

**File:** `Telemetry-pipeline-and-investigation-workflow.png`

This diagram focuses on the end-to-end SOC workflow after telemetry is generated.

The workflow includes:

1. Event generation
2. Telemetry collection
3. Splunk detection rules
4. Alert generation
5. n8n alert ingestion
6. Threat intelligence enrichment
7. Alert storage and lifecycle management
8. Grafana alert queue
9. Analyst investigation workflow
10. Escalation and response actions
11. Host isolation through LimaCharlie
12. Alert closure and reporting

This diagram demonstrates how the lab simulates a SOC environment from initial detection through incident response.

---

## Related Documentation

For additional context, refer to:

* `../docs/lab-overview.md`
* `../docs/architecture.md`
* `../docs/telemetry-pipeline.md`
* `../docs/incident-response-workflow.md`

These documents provide detailed explanations of the components and workflows represented in the diagrams.

---

## Purpose

The architecture diagrams serve as a visual reference for understanding:

* Infrastructure design
* Data flow
* Detection engineering workflows
* Alert enrichment processes
* Investigation workflows
* Automated response actions

Together, these diagrams provide a complete view of how the SOC Automation & Detection Engineering Lab operates.

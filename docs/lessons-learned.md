# Lessons Learned

## Overview

Building this SOC Automation and Detection Engineering Lab provided practical experience across multiple areas of cybersecurity, including detection engineering, threat monitoring, incident response, security automation, phishing simulation, and dashboard development.

While many security concepts can be learned through documentation and training courses, implementing them in a functioning environment revealed challenges and considerations that are difficult to understand without hands-on experience.

This document summarizes the key technical and operational lessons learned throughout the project.

---

## Detection Engineering Requires Data Understanding

One of the most important lessons learned was that effective detections depend heavily on understanding the underlying telemetry.

Creating detection rules involved:

* Reviewing raw event logs
* Understanding field mappings
* Normalizing data across sources
* Reducing false positives
* Testing attacker techniques

Simply knowing a MITRE ATT&CK technique was not enough.

Successful detections required understanding:

* Windows Event Logs
* Sysmon telemetry
* Network traffic
* ModSecurity events
* Suricata alerts

The quality of telemetry directly impacted the quality of detections.

---

## Alert Context Matters More Than Alert Volume

Generating alerts is relatively easy.

Generating useful alerts is significantly more difficult.

Early detections produced large amounts of noisy results that were not useful for investigations.

Improving detections required:

* User filtering
* Service account exclusions
* Risk scoring
* Severity classification
* Context enrichment

This reinforced the importance of prioritizing quality over quantity.

---

## Automation Significantly Reduces Analyst Workload

Before implementing automation workflows, alert handling required multiple manual steps.

After integrating n8n workflows:

* Alert IDs were automatically generated
* Alerts were normalized automatically
* VirusTotal enrichment occurred automatically
* Timelines were updated automatically
* Notifications were sent automatically

Automation reduced repetitive work and allowed investigations to focus on analysis rather than administration.

---

## Visualization Improves Investigation Efficiency

Grafana dashboards transformed raw alert data into actionable information.

Investigation became significantly faster when analysts could immediately view:

* Alert details
* Asset context
* Threat intelligence
* Timeline history
* Alert metrics

The investigation dashboard became a central component of the SOC workflow.

This highlighted the importance of visualization in security operations.

---

## Detection Engineering and SOAR Work Together

Detections alone do not create an effective SOC.

Automation alone does not create an effective SOC.

The most valuable outcome of the project was understanding how both areas complement each other.

The workflow became:

```text
Telemetry
    ↓
Detection
    ↓
Enrichment
    ↓
Investigation
    ↓
Response
    ↓
Closure
```

Each stage depended on the previous stage functioning correctly.

---

## MITRE ATT&CK Provides Valuable Structure

Mapping detections to MITRE ATT&CK techniques helped organize security coverage.

Examples included:

| Detection          | ATT&CK Technique |
| ------------------ | ---------------- |
| Credential Dumping | T1003            |
| PowerShell Abuse   | T1059.001        |
| Brute Force        | T1110            |
| Valid Accounts     | T1078            |
| Discovery Commands | T1082            |
| Data Exfiltration  | T1041            |
| SQL Injection      | T1190            |

Using ATT&CK made it easier to understand which attack behaviors were covered and where detection gaps existed.

---

## Telemetry Correlation Creates Better Visibility

Individual events rarely provide the full picture.

Correlating multiple telemetry sources provided significantly more visibility.

Examples included:

* Sysmon process execution
* Windows authentication events
* Suricata network alerts
* ModSecurity WAF events
* Firewall logs

Combining these sources enabled broader visibility across attacker activity.

---

## Phishing Simulations Create Realistic Attack Scenarios

The phishing lab demonstrated how multiple attack stages connect together.

The simulation covered:

* Initial access
* Payload delivery
* User interaction
* Command execution
* Discovery activity
* Data exfiltration
* Detection generation
* Incident response

This provided a much deeper understanding of the Cyber Kill Chain compared to studying theory alone.

---

## Incident Response Is More Than Detection

A detection is only the starting point of an investigation.

The project emphasized the importance of:

* Triage
* Investigation
* Escalation
* Containment
* Documentation
* Resolution

Features such as analyst actions, timelines, and host isolation highlighted how response activities are integrated into SOC operations.

---

## Documentation Is Critical

As the environment grew in complexity, documentation became increasingly important.

Maintaining documentation for:

* Architecture
* Detections
* Workflows
* Dashboards
* Attack simulations

made the environment easier to understand, troubleshoot, and maintain.

Good documentation also improves portfolio quality and knowledge transfer.

---

## Key Technical Skills Developed

Through this project, practical experience was gained in:

### Security Operations

* Alert triage
* Incident investigation
* Threat hunting concepts
* MITRE ATT&CK mapping

### Detection Engineering

* SPL development
* Log analysis
* Detection tuning
* Risk scoring

### Security Automation

* n8n workflow development
* API integrations
* SOAR concepts
* Automated response actions

### Monitoring and Visualization

* Grafana dashboards
* Alert metrics
* Investigation workflows
* Operational reporting

### Infrastructure and Security Tooling

* Splunk
* Sysmon
* LimaCharlie
* Suricata
* ModSecurity
* OWASP CRS
* pfSense
* Gophish
* Sliver
* Thunderbird

---

## Future Improvements

Potential future enhancements include:

* Additional detection rules
* Threat hunting dashboards
* Automated case management
* Threat intelligence feeds
* User behavior analytics
* Sigma rule support
* Detection-as-Code workflows
* Additional attack simulations
* Cloud telemetry integration

---

## Final Thoughts

This project evolved from a simple SOC lab into a complete security operations environment that combines detection engineering, security monitoring, incident response, threat intelligence enrichment, automation, and phishing simulation.

More importantly, it demonstrated how individual security tools can be integrated into a cohesive workflow that mirrors many of the processes used in modern Security Operations Centers.

The most valuable outcome was not a specific dashboard, workflow, or detection rule, but the practical understanding gained from designing, building, testing, and operating the entire environment end-to-end.

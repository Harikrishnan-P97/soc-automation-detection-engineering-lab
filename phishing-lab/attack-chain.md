# Attack Chain Walkthrough

## Overview

This document follows the complete phishing attack lifecycle executed within the lab environment.

The objective of the exercise was to simulate a realistic phishing campaign, establish access to a victim endpoint, perform post-exploitation activities, generate security telemetry, and validate the effectiveness of custom detection engineering and SOC automation workflows.

The attack chain aligns closely with the Cyber Kill Chain and MITRE ATT&CK framework.

---

# Stage 1: Infrastructure Preparation

## Objective

Prepare attacker infrastructure capable of delivering phishing emails and receiving connections from compromised systems.

## Actions Performed

The attacker machine was configured with:

* Gophish
* Sliver C2 Framework
* Netcat Listener
* Python Web Server

The Ubuntu attack server served as the central platform for phishing delivery and post-exploitation operations.

## Outcome

The phishing infrastructure was operational and ready to deliver payloads to the victim environment.

---

# Stage 2: Phishing Campaign Creation

## Objective

Create a phishing campaign targeting the victim workstation.

## Actions Performed

A phishing campaign was created in Gophish.

The campaign included:

* Email template
* Landing page
* Target recipient
* Payload download link

The email was designed to mimic a legitimate business communication to encourage user interaction.

## MITRE ATT&CK

* T1566 – Phishing

## Outcome

The phishing email was successfully delivered to the victim mailbox.

---

# Stage 3: Email Delivery

## Objective

Deliver the phishing lure to the victim.

## Actions Performed

The victim accessed Thunderbird Mail Client and received the phishing email.

The email contained:

* Social engineering content
* Download instructions
* Malicious attachment

## MITRE ATT&CK

* T1566.001 – Spearphishing Attachment

## Outcome

The victim interacted with the email and downloaded the attachment.

---

# Stage 4: Payload Execution

## Objective

Establish initial access on the victim endpoint.

## Actions Performed

The downloaded archive was extracted by the user.

The payload contained a Sliver implant that was executed on the Windows 11 host.

Upon execution, the implant established communication with the attacker's command-and-control infrastructure.

## MITRE ATT&CK

* T1204 – User Execution
* T1059 – Command Execution

## Outcome

A successful Sliver session was established.

---

# Stage 5: Initial Foothold

## Objective

Verify compromise and establish control of the victim system.

## Actions Performed

The attacker validated access by:

* Opening an active Sliver session
* Running basic commands
* Confirming endpoint connectivity

## MITRE ATT&CK

* T1071 – Application Layer Protocol

## Outcome

The victim endpoint became fully accessible through the Sliver framework.

---

# Stage 6: Host Discovery

## Objective

Collect information about the compromised system.

## Actions Performed

Several reconnaissance commands were executed including:

* whoami
* hostname
* ipconfig
* systeminfo
* tasklist
* net user
* net localgroup

These commands were used to identify:

* Logged-in users
* Host details
* Network configuration
* Running processes
* Available accounts

## MITRE ATT&CK

* T1082 – System Information Discovery
* T1033 – Account Discovery

## Outcome

The attacker obtained sufficient information about the victim environment.

---

# Stage 7: Credential Access Simulation

## Objective

Simulate credential theft activity.

## Actions Performed

Credential dumping tools were executed on the victim host.

Examples included:

* Mimikatz
* LaZagne
* ProcDump

The activity generated Sysmon process creation events and triggered custom Splunk detections.

## MITRE ATT&CK

* T1003 – OS Credential Dumping

## Outcome

Credential access activity was successfully detected.

---

# Stage 8: Command and Control Activity

## Objective

Maintain communication with the compromised endpoint.

## Actions Performed

The Sliver implant maintained communication with the attacker infrastructure.

Additional commands were executed remotely through the established session.

## MITRE ATT&CK

* T1071 – Application Layer Protocol

## Outcome

Persistent attacker interaction with the endpoint was maintained.

---

# Stage 9: Data Collection

## Objective

Gather files for exfiltration.

## Actions Performed

Sensitive files were identified and staged for transfer.

Sample files containing simulated business information were collected from the victim workstation.

## MITRE ATT&CK

* T1005 – Data from Local System

## Outcome

Files were prepared for exfiltration.

---

# Stage 10: Data Exfiltration

## Objective

Transfer data from the victim system to the attacker infrastructure.

## Actions Performed

Data was transmitted using utilities such as:

* ncat
* curl
* wget
* PowerShell web requests

Network connections were established from the victim system to the attacker-controlled host.

## MITRE ATT&CK

* T1041 – Exfiltration Over C2 Channel

## Outcome

Data exfiltration activity successfully generated telemetry and triggered detection rules.

---

# Stage 11: Detection Generation

## Objective

Validate custom Splunk detection content.

## Actions Performed

Sysmon and Windows logs were forwarded into Splunk.

Custom detections identified:

* Credential dumping
* Suspicious PowerShell activity
* Post-exploitation reconnaissance
* Data exfiltration
* Failed logons
* Successful logons
* Brute-force activity

Alerts were generated and normalized for downstream processing.

## Outcome

Detection engineering content successfully identified attacker behavior.

---

# Stage 12: Alert Processing

## Objective

Automate alert handling.

## Actions Performed

Alerts generated in Splunk were forwarded into n8n.

The workflow performed:

* Alert enrichment
* Alert normalization
* Alert tracking
* Timeline generation
* Severity classification

## Outcome

Alerts entered the SOC workflow pipeline.

---

# Stage 13: SOC Investigation

## Objective

Simulate analyst investigation activities.

## Actions Performed

Alerts were displayed within Grafana dashboards.

Analysts could review:

* Alert metadata
* Asset context
* Threat context
* Investigation timeline
* Analyst notes

## Outcome

The attack became fully visible through the SOC investigation workflow.

---

# Stage 14: Incident Response

## Objective

Contain the compromised endpoint.

## Actions Performed

Response actions were executed through LimaCharlie.

Available actions included:

* Host Isolation
* Host Unisolation

These actions were integrated directly into the SOC workflow.

## MITRE ATT&CK

* M1030 – Network Segmentation

## Outcome

The compromised endpoint could be contained without leaving the investigation platform.

---

# Summary

The phishing simulation successfully demonstrated the complete attack lifecycle from phishing email delivery to endpoint compromise, post-exploitation activity, detection generation, analyst investigation, and incident response.

The exercise validated:

* Detection engineering content
* Splunk alerting
* n8n automation workflows
* Grafana investigation dashboards
* LimaCharlie response actions
* SOC operational processes

The resulting environment provides a repeatable platform for testing security monitoring and incident response capabilities in a realistic and controlled setting.

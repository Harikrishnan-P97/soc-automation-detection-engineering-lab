# Related Writeups

## Overview

This phishing simulation lab was developed alongside a series of technical articles documenting the design decisions, attack execution process, detection engineering efforts, and SOC automation workflows implemented throughout the project.

The GitHub repository focuses on the technical implementation and supporting artifacts, while the articles provide additional context, lessons learned, and detailed walkthroughs of the lab development process.

---

## 1. I Built a Phishing Lab to Finally Understand the Cyber Kill Chain

**Medium Article**

https://medium.com/@harikrishnan.p097/i-built-a-phishing-lab-to-finally-understand-the-cyber-kill-chain-9aad7c10e8c4

### Summary

This article documents the complete phishing attack lifecycle and maps each stage to the Cyber Kill Chain framework.

Topics covered include:

* Reconnaissance
* Weaponization
* Delivery
* Exploitation
* Installation
* Command and Control
* Actions on Objectives
* SOC visibility across the attack chain

The article demonstrates how theoretical attack stages can be translated into observable events, detections, and analyst investigations within a controlled lab environment.

---

## 2. Inside My Phishing Simulation Lab: Red Team Meets Blue Team

**Medium Article**

https://medium.com/@harikrishnan.p097/inside-my-phishing-simulation-lab-red-team-meets-blue-team-05731f401bb9

### Summary

This article provides a detailed walkthrough of the phishing simulation lab architecture and supporting infrastructure.

Topics covered include:

* Gophish phishing campaigns
* Sliver command-and-control infrastructure
* Windows 11 victim environment
* Sysmon telemetry collection
* Splunk detection engineering
* n8n SOC automation workflows
* Grafana investigation dashboards
* LimaCharlie response actions

The article focuses on how offensive security activities generate telemetry that can be leveraged by defenders to build detections and automate incident response workflows.

---

## Repository Resources

The following sections of this repository contain the technical artifacts referenced throughout the articles:

| Repository Section | Description                                        |
| ------------------ | -------------------------------------------------- |
| `phishing-lab/`    | Attack simulation documentation                    |
| `detections/`      | Detection engineering content and Splunk searches  |
| `workflows/`       | n8n automation workflows                           |
| `dashboards/`      | Grafana dashboard exports                          |
| `docs/`            | Supporting architecture and workflow documentation |

---

## Future Writeups

As the lab evolves, additional articles covering detection engineering, threat hunting, SOC automation, incident response, and purple-team exercises will be added to this section.

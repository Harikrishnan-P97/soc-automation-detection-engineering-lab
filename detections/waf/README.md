# Web Application Firewall (WAF) Detection Coverage

## Overview

The SOC lab includes a Web Application Firewall (WAF) built using ModSecurity and the OWASP Core Rule Set (CRS).

The WAF is deployed in front of the Damn Vulnerable Web Application (DVWA) hosted on the Windows victim machine and is responsible for detecting and logging malicious web requests before they reach the application.

Generated WAF telemetry is forwarded into Splunk where additional detection logic, alerting, and SOC workflows are performed.

---

## WAF Architecture

Client Request
      ↓
ModSecurity + OWASP CRS
      ↓
DVWA Web Application
      ↓
Audit Logs
      ↓
Splunk Universal Forwarder
      ↓
Splunk Enterprise
      ↓
n8n Automation
      ↓
Grafana SOC Dashboards

---

## Technologies Used

| Component | Purpose |
|------------|----------|
| ModSecurity | Web Application Firewall |
| OWASP CRS | Attack detection rules |
| DVWA | Vulnerable web application |
| XAMPP / Apache | Web server |
| Splunk UF | Log forwarding |
| Splunk Enterprise | Detection and alerting |

---

## OWASP Core Rule Set (CRS)

The OWASP Core Rule Set provides pre-built detection logic for common web application attacks.

The SOC lab uses CRS to generate realistic WAF telemetry that can be monitored, investigated, and correlated within Splunk.

Reference:

https://coreruleset.org

---

## Attack Coverage

The WAF generates telemetry for attacks including:

### SQL Injection (SQLi)

Example:

```sql
' OR 1=1 --
```

MITRE ATT&CK:

- T1190 – Exploit Public-Facing Application

---

### Cross-Site Scripting (XSS)

Example:

```html
<script>alert('xss')</script>
```

MITRE ATT&CK:

- T1059 – Command and Scripting Interpreter

---

### Command Injection

Example:

```bash
; whoami
```

MITRE ATT&CK:

- T1190 – Exploit Public-Facing Application

---

### Directory Traversal

Example:

```text
../../../../windows/win.ini
```

MITRE ATT&CK:

- T1006 – Path Traversal

---

### Web Brute Force

Examples:

- Repeated login attempts
- Credential guessing activity

MITRE ATT&CK:

- T1110 – Brute Force

---

### Malicious User Agents

Examples:

- sqlmap
- nikto
- curl
- custom reconnaissance tools

MITRE ATT&CK:

- T1595 – Active Scanning

---

## Log Sources

WAF telemetry collected in the lab includes:

- ModSecurity Audit Logs
- Apache Access Logs
- Apache Error Logs
- HTTP Request Metadata
- Rule Trigger Events

These logs are forwarded into Splunk for centralized analysis.

---

## Splunk Integration

WAF events are indexed within:

```text
index=waf
```

The generated telemetry supports:

- Alert generation
- Threat hunting
- Investigation workflows
- MITRE ATT&CK mapping
- Dashboard visualizations

---

## Related Detections

Custom Splunk detections built on WAF telemetry include:

- SQL Injection Detection
- XSS Detection
- Command Injection Detection

Detailed SPL queries for these detections are available within the `/web` directory.

---

## Validation

The WAF detections were validated using attack simulations against DVWA including:

- SQL Injection
- Cross-Site Scripting
- Command Injection
- Directory Traversal
- Brute Force Authentication
- Reconnaissance Activity

All testing was performed inside a controlled lab environment.
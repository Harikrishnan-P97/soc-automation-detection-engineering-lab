# Suspicious PowerShell Detection

## Description

Detects PowerShell execution with flags commonly associated with attacker activity, malware execution, defense evasion, and fileless attacks.

PowerShell is frequently abused because it is built into Windows and provides direct access to system administration and automation capabilities.

This detection identifies potentially malicious PowerShell execution using:

- Encoded commands
- Execution policy bypasses
- Hidden windows
- Non-interactive execution
- No-profile execution

These techniques are commonly observed during malware infections, post-exploitation activity, and red team operations.

---

## MITRE ATT&CK

| Tactic | Technique |
|----------|----------|
| Execution | T1059.001 – PowerShell |

---

## Data Source

- Microsoft Sysmon
- Event ID 1 (Process Creation)

---

## Detection Logic

The detection monitors PowerShell executions containing suspicious command-line arguments.

Examples include:

| Flag | Description |
|--------|-------------|
| -enc | Encoded command execution |
| -nop | No profile |
| -w hidden | Hidden PowerShell window |
| -windowstyle hidden | Hidden PowerShell window |
| -ep bypass | Execution policy bypass |
| -executionpolicy bypass | Execution policy bypass |
| -noni | Non-interactive mode |

These flags are frequently chained together during malicious activity.

Example:

```powershell
powershell.exe -nop -w hidden -enc <base64_payload>
```

---

## SPL Detection

```spl
index=pc1 sourcetype=WinEventLog LogName="Microsoft-Windows-Sysmon/Operational" EventCode=1
| `pc1_sysmon_process_normalization`

| eval cmd=lower(CommandLine)

| where process_name="powershell.exe" AND (
      like(cmd, "%-nop%")
   OR like(cmd, "%-w hidden%")
   OR like(cmd, "%-windowstyle hidden%")
   OR like(cmd, "%-noni%")
   OR like(cmd, "%-ep bypass%")
   OR like(cmd, "%-executionpolicy bypass%")
   OR like(cmd, "%-enc%")
)

| eval suspicious_flag=case(
    like(cmd,"% -enc%"),"Encoded Command",
    like(cmd,"% -nop%"),"No Profile",
    like(cmd,"% -w hidden%") OR like(cmd,"% -windowstyle hidden%"),"Hidden Window",
    like(cmd,"% -ep bypass%") OR like(cmd,"% -executionpolicy bypass%"),"Execution Policy Bypass",
    like(cmd,"% -noni%"),"Non Interactive",
    true(),"Unknown"
)

| eval alert_name="Suspicious PowerShell Flags"
| eval severity="high"
| eval mitre_tactic="Execution"
| eval mitre_technique="T1059.001"
| eval risk_score=80
| eval alert_type="endpoint"

| eval index_name="pc1"
| eval event_source="Sysmon"
| eval event_id="1"

| rename dest as dest_host

| table _time dest_host user process_name CommandLine suspicious_flag alert_name severity mitre_tactic mitre_technique risk_score alert_type index_name event_source event_id

| sort - _time
```

---

## Example Alert

Fields returned:

- User
- Host
- Process Name
- Command Line
- Suspicious Flag
- Risk Score
- MITRE ATT&CK Mapping

---

## Detection Examples

### Encoded Command

```powershell
powershell.exe -enc SQBFAFgA
```

### Hidden PowerShell Window

```powershell
powershell.exe -w hidden
```

### Execution Policy Bypass

```powershell
powershell.exe -ExecutionPolicy Bypass
```

### No Profile

```powershell
powershell.exe -nop
```

---

## Lab Validation

Validated using manually executed PowerShell commands containing:

- Encoded payloads
- Hidden execution flags
- Execution policy bypasses
- No-profile execution

The resulting Sysmon process creation events successfully triggered Splunk alerts and appeared in the SOC investigation workflow.
# Suspicious Parent-Child Process Detection

## Description

Detects suspicious parent-child process relationships that are commonly observed during malware execution, phishing attacks, script-based execution, and post-exploitation activity.

Many legitimate Windows processes rarely spawn certain child processes during normal operations. When these unusual process relationships occur, they may indicate attacker activity.

Examples include:

- Office applications spawning PowerShell
- Office applications spawning Command Prompt
- Explorer spawning PowerShell unexpectedly
- Script interpreters spawning administrative tools
- LOLBins launching secondary payloads

This detection focuses on behavioral anomalies rather than specific malware signatures.

---

## MITRE ATT&CK

| Tactic | Technique |
|----------|----------|
| Execution | T1059 – Command and Scripting Interpreter |

---

## Data Source

- Microsoft Sysmon
- Event ID 1 (Process Creation)

---

## Detection Logic

The detection uses a custom Splunk macro:

```spl
pc1_suspicious_parent_child_process
```

The macro identifies suspicious process creation chains and returns:

- Parent Process
- Child Process
- Command Line
- User Context
- Host Information

Examples of suspicious relationships:

| Parent Process | Child Process |
|----------------|--------------|
| WINWORD.EXE | powershell.exe |
| EXCEL.EXE | cmd.exe |
| OUTLOOK.EXE | powershell.exe |
| explorer.exe | powershell.exe |
| wscript.exe | cmd.exe |
| cscript.exe | powershell.exe |

---

## SPL Detection

```spl
index=pc1 EventCode=1

| `pc1_suspicious_parent_child_process`

| eval alert_name="Suspicious Parent-Child Process"
| eval severity="high"

| eval mitre_tactic="Execution"
| eval mitre_technique="T1059"

| eval risk_score=85
| eval alert_type="endpoint"

| eval index_name="pc1"
| eval event_source="Sysmon"
| eval event_id="1"

| rename ComputerName as dest_host

| eval suspicious_process=parent_process_name . " -> " . process_name

| table _time dest_host user parent_process_name process_name CommandLine suspicious_process alert_name severity mitre_tactic mitre_technique risk_score alert_type index_name event_source event_id

| sort - _time
```

---

## Example Alert

Fields returned:

- User
- Host
- Parent Process
- Child Process
- Command Line
- Suspicious Process Chain
- Risk Score
- MITRE ATT&CK Mapping

Example:

```text
Parent Process:
WINWORD.EXE

Child Process:
powershell.exe

Suspicious Process Chain:
WINWORD.EXE -> powershell.exe
```

---

## Why This Detection Matters

Traditional detections often focus on known malicious files or hashes.

Parent-child process monitoring helps identify:

- Malicious Office macros
- Fileless malware
- Script-based attacks
- Initial payload execution
- Living-off-the-land techniques (LOLBins)

Because it focuses on behavior rather than signatures, it remains effective even when attackers change tools.

---

## Lab Validation

Validated through simulated attacker activity that generated abnormal process creation chains involving:

- PowerShell
- Command Prompt
- Script interpreters
- Office applications

The resulting Sysmon process creation events successfully triggered Splunk alerts and appeared within the SOC investigation workflow.
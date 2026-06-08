# Credential Dumping Detection

## Description

Detects execution of credential dumping tools and techniques commonly used by attackers to extract credentials from memory.

The detection identifies:

- Mimikatz execution
- LaZagne execution
- ProcDump targeting LSASS
- Mimikatz credential dumping modules
  - sekurlsa
  - logonpasswords

Credential dumping is a common post-compromise activity used to obtain plaintext credentials, NTLM hashes, Kerberos tickets, and other authentication material.

---

## MITRE ATT&CK

| Tactic | Technique |
|----------|----------|
| Credential Access | T1003 – OS Credential Dumping |

---

## Data Source

- Microsoft Sysmon
- Event ID 1 (Process Creation)

---

## Detection Logic

The detection looks for:

- Known credential dumping tools
- Credential dumping command-line arguments
- LSASS targeting behavior

Examples:

- mimikatz.exe
- lazagne.exe
- procdump.exe
- sekurlsa
- logonpasswords

---

## SPL Detection

```spl
index=pc1 sourcetype=WinEventLog EventCode=1
| `pc1_sysmon_process_normalization`
| rex field=Hashes "SHA256=(?<file_hash>[A-Fa-f0-9]{64})"
| where process_name IN ("mimikatz.exe","lazagne.exe","procdump.exe")
    OR like(CommandLine,"%sekurlsa%")
    OR like(CommandLine,"%logonpasswords%")
| eval process_lower=lower(process_name)
| eval alert_name="Credential Dumping Tool Execution"
| eval severity="critical"
| eval mitre_tactic="Credential Access"
| eval mitre_technique="T1003"
| eval risk_score=95
| eval alert_type="endpoint"
| eval index_name="pc1"
| eval event_source="Sysmon"
| eval event_id=1
| rename ComputerName as dest_host
| eval src_ip=coalesce(SourceIp, src_ip)
| eval suspicious_process=process_name
| eval suspicious_flag=case(
    process_lower="mimikatz.exe","mimikatz",
    process_lower="lazagne.exe","lazagne",
    process_lower="procdump.exe","procdump",
    like(lower(CommandLine),"%sekurlsa%"),"sekurlsa",
    like(lower(CommandLine),"%logonpasswords%"),"logonpasswords",
    true(),"credential_dumping"
)
| eval parent_process=ParentImage
| eval user=coalesce(user, User, Account_Name, "unknown-user")
| table _time dest_host user process_name process_path CommandLine parent_process src_ip file_hash suspicious_process suspicious_flag alert_name severity mitre_tactic mitre_technique risk_score alert_type index_name event_source event_id
| sort - _time
```

---

## Example Alert

Fields returned:

- User
- Host
- Process Name
- Command Line
- Parent Process
- SHA256 Hash
- Risk Score
- MITRE ATT&CK Mapping

---

## Lab Validation

Validated using:

- Mimikatz
- LaZagne
- ProcDump

The generated Sysmon process creation events successfully triggered Splunk alerts and appeared within the SOC investigation workflow.
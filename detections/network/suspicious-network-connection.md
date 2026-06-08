# Network Connection from Suspicious Process

## Objective

Detect outbound network connections initiated by commonly abused Windows processes frequently leveraged for command-and-control communication, malware execution, and post-exploitation activity.

---

## Detection Summary

| Field                  | Value                                      |
| ---------------------- | ------------------------------------------ |
| Detection Name         | Network Connection from Suspicious Process |
| Event ID               | Sysmon Event ID 3                          |
| Severity               | High                                       |
| MITRE ATT&CK Tactic    | Command and Control                        |
| MITRE ATT&CK Technique | T1071 - Application Layer Protocol         |
| Data Source            | Sysmon                                     |

---

## Detection Logic

This detection identifies external network connections initiated by processes commonly abused by attackers.

Monitored processes include:

* powershell.exe
* cmd.exe
* wscript.exe
* cscript.exe
* mshta.exe
* rundll32.exe
* regsvr32.exe

The rule excludes:

* RFC1918 private networks
* Localhost traffic

This allows the detection to focus on outbound communications to external destinations.

---

## SPL Query

```spl
index=pc1 sourcetype=WinEventLog LogName="Microsoft-Windows-Sysmon/Operational" EventCode=3
| `pc1_sysmon_process_normalization`
| eval process_lower=lower(process_name)
| where process_lower IN (
    "powershell.exe",
    "cmd.exe",
    "wscript.exe",
    "cscript.exe",
    "mshta.exe",
    "rundll32.exe",
    "regsvr32.exe"
)
| where NOT cidrmatch("10.0.0.0/8", DestinationIp)
| where NOT cidrmatch("172.16.0.0/12", DestinationIp)
| where NOT cidrmatch("192.168.0.0/16", DestinationIp)
| where DestinationIp!="127.0.0.1"
| eval alert_name="Network Connection from Suspicious Process"
| eval severity="high"
| eval mitre_tactic="Command and Control"
| eval mitre_technique="T1071"
```

---

## Detection Logic Explanation

Attackers frequently abuse legitimate Windows binaries to establish outbound communications.

This detection focuses on identifying:

* PowerShell-based C2 channels
* Living-off-the-Land (LotL) activity
* Script-based malware
* Suspicious external communications
* Potential beaconing behavior

---

## Validation Procedure

1. Launch PowerShell.
2. Connect to an external host.
3. Generate Sysmon Event ID 3.
4. Verify event ingestion.
5. Confirm alert generation.

---

## MITRE ATT&CK Mapping

| Technique ID | Technique                  |
| ------------ | -------------------------- |
| T1071        | Application Layer Protocol |

---

## Sample Output

![Triggered Alerts](screenshots/splunk/Triggered-Alerts.png)

---

## Lessons Learned

Network connection telemetry provides valuable visibility into post-exploitation activity. Monitoring outbound communications from commonly abused administrative tools can reveal malicious behavior that may not be detected through process monitoring alone.

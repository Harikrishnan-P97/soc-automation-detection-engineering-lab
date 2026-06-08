# Failed User Login Detection

## Objective

Detect failed authentication attempts against Windows endpoints that may indicate password guessing, brute-force activity, credential misuse, or unauthorized access attempts.

---

## Detection Summary

| Field                  | Value                       |
| ---------------------- | --------------------------- |
| Detection Name         | Failed User Login           |
| Event ID               | 4625                        |
| Severity               | High                        |
| MITRE ATT&CK Tactic    | Credential Access           |
| MITRE ATT&CK Technique | T1110 - Brute Force         |
| Data Source            | Windows Security Event Logs |

---

## Log Source

Windows Security Event Log

Event ID:

```text
4625
```

This event is generated whenever a Windows authentication attempt fails.

---

## Detection Logic

```spl
index=pc1 EventCode=4625 (Logon_Type=2 OR Logon_Type=10)
| `pc1_auth_normalization`
| where isnotnull(user)
| where NOT user IN ("SYSTEM","LOCAL SERVICE","NETWORK SERVICE","-")
| where NOT match(user,"^(DWM-|UMFD-)")
| eval Login_Type=case(logon_type=2,"Interactive",logon_type=10,"RDP")
| eval alert_name="Failed User Login"
| eval severity="high"
| eval mitre_tactic="Credential Access"
| eval mitre_technique="T1110"
| eval risk_score=70
| table _time dest_host user Login_Type src_ip Failure_Reason
```

---

## Detection Logic Explanation

The detection identifies failed authentication events while filtering out:

* System accounts
* Service accounts
* Desktop Window Manager accounts
* User Mode Font Driver accounts

The rule focuses on:

* Interactive logons
* Remote Desktop (RDP) logons

This helps reduce noise and prioritize user-driven authentication failures.

---

## Validation Procedure

1. Attempt login using an invalid password.
2. Generate Windows Event ID 4625.
3. Verify the event is ingested into Splunk.
4. Confirm the detection generates an alert.

---

## Expected Alert Output

The alert should contain:

* Username
* Destination Host
* Source IP Address
* Login Type
* Failure Reason
* Severity
* MITRE ATT&CK Mapping

---

## MITRE ATT&CK Mapping

| Technique ID | Technique   |
| ------------ | ----------- |
| T1110        | Brute Force |

---

## Lessons Learned

Authentication failures generate valuable telemetry for identifying brute-force activity and unauthorized access attempts. Proper filtering significantly reduces noise while maintaining visibility into potentially malicious behavior.

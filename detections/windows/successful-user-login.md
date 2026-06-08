# Successful User Login Detection

## Objective

Detect successful authentication events to provide visibility into user access activity and support investigation workflows.

---

## Detection Summary

| Field                  | Value                       |
| ---------------------- | --------------------------- |
| Detection Name         | Successful User Login       |
| Event ID               | 4624                        |
| Severity               | Medium                      |
| MITRE ATT&CK Tactic    | Initial Access              |
| MITRE ATT&CK Technique | T1078 - Valid Accounts      |
| Data Source            | Windows Security Event Logs |

---

## Log Source

Windows Security Event Log

Event ID:

```text
4624
```

This event is generated whenever a Windows authentication attempt succeeds.

---

## Detection Logic

```spl
index=pc1 EventCode=4624 (Logon_Type=2 OR Logon_Type=10)
| `pc1_auth_normalization`
| where isnotnull(user)
| where NOT user IN ("SYSTEM","LOCAL SERVICE","NETWORK SERVICE","-")
| where NOT match(user,"^(DWM-|UMFD-)")
| eval Login_Type=case(logon_type=2,"Interactive",logon_type=10,"RDP")
| eval alert_name="Successful User Login"
| eval severity="medium"
| eval mitre_tactic="Initial Access"
| eval mitre_technique="T1078"
| table _time dest_host user Login_Type src_ip
```

---

## Detection Logic Explanation

The detection identifies successful user authentication activity and filters out common system-generated logons.

The rule monitors:

* Interactive logins
* Remote Desktop (RDP) logins

Successful login visibility is useful for:

* Account monitoring
* Access tracking
* Incident investigations
* Correlation with suspicious activity

---

## Validation Procedure

1. Log in successfully to the Windows endpoint.
2. Generate Windows Event ID 4624.
3. Verify ingestion into Splunk.
4. Confirm alert generation.

---

## Expected Alert Output

The alert should contain:

* Username
* Destination Host
* Source IP
* Login Type
* Severity
* ATT&CK Mapping

---

## MITRE ATT&CK Mapping

| Technique ID | Technique      |
| ------------ | -------------- |
| T1078        | Valid Accounts |

---

## Lessons Learned

Successful authentication events provide important context during investigations and can be correlated with other detections to identify compromised accounts, lateral movement, or unauthorized access activity.

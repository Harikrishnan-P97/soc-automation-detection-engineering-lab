# Possible Brute Force Attack Detection

## Objective

Detect repeated failed authentication attempts that may indicate password guessing, credential stuffing, or brute-force activity against Windows systems.

---

## Detection Summary

| Field                  | Value                       |
| ---------------------- | --------------------------- |
| Detection Name         | Possible Brute Force Attack |
| Event ID               | 4625                        |
| Severity               | Critical                    |
| MITRE ATT&CK Tactic    | Credential Access           |
| MITRE ATT&CK Technique | T1110 - Brute Force         |
| Data Source            | Windows Security Event Logs |

---

## Detection Logic

This detection identifies users generating three or more failed login attempts within a five-minute period.

The rule focuses on:

* Interactive logons
* Remote Desktop (RDP) logons
* User-generated authentication failures

System and service accounts are excluded to reduce false positives.

---

## SPL Query

```spl
index=pc1 EventCode=4625 (Logon_Type=2 OR Logon_Type=10)
| `pc1_auth_normalization`
| where isnotnull(user)
| where NOT user IN ("SYSTEM","LOCAL SERVICE","NETWORK SERVICE","-")
| where NOT match(user,"^(DWM-|UMFD-)")
| bucket span=5m _time
| stats count values(src_ip) as src_ip by _time dest user logon_type
| where count >= 3
| eval Login_Type=case(logon_type=2,"Interactive",logon_type=10,"RDP")
| eval alert_name="Possible Brute Force Attack"
| eval severity="critical"
| eval mitre_tactic="Credential Access"
| eval mitre_technique="T1110"
```

---

## Detection Logic Explanation

The rule aggregates failed login events over five-minute windows and generates an alert whenever a user account experiences three or more failures.

This helps identify:

* Password guessing attacks
* Brute-force attempts
* Misconfigured authentication tools
* Unauthorized access attempts

---

## Validation Procedure

1. Attempt multiple failed logins against a Windows account.
2. Generate Event ID 4625 repeatedly.
3. Verify aggregation occurs within five minutes.
4. Confirm alert generation.

---

## MITRE ATT&CK Mapping

| Technique ID | Technique   |
| ------------ | ----------- |
| T1110        | Brute Force |

---

## Sample Output

Insert screenshot:

```text
screenshots/splunk/Port-Scanning-Detection-Suricata.png
```

(Replace with your actual brute-force screenshot if available.)

---

## Lessons Learned

Authentication telemetry can provide early indicators of attacker activity. Aggregating multiple failed login events significantly improves detection fidelity compared to alerting on individual failures.

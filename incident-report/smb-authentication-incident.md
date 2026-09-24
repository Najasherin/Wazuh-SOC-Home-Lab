# SOC Incident Report - Repeated SMB Authentication Failures

## 1. Incident Summary

A controlled authentication attack simulation was performed from Kali Linux against a Windows 10 endpoint.

Multiple incorrect SMB authentication attempts were submitted against a Windows account.

Windows generated Event ID 4625, and Wazuh detected the activity using Rule 60122.

The test was performed entirely inside the isolated home lab.

---

## 2. Incident Details

| Field | Value |
|---|---|
| Source | Kali Linux |
| Source IP | `10.0.2.4` |
| Target | Windows 10 |
| Target IP | `10.0.2.8` |
| Event | `4625` |
| Wazuh Rule | `60122` |
| Rule Level | `5` |
| Logon Type | `3` |
| Authentication | `NTLM` |
| Logon Process | `NtLmSsp` |

---

## 3. Timeline

| Time | Activity |
|---|---|
| ~23:16 | Initial failed SMB authentication |
| 23:16–23:20 | Multiple Event 4625 events generated |
| 23:16–23:20 | Wazuh Rule 60122 detected failures |
| 23:20:09 | Latest investigated failed authentication event |
| After detection | Wazuh alert investigated |

---

## 4. Investigation

The source address was identified as:

```text
10.0.2.4
```

This corresponded to the Kali VM used for the controlled attack simulation.

The target endpoint was:

```text
10.0.2.8
```

The authentication event showed:

```text
Event ID: 4625
Logon Type: 3
Authentication Package: NTLM
Logon Process: NtLmSsp
```

The failure status was:

```text
0xC000006D
```

with sub-status:

```text
0xC000006A
```

The Windows event did not provide a useful caller process:

```text
Process ID: 0x0
Process Name: -
```

Therefore, no process was inferred.

---

## 5. Assessment

The evidence demonstrates repeated failed network authentication attempts originating from the Kali lab machine.

The activity matched the controlled SMB authentication test.

There was no evidence of successful authentication or account compromise in the investigated events.

---

## 6. Response

For a real production incident, an analyst could:

1. Validate the source IP.
2. Review surrounding Event 4625 events.
3. Search for successful Event 4624 logons.
4. Investigate the targeted account.
5. Investigate the source endpoint.
6. Apply appropriate account protection measures if malicious activity is confirmed.

No production response was required because this was an intentional lab exercise.

---

## 7. SOC Workflow Demonstrated

```text
Generate Event
      ↓
Detect Alert
      ↓
Investigate
      ↓
Identify Source
      ↓
Identify Target
      ↓
Extract Evidence
      ↓
Build Timeline
      ↓
Document Incident
```

---

## 8. Conclusion

The Wazuh home lab successfully demonstrated an end-to-end SOC investigation of repeated Windows authentication failures.

The investigation identified the source IP, target endpoint, authentication method, Windows event, Wazuh rule and available process information.

The activity was intentionally generated within the controlled lab environment.

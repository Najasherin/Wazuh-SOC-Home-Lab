# SMB Authentication Attack Simulation

## Objective

Generate repeated failed SMB authentication attempts from Kali against Windows and investigate the resulting Wazuh alerts.

## Lab Systems

```text
Kali:
10.0.2.4

Windows:
10.0.2.8
```

## Initial Failed Authentication

The first controlled failed SMB authentication was generated using:

```bash
smbclient -L //10.0.2.8 -U 'najas%WrongPassword123!'
```

The authentication failed as expected.

## Repeated Attempts

Multiple controlled failed authentication attempts were then generated:

```bash
for i in {1..5}; do
  smbclient -L //10.0.2.8 -U "najas%WrongPassword$i" >/dev/null 2>&1
  sleep 2
done
```

## Windows Detection

Windows generated:

```text
Event ID: 4625
```

with the failure reason:

```text
Unknown user name or bad password
```

## Wazuh Detection

Wazuh detected the failed authentication activity using:

```text
Rule ID: 60122
Rule Level: 5
```

Description:

```text
Logon Failure - Unknown user or bad password
```

Six matching events were observed during the investigation.

## Investigation

The final investigated event showed:

```text
Source IP:          10.0.2.4
Target Host:        DESKTOP-7BBN068
Target Account:     najas
Event ID:           4625
Logon Type:         3
Authentication:     NTLM
Logon Process:      NtLmSsp
Source Port:        39040
Status:             0xC000006D
Sub-status:         0xC000006A
```

## Process Information

The event contained:

```text
Caller Process ID: 0x0
Caller Process Name: -
```

Therefore, the process was not identifiable from this event.

## Result

The test successfully demonstrated:

```text
Kali
  ↓
SMB authentication failures
  ↓
Windows Event 4625
  ↓
Wazuh Rule 60122
  ↓
Threat Hunting
  ↓
Alert Investigation
```

No successful account compromise was demonstrated.

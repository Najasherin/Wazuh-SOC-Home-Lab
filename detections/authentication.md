# Windows Authentication Monitoring

## Objective

Detect failed Windows authentication attempts using Wazuh.

## Windows Event

```text
Event ID: 4625
```

Event 4625 represents a failed logon attempt.

## Wazuh Rule

```text
Rule ID: 60122
Rule Level: 5
```

Description:

```text
Logon Failure - Unknown user or bad password
```

## Initial Test

A controlled incorrect password was entered against the Windows endpoint.

The resulting Windows Event 4625 was collected by the Wazuh Agent.

## Investigation Fields

The following fields were examined:

- Source IP
- Target username
- Event ID
- Logon type
- Authentication package
- Source port
- Failure status
- Wazuh rule

## Result

Wazuh successfully detected Windows authentication failures.

This detection was later used in the SMB authentication attack simulation.

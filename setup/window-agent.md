# Windows Wazuh Agent Setup

## Windows Endpoint

Windows 10 was configured as the monitored endpoint.

```text
IP: 10.0.2.8
Agent ID: 004
Agent Name: DESKTOP-7BBN068
```

## Wazuh Manager

The agent was configured to communicate with:

```text
Manager: 10.0.2.9
Port: 1514/TCP
```

## Connectivity Test

From Windows PowerShell:

```powershell
Test-NetConnection 10.0.2.9 -Port 1514
```

The test returned:

```text
TcpTestSucceeded : True
```

## Agent Verification

The Wazuh Agent service was verified as running.

The Wazuh Manager also showed Agent `004` as active.

## Result

The Windows endpoint successfully communicated with the Wazuh Manager and began sending security telemetry.

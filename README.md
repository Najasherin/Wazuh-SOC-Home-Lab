# Wazuh SOC Home Lab

A hands-on SOC home lab built using **Wazuh, Ubuntu Server, Windows 10, Kali Linux, and VirtualBox**.

This project demonstrates endpoint monitoring, security event collection, File Integrity Monitoring (FIM), Windows authentication monitoring, PowerShell detection, registry monitoring, network reconnaissance, controlled SMB authentication attacks, alert investigation, and incident reporting.

---

## Lab Architecture

```text
                  VirtualBox NAT Network
                       10.0.2.0/24

        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
   Kali Linux        Windows 10       Ubuntu Server
   10.0.2.4          10.0.2.8          10.0.2.9
   Attacker          Endpoint          Wazuh SIEM
```

### Components

| System | Role | IP |
|---|---|---|
| Kali Linux | Attack simulation | `10.0.2.4` |
| Windows 10 | Monitored endpoint | `10.0.2.8` |
| Ubuntu Server | Wazuh Manager / Indexer / Dashboard | `10.0.2.9` |

A VirtualBox Host-only adapter was also configured on Ubuntu to allow access to the Wazuh Dashboard from the physical host.

---

## Technologies

- Wazuh
- Ubuntu Server
- Windows 10
- Kali Linux
- VirtualBox
- PowerShell
- Nmap
- SMB / smbclient
- Windows Event Logs
- File Integrity Monitoring
- Threat Hunting

---

## Lab Workflow

```text
Configure Wazuh
      ↓
Install Windows Agent
      ↓
Collect Windows Telemetry
      ↓
Test FIM
      ↓
Detect Authentication Failures
      ↓
Monitor PowerShell
      ↓
Monitor Registry
      ↓
Configure Kali
      ↓
Perform Nmap Reconnaissance
      ↓
Simulate SMB Authentication Failures
      ↓
Investigate Wazuh Alert
      ↓
Build Timeline
      ↓
Write Incident Report
```

---

## Detection Scenarios

### File Integrity Monitoring

Monitored:

```text
C:\Users\Wazuh Test
```

Tested:

- File creation
- File modification
- File deletion

### Windows Authentication

Detected:

```text
Event ID: 4625
Wazuh Rule: 60122
```

### PowerShell

Configured PowerShell Operational logging and Script Block Logging.

Detected:

```text
Event ID: 4104
Rule: 91815
```

for PowerShell process discovery.

### Registry

Tested Windows Registry Integrity Monitoring using Wazuh Syscheck.

### Network Reconnaissance

Performed:

```bash
nmap -sV 10.0.2.8
```

### SMB Authentication Attack

Generated repeated failed SMB authentication attempts from Kali against Windows.

Detected:

```text
Windows Event: 4625
Wazuh Rule: 60122
```

---

## Final SOC Investigation

The final investigation identified:

```text
Source IP:       10.0.2.4
Target IP:       10.0.2.8
Target Account:  lab Windows account
Event ID:        4625
Wazuh Rule:      60122
Logon Type:      3
Authentication:  NTLM
Logon Process:   NtLmSsp
```

The exercise demonstrated the complete SOC workflow:

```text
Generate Event
     ↓
Detect
     ↓
Investigate
     ↓
Identify Source / Target
     ↓
Extract Evidence
     ↓
Build Timeline
     ↓
Document Incident
```

---

## Key Learning Outcomes

- Wazuh SIEM deployment
- Windows endpoint onboarding
- Windows event monitoring
- File Integrity Monitoring
- Authentication event investigation
- PowerShell telemetry
- Registry monitoring
- Network reconnaissance
- SMB authentication monitoring
- Threat Hunting
- Incident timeline creation
- SOC incident reporting

---

## Disclaimer

All security testing was performed against intentionally configured virtual machines in a controlled home lab environment.

No production systems were targeted.

# Nmap Network Reconnaissance

## Objective

Perform controlled network reconnaissance from Kali against the Windows lab endpoint.

## Source

```text
Kali Linux
10.0.2.4
```

## Target

```text
Windows 10
10.0.2.8
```

## Command

```bash
nmap -sV 10.0.2.8
```

## Results

The scan identified:

```text
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
```

Nmap also identified the target as a Microsoft Windows system.

## Wazuh Observation

The Nmap scan did not generate a direct reconnaissance alert in the current Wazuh Windows endpoint configuration.

This demonstrates that endpoint telemetry alone does not provide complete network packet visibility.

## Result

The reconnaissance activity was successfully performed and documented, but no direct Wazuh reconnaissance alert was generated.

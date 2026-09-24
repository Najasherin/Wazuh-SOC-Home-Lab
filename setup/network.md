# Network Setup

## VirtualBox Network

The three virtual machines were connected to the same **NAT Network**.

```text
NAT Network
10.0.2.0/24

Kali
10.0.2.4
   |
   +---- Windows
   |     10.0.2.8
   |
   +---- Ubuntu/Wazuh
         10.0.2.9
```

## Final IP Addresses

| VM | IP | Role |
|---|---|---|
| Kali | `10.0.2.4` | Attacker simulation |
| Windows 10 | `10.0.2.8` | Wazuh endpoint |
| Ubuntu | `10.0.2.9` | Wazuh server |

## Ubuntu Host-only Adapter

A second Host-only adapter was added to Ubuntu so the physical host could access the Wazuh Dashboard.

The NAT Network configuration was kept unchanged.

## Connectivity Test

From Kali:

```bash
ping -c 4 10.0.2.8
```

The Windows endpoint responded successfully.

## Kali IP Verification

```bash
ip -4 addr show eth0
```

Result:

```text
inet 10.0.2.4/24
```

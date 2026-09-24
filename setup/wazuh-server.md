# Wazuh Server Setup

## Ubuntu Server

Ubuntu Server was used as the Wazuh server.

VM resources:

```text
RAM: 8 GB
CPU: 4 cores
Disk: 50 GB
```

The VM disk was expanded during the setup to provide sufficient storage.

## Wazuh Installation

The Wazuh all-in-one installation was performed using:

```bash
sudo bash ./wazuh-install.sh -a -i
```

This installed the main Wazuh components:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Filebeat

## Dashboard

The Wazuh Dashboard was accessed through the Ubuntu Host-only interface.

```text
https://<Ubuntu-Host-Only-IP>
```

The exact private host-only address is intentionally not documented here.

## Result

The Wazuh server was successfully deployed and used as the central SIEM for the lab.

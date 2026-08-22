# Cloud Infrastructure

## Overview

The cloud portion of the lab is hosted on Oracle Cloud Infrastructure (OCI).

The OCI environment provides the remote infrastructure required for the hybrid SOC architecture and hosts the Ubuntu CLI testing system and Wazuh SIEM.

## OCI Network

The cloud environment consists of:

- OCI VCN
- Ubuntu CLI instance
- Wazuh Server instance
- Tailscale connectivity

## OCI Instances

### Ubuntu CLI Instance

The Ubuntu CLI instance is used for controlled security testing.

Kali Linux runs through Docker on this instance.

The environment is used to:

- Generate controlled security traffic
- Perform SSH testing
- Test connectivity
- Execute security tools
- Interact with the lab environment

### Wazuh Server Instance

The second OCI instance hosts the Wazuh Server/SIEM.

It provides:

- Centralized log collection
- Security event monitoring
- Alert generation
- Detection engineering
- Investigation capabilities

## Tailscale Connectivity

The OCI instances are connected to the local lab through Tailscale.

Tailscale provides private connectivity between the local environment and OCI while bypassing the ISP CGNAT limitation.

```text
Local Lab
   |
   | Tailscale VPN
   | CGNAT Bypass
   v
OCI VCN
   |
   +-------------------+
   |                   |
   v                   v
Ubuntu CLI         Wazuh Server
Instance           Instance
   |                   |
Kali via Docker    Wazuh SIEM

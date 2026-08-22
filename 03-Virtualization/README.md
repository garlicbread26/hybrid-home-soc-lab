# Virtualization

## Overview

The local SOC environment runs on a Windows physical host using VMware Workstation Pro.

VMware provides the virtualization layer for the local security infrastructure and allows the lab to operate multiple isolated systems on the same physical machine.

## Physical Host

- Windows host machine
- VMware Workstation Pro

## Virtual Machines

### pfSense

pfSense runs as a virtual firewall and provides the primary network security layer for the local lab.

It includes:

- Firewall
- Guest VLAN
- Suricata IDS/IPS
- pfBlockerNG
- Syslog-based security telemetry

### Ubuntu Desktop

An Ubuntu Desktop VM operates inside the guest VLAN.

It is used as:

- Test endpoint
- Defender/test system
- Controlled target for security testing
- Source of endpoint and network activity

## Virtualization Layout

```text
Windows Physical Host
        |
        v
VMware Workstation Pro
        |
        +----------------------+
        |                      |
        v                      v
   pfSense VM          Ubuntu Desktop VM
        |                      |
        |                      |
   Firewall / IDS         Test / Defender
   pfBlockerNG             Guest VLAN
        |
        |
   Tailscale Connectivity
        |
        v
      OCI VCN

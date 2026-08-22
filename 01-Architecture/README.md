# Hybrid Home SOC Lab — Architecture

## Overview

This lab is a hybrid home Security Operations Center (SOC) environment combining on-premises virtualization and network security with cloud infrastructure.

The lab currently consists of:

- Windows physical host
- VMware Workstation Pro
- pfSense firewall
- Suricata IDS/IPS
- pfBlockerNG
- Ubuntu Desktop test/defender VM
- Oracle Cloud Infrastructure (OCI) VCN
- Two OCI compute instances
- Tailscale VPN for private connectivity and CGNAT bypass
- Kali Linux running through Docker
- Wazuh Server / SIEM
- Windows Sysmon telemetry
- Wazuh Agent
- pfSense Syslog telemetry

## Network Architecture

```text
                         INTERNET
                            |
                            |
                  +--------------------+
                  |   Windows Host     |
                  |   Physical Laptop  |
                  |                    |
                  | VMware Workstation |
                  +---------+----------+
                            |
                     +------+------+
                     |   pfSense   |
                     |  Firewall   |
                     |            |
                     |  Suricata  |
                     | pfBlockerNG|
                     +------+------+
                            |
                     Local Lab Network
                            |
                   +--------+--------+
                   |                 |
          +--------+-------+   +-----+----------+
          | Ubuntu Desktop |   | Windows Host   |
          | Test/Defender  |   | Sysmon         |
          | VM             |   | Wazuh Agent    |
          +----------------+   +----------------+

                            |
                       Tailscale VPN
                       CGNAT Bypass
                            |
                            |
                 +----------+-----------+
                 |       OCI VCN        |
                 |                      |
        +--------+---------+  +---------+--------+
        | Ubuntu CLI       |  | Wazuh Server     |
        | OCI Instance     |  | OCI Instance     |
        |                  |  |                  |
        | Kali via Docker  |  | Wazuh SIEM       |
        +------------------+  +------------------+

## Architecture Components

### Windows Physical Host

The Windows laptop is the physical host for the on-premises portion of the lab.

VMware Workstation Pro runs the local virtual infrastructure on this host.

### VMware Workstation Pro

VMware provides the virtualization layer for the local lab.

The main virtual systems are:

- pfSense firewall
- Ubuntu Desktop test/defender VM

### pfSense Security Layer

pfSense acts as the network security gateway for the local environment.

Security services deployed on pfSense include:

- Suricata IDS/IPS
- pfBlockerNG
- Firewall rules
- Guest VLAN
- Syslog forwarding

### Guest VLAN

The Ubuntu Desktop test/defender VM is placed behind pfSense on the Guest VLAN.

This provides an isolated environment for generating and observing security activity.

### Tailscale VPN

Tailscale provides private connectivity between the on-premises lab and OCI.

It is used to overcome the CGNAT limitation of the home Internet connection.

The connection path is:

```text
Local Lab
    |
  pfSense
    |
Tailscale
    |
  OCI VCN

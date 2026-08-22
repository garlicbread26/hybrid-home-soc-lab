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
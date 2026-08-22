# Network Infrastructure

## Overview

The local network infrastructure is built around a pfSense firewall running as a virtual machine on VMware Workstation Pro.

pfSense provides the primary network security and traffic-control layer for the home SOC lab.

## Network Components

- Windows physical host
- VMware Workstation Pro
- pfSense firewall VM
- Suricata IDS/IPS
- pfBlockerNG
- Guest VLAN
- Ubuntu Desktop test/defender VM
- Tailscale VPN connectivity to the OCI environment

## Network Topology

```text
                         INTERNET
                            |
                            |
                    +---------------+
                    | Windows Host  |
                    |               |
                    | VMware        |
                    | Workstation   |
                    +-------+-------+
                            |
                            |
                    +-------+-------+
                    |    pfSense    |
                    |   Firewall    |
                    |               |
                    |   Suricata    |
                    |  pfBlockerNG  |
                    +-------+-------+
                            |
                       Guest VLAN
                            |
                    +-------+-------+
                    | Ubuntu Desktop|
                    | Test/Defender |
                    |      VM       |
                    +---------------+

                            |
                     Tailscale VPN
                      CGNAT Bypass
                            |
                            v
                    +---------------+
                    |    OCI VCN    |
                    +-------+-------+
                            |
                 +----------+----------+
                 |                     |
          Ubuntu CLI Instance    Wazuh Instance
          Kali via Docker        Wazuh SIEM

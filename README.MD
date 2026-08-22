# Hybrid Home SOC Lab

A hybrid cybersecurity home lab built to simulate a small Security Operations Center (SOC) using on-premises virtualization, network security, cloud infrastructure, endpoint telemetry, SIEM monitoring, detection engineering, and security investigation.

## Lab Overview

The lab combines a local virtualized network environment with Oracle Cloud Infrastructure (OCI).

The current environment consists of:

- Windows physical host
- VMware Workstation Pro
- pfSense firewall
- Suricata IDS/IPS
- pfBlockerNG
- Ubuntu Desktop test/defender VM
- Oracle Cloud Infrastructure (OCI) VCN
- Tailscale VPN for CGNAT bypass and connectivity between the local lab and OCI
- Ubuntu CLI OCI instance
- Kali Linux running through Docker
- Wazuh Server / SIEM OCI instance
- Sysmon endpoint telemetry
- pfSense syslog telemetry
- Wazuh-based log collection, detection and investigation

## Network Architecture

```text
                              INTERNET
                                  |
                                  |
                    +-------------------------+
                    |     Windows Host        |
                    |                         |
                    |  VMware Workstation Pro |
                    +------------+------------+
                                 |
                                 |
                    +------------+------------+
                    |         pfSense         |
                    |                         |
                    |  Firewall               |
                    |  Suricata IDS/IPS       |
                    |  pfBlockerNG             |
                    +------------+------------+
                                 |
                         Guest VLAN / LAN
                                 |
                    +------------+------------+
                    |                         |
          +---------+---------+     +---------+---------+
          | Ubuntu Desktop   |     | Windows Host      |
          | Test / Defender  |     | Sysmon             |
          | VM               |     | Endpoint Telemetry |
          +------------------+     +--------------------+
                                           |
                                           |
                                      Security Logs


                         Tailscale VPN
                       (CGNAT Bypass)
                              |
                              |
                    +---------+---------+
                    |     OCI VCN       |
                    +---------+---------+
                       |             |
                       |             |
              +--------+-----+  +----+-------------+
              | Ubuntu CLI   |  | Wazuh Server      |
              | OCI Instance |  | OCI Instance      |
              |              |  |                   |
              | Kali via     |  | Wazuh SIEM        |
              | Docker       |  |                   |
              +--------------+  +-------------------+

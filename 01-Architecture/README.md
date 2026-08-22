# Hybrid Home SOC Lab — Architecture

## Overview

This lab is a hybrid cybersecurity environment combining local virtualization, network security, endpoint telemetry, cloud infrastructure, SIEM monitoring, security investigation, and automation.

## Architecture

```text
                         INTERNET
                            |
                            v
                 +---------------------+
                 |    Windows Host     |
                 |      Laptop         |
                 +----------+----------+
                            |
                     VMware Workstation
                            |
              +-------------+-------------+
              |                           |
              v                           v
       +-------------+             +-------------+
       |   pfSense   |             |    Ubuntu   |
       |  Firewall   |             |   Test VM   |
       +-------------+             +-------------+

                 Windows Endpoint
                        |
                     Sysmon
                        |
                   Wazuh Agent
                        |
                        | Security Telemetry
                        v
              +----------------------+
              | Oracle Cloud (Mumbai)|
              |                      |
              |    Wazuh Server      |
              |       / SIEM         |
              +----------+-----------+
                         |
                         v
                      Alerts
                         |
                         v
                    Investigation
                         |
                         v
                Detection Engineering
                         |
                         v
                     Automation
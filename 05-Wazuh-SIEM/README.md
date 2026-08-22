# Wazuh SIEM

## Overview

Wazuh is the central SIEM and security monitoring platform for the lab.

The Wazuh Server runs on an OCI instance and receives security telemetry from the lab environment for monitoring, alerting, detection and investigation.

## Deployment

The Wazuh Server is deployed as an OCI instance.

The original Wazuh deployment was provided as an OVA virtual appliance.

The VMDK was extracted from the OVA, uploaded to OCI Object Storage, and used to deploy the Wazuh instance.

## Telemetry Sources

Current telemetry sources include:

- pfSense syslog
- Windows Sysmon events
- SSH authentication activity
- Linux authentication logs
- Security-related endpoint events

## Telemetry Flow

```text
pfSense
   |
   | Syslog
   v
Wazuh Server
   |
   v
Alerts / Events
   |
   v
Investigation


Windows Host
   |
   | Sysmon
   v
Wazuh Server
   |
   v
Alerts / Events
   |
   v
Investigation

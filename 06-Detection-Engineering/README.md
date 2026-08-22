# Detection Engineering

## Overview

Detection engineering focuses on creating, testing, and improving security detections within the Wazuh SIEM.

The lab uses controlled attack activity and endpoint/network telemetry to validate detection logic.

## Detection Sources

Current detection data comes from:

- pfSense syslog
- Windows Sysmon
- SSH authentication logs
- Linux authentication activity
- Wazuh agent telemetry

## Current Detections

The lab currently focuses on detecting and investigating:

- SSH brute-force activity
- Repeated SSH authentication failures
- Suspicious authentication activity
- Suspicious process execution
- File and directory activity
- System discovery activity
- Windows security events

## Detection Workflow

```text
Controlled Security Activity
          |
          v
   Network / Endpoint
       Telemetry
          |
          v
     Wazuh Server
          |
          v
    Detection Rules
          |
          v
        Alert
          |
          v
     Investigation
          |
          v
 Detection Improvement

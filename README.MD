# Hybrid Home SOC Lab

A hybrid cybersecurity home lab designed to simulate a small Security Operations Center (SOC) environment using on-premises virtualization, network security, cloud infrastructure, endpoint telemetry, SIEM, detection engineering, investigation, and automation.

## Lab Overview

This project combines:

- VMware-based virtual machines
- pfSense network security
- Ubuntu/Linux systems
- Windows endpoint monitoring
- Wazuh SIEM/XDR
- Sysmon
- Oracle Cloud Infrastructure (OCI)
- Network segmentation
- Security event detection
- SOC investigation
- Python-based security automation

## Objectives

- Build a realistic SOC-style environment at home
- Collect security telemetry from Windows and Linux endpoints
- Detect authentication attacks and suspicious activity
- Investigate security alerts using Wazuh
- Develop custom detection logic
- Automate repetitive SOC investigation tasks
- Document the complete infrastructure and security workflow

## Architecture

The lab consists of on-premises virtualized systems connected with cloud infrastructure hosted on OCI.

## Security Monitoring

Wazuh acts as the central SIEM/security monitoring platform.

Endpoint telemetry includes:

- Windows Security Events
- Sysmon events
- Linux authentication logs
- SSH authentication activity
- Process and discovery activity

## Detection Engineering

Custom Wazuh rules and alert analysis are used to identify suspicious activity such as:

- SSH brute-force attacks
- Suspicious PowerShell activity
- Suspicious process execution
- File/directory deletion
- System discovery activity

## SOC Investigation

Detected events are investigated using Wazuh alerts and supporting logs.

The lab also includes Python automation for generating structured SOC incident reports from security telemetry.

## Status

🚧 Actively developing and documenting the lab.
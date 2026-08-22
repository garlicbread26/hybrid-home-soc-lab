# SOC Investigation

## Overview

This section documents the investigation workflow used to analyze security events detected by Wazuh.

The current lab focuses on authentication attacks, endpoint activity, and centralized security event analysis.

## Investigation Workflow

```text
Security Activity
       |
       v
Telemetry Collection
       |
       v
Wazuh Alert
       |
       v
Alert Analysis
       |
       v
Source Identification
       |
       v
Timeline Analysis
       |
       v
Target / User Analysis
       |
       v
Incident Classification
       |
       v
Recommended Action

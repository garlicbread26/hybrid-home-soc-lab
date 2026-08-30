# 08 · SOC Alert Automation

## Overview

The lab was extended with an automated alert-notification pipeline using **Wazuh, n8n and Telegram**.

The objective was to move from simply detecting security events in Wazuh to automatically delivering high-priority alerts to a SOC notification channel.

### Alert Flow

Wazuh SIEM  
↓  
Wazuh Integration  
↓  
n8n Webhook  
↓  
Alert Processing / Field Mapping  
↓  
Telegram Bot  
↓  
SOC Alert Notification

---

## Components

| Component | Purpose |
|---|---|
| Wazuh | Security event detection and alert generation |
| Wazuh Integrator | Sends selected alerts to the automation endpoint |
| n8n | Receives, processes and routes alerts |
| Webhook | HTTP endpoint receiving Wazuh alert data |
| Edit Fields | Extracts and formats relevant alert information |
| Telegram Bot | Delivers the final SOC notification |

---

## n8n Workflow

The n8n workflow contains the following stages:

### 1. Webhook

The workflow starts with an n8n Webhook node.

Wazuh sends the alert payload to this endpoint when a matching security event occurs.

### 2. Alert Processing

The incoming JSON alert is processed to extract important SOC fields such as:

- Alert type
- Rule ID
- Source IP
- Target user
- Timestamp
- Severity / rule information

### 3. Telegram Notification

The processed alert is passed to a Telegram node using the `sendMessage` operation.

Example notification:

> 🚨 WAZUH SOC ALERT  
> Alert Type: SSH Brute Force  
> Rule ID: 100014  
> Source IP: 192.168.10.2  
> Target User: fakeuser

The message is automatically delivered to the configured Telegram SOC alert channel.

---

## Validation

The automation was validated using a controlled SSH brute-force simulation.

Wazuh generated the expected detection:

```text
Alert Type: SSH Brute Force
Rule ID: 100014
Source IP: 192.168.10.2
Target User: fakeuser

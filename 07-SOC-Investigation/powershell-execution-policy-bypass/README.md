# PowerShell ExecutionPolicy Bypass Detection

## 1. Overview

This investigation demonstrates the detection and analysis of suspicious PowerShell execution using the `-ExecutionPolicy Bypass` parameter.

The activity was generated on the Windows endpoint `LAPTOP-9Q4DP3FV` and detected by Wazuh using Microsoft Sysmon telemetry and a custom detection rule.

## 2. Detection Summary

| Field | Value | Description |
|---|---|---|
| Telemetry | Microsoft Sysmon | Windows process creation telemetry |
| Event | Event ID 1 | Process Creation |
| Detection | Rule 100015 | Custom Wazuh detection |
| MITRE ATT&CK | T1059.001 | PowerShell |

## 3. Detection Logic

The detection uses Wazuh rule `100015` to identify PowerShell process creation events containing the `-ExecutionPolicy Bypass` parameter.

The rule is based on Wazuh rule `92027` and matches the PowerShell command line using a PCRE2 expression.

```xml
<rule id="100015" level="10">
    <if_sid>92027</if_sid>
    <field name="win.eventdata.commandLine" type="pcre2">(?i)-ExecutionPolicy\s+Bypass</field>
    <description>Suspicious PowerShell execution detected: ExecutionPolicy Bypass</description>
    <group>windows,powershell,execution,</group>
    <mitre>
        <id>T1059.001</id>
    </mitre>
</rule>
## 4. Attack Simulation

The detection was validated by executing PowerShell with the `-ExecutionPolicy Bypass` parameter:

```powershell
powershell.exe -NoProfile -Command "Get-Process"

## 5. Detection Validation

The generated Sysmon event was successfully received by the Wazuh agent and processed by the Wazuh manager.

The event was identified as:

- **Sysmon Event ID:** 1 — Process Creation
- **Command:** PowerShell with `-ExecutionPolicy Bypass`
- **Custom Rule:** 100015
- **Alert Level:** 10
- **MITRE ATT&CK:** T1059.001 — PowerShell

The alert was visible in the Wazuh dashboard and repeatedly triggered during testing.

## 6. Investigation Evidence

The Wazuh alert provided process-level telemetry including the executable path, command line, user, integrity level, parent process, process ID, timestamp, and SHA256 hash.

This allowed the activity to be investigated from the original Sysmon process creation event through the resulting Wazuh alert.

## 7. Investigation Findings

The investigation confirmed that the detected activity was a PowerShell process created with `-ExecutionPolicy Bypass`.

Key findings:

- PowerShell executed with elevated integrity.
- The process originated from the standard Windows PowerShell executable.
- The command executed was `Get-Process`.
- Wazuh correlated the Sysmon event with custom rule `100015`.
- The alert was classified under MITRE ATT&CK `T1059.001 — PowerShell`.

The activity demonstrates how endpoint telemetry can be used to detect potentially suspicious PowerShell execution and support further SOC investigation.

## 8. Evidence

The investigation was validated using:

1. Sysmon Event ID 1 process creation telemetry.
2. Wazuh custom detection rule `100015`.
3. Wazuh alert details and process metadata.
4. Wazuh Threat Hunting / Discover views.
5. PowerShell process execution output.

## 9. Conclusion

This investigation demonstrates an end-to-end SOC detection workflow using Sysmon and Wazuh.

The activity was generated on the Windows endpoint, collected through Sysmon, analyzed by Wazuh, and detected using a custom rule mapped to MITRE ATT&CK T1059.001.

The investigation provides visibility into suspicious PowerShell execution and demonstrates the use of endpoint telemetry for SOC threat detection and investigation.

## 10. Evidence Screenshots

### 10.1 PowerShell Execution
PowerShell process execution with `-ExecutionPolicy Bypass`.

### 10.2 Wazuh Alert
Wazuh detected the activity using custom rule `100015` with alert level `10`.

### 10.3 Alert Details
Wazuh alert metadata showing the command line, process information, user, integrity level, and SHA256 hash.

### 10.4 Custom Rule
Wazuh rule `100015` and its detection logic based on rule `92027`.

### 10.5 Threat Hunting
Threat Hunting view showing repeated detections from the Windows endpoint.

### 10.6 Process Output
PowerShell `Get-Process` output generated during the detection test.

## 11. SOC Detection Workflow

The investigation followed this workflow:

1. PowerShell activity was executed on the Windows endpoint.
2. Sysmon generated Event ID 1 process creation telemetry.
3. The Wazuh agent forwarded the event to the Wazuh manager.
4. Wazuh rule `92027` identified the PowerShell process activity.
5. Custom rule `100015` matched the `-ExecutionPolicy Bypass` parameter.
6. Wazuh generated a Level 10 security alert.
7. The alert was investigated using Wazuh Discover and Threat Hunting.
8. Process and command-line telemetry were reviewed to determine the nature of the activity.

## 12. MITRE ATT&CK Mapping

| Technique | ID | Description |
|---|---|---|
| PowerShell | T1059.001 | Command and scripting interpreter: PowerShell |

## 13. Detection Engineering Notes

The custom detection rule was designed as a child rule of Wazuh rule `92027`.

The rule uses a PCRE2 expression to identify the `-ExecutionPolicy Bypass` parameter in the PowerShell command line.

This approach allows the detection to focus specifically on suspicious PowerShell execution while retaining the context provided by the underlying Sysmon event.

## 14. Investigation Outcome

**Detection:** Successful  
**Telemetry:** Sysmon Event ID 1  
**Wazuh Rule:** 100015  
**Alert Level:** 10  
**MITRE ATT&CK:** T1059.001  
**Endpoint:** LAPTOP-9Q4DP3FV

## 15. Lessons Learned

- Sysmon provides detailed endpoint process telemetry.
- Wazuh can correlate Windows events with custom detection rules.
- Command-line monitoring is valuable for detecting suspicious PowerShell activity.
- Custom rules can extend built-in SIEM detection capabilities.
- Alert investigation requires reviewing both the detection and the underlying process context.

## 16. Final Status

**Status: Detection Successfully Implemented and Validated**

The PowerShell `-ExecutionPolicy Bypass` activity was successfully detected by Wazuh using custom rule `100015`.

The investigation confirmed the complete detection path from Windows endpoint telemetry through Sysmon and Wazuh to the final SOC alert.


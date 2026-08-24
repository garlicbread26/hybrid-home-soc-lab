# Incident 01 — SSH Brute-Force Attack

## 1. Incident Overview

A simulated SSH brute-force attack was conducted against the Ubuntu
endpoint `admin` (Wazuh Agent 002) in the SOC home lab.

Wazuh detected repeated failed SSH authentication attempts and generated
custom Rule `100014` with severity level 10.

No successful SSH authentication was observed during the investigation.

---

## 2. Affected Host

| Field | Value |
|---|---|
| Hostname | admin |
| Agent ID | 002 |
| Operating System | Ubuntu Linux |
| Wazuh Version | 4.14.7 |
| IP Address | 192.168.20.100 |
| Service | SSH |
---

## 3. Detection

The SSH brute-force activity was detected by Wazuh through custom
Rule `100014`.

| Field | Value |
|---|---|
| Rule ID | 100014 |
| Severity | Level 10 |
| Description | SSH brute-force authentication attempt detected |
| MITRE ATT&CK | T1110 |
| Tactic | Credential Access |
| Technique | Brute Force |

Wazuh generated multiple alerts for this rule after observing repeated
failed SSH authentication attempts against the `admin` endpoint.

---

## 4. Evidence Collection

The triggered Wazuh alert was examined to identify the source,
target, authentication activity, and relevant event details.

### Alert Evidence

| Field | Value |
|---|---|
| Agent ID | 002 |
| Agent Name | admin |
| Agent IP | 192.168.20.100 |
| Log Source | sshd |
| Event Type | Failed SSH authentication |
| Rule ID | 100014 |
| Severity | Level 10 |
| MITRE ATT&CK | T1110 — Brute Force |

The alert contained an SSH authentication failure indicating an
attempt to authenticate using an invalid username.

The raw event data was retained as investigation evidence for
correlation with other authentication events.
---

## 5. Investigation

The investigation was performed by reviewing the Wazuh alert,
the underlying SSH authentication event, the source information,
the targeted account, and the sequence of repeated authentication
failures.

The objective was to determine:

- What system was targeted.
- Which source generated the authentication attempts.
- Which account was targeted.
- Whether authentication succeeded.
- Whether the activity was isolated or repeated.
- Whether there was evidence of successful compromise.

### 5.1 Source Analysis

The Wazuh event identified the observed source IP as:

`192.168.20.1`

The affected endpoint was:

`192.168.20.100`

The source IP represents the address observed by the target
system during the SSH authentication attempt.

The source was therefore recorded as an observed network source
rather than being automatically classified as the identity of
the attacker.

### 5.2 Target Analysis

The affected system was the Ubuntu endpoint registered in Wazuh
as agent `002`.

| Field | Value |
|---|---|
| Hostname | admin |
| Agent ID | 002 |
| IP Address | 192.168.20.100 |
| Operating System | Ubuntu Linux |
| Service | SSH |

The SSH service was the targeted authentication service.

### 5.3 Account Analysis

The authentication attempt used the username:

`fakeuser`

The Wazuh event explicitly identified this as an invalid user.

The event therefore indicates an attempt to authenticate using
a username that does not correspond to a valid account on the
target endpoint.

### 5.4 Authentication Analysis

The underlying SSH event contained the following authentication
failure:

`Failed password for invalid user fakeuser`

The event confirms that the authentication attempt failed.

No successful SSH authentication was identified during the
investigation.

This is an important distinction because the presence of
multiple authentication failures does not by itself prove that
the endpoint was compromised.

### 5.5 Repeated Activity Analysis

Multiple Wazuh alerts were generated for Rule `100014`.

The Threat Hunting view showed repeated detections within the
investigation time window.

The repeated failures indicate credential-guessing behaviour
rather than a single accidental authentication failure.

The observed pattern was:

SSH connection attempt
↓
Authentication attempt
↓
Invalid username
↓
Authentication failure
↓
Repeated attempt
↓
Wazuh detection

This behaviour is consistent with the simulated SSH brute-force
scenario.

---

## 6. Attack Timeline

The available Wazuh evidence was used to reconstruct the
sequence of events.

| Stage | Event |
|---|---|
| 1 | SSH authentication activity was generated against the Ubuntu endpoint |
| 2 | The username `fakeuser` was supplied |
| 3 | The SSH service rejected the authentication attempt |
| 4 | The failed authentication event was collected by Wazuh |
| 5 | Repeated failed authentication events were observed |
| 6 | Custom Rule `100014` generated high-severity detections |
| 7 | The events were reviewed in Wazuh Threat Hunting |
| 8 | No successful authentication was identified |

### Timeline Interpretation

The evidence shows a sequence of repeated authentication failures
against the SSH service.

The investigation did not identify evidence of a successful
credential compromise or successful SSH session.

---

## 7. Alert Correlation

The individual SSH authentication failures were correlated
through Wazuh Rule `100014`.

The correlation was based on repeated failed SSH authentication
activity.

| Correlation Field | Observed Value |
|---|---|
| Detection Rule | 100014 |
| Severity | 10 |
| Target Agent | 002 |
| Target Host | admin |
| Target IP | 192.168.20.100 |
| Source IP | 192.168.20.1 |
| Attempted Username | fakeuser |
| Service | SSH |
| Authentication Result | Failed |

The repeated events provided sufficient evidence to classify the
activity as a simulated brute-force authentication attempt.

---

## 8. MITRE ATT&CK Mapping

The activity maps to the following MITRE ATT&CK technique:

| Field | Value |
|---|---|
| Tactic | Credential Access |
| Technique | T1110 - Brute Force |
| Detection | Wazuh Rule 100014 |

The simulated activity represents repeated attempts to gain access
through credential guessing against an SSH authentication service.

---

## 9. Impact Assessment

### 9.1 Authentication Impact

Multiple authentication attempts were observed.

All investigated authentication attempts were unsuccessful.

### 9.2 Host Impact

No evidence was identified showing successful SSH access to the
affected Ubuntu endpoint.

No evidence of command execution following successful SSH
authentication was identified from the investigated events.

### 9.3 Account Impact

The attempted username was `fakeuser`.

The event identified the username as invalid.

There was therefore no evidence that the legitimate `admin`
account was successfully authenticated during this incident.

### 9.4 Compromise Assessment

Based on the collected evidence:

**Successful Authentication:** No

**Confirmed Account Compromise:** No

**Confirmed Host Compromise:** No

**Detection Status:** Successfully detected

The incident is therefore classified as an attempted attack that
was detected and did not result in confirmed compromise.

---

## 10. Investigation Conclusion

The investigation confirmed a simulated SSH brute-force attack
against the Ubuntu endpoint `admin`.

The activity consisted of repeated failed SSH authentication
attempts using the invalid username `fakeuser`.

Wazuh successfully collected the underlying SSH authentication
events and generated multiple alerts using custom Rule `100014`
with severity level 10.

The observed source IP was `192.168.20.1`, while the affected
endpoint was `192.168.20.100`.

The investigation found no evidence of successful SSH
authentication or confirmed compromise.

The incident demonstrates the complete SOC workflow:

```text
Attack Simulation
        ↓
SSH Authentication Failure
        ↓
Log Collection
        ↓
Wazuh Detection
        ↓
Alert Generation
        ↓
Evidence Collection
        ↓
Source Analysis
        ↓
Authentication Analysis
        ↓
Timeline Reconstruction
        ↓
MITRE ATT&CK Mapping
        ↓
Impact Assessment
        ↓
Investigation Conclusion
## 11. Source Analysis

The SSH authentication failures were investigated to identify the originating source.

The Wazuh event recorded the source IP as:

| Field | Value |
|---|---|
| Source IP | 192.168.20.1 |
| Destination IP | 192.168.20.100 |
| Protocol | SSH |
| Destination Service | SSH |
| Source Username | fakeuser |
| Authentication Result | Failed |

The source address `192.168.20.1` was identified as the system generating the simulated authentication attempts against the monitored Ubuntu endpoint.

---

## 12. Authentication Analysis

The raw SSH event was reviewed to determine the authentication method and result.

The event contained a failed password authentication attempt for the username `fakeuser`.

Example event pattern:

```text
Failed password for invalid user fakeuser from 192.168.20.1
## 13. Attack Pattern Analysis

Multiple SSH authentication failures were observed during the investigation window.

The activity showed repeated authentication attempts against the SSH service using the invalid username `fakeuser`.

The repeated failures from the same source were consistent with a simulated SSH brute-force attack.

The observed attack pattern was:

```text
SSH connection attempt
        ↓
Authentication attempt
        ↓
Invalid username: fakeuser
        ↓
Authentication failure
        ↓
Repeated attempts
        ↓
Wazuh Rule 100014 triggered
## 14. Successful Authentication Check

The investigation checked whether any of the observed SSH attempts resulted in successful authentication.

No successful SSH authentication associated with the investigated activity was observed.

| Check | Result |
|---|---|
| Brute-force activity | Detected |
| Failed authentication | Observed |
| Successful SSH login | Not observed |
| Confirmed account compromise | No |

The evidence therefore indicates an attempted attack without confirmed successful access.

---

## 15. Timeline Analysis

The available Wazuh events were reviewed to establish the sequence of activity.

The investigation identified repeated SSH authentication failures against the `admin` endpoint.

The activity can be summarized as:

```text
Source: 192.168.20.1
        ↓
Target: 192.168.20.100
        ↓
Service: SSH
        ↓
Username: fakeuser
        ↓
Authentication failed
        ↓
Repeated attempts detected
        ↓
Wazuh Rule 100014 generated alerts
## 16. Source and Target Analysis

The source and target information from the Wazuh event was reviewed to identify the systems involved in the authentication activity.

| Field | Value |
|---|---|
| Source IP | 192.168.20.1 |
| Target IP | 192.168.20.100 |
| Target Host | admin |
| Wazuh Agent | 002 |
| Service | SSH |
| Username | fakeuser |
| Authentication Result | Failed |

The source system generated the simulated SSH authentication attempts, while the Ubuntu `admin` endpoint received and logged the activity.

---

## 17. MITRE ATT&CK Mapping

The observed activity was mapped to the MITRE ATT&CK framework.

| Field | Value |
|---|---|
| Tactic | Credential Access |
| Technique ID | T1110 |
| Technique | Brute Force |
| Detection Rule | 100014 |

The repeated SSH authentication attempts are consistent with the Brute Force technique because multiple authentication attempts were made against the SSH service.

---

## 18. Impact Assessment

The investigation assessed whether the detected activity resulted in successful access to the affected endpoint.

No successful SSH authentication was observed during the investigation.

No evidence of successful access to the `admin` account was identified.

No post-authentication activity associated with the investigated brute-force attempt was identified.

### Assessment

```text
Attack Attempt: Confirmed
Detection: Successful
Authentication: Failed
Successful Access: Not Observed
Confirmed Compromise: No

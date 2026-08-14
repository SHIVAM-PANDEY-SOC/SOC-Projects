# SSH Log Analysis using Splunk
<img width="1145" height="793" alt="SSH Log Analysis using Splunk Overview" src="https://github.com/user-attachments/assets/7ba57b09-3601-4960-a7ec-07b114241736" />


A hands-on SOC Analyst project focused on analyzing SSH authentication logs using Splunk. This project demonstrates log ingestion, field extraction, SPL (Search Processing Language), dashboard creation, and alert configuration to detect suspicious SSH activities such as brute-force attacks and unauthorized connection attempts.

---

# Project Overview

SSH is one of the most targeted network services in enterprise environments. Attackers commonly perform brute-force attacks, password spraying, and reconnaissance against SSH servers.

In this project, Splunk Enterprise was used to ingest JSON-based SSH authentication logs, analyze security events, create dashboards, and configure alerts to identify suspicious SSH activities.

---

# Objectives

- Import SSH logs into Splunk
- Parse JSON log fields
- Analyze successful SSH logins
- Detect failed login attempts
- Identify brute-force attacks
- Monitor unauthenticated SSH connections
- Build security dashboards
- Configure Splunk alerts

---

# Tools Used

- Splunk Enterprise
- Ubuntu Linux
- SSH Log Dataset (JSON)
- SPL (Search Processing Language)

---

# Lab Environment

| Component | Details |
|-----------|---------|
| Operating System | Ubuntu |
| SIEM | Splunk Enterprise |
| Log Source | SSH Authentication Logs |
| Log Format | JSON |
| Index | ssh_logs |

---

# Project Workflow

```
SSH Logs
     │
     ▼
Data Ingestion
     │
     ▼
Field Extraction
     │
     ▼
SPL Queries
     │
     ▼
Visualization
     │
     ▼
Dashboard
     │
     ▼
Alert
```

---

# Task 1 – Log Ingestion & Validation

## Objective

Import SSH logs into Splunk and verify that all required fields are extracted successfully.

## Steps Performed

- Uploaded `ssh_logs.json`
- Selected `_json` Sourcetype
- Created custom index `ssh_logs`
- Imported log dataset
- Verified extracted fields

## SPL Query

```spl
index=ssh_logs
| table event_type auth_success auth_attempts id.orig_h id.resp_h
| head 10
```

## Extracted Fields

- event_type
- auth_success
- auth_attempts
- id.orig_h
- id.resp_h

## Screenshots

### Splunk Login

<img width="1908" height="914" alt="01_Splunk_Login png" src="https://github.com/user-attachments/assets/03cacf1e-c6fa-4e1e-bd5e-14f514583a4e" />


### Search & Reporting

<img width="1919" height="875" alt="02_Search_Reporting png" src="https://github.com/user-attachments/assets/cae6dc29-59f8-40fd-a1b9-ba36080470fe" />


### SSH Log Selected
<img width="1919" height="939" alt="04_SSH_Log_Selected png" src="https://github.com/user-attachments/assets/5d8db2d2-a381-4375-b082-74dc4df52ae3" />


### Input Settings
<img width="1863" height="876" alt="05_Input_Settings png" src="https://github.com/user-attachments/assets/c35f6116-4043-47fb-a0e5-735538807ab7" />


### Data Imported Successfully
<img width="1907" height="947" alt="06_Data_Imported png" src="https://github.com/user-attachments/assets/279354c0-7629-4d44-a7dc-f11897568bc1" />


### Field Validation
<img width="1919" height="885" alt="07_Field_Validation png" src="https://github.com/user-attachments/assets/07db15a3-4bc7-4016-88ea-081b238bedf6" />


---

# Task 2 – Failed SSH Login Analysis

## Objective

Identify source IP addresses generating failed SSH login attempts.

## SPL Query

```spl
index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h
| sort -count
| head 10
```

## Analysis

- Filtered failed login events.
- Counted failed authentication attempts by source IP.
- Ranked IP addresses based on failed login activity.
- Created a Bar Chart for better visualization.

## Screenshots

### Failed Login Statistics
<img width="1912" height="875" alt="08_Failed_Login_Stats png" src="https://github.com/user-attachments/assets/67fe16eb-d951-45e3-9383-3978cc4f2792" />


### Failed Login Bar Chart
<img width="1918" height="880" alt="Screenshot 2026-08-14 205733" src="https://github.com/user-attachments/assets/5b2db245-c27a-4f8d-89e4-d86d3b8ca94c" />


---

# Task 3 – Brute Force Detection

## Objective

Detect multiple failed SSH authentication attempts indicating brute-force attacks.

## SPL Query

```spl
index=ssh_logs event_type="Multiple Failed Authentication Attempts"
| where auth_attempts > 5
| table _time id.orig_h id.resp_h auth_attempts
| sort -auth_attempts
```

## Alert Configuration

| Setting | Value |
|----------|-------|
| Alert Name | SSH Brute Force Detection |
| Alert Type | Scheduled |
| Trigger | Number of Results > 0 |

> **Note:** The project guide recommends running the alert every 10 minutes. In the installed Splunk version, hourly scheduling was available, so the alert was configured using the closest supported schedule while keeping the same detection logic.

## Analysis

Multiple authentication failures from the same IP may indicate a brute-force attack. A scheduled alert was configured to notify analysts whenever such activity is detected.

## Screenshot

### Brute Force Alert

<img width="1871" height="616" alt="10_Brute_Force_Alert png" src="https://github.com/user-attachments/assets/9dfd71eb-d924-49c5-9097-ef3b24770552" />


---

# Task 4 – Successful SSH Login Analysis

## Objective

Monitor successful SSH logins and identify the most active source IP addresses.

## SPL Query

```spl
index=ssh_logs event_type="Successful SSH Login"
| stats count by id.orig_h
| sort -count
| head 10
```

## Analysis

- Filtered successful SSH login events.
- Counted successful logins by source IP.
- Created a Bar Chart.
- Added the visualization to the dashboard.

## Screenshot

### Successful Login Bar Chart
<img width="1916" height="888" alt="11_Successful_Login_BarChart png" src="https://github.com/user-attachments/assets/c5bf4681-dba0-4e69-a37d-2464eb4e0ab7" />


---

# Task 5 – Connection Without Authentication

## Objective

Detect SSH connections where authentication was never completed.

## SPL Query

```spl
index=ssh_logs event_type="Connection Without Authentication"
| stats count by id.orig_h
```

## Timechart Query

```spl
index=ssh_logs event_type="Connection Without Authentication"
| timechart count by id.orig_h
```

## Analysis

Repeated SSH connections without authentication may indicate reconnaissance activity, SSH scanning, or automated probing.

## Screenshot

### Connection Without Authentication

<img width="1897" height="846" alt="12_Unauthenticated_Connections png" src="https://github.com/user-attachments/assets/96088157-08e4-472b-9c45-7f8253c9f396" />


---

# Final Dashboard

The dashboard provides a centralized view of SSH authentication activities.

## Dashboard Panels

- Failed SSH Login Attempts
- Successful SSH Login Activity
- Connections Without Authentication Over Time

## Screenshot

### SSH Log Analysis Dashboard
<img width="1919" height="1079" alt="13_Final_Dashboard png" src="https://github.com/user-attachments/assets/f2ff66cc-62da-4141-b571-ebd78677339c" />


---

# Key Findings

- Successfully ingested JSON logs into Splunk.
- Parsed SSH authentication events automatically.
- Identified IPs generating failed login attempts.
- Detected brute-force attack patterns.
- Configured a scheduled Splunk alert.
- Tracked successful SSH logins.
- Monitored unauthenticated SSH connections.
- Built an operational SOC dashboard.

---

# Skills Demonstrated

- Splunk Enterprise
- SIEM Operations
- SPL (Search Processing Language)
- Log Analysis
- Threat Detection
- SSH Security Monitoring
- Dashboard Creation
- Alert Configuration
- Threat Hunting
- SOC Analyst Fundamentals

---

# Learning Outcomes

After completing this project, I gained practical experience in:

- Importing JSON logs into Splunk
- Writing SPL queries
- Investigating SSH authentication logs
- Detecting brute-force attacks
- Monitoring suspicious SSH activity
- Building dashboards
- Creating Splunk alerts

---

# Conclusion

This project demonstrates an end-to-end SOC Analyst workflow using Splunk, covering log ingestion, field extraction, security analysis, visualization, dashboard creation, and alert configuration. It provides practical experience in monitoring SSH authentication logs and identifying suspicious activities commonly encountered in enterprise environments.

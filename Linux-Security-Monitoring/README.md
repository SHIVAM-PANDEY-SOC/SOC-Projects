# Linux Security Monitoring using Wazuh

## Overview

This project demonstrates how Wazuh can be used to monitor and analyze security events on a Linux system. The lab focuses on collecting system logs, detecting suspicious activities, and investigating authentication events using Wazuh and Linux log analysis techniques.

## Objectives

* Deploy and configure a Wazuh Agent on Ubuntu.
* Monitor authentication and system logs.
* Detect failed login attempts and suspicious activities.
* Investigate security events using Linux commands.
* Improve visibility into Linux host security.

## Lab Environment

| Component        | Details                            |
| ---------------- | ---------------------------------- |
| Operating System | Ubuntu                             |
| SIEM/XDR         | Wazuh                              |
| Log Source       | Linux Authentication & System Logs |
| Environment      | Virtual Machine                    |

## Tools Used

* Wazuh
* Ubuntu Linux
* SSH
* grep
* awk
* journalctl
* systemctl

## Project Structure

```text
Linux-Security-Monitoring/
│
├── README.md
├── Screenshots/
├── Documentation/
├── Artifacts/
└── Queries/
```

## Investigation Workflow

1. Configure the Wazuh Agent.
2. Generate Linux authentication events.
3. Collect security logs.
4. Analyze authentication activity.
5. Investigate suspicious events.
6. Document findings.

## Skills Demonstrated

* Linux Log Analysis
* Security Monitoring
* Authentication Log Investigation
* Wazuh Deployment
* Incident Investigation
* Command-Line Log Analysis

## Future Improvements

* File Integrity Monitoring (FIM)
* Rootkit Detection
* Active Response
* Custom Detection Rules
* Email Alerting

## Author

**Shivam Pandey**

Aspiring SOC Analyst | Blue Team | Threat Detection | Linux Security Monitoring


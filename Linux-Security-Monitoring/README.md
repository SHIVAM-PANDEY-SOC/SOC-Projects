# Linux Security Monitoring using Wazuh

A hands-on Security Operations Center (SOC) lab built using Wazuh, Kali Linux, and Ubuntu. This project demonstrates endpoint monitoring, log collection, SSH attack simulation, and threat hunting.


## 📌 Project Overview

This project demonstrates **Linux Security Monitoring** using **Wazuh** to collect, monitor, and analyze security events from a Linux endpoint.
It focuses on authentication monitoring, SSH log analysis, threat hunting, and alert investigation, providing hands-on experience with core SOC Analyst and Blue Team operations.
---

## 🏗️ Lab Architecture

```mermaid
flowchart LR

    A[Kali Linux<br/>Attacker Machine]

    B[Ubuntu Server<br/>Wazuh Agent]

    C[Wazuh Manager<br/>Log Analysis & Rule Engine]

    D[Wazuh Dashboard<br/>Threat Hunting & Monitoring]

    A -->|SSH Brute Force Attack| B
    B -->|Security Logs| C
    C -->|Alerts & Events| D
```


---

## 🛠️ Technologies Used

- Wazuh Manager
- Wazuh Dashboard
- Ubuntu Server
- Kali Linux
- OpenSSH
- Linux Audit Logs

---

## 📂 Project Structure

```
Mini-SOC-Lab/
│
├── README.md
├── images/
│   ├── architecture.png
│   ├── endpoint.png
│   ├── auth-log.png
│   ├── threat-dashboard.png
│   ├── ssh-events.png
│   └── brute-force-alert.png
└── documentation/
```

---

# Exercise 1 – Deploying Wazuh Agent

### Screenshot

![Endpoint Dashboard] <img width="1311" height="943" alt="01-Agent-Deployment png" src="https://github.com/user-attachments/assets/20b1448c-50b5-4642-90e9-24359904aa2d" />


---

# Exercise 2 – Verifying Agent Connectivity

### Screenshot

![Connected Agent](images/agent-status.png)

---

# Exercise 3 – Monitoring Authentication Logs

### Command

```bash
sudo tail -20 /var/log/auth.log
```

### Screenshot

![Authentication Logs] <img width="1914" height="865" alt="03-Threat Hunting Dashboard – Authentication Monitoring Overview" src="https://github.com/user-attachments/assets/8116623e-f78a-4483-9beb-5d62ecf56217" />


---

# Exercise 4 – Simulating SSH Brute Force Attack

### Command

```bash
hydra -l fakeuser -P passwords.txt ssh://<Target-IP>
```

### Screenshot

![SSH Attack]  <img width="1865" height="531" alt="06-SSH-Authentication-Alerts png" src="https://github.com/user-attachments/assets/1d42f78f-9b3b-4c3d-960b-fe67faa9345c" />


---

# Exercise 5 – Detecting Alerts in Wazuh

### Screenshot

![Brute Force Alerts] <img width="1914" height="865" alt="03-Threat Hunting Dashboard – Authentication Monitoring Overview" src="https://github.com/user-attachments/assets/574e8ede-e578-424c-9629-2f8b6a179882" />

---

# Exercise 6 – Threat Hunting Dashboard

### Screenshot

![Threat Hunting Dashboard] <img width="947" height="858" alt="02-Threat-Hunting-Dashboard png" src="https://github.com/user-attachments/assets/818c25c2-2f68-4c7b-a40d-ac608f7fedce" />


---

# Exercise 7 – SSH Authentication Events

### Screenshot

![SSH Events Dashboard]  <img width="1908" height="1079" alt="SSH Authentication Failure Analysis" src="https://github.com/user-attachments/assets/24af124e-ec07-4866-a002-31862b4eab4e" />


---

## 🔍 Key Findings

- Wazuh successfully detected SSH authentication failures.
- Brute force attempts generated security alerts.
- Authentication logs were forwarded to the Wazuh Manager.
- Threat Hunting dashboard visualized attack activity in real time.

---

## 📖 Learning Outcomes

- Wazuh Deployment
- Endpoint Monitoring
- SSH Log Analysis
- Brute Force Detection
- Threat Hunting
- Alert Investigation
- Basic SOC Operations

---

## 👨‍💻 Author

**Shivam Pandey**

Aspiring SOC Analyst | Blue Team | Threat Hunting

TryHackMe: Top 2%

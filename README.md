# 🛡️ SOC Detection Pipeline (Home Lab)

This project simulates a real-world SOC detection pipeline using open-source tools in a home lab environment. This lab focuses on capturing endpoint telemetry, tuning detections, and mapping alerts to MITRE ATT&CK techniques using Wazuh, Sysmon, and Elasticsearch. 
Based on the MyDFIR YouTube

---

## 🚀 Project Objectives

- Build and configure a lightweight SIEM pipeline
- Ingest rich endpoint telemetry from a Windows system
- Create and tune detection rules using Wazuh
- Validate alerts for simulated attacker behavior (e.g., Mimikatz)
- Map detections to MITRE ATT&CK techniques

---

## 🧰 Technologies Used

| Component         | Technology                     |
|------------------|---------------------------------|
| Virtualization    | VirtualBox / VMware            |
| SIEM              | Wazuh (Manager + Agent)        |
| Log Storage       | Elasticsearch                  |
| Log Forwarding    | Filebeat / Winlogbeat          |
| Endpoint Logging  | Sysmon (with custom config)    |
| Visualization     | Wazuh Dashboard (OpenSearch UI)|
| Operating Systems | Ubuntu Server, Windows 10      |
| Backend Services  | Cassandra (Wazuh dependency)   |

---

## 📚 Project Breakdown

### ✅ Part 1 – Initial Lab Setup

- Set up two VMs:
  - **Ubuntu Server**: Hosts Wazuh Manager and Elasticsearch
  - **Windows 10**: Used as the monitored endpoint
- Installed:
  - Wazuh Manager, Wazuh API, Elasticsearch
- Registered the Windows endpoint with the Wazuh Manager
- Verified communication and log ingestion using the Wazuh Dashboard

*Initial project diagram*

<img src="1.diagram.png" alt="Project Diagram" width="500"/>

*Created/Altered firewall rules*

<img src="4.firewall-config.png" alt="Firewall Config" width="500"/>

*Configuring The Hive*

<img src="5.config-hive.png" alt="Hive Config" width="500"/>

*Verfied Communication and Log Ingestion*

<img src="wazuh+mimikatz.png" alt="Firewall Config" width="500"/>

---

### 🔒 Part 2 – Endpoint Telemetry with Sysmon

- Installed **Sysmon** and the **Wazuh Agent** on the Windows VM
- Applied a custom **Sysmon configuration**
- Configured **Winlogbeat/Filebeat** to ship Windows Event Logs to Wazuh
- Captured key telemetry:
  - Process creation
  - Network connections
  - DLL loading

*Installing sysmon through admin powershell*

<img src="2.powershell-install-sysmon.png" alt="Sysmon" width="500"/>

---

### 🧠 Part 3 – MITRE ATT&CK Alerting

- Explored how Wazuh rules map to **MITRE ATT&CK techniques**
- Filtered and reviewed MITRE-mapped alerts in the **Wazuh Dashboard**
- Simulated suspicious behavior to trigger built-in MITRE-mapped detections

*Logged Mimikatx on Wazuh Secuirty Events Dashboard*

<img src="7.logged-mimikatz.png" alt="mimikatz" width="500"/>

---

### 🧪 Part 4 – Rule Tuning & Custom Detection

- Modified Wazuh configuration to collect all events for testing purposes
- Created a **custom detection rule** to identify **Mimikatz** execution (even when renamed)
- Mapped the rule to:
  - **MITRE ATT&CK ID:** `T1003 – Credential Dumping`
- Validated detection successfully via Wazuh alerting

---



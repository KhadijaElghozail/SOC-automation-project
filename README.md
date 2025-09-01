# SOC-automation-project

![Status](https://img.shields.io/badge/Project-SOC_Automation-blue?style=for-the-badge)
![Wazuh](https://img.shields.io/badge/-Wazuh_SIEM-3595F9?&style=for-the-badge&logo=wazuh&logoColor=white)
![TheHive](https://img.shields.io/badge/-TheHive_SIRP-FFD700?&style=for-the-badge&logo=apachehive&logoColor=black)
![Shuffle](https://img.shields.io/badge/-Shuffle_Automation-FF5733?&style=for-the-badge&logo=shuffles&logoColor=white)
![Sysmon](https://img.shields.io/badge/-Sysmon_Telemetry-808080?&style=for-the-badge&logo=windows&logoColor=white)




## 🎯 Objectives

The main goals of the project are:

1. Collect endpoint telemetry using **Sysmon** and **Wazuh agents**.
2. Aggregate and analyze logs in **Wazuh**.
3. Detect suspicious activity (e.g., **Mimikatz execution**).
4. Automate enrichment and response using **Shuffle** + **VirusTotal**.
5. Escalate incidents automatically into **TheHive** for case management.


## 🛠️ Methodology

### 1. Endpoint Telemetry
- Install **Sysmon** on Windows machines to capture:
  - Process creation
  - File changes
  - Network connections
  - Registry modifications  
- Deploy **Wazuh Agent** to forward logs to the manager.

### 2. Centralized Monitoring
- Deploy **Wazuh Manager** on Google Cloud.
- Configure **Filebeat** to send logs to **OpenSearch/Elasticsearch**.
- Set up dashboards for real-time and archived log analysis.

### 3. Detection & Alerting
- Create custom **Wazuh rules** (e.g., detect `mimikatz.exe` execution).
- Validate alerts via controlled attack simulations.

### 4. Automated Response
- **Shuffle** receives Wazuh alerts via webhook.
- Enrich alerts with **VirusTotal** lookups.
- Create incidents automatically in **TheHive**.
- Notify SOC analysts via email.


## 🔍 Testing

- Simulated **Mimikatz execution** on Windows endpoint
- Verified detection in **Wazuh Discover**
- Triggered custom rule → Alert generated
- Alert forwarded via **Shuffle Webhook**
- **VirusTotal enrichment** executed
- Automatic **case creation in TheHive**

## 📊 Architecture Overview

```mermaid
flowchart TD
    A[Sysmon on Windows] -->|Telemetry| B[Wazuh Agent]
    B -->|Forward logs| C[Wazuh Manager]
    C --> D[OpenSearch / Wazuh Dashboard]
    C -->|Alerts| E[Shuffle Automation]
    E -->|Enrich| F[VirusTotal]
    E -->|Escalate| G[TheHive SIRP]
    E -->|Notify| H[Email to Analysts]

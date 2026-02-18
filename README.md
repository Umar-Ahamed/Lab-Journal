# Local SOC Lab: Wazuh EDR & Splunk SIEM Integration

A streamlined, single-node Security Operations Center (SOC) environment built on **Ubuntu** to facilitate hands-on practice in **threat hunting**, **telemetry analysis**, and **incident response**.

## 🎯 Objective
Architect a functional security monitoring pipeline on a single host to observe real-time attack patterns and validate defensive configurations.

## 🛠 Technologies Used
*   **Host OS:** [Ubuntu 22.04/24.04 LTS](https://ubuntu.com)
*   **EDR:** [Wazuh](https://documentation.wazuh.com) (Endpoint Detection & Response)
*   **SIEM:** [Splunk Enterprise](https://www.splunk.com) (Log Aggregation & Visualization)
*   **Automation:** Bash (Attack Simulation & Logistics)

## 🚀 Implementation Steps

### 1. Agent Deployment
Deployed the Wazuh agent via CLI and forced communication through the loopback interface to maintain a self-contained environment.

# 🛡️ Ubuntu SOC Home Lab
Integrated Wazuh EDR and Splunk SIEM to monitor system integrity and practice threat hunting.

## 📁 Investigation Logs
* [**Baseline Analysis:** Identifying Noise & CIS Compliance](./Baseline_Analysis.md)

## 🛠️ Tech Stack
* **EDR:** Wazuh
* **SIEM:** Splunk Enterprise
* **OS:** Ubuntu (Guest)
* **Main OS** Windows 11 pro (Host)

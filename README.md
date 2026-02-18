# 🛡️ Ubuntu SOC Home Lab
**Integrated Wazuh EDR & Splunk SIEM Monitoring Environment**

A streamlined, single-node Security Operations Center (SOC) environment designed to facilitate hands-on practice in **threat hunting**, **telemetry analysis**, and **incident response**.

## 🎯 Project Objective
Architect a functional security monitoring pipeline to observe real-time attack patterns, validate defensive configurations, and bridge the gap between endpoint telemetry (EDR) and centralized log analysis (SIEM).

---

## 📂 Investigation Logs
This repository serves as a technical journal for specific security scenarios and troubleshooting.

* [**Baseline Analysis:** Identifying Noise & CIS Compliance](./Baseline_Analysis.md)
* [**SSH Brute Force Detection:** Troubleshooting Telemetry & SIEM Integration](./SSH_BruteForce_Detection.md)

---

## 🛠️ Tech Stack
* **EDR:** [Wazuh](https://documentation.wazuh.com) (Endpoint Detection & Response)
* **SIEM:** [Splunk Enterprise](https://www.splunk.com) (Log Aggregation & Visualization)
* **Virtualization:** Oracle VirtualBox
* **Operating Systems:** * **Target:** Ubuntu 24.04 LTS (Guest VM)
  * **Attacker/Host:** Windows 11 Pro (Physical Host)
* **Automation:** Bash (Attack Simulation & Logistics)

---

## 🚀 Environment Implementation

### 1. Agent Deployment
The Wazuh agent was deployed via CLI to the Ubuntu endpoint. Communication was forced through the loopback interface to maintain a self-contained environment while ensuring consistent telemetry flow to the manager.

### 2. SIEM Integration
Configured Splunk to ingest JSON alerts from Wazuh, allowing for advanced querying, correlation, and visualization of security events.

### 3. Attack Simulation
Utilized custom scripts and host-to-guest network requests to generate authentic attack signatures, including SSH brute force attempts and unauthorized privilege escalation checks.

---

## 💡 Key Lessons
* **Visibility:** Security tools are only as effective as the services they monitor (e.g., verifying `sshd` status).
* **Data Integrity:** Structured JSON logging is critical for high-fidelity SIEM analysis.
* **Architecture:** Understanding the "plumbing" of a data pipeline is essential for root-cause analysis during telemetry gaps.

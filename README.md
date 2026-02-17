#Local SOC Lab: Wazuh EDR & Splunk SIEM Integration
Objective
To architect a functional Security Operations Center (SOC) environment on a single Ubuntu instance to practice threat hunting and incident response.

Technologies Used
Ubuntu 22.04/24.04 (Host OS)

Wazuh (Endpoint Detection & Response)

Splunk Enterprise (SIEM)

Bash (Automation & Attack Simulation)

Implementation Steps
Agent Deployment: Deployed Wazuh agents using CLI and configured communication via loopback (127.0.0.1).

Data Pipeline: Integrated Wazuh alerts.json with Splunk using the splunk add monitor utility.

Telemetry Validation: Verified log flow by simulating unauthorized sudo attempts and monitoring AppArmor blocks.

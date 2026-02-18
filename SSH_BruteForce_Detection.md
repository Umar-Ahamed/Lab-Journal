# 🛡️ Project: SSH Brute Force Detection & SIEM Integration

**Date:** February 17, 2026  
**Environment:** Ubuntu 24.04 (Target), Windows 11 (Host/Attacker), Wazuh Manager (EDR), Splunk Enterprise (SIEM)

## 🎯 Project Overview
The objective of this lab was to establish a functional security monitoring pipeline to detect and visualize unauthorized SSH access attempts. This project demonstrates the critical integration between an Endpoint Detection and Response (EDR) tool (Wazuh) and a Security Information and Event Management (SIEM) platform (Splunk).

## 🚧 Challenge: Identifying the Telemetry Gap
Initially, the Splunk dashboard yielded **"No results found"** for network-based attacks. 

* **Observation:** Investigation via the Ubuntu terminal revealed that the only recorded "Failed password" events were local administrative `grep` commands rather than actual network traffic.
* **Diagnosis:** System errors confirmed that the `ssh.service` was not found on the Ubuntu VM, meaning the "door" was closed to all external connection attempts.

## 🛠️ Implementation & Remediation

### 1. Service Installation & Configuration
To enable network-based logging, I installed the OpenSSH server and updated firewall rules to allow traffic on Port 22:

# Installing the missing service
```
sudo apt update && sudo apt install openssh-server -y
sudo systemctl enable --now ssh
```
# Opening the firewall
```
sudo ufw allow 22/tcp
```
### 2. Attack Simulation
After installing SSH, I initiated an authentication request from the host machine (IP: 10.0.0.136) to the target VM (10.0.0.109):
```
ssh attacker0x10@10.0.0.109
```
![](https://raw.githubusercontent.com/Umar-Ahamed/Lab-Journal/refs/heads/main/images/External%20host%20trying%20to%20ssh%20into%20guest%20vm%20.png)

### 3. SIEM Investigation & Querying
I looked at the Splunk SIEM on the guest machine and executed a query to isolate the attack while filtering out local administrative noise:

```
index=main "Failed password" NOT "grep"
```

### 📊 Results: Evidence of Detection
The pipeline successfully captured and parsed the attack. Wazuh normalized the raw syslog data into a structured JSON format, providing the SIEM with high-fidelity attribution data.

![](https://raw.githubusercontent.com/Umar-Ahamed/Lab-Journal/refs/heads/main/images/Splunk%20finding%20ssh%20brute%20force%20attack%20.png)

Validated Detection Log (JSON)
JSON
```
{
    "timestamp": "2026-02-17T15:16:43.822-0800",
    "agent": {
        "name": "wazuh-VirtualBox",
        "id": "000"
    },
    "data": {
        "srcip": "10.0.0.136",
        "srcuser": "attacker0x10"
    },
    "full_log": "2026-02-17T15:16:43.348333-08:00 wazuh-VirtualBox sshd[21589]: Failed password for invalid user attacker0x10 from 10.0.0.136 port 61008 ssh2",
    "rule": {
        "description": "sshd: Attempt to login using a non-existent user",
        "id": "5710"
    },
    "location": "/var/log/auth.log",
    "sourcetype": "wazuh_json"
}

```

### Summary
A SIEM is only as effective as the telemetry it receives. By identifying the "blind spot" (the missing SSH service), I was able to transform a non-functional dashboard into a reactive security tool. This lab underscores the importance of endpoint configuration and service availability in achieving full SOC visibility.   

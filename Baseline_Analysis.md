# SOC Investigation: Baseline & Noise Analysis
**Date:** Feb 16, 2026
**Tooling:** Wazuh EDR, Splunk Enterprise

## 🔍 Incident Overview
Initial telemetry collection showed high event volume originating from the host machine. Statistical analysis was required to distinguish between system noise and potential threats.

## 📊 Evidence
![Splunk Frequency Analysis](images/First%20Analysis%20Lookup.jpg)

## 💡 Findings
* **Top Event:** `Apparmor DENIED` (80.05% of traffic). 
* **Diagnosis:** Benign activity from Firefox memory polling.
* **SOC Recommendation:** Create an exclusion filter for this specific PID/Path to reduce "Analyst Fatigue."

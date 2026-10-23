# Ticket #05: Host Resource Exhaustion & CloudWatch In-Alarm Validation

## 🚨 Customer Incident Report
- **Symptom:** Automated platform monitoring policies triggered alerts regarding system compute health boundaries. 
- **Behavior:** The infrastructure state matrix updated to a critical alert flag. Internal processes remain active, but hyper-utilization warnings require investigation.

## 🔍 Engineering Triage & Diagnostics
1. **Host Connection Mapping:** Logged into the underlying Linux instance securely using shell utilities to check running process footprints.
2. **Metric Aggregation Audit:** Checked the central monitoring plane inside the AWS CloudWatch Alarms dashboard interface. The configured tracking alarm `High-CPU-Alarm-Lab1` actively crossed standard operational thresholds.

## 🛠️ Root Cause Analysis (RCA) & Resolution
- **Root Cause:** An engineer initiated high-intensity benchmarking tools (`stress --cpu 2 --timeout 600s`) directly on the target host compute node, maxing out CPU utilization metrics past the designated 70% threshold boundary limit for an extended evaluation timeline.
- **Applied Fix:** Monitored the host shell until the active benchmarking script completed its pre-configured timeout countdown window. Alternatively, application processes can be selectively intercepted or terminated early using process keys (`Ctrl + C` or `kill`). 

## ✅ Fix Verification
Once the stress-testing loop completed its cycle, resource demands dropped back to normal parameters, and the alarm state transitioned cleanly back down from critical warning states into an `OK` verification landscape.

### 🖼️ Diagnostic Evidence
**Figure 5.1: AWS CloudWatch Alarm Dashboard Reflecting Active High-CPU Critical Violation**
![CloudWatch Metric Alarm Triggered]<img width="1917" height="1030" alt="case5-cloudwatch-alarm" src="https://github.com/user-attachments/assets/c1b06f2b-6973-4c03-bafe-58d6be19287d" />



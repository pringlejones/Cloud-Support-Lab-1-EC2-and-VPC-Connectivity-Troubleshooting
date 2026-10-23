# Ticket #04: Application Layer Web Hosting Service Crash (Nginx Service Interruption)

## 🚨 Customer Incident Report
- **Symptom:** Monitoring tools report web page execution failure. External connection attempts return an instantaneous `Connection Refused` code.

## 🔍 Engineering Triage & Diagnostics
1. **Network Infrastructure Status:** Verified that the instance can be accessed via secure shell (SSH), confirming the network path, security filters, routing policies, and NACLs are fully functional.
2. **Host Port Validation:** Executed modern network socket tracking tools (`sudo ss -tulpn`) inside the running instance shell.

## 🛠️ Root Cause Analysis (RCA) & Resolution
- **Root Cause:** System diagnostic mapping via socket evaluation revealed that **TCP Port 80 (HTTP)** was completely missing from the host's active listener socket pool. The actual underlying `nginx` background software service had stopped executing.
- **Applied Fix:** Restored standard application operational cycles via host service management utilities:
  ```bash
  sudo systemctl start nginx
  ```

## ✅ Fix Verification
Post-fix analysis verified that the listener socket attached to port 80 successfully bound back onto the system landscape, rendering traffic visible again.

### 🖼️ Diagnostic Evidence
**Figure 4.1: Socket Listener Triage Log Before and After Service Crash Resolution**
![Nginx Port Triage Log]<img width="1917" height="686" alt="ticket04-service-ports-triage" src="https://github.com/user-attachments/assets/34a696d1-e74f-4415-a9ba-e98f98e119b2" />



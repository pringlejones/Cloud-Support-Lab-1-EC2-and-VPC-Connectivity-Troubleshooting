# Ticket #01: EC2 Inbound Connection Timeout Fault

## 🚨 Customer Incident Report
- **Symptom:** Remote deployment engineer reports an inability to access the primary web server via SSH over Port 22. 
- **Behavior:** Attempts to connect freeze instantly at the command line terminal environment and eventually drop out with an explicit network error string: `Connection timed out`.

## 🔍 Engineering Triage & Diagnostics
1. **Initial Assessment:** Verified that the target EC2 compute host instance profile was in an active, healthy `Running` state within the cloud control layer.
2. **Isolation Action:** Checked incoming connection streams. The terminal drops packets during validation, pointing to an external firewall block layer rather than an internal operating system crash.

## 🛠️ Root Cause Analysis (RCA) & Resolution
- **Root Cause:** Analysis of the stateful security filter mechanism (`web-server-sg`) revealed that the explicit inbound rule assignment for **TCP Port 22 (SSH)** had been completely dropped or omitted from the active configuration matrix.
- **Applied Fix:** Modified the security group properties by appending an explicit incoming traffic allowance rule:
  - **Type:** SSH | **Protocol:** TCP | **Port Range:** 22
  - **Source Filter:** Configured strictly to `My IP` boundary tracking as an operational security best practice to prevent public brute-force attempts.

## ✅ Fix Verification
Following rule implementation, connection testing was re-evaluated via PowerShell terminal. Remote authentication passed instantly, transitioning securely into the shell environment.

### 🖼️ Diagnostic Evidence
**Figure 1.1: PowerShell Connection Drop State**
![SSH Timeout Fault](<img width="1475" height="748" alt="ticket01-ssh-timeout" src="https://github.com/user-attachments/assets/08d78433-5fb4-4211-8964-c705c2a03e01" />)

**Figure 1.2: Successful Infrastructure Entry After Security Group Fix**
![SSH Session Resolved](<img width="1917" height="1024" alt="ticket01-ssh-resolved" src="https://github.com/user-attachments/assets/4d15ab09-8342-4ef9-a864-6314c23e33e0" />)


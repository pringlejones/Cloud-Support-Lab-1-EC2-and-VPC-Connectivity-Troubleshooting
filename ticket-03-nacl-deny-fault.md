# Ticket #03: Stateless Network Access Control List (NACL) Implicit Block

## 🚨 Customer Incident Report
- **Symptom:** Network automation tests reporting full communication failure across the entire server subnet segment.
- **Behavior:** Basic external health evaluation utilities (ICMP ping streams) return `100% packet loss` failures.

## 🔍 Engineering Triage & Diagnostics
1. **Security Group Mapping:** Verified security groups allow standard operational traffic.
2. **Layer-4 Isolation:** Because multiple services are blocked across the entire subnet simultaneously, triage moved from the instance-specific security groups to the subnet network partition wall.

## 🛠️ Root Cause Analysis (RCA) & Resolution
- **Root Cause:** A high-priority stateless **Network ACL (NACL) Inbound Rule** (Rule #1) was injected with a catch-all `0.0.0.0/0 Deny` policy, blocking incoming traffic before evaluation rules further down the stack could process.
- **Applied Fix:** Purged the rule from the active inbound block stack, restoring traffic processing priority flow back to default parameters.

## ✅ Fix Verification
Running basic diagnostic pings from local terminal networks demonstrated immediate system recovery.

### 🖼️ Diagnostic Evidence
**Figure 3.1: Terminal ICMP Ping Packet Drop Log**
![NACL Ping Drop]<img width="1479" height="750" alt="ticket03-nacl-ping-drop" src="https://github.com/user-attachments/assets/6af68d06-998f-4d7a-979b-d5bbf5d0bf0d" />



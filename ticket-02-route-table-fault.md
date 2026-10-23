# Ticket #02: Missing Internet Gateway Route in Public Subnet Route Table

## 🚨 Customer Incident Report
- **Symptom:** End-users report that the external website application hosted at `34.205.75.22` is entirely unavailable.
- **Behavior:** Web browsers throw an explicit `ERR_CONNECTION_TIMED_OUT` error message. Existing open SSH terminal sessions freeze completely and drop out.

## 🔍 Engineering Triage & Diagnostics
1. **Security Group Audit:** Validated that inbound rules for HTTP (Port 80) and SSH (Port 22) are correctly open and unchanged.
2. **Network Analysis Pathing:** Utilized the AWS VPC Reachability Analyzer tool to map the path between the host EC2 instance and the Internet Gateway.

## 🛠️ Root Cause Analysis (RCA) & Resolution
- **Root Cause:** The Reachability Analyzer returned an explicit **`NO_ROUTE_TO_DESTINATION`** alert flag. The subnet routing table `rtb-0125da6eb5a73c617` lacked an active destination route entry (`0.0.0.0/0`) mapping out to the public internet gateway (`igw-096ed57e30758f825`).
- **Applied Fix:** Edited the public route table configuration, appending a new destination entry (`0.0.0.0/0`) pointed to the VPC Internet Gateway.

## ✅ Fix Verification
As soon as the route entry updated, HTTP external requests healed instantly, and the standard web landing content rendered on demand.

### 🖼️ Diagnostic Evidence
**Figure 2.1: Target Web Application Unreachable Status**
![Browser Timeout]<img width="1917" height="1024" alt="ticket02-browser-timeout" src="https://github.com/user-attachments/assets/194daa72-dd54-495b-b44b-7b5f459b9f39" />


**Figure 2.2: AWS Reachability Analyzer Tracking Failure Log**
![Reachability Analyzer Alert]<img width="1917" height="1026" alt="ticket02-reachability-analyzer" src="https://github.com/user-attachments/assets/5a91a313-21e2-4ec8-9dd4-4bb3b4454d2f" />


# Cloud-Support-Lab-1-EC2-and-VPC-Connectivity-Troubleshooting
## 🌐 Lab 1: AWS EC2 & VPC Connectivity Fault Analysis

This module evaluates core network path routing, traffic filtering boundaries, and application layer health cycles inside an Amazon Web Services (AWS) ecosystem. 

### 🔀 Infrastructure Architecture Map
*Built with draw.io:*
- **Public Subnet (10.0.0.0/24):** Hosts the active `t2.micro` Linux EC2 Compute instance running an Nginx Web Server engine.
- **Private Subnet (10.0.1.0/24):** Isolated backend staging block segment.
- **Edge Security Controls:** Statefully filtered by Instance Security Groups and statelessly guarded at the subnet perimeter by Network Access Control Lists (NACLs).

---

### 📋 Documented Engineering Incidents (Troubleshooting Tickets)

Every scenario represents a distinct, isolated platform infrastructure failure engineered to trace anomalies down to the root cause.

| Ticket Reference | Infrastructure Component | Observed System Symptom | Applied Resolution Strategy |
| :--- | :--- | :--- | :--- |
| **[Ticket #01: Security Group Fault](./lab1-aws-vpc-ec2/ticket-01-ssh-timeout.md)** | EC2 Inbound Security Filters | Shell authentication requests freeze indefinitely and return standard network connection time-outs. | Injected explicit TCP Port 22 rules scoped exclusively to target administrative home IP boundaries. |
| **[Ticket #02: Route Table Fault](./lab1-aws-vpc-ec2/ticket-02-route-table-fault.md)** | VPC Subnet Routing Matrix | External HTTP applications drop off completely; Automated AWS Reachability Analyzer logs drop errors. | Restored the missing `0.0.0.0/0` edge routing string directed at the local VPC Internet Gateway. |
| **[Ticket #03: Network ACL Fault](./lab1-aws-vpc-ec2/ticket-03-nacl-deny-fault.md)** | Stateless Subnet Boundary Firewalls | Total network path failure across all protocols; Local ICMP network pings return 100% data loss profiles. | Purged the high-priority stateless `Deny All` entry to clear lower-level network evaluation flows. |
| **[Ticket #04: Nginx Service Fault](./lab1-aws-vpc-ec2/ticket-04-nginx-service-crash.md)** | Host System Application Layer | Browser connections drop immediately with `Connection Refused`. Linux socket trackers show Port 80 is inactive. | Analyzed background loops using `ss -tulpn` and re-initiated host processes via system utilities. |
| **[Ticket #05: Monitoring Alert](./lab1-aws-vpc-ec2/ticket-05-cloudwatch-alarm.md)** | Amazon CloudWatch Service | Host CPU utilization limits breached; Monitoring dashboard flags a severe system resource exception. | Engineered simulated system loads using `stress` packages to trigger state modifications. |


---

### 🛠️ Core Toolkit Demonstrated
- **Infrastructure Automation & Management:** AWS VPC Subnet Wizards, Security Group Matrix Filters, Network Access Control Lists.
- **Diagnostic Instrumentation Tools:** AWS Reachability Analyzer, Linux Socket Inspection Utilities (`ss`), System Lifecycle Engines (`systemctl`).

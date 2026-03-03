# Cloud-Based SIEM Setup: RDP Brute-Force Detection Using AWS and Splunk

## 1. Project Overview

This project demonstrates the implementation of a cloud-based SOC monitoring lab using AWS and Splunk Enterprise. The lab simulates RDP brute-force attacks and implements detection, alerting, and monitoring dashboards.

The objective of this project is to understand cloud networking, secure log forwarding, and detection engineering fundamentals.

---
## 2. Folder Structure

```
Cloud-SIEM-Lab/
│
├── README.md                             # Project overview and summary
├── Project_Flow.md                       # Complete architecture and workflow explanation
├── concept_explanation.md                # General concepts (VPC, Subnet, IGW, SG, Event Codes, Logon Types)
├── RDP Brute-force Detection Rule.md     # SPL query and alert configuration
│
├── Screenshots/
│   ├── Cloud_configuration.md            # AWS infrastructure screenshots and explanation
│   └── Log_forward.md                    # Splunk ingestion, alert, and dashboard screenshots
│
└── LICENSE
```
## 3. Project Architecture Summary

The lab includes:

1. Custom VPC
2. Public Subnet
3. Internet Gateway
4. Route Table configuration
5. Security Group hardening
6. Windows EC2 deployment
7. Splunk Universal Forwarder installation
8. Secure log transmission using Tailscale
9. Splunk detection rule for RDP brute-force
10. Dashboard visualization

Detailed flow explanation is available in:

- [Project Flow](Project_Flow.md)
- [Concepts Explanation](concept_explanation.md)
- [RDP Brute-Force Detection Rule](RDP%20Brute-force%20Detection%20Rule.md)

---

## 4. Key Features

1. Cloud network isolation using VPC
2. Controlled inbound access via Security Groups
3. Secure log forwarding architecture
4. Detection logic using SPL
5. Scheduled alert configuration using Cron
6. Monitoring dashboard

---

## 5. Detection Implemented

RDP Brute-Force Detection using:

- Windows Event ID 4625
- Threshold-based logic (more than 5 failed attempts within 5 minutes)

Full query explanation available in:
[RDP Brute-Force Detection Rule](RDP%20Brute-force%20Detection%20Rule.md)


---






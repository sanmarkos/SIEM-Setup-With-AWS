# Cloud-Based SIEM Setup: RDP Brute-Force Detection Using AWS and Splunk

## 1. Project Overview

This project demonstrates the implementation of a cloud-based SOC monitoring lab using AWS and Splunk Enterprise. The lab simulates RDP brute-force attacks and implements detection, alerting, and monitoring dashboards.

The objective of this project is to understand cloud networking, secure log forwarding, and detection engineering fundamentals.

---
## 2. Folder Structure

```
Cloud-SOC-Lab/
├── README.md
├── Project_Flow.md
├── Concepts_Explanation.md
├── Architecture/
├── Queries_and_Alerts/
└── Screenshots/
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

- Project_Flow.md
- Concepts_Explanation.md
- Queries_and_Alerts/rdp_bruteforce_detection.md

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
Queries_and_Alerts/rdp_bruteforce_detection.md

---






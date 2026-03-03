# Project Flow and Architecture Explanation

## 1. Network Architecture Flow
```
Internet
→ Internet Gateway
→ VPC
→ Public Subnet
→ Route Table (0.0.0.0/0 → Internet Gateway)
→ Security Group
→ Windows EC2
→ Splunk Universal Forwarder
→ Tailscale Secure Tunnel
→ Local Splunk Enterprise
→ Detection Rule
→ Alert
→ Dashboard
```
---

## 2. Step-by-Step Flow Explanation

1. A custom VPC was created to isolate the cloud environment.
2. A public subnet was configured inside the VPC.
3. An Internet Gateway was attached to enable internet access.
4. The route table was configured to send 0.0.0.0/0 traffic to the Internet Gateway.
5. A Security Group was created to allow RDP access only from a trusted IP.
6. A Windows EC2 instance was launched inside the public subnet.
7. Splunk Universal Forwarder was installed on the EC2 instance.
8. Logs were securely transmitted to local Splunk using Tailscale.
9. Detection rules were created to monitor failed RDP login attempts.
10. A scheduled alert was configured using Cron expression */5 * * * *.
11. A monitoring dashboard was built to visualize authentication activity.

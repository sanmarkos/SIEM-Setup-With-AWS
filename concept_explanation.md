# General Concepts Explanation

## 1. What is VPC?

A Virtual Private Cloud (VPC) is a logically isolated network inside AWS where you deploy cloud resources.

Simple Example:
Think of VPC as your private apartment building inside AWS. Only resources inside this building can communicate internally unless you allow external access.

Example in this project:
- Created a VPC with CIDR 10.0.0.0/16
- All EC2 resources are deployed inside this VPC.

---

## 2. What is a Subnet?

A Subnet is a smaller network segment inside a VPC.

Simple Example:
If VPC is the apartment building, a subnet is a floor inside that building.

Types:
1. Public Subnet – Has internet access.
2. Private Subnet – No direct internet access.

Example in this project:
- Windows EC2 is deployed inside a Public Subnet.
- CIDR: 10.0.1.0/24

---

## 3. What is an Internet Gateway (IGW)?

An Internet Gateway allows communication between the VPC and the internet.

Simple Example:
It is the main gate of your apartment building that connects you to the outside world.

Without IGW:
- EC2 cannot have public IP access.
- RDP from external network will not work.

Example in this project:
- IGW attached to VPC.
- Route table configured to send 0.0.0.0/0 traffic to IGW.

---

## 4. What is a Route Table?

A Route Table defines how network traffic is directed.

Simple Example:
It works like Google Maps for network traffic.

Example Rule:
Destination: 0.0.0.0/0  
Target: Internet Gateway  

Meaning:
All internet traffic goes to the Internet Gateway.

Example in this project:
- Public subnet associated with route table.
- Route sends internet-bound traffic to IGW.

---

## 5. What is a Security Group?

A Security Group acts as a virtual firewall for an EC2 instance.

It controls:
- Which ports are open
- From which IP addresses

Simple Example:
It is a security guard checking who can enter your apartment.

Example in this project:
- Allowed RDP (Port 3389) from only my public IP.
- Blocked all other incoming traffic.

---

## 6. What is Windows EC2?

EC2 is a virtual machine running inside AWS.

In this project:
- Windows Server installed
- Generates security logs
- Hosts RDP service
- Runs Splunk Universal Forwarder

---

## 7. What is Splunk Universal Forwarder?

Splunk Universal Forwarder is a lightweight agent installed on the EC2 instance.

Purpose:
- Collect Windows Event Logs
- Send logs to Splunk Enterprise

Simple Example:
It works like a courier service delivering logs to the SOC system.

---

## 8. What is Splunk Enterprise?

Splunk Enterprise is a log management and analysis platform.

It performs:
1. Log ingestion
2. Indexing
3. Searching using SPL
4. Alert generation
5. Dashboard visualization

In this project:
- Received Windows logs
- Detected RDP brute-force attempts
- Triggered alerts
- Displayed dashboard

---

## 9. What is Tailscale?

Tailscale is a secure VPN solution.

Purpose in this project:
- Create encrypted tunnel between EC2 and local Splunk
- Avoid exposing Splunk to public internet

Simple Example:
It is a private underground tunnel between two buildings.

# Windows Security Event Codes Reference

## Authentication Events

4624 – Successful logon  
4625 – Failed logon  
4634 – Logoff  
4647 – User initiated logoff  
4648 – Logon using explicit credentials  
4672 – Special privileges assigned to new logon  

---

## Account Management

4720 – User account created  
4722 – User account enabled  
4723 – Password change attempt  
4724 – Password reset attempt  
4725 – User account disabled  
4726 – User account deleted  

---

## Group Management

4732 – Member added to security-enabled local group  
4733 – Member removed from security-enabled local group  

---

## Audit & Policy Changes

4719 – System audit policy changed  
4739 – Domain policy changed  

---

## Process Monitoring

4688 – New process created  
4689 – Process terminated  

---

## Other Useful Events

4776 – NTLM authentication attempt  
4768 – Kerberos authentication ticket requested  
4769 – Kerberos service ticket requested  

# Windows Logon Types Explanation

Logon Type defines how the authentication occurred.

1 – Interactive  
User logged in locally using keyboard.

2 – Interactive (Same as 1 in many cases)  
Local console login.

3 – Network  
Accessed a shared resource over network (SMB, file share).  
Common for brute-force attempts with NLA enabled.

4 – Batch  
Scheduled task login.

5 – Service  
Service account logon.

6 – Proxy  
Rarely used.

7 – Unlock  
User unlocked workstation.

8 – NetworkCleartext  
Password sent in clear text over network.

9 – NewCredentials  
Used with RunAs command.

10 – RemoteInteractive  
Remote Desktop (RDP) login session.

Important for this project:
- Logon Type 10 = RDP login
- Logon Type 3 = Network logon (may appear for failed RDP with NLA)


# Project Screenshots and Explanation

This section provides visual proof of the cloud infrastructure.

---

## 1. EC2 Instance Running
<img width="1561" height="792" alt="Screenshot 2026-03-03 204203" src="https://github.com/user-attachments/assets/6843186c-8c4c-4192-84ed-db27c111806b" />

Description:
This screenshot shows the Windows EC2 instance running inside the AWS console. The instance is deployed within a custom VPC and public subnet. It has a public IP address assigned and is associated with a Security Group that allows controlled RDP access.

Key Points:
- Instance State: Running
- Public IP: Enabled
- Security Group attached
- Launched inside custom VPC

---

## 2. Windows Server via RDP
<img width="1920" height="1080" alt="Screenshot 2026-03-03 205252" src="https://github.com/user-attachments/assets/2a6ad0cb-5573-4c13-aefe-1af174871896" />

Description:

This screenshot shows the Windows Server accessed via Remote Desktop Protocol (RDP). This confirms that network routing, Internet Gateway, and Security Group rules are correctly configured.

Key Points:
- RDP connection established
- Windows Event Logs generated
- Splunk Universal Forwarder installed on this system

---

## 3. VPC Configuration

<img width="1560" height="789" alt="Screenshot 2026-02-28 231015" src="https://github.com/user-attachments/assets/30a3bb38-1cbc-402c-acf4-5fc9ed6b23dd" />

Description:

This screenshot displays the custom VPC created for the SOC lab environment.

Key Points:
- CIDR block defined (e.g., 10.0.0.0/16)
- Logical network isolation
- Foundation for subnets and routing

Purpose:
To isolate and control cloud network traffic.

---

## 4. Subnet Configuration

<img width="1567" height="801" alt="Screenshot 2026-02-28 231402" src="https://github.com/user-attachments/assets/82d2bca2-4c43-4f6e-8367-3183b5a5585b" />

Description:

This screenshot shows the Public Subnet created inside the VPC.

Key Points:
- Subnet CIDR (e.g., 10.0.1.0/24)
- Associated with route table
- Used to deploy Windows EC2

Purpose:
To logically segment the VPC network.

---

## 5. Internet Gateway Attachment

<img width="1590" height="557" alt="Screenshot 2026-02-28 231220" src="https://github.com/user-attachments/assets/ed9899c1-8eec-4505-9ffd-53a877a31238" />

Description:

This screenshot shows the Internet Gateway attached to the VPC.

Key Points:
- IGW successfully attached
- Enables internet access for public subnet
- Required for RDP access

Purpose:
To allow external connectivity to EC2.

---

## 6. Route Table Configuration

<img width="1583" height="668" alt="Screenshot 2026-02-28 231155" src="https://github.com/user-attachments/assets/103e6595-9dc0-4c4a-9653-69c98331dc29" />

Description:

This screenshot shows the route table associated with the public subnet.

Key Route:
Destination: 0.0.0.0/0  
Target: Internet Gateway

Purpose:
To route internet-bound traffic through the Internet Gateway.

---
## 7. Security Group Configuration
<img width="1587" height="616" alt="Screenshot 2026-02-28 223629" src="https://github.com/user-attachments/assets/46ef6dcf-a2e2-412f-98bf-ad1572f01dea" />

Description:

This screenshot shows the Security Group attached to the Windows EC2 instance. The Security Group acts as a virtual firewall controlling inbound and outbound traffic to the instance.

Key Inbound Rules:

- RDP (Port 3389) allowed only from my public IP address.
- All other inbound traffic restricted.

Key Outbound Rules:

- Default rule allowing outbound traffic to 0.0.0.0/0.

Purpose:

The Security Group ensures that only authorized users can access the EC2 instance via Remote Desktop Protocol (RDP). Restricting RDP access to a specific IP address reduces the attack surface and prevents unauthorized brute-force attempts from random internet sources.

Security Importance:

1. Limits exposure of the EC2 instance.
2. Prevents open RDP access to the internet.
3. Enforces least privilege access control.
4. Acts as the first layer of network-level defense.

---
## 8. EC2 Network Settings During Launch

<img width="1210" height="689" alt="Screenshot 2026-02-28 222841" src="https://github.com/user-attachments/assets/6a02af48-18b7-4d06-bb0f-f65a0732f557" />

Description:

This screenshot shows the network configuration while creating the EC2 instance.

Key Settings:
- Selected custom VPC
- Selected public subnet
- Auto-assign public IP enabled
- Security Group configured for RDP access

Purpose:
To ensure the instance is deployed inside the correct network architecture.

---

## Summary

These screenshots validate the complete infrastructure setup, including:

1. Custom network configuration
2. Secure instance deployment
3. Proper routing
4. Controlled inbound access
5. Functional RDP connectivity

All components together enable secure log generation and forwarding to Splunk Enterprise for monitoring and detection.

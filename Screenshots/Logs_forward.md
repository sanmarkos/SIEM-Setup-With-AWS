# Monitoring and Detection Results

This section provides screenshots and explanation of monitoring components, detection queries, and alert behavior.

---

## 1. Tailscale Connected Devices
<img width="1491" height="510" alt="Screenshot 2026-03-01 125205" src="https://github.com/user-attachments/assets/6be9148b-da6e-4fb7-93c3-d9a017cb3d74" />


Description:

This screenshot shows the Tailscale dashboard displaying connected devices. The Windows EC2 instance and local Splunk system are connected using a private encrypted tunnel.

Purpose:

1. Secure log forwarding without exposing Splunk to public internet.
2. Private IP communication using 100.x.x.x Tailscale network.
3. Encrypted peer-to-peer connectivity.

Security Importance:

This prevents opening Splunk receiving port (9997) to the internet, reducing attack surface.

---

## 2. Splunk Search Result – Windows Logs (index=main)
<img width="1849" height="944" alt="Screenshot 2026-03-01 221804" src="https://github.com/user-attachments/assets/050835db-3fc9-4338-bef8-5852f06dbf0a" />

Query Used:

index=main host="EC2AMAZ-8CSRLOB"

Explanation of Query Components:

index=main  
- "main" is the default index in Splunk.
- Where logs go if you don’t specify any other index
- In this project, Windows event logs are stored in the main index.

host="EC2AMAZ-8CSRLOB"  
- Filters logs from the Windows EC2 instance.
- Ensures we only analyze logs from that specific machine.

What This Screenshot Shows:

1. Windows Application and System logs.
2. EventCode values.
3. Log source (WinEventLog:Application, WinEventLog:System).

Purpose:

To verify that logs from EC2 are successfully ingested into Splunk.

---

## 3. Splunk Internal Logs – Forwarder Communication
<img width="1850" height="940" alt="Screenshot 2026-03-01 213312" src="https://github.com/user-attachments/assets/e3d27898-5d54-457a-9db7-94492ad70cd6" />

Query Used:

index=_internal "TcpInputProc" host="EC2AMAZ-8CSRLOB"

Explanation of Query Components:

index=_internal  
- "_internal" is a special Splunk system index.
- Stores Splunk’s own operational logs.
- Used for troubleshooting ingestion and connectivity issues.
```
Splunk
 ├── main
 ├── _internal
 ├── security
 ├── windows
 └── linux
```
Each one is index

TcpInputProc  
- Internal Splunk process responsible for handling TCP inputs.
- Manages incoming data from forwarders.
- Confirms that Splunk is receiving data over TCP (port 9997).

host="EC2AMAZ-8CSRLOB"  
- Filters logs related to the specific forwarder host.

What This Screenshot Confirms:

1. Splunk forwarder is connected.
2. TCP input is active.
3. Logs are being processed correctly.

Difference Between main and _internal:

main  
> - Stores collected logs (Windows logs in this project.

_internal  
> - Stores Splunk’s own system and operational logs.
---

## 4. RDP Brute-Force Alert Triggered
<img width="1861" height="375" alt="Screenshot 2026-03-03 162731" src="https://github.com/user-attachments/assets/ea2b6158-e4da-4934-9c2b-3bcda217b2cf" />

Description:

This screenshot shows the triggered alert after multiple failed RDP login attempts.

Detection Logic:

index=main EventCode=4625
| stats count by Source_Network_Address
| where count > 5

Explanation:

1. EventCode 4625 represents failed logon attempts.
2. The query counts failed attempts grouped by source IP.
3. If more than 5 failures occur within 5 minutes, the alert triggers.

Alert Configuration:

- Scheduled
- Cron: */5 * * * *
- Time range: Last 5 minutes
- Trigger condition: Results > 0

Purpose:

Detect potential brute-force attacks against the Windows EC2 instance.

---

## 5. SOC Monitoring Dashboard
<img width="1851" height="945" alt="Screenshot 2026-03-03 144923" src="https://github.com/user-attachments/assets/8549bd48-8178-44ea-af43-ada8aea8ff53" />

Description:

This screenshot shows the monitoring dashboard created in Splunk.

Panels Included:

1. Failed Logon Attempts (EventCode 4625)
2. Successful Logon Attempts (EventCode 4624)

Purpose:

1. Real-time monitoring of authentication events.
2. Visual analysis of attack patterns.
3. SOC-style monitoring interface.

Outcome:

The dashboard provides centralized visibility into authentication behavior and potential brute-force activity.

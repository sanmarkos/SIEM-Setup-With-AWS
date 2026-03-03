# RDP Brute-Force Detection Rule

## 1. Log Source

Windows Security Event Log

Event ID: 4625 (Failed Logon)

## 2. Detection Query
To Detect the Failed RDP Logon
```
index=main EventCode=4625 Logon_type=3
| stats count by host Source_Network_Address
| where count > 5
```
To Detect Successful RDP logon
```
index=main EventCode=4625 Logon_type=10
| timechart count
```

## 3. Alert Configuration

Alert Type: Scheduled
Cron Expression: */5 * * * *
Time Range: Last 5 minutes
Trigger Condition: Number of results > 0

## 4. Detection Logic Explanation

The rule counts failed login attempts grouped by source IP address. If any IP generates more than 5 failed attempts within 5 minutes, the alert triggers.

## 5. Purpose

To detect potential RDP brute-force attack attempts against the Windows EC2 instance.

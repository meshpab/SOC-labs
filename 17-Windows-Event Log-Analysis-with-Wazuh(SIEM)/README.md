# Lab 17 - Windows Event Log Analysis with Wazuh(SIEM)

## Objective

The goal of this lab is to monitor and analyze Windows Security Event Logs using Wazuh SIEM. The lab demonstrates how Windows events are collected by the Wazuh agent, forwarded to the Wazuh manager, and analyzed through the Wazuh Dashboard. It focuses on investigating authentication events, user account activity, and security-related logs commonly used during SOC investigations.

## Lab Environment

| Component     | Role                 | IP Address    |
| ------------- | -------------------- | ------------- |
| Kali Linux    | Attacker Machine     | 192.168.56.15 |
| Windows 10    | Target + Wazuh Agent | 192.168.56.11 |
| Ubuntu Server | Wazuh Manager        | 192.168.56.13 |

## Step 1 – Verify Wazuh Agent Status

Before analyzing Windows logs, ensure that the Windows endpoint is actively communicating with the Wazuh Manager.

```
sudo /var/ossec/bin/agent_control -l
```
sudo - Admin mode

/var/ossec/bin/ -wazuh management binaries directory

agent_control- Wazuh management utility used to view and manage all registered agents connected to the Wazuh Manager.

-l -list

![Window agent verification](screenshots/agent-status.png)

### Analysis

Windows agent is Active and is successfully communicating with the Wazuh Manager and sending logs for analysis.

## Step 2 – Verify Windows Security Events Are Being Collected

Now that the Windows Wazuh agent is active, lets confirm that Windows Security Event Logs are being forwarded to the Wazuh Manager and are visible in the Wazuh Dashboard.

Access the Wazuh Dashboard.

Filter to your active agent
```
agent.name:windows10
```
![Wazuh windows event logs](screenshots/windows-events.png)

## Step 3 – Generating Windows Authentication Events (Event IDs 4624 & 4625)

The goal of this step is to generate real Windows authentication events by performing both successful and failed login attempts. These events will be collected by the Wazuh Agent, forwarded to the Wazuh Manager, and displayed in the Wazuh Dashboard for analysis.

| Event ID | Description          |
| -------- | -------------------- |
| 4624     | Successful logon     |
| 4625     | Failed logon attempt |

Lock the Windows Workstation, Generate Failed Logins then Log In Successfully

![Windows event logs](screenshots/windows-logs.png)

3 failed attempts one succsesful login

Verification in Wazuh

Open the Wazuh Dashboard and search for the events:

![Wazuh - windows logs](screenshots/wazuh-logs.png)

Expected Result

You should see entries containing information similar to:

Event ID

Username

Computer Name

Logon Type

Authentication Package

Time Generated

Wazuh Rule Description

Rule Level

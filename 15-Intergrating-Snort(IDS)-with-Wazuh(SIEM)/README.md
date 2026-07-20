# Lab 15 – Integrating Snort IDS with Wazuh SIEM

## Overview

This lab demonstrates how to integrate Snort Intrusion Detection System (IDS) with Wazuh SIEM to centralize network security alerts. By forwarding Snort alerts to Wazuh, security analysts can monitor, investigate, and respond to network-based threats through a single dashboard.

The lab simulates malicious network activity from an attacker machine, detects it with Snort, and forwards the generated alerts to Wazuh for analysis.

## Objectives

- Integrate Snort IDS with Wazuh SIEM.
- Configure Wazuh to collect Snort alert logs.
- Generate network attacks that trigger Snort signatures.
- Verify Snort alerts within the Wazuh Dashboard.
- Investigate network intrusion events using Wazuh.
- Understand how IDS and SIEM platforms work together in a Security Operations Center (SOC).

 ## Lab Environment
 
| Machine       | Role                      | Operating System |
| ------------- | ------------------------- | ---------------- |
| Kali Linux    | Attacker                  | Kali Linux       |
| Ubuntu Server | Snort IDS & Wazuh Manager | Ubuntu Server    |
| Windows 10    | Target                    | Windows 10       |

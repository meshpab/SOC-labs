# Lab 08 - Detecting Network Reconnaissance Using Nmap and Wireshark

## Scenario

A network administrator reports unusual network activity originating from a workstation. You have been tasked with investigating the traffic to determine whether it is consistent with reconnaissance activity.

## Objective

The objective of this lab is to detect and analyze network reconnaissance performed using Nmap by capturing and examining the generated traffic in Wireshark. The lab demonstrates how reconnaissance appears on a network, identifies indicators of scanning activity, and explains how one can recognize and investigate suspicious network behavior.

## Tools Used

| Tool      | Purpose                                  |
| --------- | ---------------------------------------- |
| Nmap      | Network reconnaissance and port scanning |
| Wireshark | Network traffic capture and analysis     |

STEP 1 - Perform nmap scan with different sscans -sn, -sS, -sT, -Sv

STEP 2 -Perform wireshark Aanalysis and filter for specific protocol, ip, port e.t.c

## Wireshark Analysis

### Host Discovery

#### Observation

ICMP Echo Request packets were transmitted from Kali to Ubuntu to determine whether the target was online.

#### Analysis

The target responded with ICMP Echo Replies, confirming it was reachable before further reconnaissance began.

### SYN Scan

#### Observation

Numerous TCP SYN packets were transmitted to different destination ports.

#### Analysis

The scanner attempted to identify open TCP ports without completing the TCP three-way handshake, which is characteristic of an Nmap SYN scan.

### TCP Connect Scan

#### Observation

Complete TCP three-way handshakes (SYN → SYN/ACK → ACK) were observed.

#### Analysis

Unlike the SYN scan, the TCP Connect scan established full connections with open ports, making it more likely to appear in server logs.

#### Detection Rules

| Suspicious Behavior                          | Detection Logic              |
| -------------------------------------------- | ---------------------------- |
| High number of SYN packets to multiple ports | Possible SYN scan            |
| ICMP Echo Requests to many hosts             | Possible host discovery      |
| Connections to many ports in a short time    | Possible reconnaissance      |
| Service probes after connections             | Possible service enumeration |



### Recommendations After results

- Monitor for repeated SYN scans.

- Deploy an IDS/IPS such as Suricata or Snort to detect scanning activity.

- Restrict unnecessary open ports.

- Use firewall rules to limit access to sensitive services.

- Configure alerts for abnormal port-scanning behavior.

- Regularly review firewall and network logs for reconnaissance attempts.

## Skills Demonstrated

- Captured and analyzed network traffic using Wireshark.

- Detected network reconnaissance using Nmap.

- Identified ICMP and TCP scan patterns.

- Applied Wireshark display filters to isolate suspicious traffic.

- Correlated Nmap scan types with observed network behavior.

- Documented indicators of compromise (IOCs).

- Mapped observed activity to the MITRE ATT&CK framework.

- Produced an investigation report with findings and recommendations.

  ## Conclusion

This lab demonstrated how network reconnaissance performed with Nmap can be detected through packet analysis in Wireshark. Host discovery, SYN scanning, TCP Connect scanning, and service version detection each produced identifiable traffic patterns that were successfully analyzed. From a SOC perspective, recognizing reconnaissance activity is essential because it often represents the earliest observable stage of an attack

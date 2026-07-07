# Lab 08 – Detecting Network Reconnaissance Using Nmap and Wireshark

This lab simulates a SOC investigation into suspected network reconnaissance on an internal network.

## Objective

The objective of this investigation is to detect, analyze, and document network reconnaissance performed using Nmap. Packet captures collected with Wireshark are analyzed to identify host discovery, port scanning, and service enumeration activities while documenting indicators of compromise (IOCs) and defensive recommendations.

## Lab Environment


| Component           | Details                      |
| ------------------- | ---------------------------- |
| Attacker            | Kali Linux                   |
| Target              | Ubuntu Server                |
| Packet Analyzer     | Wireshark                    |
| Tool                | Nmap                         |

## Investigation Workflow

i) Reconnaissance Alert
       
ii) Capture Network Traffic
        
iii) Analyze Packet Capture
      
iv) Identify Scan Type
       
v) Collect Evidence
        
vi) Document Findings
        
vii) Recommend Mitigation

## Tools

| Tool              | Purpose                                               |
| ----------------- | ----------------------------------------------------- |
| Nmap              | Host discovery, port scanning and service enumeration |
| Wireshark         | Packet capture and protocol analysis                  |
| Ubuntu SSH Server | Target host     (192.168.56.13)                       |
| Kali Linux        | Scanning workstation    (192.168.56.129)              |

## Investigation Procedure

#### Step 1

Verify connectivity between Kali and Ubuntu.

#### Step 2

Start packet capture using Wireshark.

#### Step 3

Perform Host Discovery

```bash
nmap -sn 192.168.56.13
```
![ARP H0st Discovery](screenshots/ARP-host-discovery.png)

#### Analysis

The successful responses confirmed that the target was online. Host discovery reduces unnecessary scanning by identifying active hosts before port enumeration.

#### Step 4

Perform SYN Scan (TCP half-scan)

Observe open port 22

```bash
sudo nmap -sS 192.168.56.13
```
![TCP Half Scan](screenshots/TCP-Half-scan.png)

#### Analysis

This packet sequence (SYN → SYN/ACK → RST) is characteristic of an Nmap SYN (half-open) scan. By terminating the connection with an RST, Nmap identifies open ports without establishing a complete TCP session.

Step 5

Perform TCP Connect Scan (TCP Full-scan)

```bash
nmap -sT 192.168.56.13
```
Observe open port 22

![TCP Full Scan](screenshots/TCP-full-scan.png)

#### Analysis

The completed handshake (SYN → SYN/ACK → ACK) confirms that this was a TCP Connect scan. Since a full TCP connection was established, the scan is more likely to generate host or application logs than a SYN scan

Step 6

Perform Service Enumeration

Observe open port 22

```bash
sudo nmap -sV 192.168.56.13
```
![Service Version enumeration](screenshots/Service-enumeration.png)

#### Analysis

Unlike a basic port scan, service version detection performs application-level communication to identify services. This provides valuable information, such as the SSH server software and version, which an attacker could use to identify known vulnerabilities or plan further attacks.

## Key Takeaways

- Network reconnaissance is often the first stage of a cyber attack and can be detected through packet analysis.

- Host discovery identifies live systems before port scanning begins.

- A SYN scan identifies open ports without completing the TCP handshake, whereas a TCP Connect scan establishes a full TCP session.

- Service version detection gathers application information that could aid an attacker in identifying potential vulnerabilities.

- Wireshark provides packet-level visibility that complements operating system and application logs.

- Understanding TCP flags and connection states is essential for recognizing reconnaissance activity and differentiating scan types.

## Skills Demonstrated

- Network reconnaissance using multiple Nmap scan techniques.

- Captured and analyzed packet traffic using Wireshark.
  
- Distinguished between different  Nmap scan techniques
  
- Interpreted TCP flags (SYN, ACK, and RST) to determine port states.
  
- Identified reconnaissance activity through packet patterns.
  
- Applied Wireshark display filters to isolate relevant traffic.
  
- Correlated Nmap scan types with observed network behavior.
  
- Documented evidence and produced investigation findings.
  
- Mapped reconnaissance activity to the MITRE ATT&CK framework (Active Scanning – T1595).

Conclusion

This lab demonstrated how Nmap reconnaissance can be detected and investigated using Wireshark. By analyzing host discovery, SYN scans, TCP Connect scans, and service version detection, it was possible to identify the packet patterns associated with each scanning technique. Although Ubuntu host logs showed limited differences between SYN and TCP Connect scans in this lab environment, Wireshark clearly revealed the distinction at the packet level through the TCP handshake behavior. This exercise strengthened practical skills in packet analysis, reconnaissance detection, and documenting security findings from a SOC analyst's perspective.



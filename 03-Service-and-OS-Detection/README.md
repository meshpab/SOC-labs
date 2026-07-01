## 03: Service & Operating System Detection
## Objective

The objective of this lab is to identify services, service versions, and operating systems running on target machines using Nmap. This information helps security analysts understand a target's attack surface during the reconnaissance phase of a security assessment.

##Lab Environment
| Machine  | Operating System | Purpose         |
| -------- | ---------------- | --------------- |
| Attacker | Linux            | Runs Nmap scans |
| Target 1 | Windows          | Scan target     |
| Target 2 | Ubuntu           | Scan target     |


## Tools Used
Nmap

### Task 1 - Identify Target IP Addresses

Windows

on cmd Run:

```
ipconfig
```

Record the IPv4 Address.

Ubuntu

on the terminal Run:

```
ip addr
```

Record IP address

## Task 2 – Service Version Detection

Windows Target

Run:
```
nmap -sV <Windows-IP>
```
mY IP:

```
nmap -sV 192.168.56.11
```

Expected Outcome:

-Detect open ports

-Identify running services

-Display software versions

## Screenshot

Ubuntu Target

Run
```
nmap -sV <Ubuntu-IP>
```
My IP:

```
nmap -sV 192.168.56.13
```

Expected Outcome:

-Detect running services

-Identify application versions

### Screenshot

## Task 3 – Operating System Detection

Windows Target

Run:
```
sudo nmap -O <Windows-IP>
```
My IP

```
sudo nmap -O 192.168.56.11
```
Expected Outcome:

-Detect operating system

-Display OS fingerprint

-Estimate network distance

### Screenshot

Ubuntu Target

Run:

```
sudo nmap -O <Ubuntu-IP>
```
My IP
```
sudo nmap -O 192.168.56.13
```

Expected Outcome:

-Detect Linux operating system

-Display OS fingerprint

### Screenshot



## Observations & Analysis

Windows Service Version Detection (nmap -sV)

### Observations
The Windows host was reachable and responded to Nmap probes.

Three TCP ports were open: 135 (MSRPC), 139 (NetBIOS-SSN), and 445 (Microsoft-DS).

Nmap successfully identified Microsoft services running on the target.

The service information indicated that the operating system is Windows.

### Analysis

The detected services are commonly used for Windows networking and file sharing. These services can be useful for system administration but should be secured because they are frequent targets for attackers.

Windows OS Detection (nmap -O)

### Observations

Nmap identified the target as Microsoft Windows 10.

The OS detection accuracy was high.

The estimated network distance was 1 hop, indicating the target was on the same local network.

### Analysis

OS fingerprinting successfully identified the target operating system, providing valuable information for security assessments and vulnerability identification.

Ubuntu Service Version Detection (nmap -sV)

### Observations

The Ubuntu host responded successfully.

Only port 22 (SSH) was open.

Nmap identified OpenSSH 9.6p1 running on Ubuntu.

The service information confirmed the operating system as Linux.

### Analysis

The Ubuntu system exposed only the SSH service, indicating a smaller attack surface compared to the Windows host.

## Key Takeaways
Service version detection identifies applications running on open ports.

OS detection estimates the target operating system using TCP/IP fingerprinting.

Windows exposed more services than Ubuntu in this lab.

Ubuntu presented a smaller attack surface with only SSH exposed.

Firewalls can limit the amount of information revealed during reconnaissance.

Combining service and OS detection provides a better understanding of the target environment.

Ubuntu OS Detection (nmap -O)

### Observations

Nmap identified the target as a Linux-based operating system.

The scan estimated a Linux kernel version.

Network distance was 1 hop, confirming local network connectivity.

### Analysis

OS detection successfully recognized the target as Linux. Although Nmap listed several possible Linux variants, it correctly classified the operating system family.

## Firewall Observation

During the initial scans, the Windows firewall prevented Nmap from accurately identifying services and the operating system. After temporarily disabling the firewall, the scans successfully detected open ports, service versions, and operating system information.

This demonstrates that host-based firewalls can significantly reduce the amount of information exposed during network reconnaissance and help protect systems from unauthorized enumeration.

## Conclusion
This lab demonstrated how to use Nmap to identify running services, software versions, and operating systems on Windows and Ubuntu targets. The information collected during this phase helps security analysts understand the target environment, identify potential vulnerabilities, and plan further security assessments.

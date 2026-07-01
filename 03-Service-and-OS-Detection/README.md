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
-Nmap

### Task 1 - Identify Target IP Addresses
Windows

on cmd Run:

'ipconfig'

Record the IPv4 Address.

Ubuntu

on the terminal Run:

'ip addr'

Record IP address

## Task 2 – Service Version Detection

Windows Target

Run:

nmap -sV <Windows-IP>

nmap -sV 192.168.56.11

Expected Outcome
-Detect open ports
-Identify running services
-Display software versions

## Screenshot

Ubuntu Target

Run

nmap -sV <Ubuntu-IP>

nmap -sV 192.168.56.13

Expected Outcome
-Detect running services
-Identify application versions

### Screenshot

## Task 3 – Operating System Detection

Windows Target

Run:

sudo nmap -O <Windows-IP>

Expected Outcome
-Detect operating system
-Display OS fingerprint
-Estimate network distance

### Screenshot

Ubuntu Target

Run:

sudo nmap -O <Ubuntu-IP>

Expected Outcome
-Detect Linux operating system
-Display OS fingerprint

### Screenshot



## Important Analysis quiz
1.Which ports were open?
2.Which services were detected?
3.What versions of the services were identified?
4.Was the operating system correctly identified?
5.Why is service and OS detection important during reconnaissance?

## Key Takeaways
-Service version detection identifies applications running on open ports.
-Operating system detection estimates the target's operating system through TCP/IP fingerprinting.
-Combining these scans provides valuable information for vulnerability assessment and network security analysis.

## Conclusion

This lab demonstrated how to use Nmap to identify running services, software versions, and operating systems on Windows and Ubuntu targets. The information collected during this phase helps security analysts understand the target environment, identify potential vulnerabilities, and plan further security assessments.

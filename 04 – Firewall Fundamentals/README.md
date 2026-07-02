## Lab 04 - Firewall Fundamentals

## Objective

Learn the fundamentals of host-based firewalls by configuring firewall rules on Windows 10 and Ubuntu Server, then observe how those rules affect network reconnaissance using Nmap from Kali Linux.

## Lab Environment

| Machine  | Operating System                     | Role                      |
| -------- | ------------------------------------ | ------------------------- |
| Attacker | Kali Linux                           | Reconnaissance & Scanning |
| Target 1 | Windows 10                           | Windows Target            |
| Target 2 | Ubuntu Server                        | Linux Server Target       |
| Tools    | Nmap, Windows Defender Firewall, UFW | Security Tools            |


## STEP 1 — Identify IP Addresses

Before scanning, determine the IP address of each machine.

Kali Linux:

```Bash
ip addr
```
or


```Bash
ip a
```
Kali IP: 192.168.56.15

Windows 10:

Open Cmd:

```
ipconfig
```

Windows IP: 192.168.56.11

Ubuntu server:

```Bash
ip addr
```

or

```Bash
ip a
```
Ubuntu IP: 192.168.56.13

## STEP 2 — Verify Connectivity

From Kali Linux:

```
ping <Windows-IP>
```
Then,

```
ping <Ubuntu-IP>
```

### Observation

Are replies received?

Any packet loss?


![Host up](Host-up.png)


Host up and active

ping 192.168.56.11 (windows machine) 5 packets transmitted, 5 packets received, 0% packet loss

ping 192.168.56.11 (Ubuntu server machine) 5 packets transmitted, 5 packets received, 0% packet loss

Host down
 
![Host down](Host-down.png)

ping 192.168.56.11 (windows machine) 6 packets transmitted, 0 packets received, 100% packet loss

ping 192.168.56.13 (Ubuntu server  machine) 8 packets transmitted, 0 packets received, 100% packet loss




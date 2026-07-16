# Lab 05 - Nmap Scripting Engine (NSE)

## Objective

Use Nmap Scripting Engine (NSE) to gather more information about target systems and perform safe enumeration of network services.

## Lab Environment

| Machine       | Operating System | Role     |
| ------------- | ---------------- | -------- |
| Kali Linux    | Linux            | Attacker |
| Windows 10    | Windows          | Target   |
| Ubuntu Server | Ubuntu           | Target   |

## Tools

-Nmap

-NSE Scripts

### Commands

nmap -Pn -sC 

nmap -Pn --script banner

### Windows

### Default NSE script
```bash
nmap -Pn -sC 192.168.56.11
```

![Windows-NSE-scripts](screenshots/Windows-default-NSE.png)

### Observation 

Target successfully reached and responded to the scan.

Identified 3 open TCP ports

NSE scripts gathered additional SMB information, security mode indicated that message signing was enabled but not required.

Identified the NetBIOS computer name of the Windows host.

These reconnaissance  provide useful information for identifying Windows systems and exposed services.

### Banner grabbing

```bash
nmap -Pn ---script banner 192.168.56.11
```

![Windows-banner](screenshots/Windows-banner.png)

### Observation 

Banner grabbing successfully identified the services running on the open ports.

Target operating system identifiied as Windows.

Banner information helps verify exposed services 

### Ubuntu Server

Since UFW blocked all incoming services, port 22 (SSH) was temporarily allowed to demonstrate safe NSE enumeration.

 ### Banner grabbing
 
 ```bash
 nmap -Pn -sV --script banner 192.168.56.13
 ```
![Ubuntu-banner-retrieval](screenshots/ubuntu-banner-retrieval.png)

### ssh-hostkey retrieval
```bash
nmap -Pn --script ssh-hostkey 192.168.56.13
```

![Ubuntu-ssh-hostkey](screenshots/ubuntu-ssh-hostkey.png)

### Assessment 

| Assessment                  | Result                        |
| --------------------------- | ----------------------------- |
| Host Reachability           | ✅ Reachable                   |
| Firewall Status             | ✅ Active (999 ports filtered) |
| Exposed Service             | SSH (Port 22)                 |
| Banner Retrieved            | ✅ Successfully                |
| SSH Host Keys Retrieved     | ✅ Successfully                |
| Operating System Identified | Ubuntu Linux                  |

## Conclusion

NSE provided additional service information beyond a basic port scan while using safe enumeration techniques. Firewall controls significantly reduced exposed services, and controlled access to SSH enabled successful banner and host-key retrieval for analysis.

## Key Takeaways

UFW successfully blocked all unnecessary ports.

SSH was intentionally allowed for controlled testing.

Banner grabbing revealed the running SSH software and version.

The ssh-hostkey NSE script retrieved the server's public cryptographic identity.

Limiting exposed services significantly reduces the system's attack surface while still allowing secure administration.


## Skills Demonstrated

- Nmap Scripting Engine (NSE)
  
- Default NSE Script Execution (`-sC`)
  
- Banner Grabbing
  
- SSH Host Key Enumeration
  
- SMB Enumeration
  
- Service Version Detection
  
- Windows Service Enumeration
  
- Linux Service Enumeration
  
- Firewall Analysis (UFW)
  
- Network Reconnaissance


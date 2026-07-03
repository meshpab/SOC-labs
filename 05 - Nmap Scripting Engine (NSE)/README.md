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

nmap -Pn ---script banner



### Ubuntu Server

Since UFW blocked all incoming services, port 22 (SSH) was temporarily allowed to demonstrate safe NSE enumeration.
 banner grabbing
 
 ```bash
nmap -Pn --script banner 192.168.56.13
```

![Ubuntu-banner-retrieval](screenshots/ubuntu-banner-retrieval.png)

### ssh-hostkey retrieval

```bash
nmap -Pn --script ssh-hostkey 192.168.56.13
```
![Ubuntu-ssh-hostkey](screenshots/ubuntu-ssh-hostkey.png)

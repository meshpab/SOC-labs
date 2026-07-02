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


sudo nmap -Pn -sV -sC

Firewall blocks open ports therefore we intentionally open port 22 for observation

![Default-NSE-script](screenshots/default-NSE-script)

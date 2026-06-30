# Lab 01 - Network Discovery

## Objective

Perform host discovery on the VMware Host-Only network to identify active devices and verify their IP addresses using Nmap/Zenmap 

## Environment

- VMware Workstation
- Kali Linux
- Ubuntu Server
- Windows 10

## Network Configuration

- Network Type: Host-Only
- Subnet: 192.168.56.0/24

## Commands Used

### Kali Linux

```bash
ip addr
nmap -sn 192.168.56.0/24
```
ip addr/ ip a -to discover ip address and subnet iof KALI linux
nmap -sn 192.168.56.0/24 - nmap command to discover active devices in the Host-Only network
### Windows

```cmd
ipconfig
```
ipconfig - to find the ip and subnet of the windows machine

### Ubuntu

```bash
ip addr
```

ip addr/ ip a -to discover ip address and subnet of the Ubuntu 

## Findings

| Device              | IP Address     | Notes                    |
| ------------------- | -------------- | ------------------------ |
| Windows 10          | 192.168.56.11  | Virtual Machine          |
| Ubuntu              | 192.168.56.13  | Virtual Machine          |
| Kali Linux          | 192.168.56.129 | Virtual Machine          |
| VMware Host Adapter | 192.168.56.1   | VMware Host-Only Adapter |
| VMware DHCP Service | 192.168.56.254 | VMware DHCP Service      |


## Analysis

The scan discovered five active hosts.

Three of the hosts were the virtual machines running in VMware. The remaining two IP addresses belonged to VMware networking services, showing that host discovery can identify both end devices and supporting network infrastructure.

## Evidence

screenshots available on screenshot folder

## Lessons Learned

- Determined the subnet using `ip addr``ip a`.
- Performed host discovery using Nmap.
- Verified IP addresses on Windows and Ubuntu.
- Identified VMware virtual networking components.

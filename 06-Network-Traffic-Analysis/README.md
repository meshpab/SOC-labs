# 06 – Network Traffic Analysis

## Objective

Capture and analyze network traffic  to identify common network protocols and understand communication between hosts.

## Lab Environment

| Machine       | Operating System | Role           |
| ------------- | ---------------- | -------------- |
| Kali Linux    | Linux            | Packet Capture |
| Windows 10    | Windows          | Target         |


## Tools

Wireshark

Ping

Nmap

### ICMP Analysis

```bash
ping 192.168.56.11
```
![Wireshark-ICMP-Analysis](screenshots/Wireshark-ICMP.png)

### TCP Analysis

```bash
nmap -Pn 192.168.56.11
```
![Wireshark-TCP-Analysis](screenshots/Wireshark-TCP.png)

## Observations

ICMP packets showed successful communication between hosts.

TCP packets revealed the connection attempts made during the Nmap scan.

Packet analysis identified the protocols used during communication.

Wireshark provided visibility into individual packets exchanged across the network.

## Skills Demonstrated

- Packet Capture
  
- Packet Analysis
  
- Protocol Identification
  
- ICMP Traffic Analysis
  
- TCP Traffic Analysis
  
- Wireshark Filtering
  
- Network Monitoring
  
- Basic SOC Investigation

## Conclusion

Wireshark enabled detailed inspection of network traffic generated during communication and scanning activities. Packet analysis provided visibility into protocols, connection behavior, and network events, demonstrating a core skill required for SOC analysts.

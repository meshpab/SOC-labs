# Lab 11 – Investigating TCP Connections and the Three-Way Handshake Using Wireshark

## Scenario

The Security Operations Center (SOC) received an alert indicating that a Windows 10 workstation established a TCP connection with an internal Ubuntu web server. As a SOC analyst, you have been tasked with investigating the network traffic to determine how the connection was established, verify whether communication completed successfully, and identify any indicators of suspicious network activity.

## Objective

The objective of this investigation is to capture and analyze TCP traffic generated between a Windows 10 workstation and an Ubuntu Server hosting a Python HTTP web server. The investigation focuses on identifying the TCP three-way handshake, analyzing TCP flags, sequence and acknowledgement numbers, application-layer communication, connection termination, and retransmissions to understand normal TCP communication and establish a baseline for future threat investigations.

## Lab Environment

| Component      | Description                    |
| -------------- | ------------------------------ |
| Client         | Windows 10                     |
| Server         | Ubuntu Server                  |
| Packet Capture | Wireshark                      |
| Web Server     | Python HTTP Server             |
| Browser        | Microsoft Edge / Google Chrome |
| Network Mode   | NAT                            |
| Protocols      | TCP, HTTP                      |

## Tools Used

Wireshark

Windows Command Prompt

Ubuntu Terminal

Python 3

Web Browser

## Network Topology

                  NAT Network

        +---------------------------+
        | Ubuntu web Server             |
        | Python HTTP Server        |
        | TCP Port 8080             |
        +-------------+-------------+
                      |
                TCP Communication
                      |
        +-------------+-------------+
        | Windows 10                |
        | Wireshark Packet Capture  |
        | Web Browser               |
        +---------------------------+

## Step 1 – Verify Network Connectivity

Command

```cmd
ping <Ubuntu-IP>
```
### Observation

Ubuntu Server replies successfully.

Packet loss (if any).

Average round-trip time (RTT).
Analysis

Successful replies confirm that both hosts can communicate before application traffic is generated.

[!Network Connectivity](screenshots/Network-connectivity.png)

## Step 2 – Identify the Ubuntu Server IP Address

Command (Ubuntu)

```
ip addr
```
#### Observation

Record the server's IPv4 address.

#### Analysis

The IP address identifies the destination host for the upcoming TCP session and helps correlate captured packets.

![Ubuntu server ip addr](screenshots/Ubuntu-ip.png)

Step 3 – Start the Python HTTP Server

Ensure firewall allows the listening port 8080

Command
```
python3 -m http.server 8080
```
#### Observation

The terminal displays a message indicating that the server is listening on TCP port 8080.

#### Analysis

The Ubuntu Server is now ready to accept incoming HTTP connections from the Windows workstation.

![Start server port 8080](screenshots/start.server.png)

### Step 4 – Start Packet Capture

Open Wireshark on Windows.

Select the active network adapter.

Click Start Capture.

Observation

Packet capture begins successfully.

Analysis

Capturing before any communication ensures the complete TCP session is recorded, including connection establishment and termination.

![Start wireshark](screenshots/Wireshark.Ethernet0.png)

### Step 5 – Generate TCP Traffic

Open a browser on Windows and visit:
```
http://<Ubuntu-I>:8080
```
#### Observation

The browser successfully loads the default Python web server page.

Ubuntu terminal logs the incoming HTTP request.

### Analysis

Opening the webpage generates a complete TCP communication session suitable for packet analysis.

![Generate TCP traffic](screenshots/HTTP-traffic.png)

Browser displaying the webpage.

Ubuntu terminal showing the HTTP request.

### Step 6 – Filter TCP Traffic

Wireshark Filter
```
tcp.port == 8080
```
#### Observation

Only TCP packets exchanged between Windows and Ubuntu are displayed for port 8080.

#### Analysis

Filtering removes unrelated traffic and simplifies the investigation.

![Packet filtration port 8080](screenshots/TCP-filtered.png)

## Step 7 – Investigate the TCP Three-Way Handshake

Locate the following packets:

SYN

SYN, ACK

ACK

### Observe

Source IP

Destination IP

Source Port

Destination Port

Sequence Number

Acknowledgement Number

TCP Flags

Timestamp

#### Analysis

The three packets confirm successful connection establishment.

| Packet   | Purpose                          |
| -------- | -------------------------------- |
| SYN      | Client requests a TCP connection |
| SYN, ACK | Server acknowledges the request  |
| ACK      | Client confirms the connection   |



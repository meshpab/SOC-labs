# Port Scanning with Nmap

## Objective

Perform TCP port scanning against Windows 10 and Ubuntu Server using Nmap to identify exposed network services and compare how different scan techniques reveal system information.

## Lab Environment

| Component  | Details             |
| ---------- | ------------------- |
| Hypervisor | VMware Workstation  |
| Attacker   | Kali Linux          |
| Target 1   | Windows 10          |
| Target 2   | Ubuntu Server (CLI) |
| Network    | VMware Host-Only    |


### Tools Used

Nmap

Kali Linux

VMware Workstation

### Scan techniques

| Scan Type        | Command                     | Purpose                              |
| ---------------- | --------------------------- | ------------------------------------ |
| Default Scan     | `nmap <IP>`                 | Scan the 1,000 most common TCP ports |
| Specific Ports   | `nmap -p 22,80,443 <IP>`    | Scan selected ports                  |
| Port Range       | `nmap -p 1-1000 <IP>`       | Scan a defined range                 |
| Full TCP Scan    | `nmap -p- <IP>`             | Scan all 65,535 TCP ports            |
| TCP Connect Scan | `nmap -sT <IP>`             | Complete TCP three-way handshake     |
| SYN Scan         | `sudo nmap -sS <IP>`        | Perform a half-open (stealth) scan   |
| Save Output      | `nmap -oN results.txt <IP>` | Save scan results to a text file     |

## Results

### Windows 10

### Default Scan

Command

```bash
nmap 192.168.56.11
```
### Evidence

![Windows Default Port Scan](screenshots/01-default-port-scan-windows.png)

### Observation

Host was reachable. 

Several ports appeared filtered, indicating firewall restrictions.

### Specific port scan

command 
```bash
nmap -p 22,80,443 192.168.56.11
```
nmap
![Windows Specific Ports](screenshots/02-specific-ports-windows.png)

### Observation

The scan identified ports 22, 80, and 443 as filtered. This indicates that inbound traffic to these ports was being filtered by the host firewall, reducing the system's exposure to network reconnaissance.

port range scan 
Command

```bash
nmap -p 1-1000 <target-ip>
```

### Evidence

![Windows Port Range](screenshots/03-port-range-windows.png)

### SYN Scan

Command

```bash
sudo nmap -sS 192.168.56.11
```
### Evidence

![Windows SYN Scan](screenshots/05-syn-scan-windows.png)

### Observation

Port 7680/TCP was identified as open.
SYN scanning revealed additional information compared to the default scan.

## Ubuntu Server

### Default Scan

 Command

```bash
nmap 192.168.56.13
```

### Evidence

![Default Port Scan](screenshots/01-default-port-scan.Ubuntu.png)

### Observation

Port 22/TCP (SSH) was open.

Remaining common ports were closed.

### Full Port Scan

Command

```bash
nmap -p- 192.168.56.13
```
### Evidence

![Ubuntu All Ports](screenshots/04-all-ports-scan.Ubuntu.png)

### Observation

The full TCP scan identified additional services including:



22	SSH

1514	Wazuh Agent Communication

1515	Wazuh Enrollment

5601	Kibana Dashboard

| Feature      | Windows 10                      | Ubuntu Server                  |
| ------------ | ------------------------------- | ------------------------------ |
| Default Scan | Multiple filtered ports         | SSH detected                   |
| Full Scan    | Limited due to firewall         | Additional services discovered |
| SYN Scan     | Revealed additional information | Confirmed exposed services     |






### 3. Scan a Range of Ports

```bash
nmap -p 1-1000 <target-ip>
```

**Explanation**

- `-p` = **Ports**
- `1-1000` = Scans ports 1 through 1000.

---

### 4. Scan All TCP Ports

```bash
nmap -p- <target-ip>
```

**Explanation**

- `-p-` = Scans **all TCP ports (1–65535)**.

---

### 5. TCP Connect Scan

```bash
nmap -sT <target-ip>
```

**Explanation**

- `-sT` = **TCP Connect Scan**
- Performs a full TCP three-way handshake.
- Does **not** require root/administrator privileges.

---

### 6. SYN Scan

```bash
sudo nmap -sS <target-ip>
```

**Explanation**

- `sudo` = Runs the command with administrator (root) privileges.
- `-sS` = **SYN Scan** (also called a stealth or half-open scan).
- Faster than a TCP Connect scan and commonly used in security assessments.

---

### 7. Save Scan Results

```bash
nmap -oN port-scan-results.txt <target-ip>
```

**Explanation**

- `-oN` = **Output Normal**. Saves the scan output in a human-readable text file.
- `port-scan-results.txt` = Name of the output file.

## Results
### 1. Default Port Scan

**Command**

```bash
nmap <target-ip>
```


#### Ubuntu


**Findings**

- Host was up.
- Port 22 (SSH) was open.
- Remaining common ports were closed.

#### Windows



**Findings**

- Host was reachable.
- Most ports were filtered.
- Firewall appeared to block scan responses.

---
### 2. Specific Ports Scan

```bash
nmap -p 22,80,443 <target-ip>
```

#### Ubuntu

![Ubuntu Specific Port Scan](screenshots/02-specific-ports-scan.Ubuntu.png)

#### Windows


---
### 3. Port Range Scan

```bash
nmap -p 1-1000 <target-ip>
```

#### Ubuntu

![Ubuntu Port Range](screenshots/03-port-range-scan.Ubuntu.png)

#### Windows



---
### 4. All Ports Scan

```bash
nmap -p- <target-ip>
```

#### Ubuntu



#### Windows

![Windows All Ports](screenshots/04-all-ports-windows.png)

---
### 5. SYN Scan

```bash
sudo nmap -sS <target-ip>
```

#### Ubuntu



#### Windows



---
## Analysis


The port scans demonstrated how Nmap identifies network services exposed on different operating systems. The Ubuntu machine consistently showed port 22 (SSH) as open, indicating that remote access via SSH was enabled. When all TCP ports were scanned, additional open ports (1514, 1515, and 5601) were discovered, showing that a full port scan can reveal services that are not identified during the default scan.

The Windows machine produced different results, with many ports appearing as filtered during the default scan. This suggests that firewall rules were restricting responses to Nmap probes. However, the SYN scan detected port 7680 as open, demonstrating that different scanning techniques can produce different results depending on the target's configuration.

Overall, the lab highlighted the importance of selecting appropriate scan types and interpreting scan results based on the operating system and network security controls.


## Key Takeaways


- Learned how to perform port scanning using Nmap.
- Understood the purpose of the default, specific port, port range, full port, and SYN scans.
- Learned the difference between open, closed, and filtered ports.
- Observed that Ubuntu and Windows respond differently to port scans.
- Discovered that scanning all ports may reveal additional services not detected by a default scan.
- Improved understanding of how firewall configurations affect scan results.

## Conclusion

This lab introduced the fundamentals of port scanning using Nmap in a controlled environment. By scanning both Ubuntu and Windows systems, I gained practical experience in identifying open ports, interpreting scan results, and comparing how different operating systems respond to network reconnaissance. The knowledge gained from this lab provides a solid foundation for the next stage of reconnaissance, which involves identifying the services and operating systems running on the discovered open ports.

## Next Steps

The next lab will focus on Service Version Detection and Operating System Detection using Nmap to identify the software versions and operating systems running on the discovered open ports.

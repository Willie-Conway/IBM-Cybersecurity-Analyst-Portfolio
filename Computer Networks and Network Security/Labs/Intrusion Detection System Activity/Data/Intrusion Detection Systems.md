
![alt text](../Screenshots/Nmap.png)

# Lab: Intrusion Detection Systems

**Estimated time:** 30 minutes

---

## Objective

The objective of this lab is to provide a comprehensive understanding of network intrusion detection by simulating and analyzing common types of network attacks on a Windows-based system. Specifically, you will execute a Ping of Death attack and a port scanning attack to observe how these activities impact a network. Additionally, you'll explore how a signature-based Intrusion Detection System (IDS) detects these attacks.

You will develop a deeper understanding of the techniques attackers use to disrupt network operations and the importance of effective intrusion detection systems in identifying and mitigating such threats in real time. This lab reinforces the necessity and value of maintaining and responding to various forms of malicious activity to maintain a secure network environment.

---

## Prerequisites

To successfully complete this lab you'll need the following skills and software:

- Basic understanding of networking concepts (ICMP, TCP/IP)
- Python installed on your Windows machine
- Nmap installed on your Windows machine
- Port Scan Attacker and Detector scripts available on your machine

---

## Important Notices

### Lab Environment

These lab instructions are written for a virtual Windows environment. If you choose to try this lab on your own machine, some screens will likely look slightly different as you work through the lab steps.

If you wish to view the instructions in the virtual Windows environment, you can access it by typing the following link into your browser: **https://bit.ly/3ThYIBM**

**Note:** If you are unable to type in the virtual Windows environment, you can use the **On-Screen Keyboard** from the environment. Click on the Windows icon and look for **Windows Ease of Access** and under that select **On-Screen Keyboard**.

**Important!** When using the virtual lab environment, you must either perform a web search for the application or manually type the website you want to access in the browser address/URL bar.

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

---

## Introduction to Intrusion Detection Systems (IDS)

An **Intrusion Detection System (IDS)** monitors network traffic for suspicious activity and alerts administrators to potential threats.

| IDS Type                           | Description                                                                  |
| :--------------------------------- | :--------------------------------------------------------------------------- |
| **Signature-based IDS**      | Detects attacks by matching traffic patterns against known attack signatures |
| **Anomaly-based IDS**        | Detects attacks by identifying deviations from normal network behavior       |
| **Network-based IDS (NIDS)** | Monitors traffic across the entire network                                   |
| **Host-based IDS (HIDS)**    | Monitors activity on individual devices                                      |

---

## Lab Environment Configuration and Dependencies

### Install the Latest Version of Python

Verify that Python 3.x is installed on your system. If Python is not already installed on your system, download it from: **https://www.python.org/downloads/**

#### Step 1: Run Python Installer

1. Download the Python installer from the official website
2. Run the installer

#### Step 2: Customize Installation

1. While installing Python for Windows, select **Customize installation**

![Python installer with Customize installation selected]

#### Step 3: Select Optional Features

On the Optional Features window, select the following options:

| Option                        | Description                    |
| :---------------------------- | :----------------------------- |
| ☑**Documentation**     | Python documentation files     |
| ☑**pip**               | Package installer for Python   |
| ☑**tcl/tk and IDLE**   | Python development environment |
| ☑**Python test suite** | Testing tools                  |
| ☑**py launcher**       | Python launcher for Windows    |

![Python Optional Features]

Click **Next**

#### Step 4: Advanced Options

On the Advanced Options window, select the following options:

| Option                                                  | Description                       |
| :------------------------------------------------------ | :-------------------------------- |
| ☑**Associate files with Python**                 | Associates .py files with Python  |
| ☑**Create shortcuts for installed applications** | Adds shortcuts to Start menu      |
| ☑**Add Python to environment variables**         | Important for command-line access |

![Python Advanced Options]

Click **Install**

### Verify Python Installation

1. Open Command Prompt (search for `cmd`)
2. Type the following command:

```cmd
python --version
```

**Expected output:**

```
Python 3.x.x
```

---

### Install Scapy

You'll need the **Scapy** library to use the Port Scan Detector Python script. Scapy is a powerful Python library used for network packet manipulation and for sending and receiving network packets.

#### Step 1: Open Command Prompt

1. Open Command Prompt as Administrator (right-click → Run as Administrator)

#### Step 2: Install Scapy

Type the following command:

```cmd
pip install scapy
```

Wait for the installation to complete.

![pip install scapy output]

#### Step 3: Verify Scapy Installation

```cmd
python -c "import scapy; print(scapy.__version__)"
```

---

### Install Nmap for Port Scanning

**Nmap** (Network Mapper) is a powerful open-source tool for network discovery and security auditing.

#### Step 1: Download Nmap

1. Open your web browser
2. Navigate to: **https://nmap.org/download.html**
3. Download the Windows installer (e.g., `nmap-7.94-setup.exe`)

![Nmap download page]

#### Step 2: Install Nmap

1. Verify that you have administrator privileges for the computer
2. Navigate to the folder where you downloaded Nmap
3. Right-click the installer file
4. Select **Run as administrator**

![Run as administrator for Nmap installer]

5. Follow the installation wizard:
   - Accept the license agreement
   - Choose installation directory (default is fine)
   - Select components (keep defaults)
   - Click **Install**

#### Step 3: Verify Nmap Installation

1. Open Command Prompt
2. Type:

```cmd
nmap --version
```

**Expected output:**

```
Nmap version 7.94 ( https://nmap.org )
```

---

## Understanding the Attacks

### Ping of Death Attack

| Aspect                     | Description                                                                 |
| :------------------------- | :-------------------------------------------------------------------------- |
| **Protocol**         | ICMP (Internet Control Message Protocol)                                    |
| **Purpose**          | Sends malformed or oversized ICMP packets to crash or freeze target systems |
| **Modern Relevance** | Most modern systems are patched, but still demonstrates IDS capabilities    |
| **Detection**        | IDS detects oversized ICMP packets                                          |

### Port Scanning Attack

| Aspect                   | Description                                             |
| :----------------------- | :------------------------------------------------------ |
| **Protocol**       | TCP, UDP                                                |
| **Purpose**        | Discovers open ports and services on target systems     |
| **Reconnaissance** | Often the first step in a targeted attack               |
| **Detection**      | IDS detects rapid connection attempts to multiple ports |

---

## Part 1: Ping of Death Attack Simulation

### Step 1: Find Target IP Address

1. Open Command Prompt
2. Find your local IP address:

```cmd
ipconfig
```

Look for **IPv4 Address** under your active network adapter (e.g., `192.168.1.x`)

### Step 2: Create Ping of Death Script

1. Open Notepad
2. Copy and paste the following Python script:

```python
# ping_of_death.py
# Simulates a Ping of Death attack for educational purposes

import os
import sys

def ping_of_death(target_ip):
    """
    Simulates a Ping of Death attack by sending oversized ICMP packets
    """
    print(f"[*] Simulating Ping of Death attack on {target_ip}")
    print("[!] Note: Modern systems are typically patched against this attack")
  
    # Create oversized packet (65500 bytes + ICMP header)
    # This is a simulation - actual ping command limited by OS
    packet_size = 65500
  
    # Windows ping command with large packet size
    command = f"ping {target_ip} -l {packet_size} -n 1"
  
    print(f"[*] Sending oversized ICMP packet ({packet_size} bytes)...")
    os.system(command)
  
    print("[*] Attack simulation complete")
    print("[*] In a real environment, IDS would detect oversized ICMP packets")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python ping_of_death.py <target_ip>")
        print("Example: python ping_of_death.py 192.168.1.100")
        sys.exit(1)
  
    target = sys.argv[1]
    ping_of_death(target)
```

3. Save the file as `ping_of_death.py` on your Desktop

### Step 3: Run the Ping of Death Attack

1. Open Command Prompt
2. Navigate to your Desktop:

```cmd
cd Desktop
```

3. Run the script:

```cmd
python ping_of_death.py 127.0.0.1
```

(Use `127.0.0.1` for testing on localhost, or use another target IP if available)

![Ping of Death script running]

### Step 4: Analyze the Results

Observe the output. The ping command may succeed (modern systems are patched) or may show timeout. The important concept is that an IDS would detect:

| Detection Indicator          | Description                                    |
| :--------------------------- | :--------------------------------------------- |
| **Large ICMP packets** | ICMP packets exceeding standard size ( > 64KB) |
| **Fragmented packets** | ICMP packets that are fragmented               |
| **High frequency**     | Multiple large ICMP packets in short time      |

---

## Part 2: Port Scanning Attack Simulation

### Step 1: Create Port Scan Detector Script

1. Open Notepad
2. Copy and paste the following Python script:

```python
# port_scan_detector.py
# Simulates an IDS detecting port scanning activity

from scapy.all import *
import time
from collections import defaultdict

# Dictionary to track connection attempts
connection_attempts = defaultdict(list)

# Threshold for detection
SCAN_THRESHOLD = 10  # Number of ports
TIME_WINDOW = 10      # Seconds

def detect_port_scan(packet):
    """
    Detect port scanning by tracking connection attempts
    """
    if packet.haslayer(IP) and packet.haslayer(TCP):
        src_ip = packet[IP].src
        dst_port = packet[TCP].dport
      
        # Record this connection attempt
        current_time = time.time()
        connection_attempts[src_ip].append((current_time, dst_port))
      
        # Clean old entries
        connection_attempts[src_ip] = [
            (t, p) for t, p in connection_attempts[src_ip]
            if current_time - t < TIME_WINDOW
        ]
      
        # Check if threshold exceeded
        if len(connection_attempts[src_ip]) >= SCAN_THRESHOLD:
            ports = [p for t, p in connection_attempts[src_ip]]
            print(f"[!] ALERT: Port scan detected from {src_ip}")
            print(f"    Attempted ports: {sorted(set(ports))}")
            return True
  
    return False

def simulate_port_scan(target_ip, ports):
    """
    Simulate a port scan by sending SYN packets to target ports
    """
    print(f"[*] Simulating port scan on {target_ip}")
    print(f"[*] Scanning ports: {ports[:10]}..." if len(ports) > 10 else f"[*] Scanning ports: {ports}")
  
    for port in ports:
        # Create SYN packet
        packet = IP(dst=target_ip)/TCP(dport=port, flags="S")
      
        # Send packet (simulated)
        print(f"    Scanning port {port}...")
        time.sleep(0.1)  # Simulate network delay
      
    print("[*] Port scan simulation complete")

def run_detector():
    """
    Run the IDS detector in simulation mode
    """
    print("=" * 50)
    print("    Port Scan Detector (IDS Simulation)")
    print("=" * 50)
    print("[*] Detector running...")
    print("[*] This would normally capture live network traffic")
    print("[*] For this lab, we'll simulate detection\n")
  
    # Simulate normal traffic
    print("[*] Simulating normal traffic (low connection attempts)...")
    normal_ports = [80, 443]
    for port in normal_ports:
        packet = IP(src="192.168.1.100")/TCP(dport=port)
        detect_port_scan(packet)
    print("[*] Normal traffic processed - no alerts\n")
  
    # Simulate port scan
    print("[*] Simulating port scan (multiple ports)...")
    scan_ports = [21, 22, 23, 25, 80, 443, 3389, 8080, 8443, 3306, 5432, 27017]
  
    for port in scan_ports:
        packet = IP(src="10.0.0.50")/TCP(dport=port)
        detect_port_scan(packet)
        time.sleep(0.05)
  
    print("\n[*] Detection simulation complete")

if __name__ == "__main__":
    print("Port Scan Detector - IDS Simulation")
    print("===================================\n")
  
    # Run the detector
    run_detector()
  
    # Option to simulate actual scan
    response = input("\nWould you like to simulate a port scan on localhost? (y/n): ")
    if response.lower() == 'y':
        target = "127.0.0.1"
        test_ports = [80, 443, 22, 23, 25, 3389, 8080]
        simulate_port_scan(target, test_ports)
```

3. Save the file as `port_scan_detector.py` on your Desktop

### Step 2: Run the Port Scan Detector

1. Open Command Prompt
2. Navigate to Desktop:

```cmd
cd Desktop
```

3. Run the detector script:

```cmd
python port_scan_detector.py
```

![Port scan detector output]

### Step 3: Perform a Real Port Scan with Nmap

1. Open a new Command Prompt (run as Administrator)
2. Perform a basic port scan on localhost:

```cmd
nmap -p 1-100 127.0.0.1
```

**Nmap scan options explained:**

| Option       | Description              |
| :----------- | :----------------------- |
| `-p 1-100` | Scan ports 1 through 100 |
| `-sS`      | SYN scan (stealth)       |
| `-sT`      | TCP connect scan         |
| `-v`       | Verbose output           |

![Nmap port scan output]

### Step 4: Detect the Port Scan

If you're running the detector script in one terminal and performing a scan in another, the detector would identify:

- Multiple connection attempts to different ports
- SYN packets sent in rapid succession
- Unusual patterns of port access

---

## Part 3: Signature-Based IDS Detection

### Understanding Snort Rules

**Snort** is a popular open-source IDS that uses signature-based detection. Here are example rules that would detect our simulated attacks:

**Ping of Death Detection Rule:**

```
alert icmp any any -> $HOME_NET any (msg:"Ping of Death Attack"; dsize: > 65535; sid:1000001;)
```

**Port Scan Detection Rule:**

```
alert tcp $EXTERNAL_NET any -> $HOME_NET 1:1024 (msg:"Port Scan Detected"; threshold: type threshold, track by_src, count 10, seconds 10; sid:1000002;)
```

### How Signature Detection Works

| Attack                  | Signature Pattern                                                                  |
| :---------------------- | :--------------------------------------------------------------------------------- |
| **Ping of Death** | ICMP packets with size > 65,535 bytes                                              |
| **Port Scan**     | Multiple connection attempts to different ports from same source within short time |
| **SYN Flood**     | Large number of SYN packets without ACK responses                                  |

---

## Part 4: Analysis and Reporting

### Step 1: Document Your Findings

Create a report file:

```cmd
notepad IDS_Lab_Report.txt
```

Copy and paste the following template:

```
IDS Lab Report
==============
Name: [Your Name]
Date: [Current Date]

Attack 1: Ping of Death
-----------------------
Target IP: _________________
Command used: _________________
Result: _________________
IDS Detection Indicators:
- _________________________________________________
- _________________________________________________

Attack 2: Port Scanning
-----------------------
Target IP: _________________
Ports scanned: _________________
Nmap command: _________________
Scan results: _________________
IDS Detection Indicators:
- _________________________________________________
- _________________________________________________

IDS Observations
----------------
1. What signatures would detect the Ping of Death?
   _________________________________________________

2. What signatures would detect the port scan?
   _________________________________________________

3. How could an attacker evade detection?
   _________________________________________________

4. Why is port scanning often the first step in an attack?
   _________________________________________________

Conclusion
----------
_________________________________________________
_________________________________________________
```

### Step 2: Take Screenshots

Take screenshots of:

1. **Ping of Death script output** – Save as `Ping_of_Death_Output.png`
2. **Port scan detector output** – Save as `Port_Scan_Detector_Output.png`
3. **Nmap scan results** – Save as `Nmap_Scan_Results.png`

---

## IDS Evasion Techniques (Optional Reading)

| Technique                      | Description                                    | Mitigation                     |
| :----------------------------- | :--------------------------------------------- | :----------------------------- |
| **Packet Fragmentation** | Splitting malicious payload into small packets | IDS must reassemble fragments  |
| **Encryption**           | Hiding malicious content in encrypted traffic  | SSL/TLS inspection             |
| **Slow Scans**           | Spreading scans over long time periods         | Anomaly detection over time    |
| **Decoy Scans**          | Spoofing source IP addresses                   | Correlation with other sensors |
| **Randomized Ports**     | Scanning ports in random order                 | Behavioral analysis            |

---

## Lab Completion Checklist

| Task                                          | Completed |
| :-------------------------------------------- | :-------- |
| Python installed and verified                 | ☐        |
| Scapy installed                               | ☐        |
| Nmap installed and verified                   | ☐        |
| Created Ping of Death script                  | ☐        |
| Executed Ping of Death simulation             | ☐        |
| Analyzed Ping of Death results                | ☐        |
| Created Port Scan Detector script             | ☐        |
| Executed Port Scan Detector simulation        | ☐        |
| Ran Nmap port scan                            | ☐        |
| Analyzed port scan results                    | ☐        |
| Understood signature-based detection concepts | ☐        |
| Created lab report                            | ☐        |

---

## Key Takeaways

| Concept                        | Key Point                                                  |
| :----------------------------- | :--------------------------------------------------------- |
| **Ping of Death**        | Oversized ICMP packets that can crash systems (historical) |
| **Port Scanning**        | Reconnaissance technique to discover open services         |
| **Signature-based IDS**  | Detects known attack patterns using predefined signatures  |
| **Detection Thresholds** | Multiple attempts within time window triggers alerts       |
| **Network Monitoring**   | Essential for identifying malicious activity               |

---

## Summary

In this hands-on lab, you have:

| Activity                                           | Completed |
| :------------------------------------------------- | :-------- |
| Installed Python and required libraries            | ✓        |
| Installed Nmap for port scanning                   | ✓        |
| Created and executed Ping of Death simulation      | ✓        |
| Created and executed Port Scan Detector simulation | ✓        |
| Performed port scanning with Nmap                  | ✓        |
| Analyzed how signature-based IDS detects attacks   | ✓        |
| Documented findings in lab report                  | ✓        |

---

## Congratulations!

You have successfully completed the **Intrusion Detection Systems** lab. You now understand:

- How Ping of Death attacks work and how they are detected
- How port scanning attacks work and how they are detected
- How signature-based IDS uses patterns to identify malicious activity
- The importance of intrusion detection in network security
- How to simulate attacks in a controlled environment for testing

These skills are essential for network security professionals who need to understand attacker methodologies and how to detect them using intrusion detection systems.

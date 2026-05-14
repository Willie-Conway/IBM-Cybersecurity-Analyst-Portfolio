
![alt text](<../Screenshots/Velociraptor_Logo.png>)

# Hands-on Lab: Endpoint Forensics and Incident Response with Velociraptor

**Estimated time:** 90-120 minutes

---

## Project Scenario

You've recently joined the **Cyber Defense team at Solara Health**, a mid-sized healthcare technology company that provides patient data management software to hospitals nationwide.

The SOC received multiple alerts this morning about suspicious PowerShell execution on several workstations. While traditional antivirus didn't detect anything malicious, endpoint detection logs show unusual outbound connections to an unfamiliar external IP address. Management is concerned about potential patient data exposure and regulatory compliance violations.

Your task is to deploy **Velociraptor**—an advanced open-source endpoint monitoring, digital forensics, and incident response tool—to hunt for signs of compromise, collect forensic artifacts, and help the team understand the scope of the potential breach .

The clock is ticking. Incident response must begin immediately.

---

## Introduction

In this lab, you will become familiar with **Velociraptor**, an enterprise-grade open-source platform for endpoint monitoring, digital forensics, and cyber response .

Unlike Snyk (code scanning), Nessus (vulnerability scanning), TheHive (case management), Splunk (SIEM), Autopsy (disk forensics), and Volatility (memory forensics), Velociraptor focuses on **live endpoint forensics and threat hunting at scale**—allowing responders to query thousands of endpoints simultaneously, collect forensic artifacts remotely, and hunt for malicious activity across an enterprise environment .

> **Why Velociraptor?** Traditional DFIR tools require collecting massive amounts of data (often gigabytes per endpoint) and moving it to a central location for analysis. Velociraptor flips this model: instead of collecting everything, it pushes targeted queries to endpoints and parses artifacts directly on the endpoint itself, dramatically reducing bandwidth and processing time .

---

## Learning Objectives

After completing this exercise, you will be able to:

| # | Objective                                                                                       |
| - | ----------------------------------------------------------------------------------------------- |
| 1 | Deploy Velociraptor in a client-server architecture                                             |
| 2 | Enroll endpoints as Velociraptor clients                                                        |
| 3 | Perform artifact collection across the enterprise                                               |
| 4 | Hunt for specific Indicators of Compromise (IOCs)                                               |
| 5 | Analyze forensic artifacts including processes, network connections, and persistence mechanisms |
| 6 | Generate incident response reports from collected data                                          |

---

## Prerequisites

You must have:

| Requirement                                              | Status | Notes                                     |
| :------------------------------------------------------- | :----- | :---------------------------------------- |
| **Computer with 8GB+ RAM**                         | ☐     | 16GB recommended for running multiple VMs |
| **20GB free disk space**                           | ☐     |                                           |
| **Virtualization software** (VMware or VirtualBox) | ☐     | For running Windows and Ubuntu VMs        |
| **Windows 10/11 ISO**                              | ☐     | For the target/client VM                  |
| **Ubuntu Server ISO**                              | ☐     | Optional for the server VM                |
| **Basic knowledge of command line**                | ☐     |                                           |

---

## What is Velociraptor?

Velociraptor is a unique, enterprise-grade open-source platform designed specifically for endpoint monitoring, digital forensics, and incident response . It covers the entirety of the attack lifecycle, providing responders with powerful capabilities to address past, present, and future security events .

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     VELOCIRAPTOR CAPABILITIES                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                      VELOCIRAPTOR PLATFORM                           │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                    │                                        │
│           ┌────────────────────────┼────────────────────────┐               │
│           │                        │                        │               │
│           ▼                        ▼                        ▼               │
│   ┌───────────────┐        ┌───────────────┐        ┌───────────────┐       │
│   │  Artifact     │        │  Hunting      │        │  Monitoring   │       │
│   │  Collection   │        │  at Scale     │        │  in Real-Time │       │
│   │               │        │               │        │               │       │
│   │ • Pre-built   │        │ • Query all   │        │ • ETW/        │       │
│   │   artifacts   │        │   endpoints   │        │   eBPF events │       │
│   │ • Custom VQL  │        │ • IOC scans   │        │ • Sigma rules │       │
│   │ • Offline     │        │ • Process     │        │ • Process     │       │
│   │   collectors  │        │   lineage     │        │   monitoring  │       │
│   └───────────────┘        └───────────────┘        └───────────────┘       │
│                                                                              │
│   Deployment Methods:                                                        │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │  Client-Server  │  Offline Collector  │  Interactive (Disk Images) │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Key Features

| Feature                             | Description                                                                                          |
| :---------------------------------- | :--------------------------------------------------------------------------------------------------- |
| **Artifact Collection**       | Pre-built and custom artifacts for collecting OS info, process memory, network connections, and more |
| **VQL Query Language**        | Powerful Velociraptor Query Language for custom detection and analysis                               |
| **Hunting at Scale**          | Query thousands of endpoints simultaneously for IOCs                                                 |
| **Real-time Monitoring**      | Continuous monitoring using ETW (Windows) and eBPF (Linux)                                           |
| **Offline Collectors**        | Pre-configured binaries for air-gapped environments                                                  |
| **Role-Based Access Control** | Least-privilege access for team members                                                              |

---

## Part 1: Lab Environment Setup

For this lab, you will set up a small Velociraptor environment with one server and one client.

### Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         LAB ARCHITECTURE                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────────────────────┐      ┌─────────────────────────────────┐  │
│   │   VELOCIRAPTOR SERVER       │      │   VELOCIRAPTOR CLIENT            │  │
│   │   (Ubuntu VM)               │◄────►│   (Windows 10 VM)                │  │
│   │                             │      │                                 │  │
│   │   • Velociraptor service    │      │   • Velociraptor client service │  │
│   │   • Web GUI (Port 8889)     │      │   • Phones home to server       │  │
│   │   • Frontend (Port 8000)    │      │                                 │  │
│   └─────────────────────────────┘      └─────────────────────────────────┘  │
│              │                                        │                       │
│              │                                        │                       │
│              └────────────────────────────────────────┘                       │
│                                                                              │
│   Communication: Client initiates connection to server (port 8000)          │
│                 This is firewall-friendly! No inbound ports needed         │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Step 1: Create Virtual Machines

**Ubuntu Server (Velociraptor Server):**

- OS: Ubuntu 22.04 LTS Server
- RAM: 2GB (minimum, 4GB recommended)
- Disk: 20GB
- Network: NAT or Bridged

**Windows 10 (Velociraptor Client):**

- OS: Windows 10/11
- RAM: 4GB
- Disk: 40GB
- Network: Same as server (must be able to communicate)

![alt text](<../Screenshots/VM_Name_and_OS.png>)

![alt text](<../Screenshots/Verify_Virtual_Hardware.png>)

![alt text](<../Screenshots/Specify_virtual_hard_disk.png>)

![alt text](<../Screenshots/Velociraptor_Server.png>)

![alt text](<../Screenshots/Ubuntu_server.png>)

![alt text](<../Screenshots/archive_mirror.png>)

**Install Ubuntu Server:**

### Installation Options Table

| Prompt | Your Selection |
|--------|----------------|
| **Language** | `English` |
| **Installer update** | `Continue without updating` |
| **Keyboard layout** | `English (US)` |
| **Network configuration** | `DHCP` (default - automatic) |
| **Proxy** | Leave **blank** (just press Enter) |
| **Ubuntu archive mirror** | Keep default (press Enter) |
| **Storage layout** | `Use an entire disk` |
| **Storage confirmation** | `Continue` (select the disk, press Enter) |
| **Profile setup - Your name** | `velo-admin` (or any name you prefer) |
| **Profile setup - Server name** | `velociraptor-server` |
| **Profile setup - Username** | `velo-admin` (or match your name) |
| **Profile setup - Password** | **Create a password you will remember** |
| **SSH setup** | ✅ **Install OpenSSH server** (press Spacebar to select) |
| **Featured snaps** | ❌ **Deselect all** (press Spacebar on any selected items) |
| **Installation complete** | `Reboot Now` |


![alt text](<../Screenshots/Profile_Configuration.png>)

![alt text](<../Screenshots/Skip_for_now.png>)

![alt text](<../Screenshots/SSH_Configuration.png>)

![alt text](<../Screenshots/Featured_Server_Snaps.png>)

![alt text](<../Screenshots/View_Full_log.png>)

![alt text](<../Screenshots/Reeboot_Now.png>)



---

### Do You Need Ubuntu Pro?

**No, Ubuntu Pro is NOT required for this lab.**

| Feature | Ubuntu Pro | Free Ubuntu (what you need) |
|---------|------------|----------------------------|
| **Cost** | Paid for commercial use | **Free** ✅ |
| **Security updates** | Extended to 10+ years | 5 years LTS (enough for this lab) |
| **Live kernel patching** | Yes | No |
| **Compliance tools** | Yes (FIPS, CIS) | No |
| **Need for this lab?** | **No** ❌ | **Yes** ✅ |

> When prompted about Ubuntu Pro during installation, select **"Skip for now"** or **"Continue without Pro"** .

---

### After Installation - First Login

Once the VM reboots, log in:

![alt text](<../Screenshots/Velociraptor_Server_Login.png>)

### Step 2: Download Velociraptor

1. Navigate to the Velociraptreleases page:

   ```
   https://github.com/Velocidex/velociraptor/releases
   ```
![alt text](<../Screenshots/Navigate_to_the_Velociraptreleases_page.png>)

2. Download the appropriate binaries for your OS:

| System                   | File to Download                         |
| :----------------------- | :--------------------------------------- |
| **Ubuntu Server**  | `velociraptor-v0.7.x-linux-amd64`      |
| **Windows Client** | `Velociraptor-0.7.x-windows-amd64.msi` |

![alt text](<../Screenshots/Download_velociraptor.png>)

---

## Part 2: Setting Up the Velociraptor Server

### Step 1: Prepare the Server

SSH into your Ubuntu VM and create the Velociraptor directory:

```bash
sudo mkdir -p /opt/velociraptor
cd /opt/velociraptor
```

![alt text](<../Screenshots/Create_the_Velociraptor_directory.png>)

Upload the Velociraptor binary to the server (using SCP or shared folder).

```bash
# Make the binary executable
sudo chmod +x velociraptor-v0.7.x-linux-amd64

# Create a symbolic link for easier access
sudo ln -s /opt/velociraptor/velociraptor-v0.7.x-linux-amd64 /usr/local/bin/velociraptor
```

### Step 2: Generate Server Configuration

```bash
sudo velociraptor config generate > server.config.yaml
```

This creates a basic configuration file. Edit it to set your server's public IP:

```bash
sudo nano server.config.yaml
```

Find the `Frontend` section and update the `hostname` to your server's IP address:

```yaml
Frontend:
  hostname: "http://<your_server_ip>:8000"
  bind_address: "0.0.0.0"
  bind_port: 8000
```

### Step 3: Start the Velociraptor Server

```bash
# Start the server in the background
sudo velociraptor --config server.config.yaml frontend -v
```

### Step 4: Set Admin Password

In a new terminal window (or separate SSH session), set the admin password:

```bash
sudo velociraptor --config server.config.yaml user add --role administrator
```

Follow the prompts to set a username and password.

### Step 5: Access the Velociraptor GUI

1. Open your browser and navigate to:

   ```
   https://<your_server_ip>:8889
   ```

   (Note: HTTPS with port 8889)
2. Accept the self-signed certificate warning
3. Log in with the admin credentials you created

![Velociraptor Login]

*[Screenshot: Velociraptor web interface login screen]*

---

## Part 3: Setting Up the Velociraptor Client (Windows)

### Step 1: Generate Client Configuration

From the Ubuntu server, generate a client configuration:

```bash
sudo velociraptor --config server.config.yaml config client > client.config.yaml
```

### Step 2: Create Client Installer

```bash
sudo velociraptor --config client.config.yaml config write_client --msi > velociraptor_client.msi
```

This creates an MSI installer that will automatically connect to your server.

### Step 3: Transfer and Install the Client

1. Transfer `velociraptor_client.msi` to your Windows VM (using SCP, shared folder, or USB)
2. On Windows, run the MSI as Administrator
3. The client service will start automatically and "phone home" to the server

### Step 4: Verify Client Connection

1. In the Velociraptor GUI, navigate to **Hunts** or **View Clients**
2. You should see your Windows client listed

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    VELOCIRAPTOR CLIENTS                                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Client ID              | OS           | Last Seen           | Labels      │
│   ───────────────────────────────────────────────────────────────────────── │
│   C.1a2b3c4d5e6f...     | Windows 10   | 2025-04-07 14:30:22  |             │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

![Client Connected]

*[Screenshot: Velociraptor client list showing connected Windows client]*

---

## Part 4: Core Velociraptor Capabilities

### Understanding Artifacts

Artifacts are pre-built VQL queries that collect specific forensic data from endpoints . Velociraptor includes a comprehensive library of artifacts :

| Category                     | Example Artifacts                                                        |
| :--------------------------- | :----------------------------------------------------------------------- |
| **System Information** | `Windows.Sysinfo`, `Windows.System.Pslist`                           |
| **Process Analysis**   | `Windows.System.Pstree`, `Windows.Detection.ProcFilter`              |
| **Network**            | `Windows.Network.Netstat`, `Windows.Network.DNSLookup`               |
| **Persistence**        | `Windows.Persistence.Autoruns`, `Windows.Persistence.ScheduledTasks` |
| **Forensics**          | `Windows.Forensics.Prefetch`, `Windows.Forensics.UserAssist`         |

### The Velociraptor Workflow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    INCIDENT RESPONSE WORKFLOW                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   1. HUNT - Search for IOCs across all endpoints                            │
│      └── "Find all processes named 'powershell.exe' with suspicious flags"  │
│                          │                                                   │
│                          ▼                                                   │
│   2. TRIAGE - Identify affected systems                                     │
│      └── "Collect basic artifacts from suspicious endpoints"                │
│                          │                                                   │
│                          ▼                                                   │
│   3. FORENSICS - Deep dive into compromised hosts                           │
│      └── "Collect full memory dump, event logs, and registry"               │
│                          │                                                   │
│                          ▼                                                   │
│   4. REMEDIATION - Take action at scale                                     │
│      └── "Execute script across all affected systems"                       │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Part 5: Core Forensic Tasks with Velociraptor

### Task 1: Collect System Information

1. In the Velociraptor GUI, go to **Collect** → **Add Collection**
2. Select your Windows client from the list
3. Search for and add the artifact `Windows.Sysinfo`
4. Click **Launch** to start the collection
5. Once complete, click on the collection to view results:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    WINDOWS.SYSINFO RESULTS                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Hostname: DESKTOP-SOLARA01                                                │
│   OS: Microsoft Windows 10 Pro  10.0.19045                                  │
│   Boot Time: 2025-04-07T08:23:15                                            │
│   CPU: Intel Core i5-10400  2.90GHz                                         │
│   RAM: 16.0 GB                                                              │
│   Current User: SOLARA\triage                                             │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Task 2: Analyze Running Processes

**Artifact:** `Windows.System.Pslist`

```bash
# This artifact can be collected via the GUI similar to above
```

**Sample output:**

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    PROCESS LIST                                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   PID   | PPID  | Name              | Create Time           | User          │
│   ──────┼───────┼───────────────────┼───────────────────────┼──────────────│
│   4     | 0     | System            | 2025-04-07 08:23:15   | NT AUTHORITY  │
│   312   | 4     | smss.exe          | 2025-04-07 08:23:15   | NT AUTHORITY  │
│   892   | 312   | csrss.exe         | 2025-04-07 08:23:17   | NT AUTHORITY  │
│   1024  | 892   | wininit.exe       | 2025-04-07 08:23:18   | NT AUTHORITY  │
│   1180  | 1024  | services.exe      | 2025-04-07 08:23:18   | NT AUTHORITY  │
│   1272  | 1180  | svchost.exe       | 2025-04-07 08:23:19   | NT AUTHORITY  │
│   2844  | 1272  | powershell.exe    | 2025-04-07 09:45:22   | SOLARA\triage │ ← Suspicious
│   2912  | 2844  | notepad.exe       | 2025-04-07 09:46:05   | SOLARA\triage │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

**What to look for :**

- Unusual parent-child relationships (e.g., `winword.exe` spawning `powershell.exe`)
- Processes running from temp directories
- Processes with obfuscated names (e.g., `svch0st.exe`)
- PowerShell executing encoded commands

### Task 3: Investigate Process Lineage

**Artifact:** `Windows.System.Pstree`

This shows the parent-child relationships between processes :

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    PROCESS TREE                                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   services.exe (1180)                                                       │
│   ├── svchost.exe (1272)                                                    │
│   │   └── powershell.exe (2844)  🔴 Suspicious!                             │
│   │       └── notepad.exe (2912)                                            │
│   │       └── cmd.exe (2956)                                                │
│   │           └── whoami.exe (2980)                                         │
│   └── lsass.exe (1192)                                                      │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

> **Key Learning:** `svchost.exe` should not typically spawn `powershell.exe`. This is a potential indicator of malicious execution .

### Task 4: Analyze Network Connections

**Artifact:** `Windows.Network.Netstat`

```bash
# Collect via GUI as before
```

**Sample output:**

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    NETWORK CONNECTIONS                                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   PID   | Process         | Local Address     | Remote Address       | State │
│   ──────┼─────────────────┼───────────────────┼──────────────────────┼───────│
│   1272  | svchost.exe     | 192.168.1.100:49155 | 8.8.8.8:53         | UDP   │
│   2844  | powershell.exe  | 192.168.1.100:49156 | 185.130.5.253:443  | ESTAB │ 🔴
│   2912  | notepad.exe     | 192.168.1.100:49157 | 185.130.5.253:443  | ESTAB │ 🔴
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

**What to look for :**

- Suspicious outbound connections to unknown IPs
- C2 beaconing patterns (regular intervals)
- Connections on non-standard ports

### Task 5: Detect Persistence Mechanisms

**Artifact:** `Windows.Persistence.Autoruns`

```bash
# Collect via GUI
```

This artifact identifies persistence mechanisms :

- Registry run keys
- Startup folders
- Scheduled tasks
- Services

**Sample output:**

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    PERSISTENCE MECHANISMS                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Name              | Path                                      | Enabled    │
│   ──────────────────┼───────────────────────────────────────────┼────────────│
│   UpdateService     | C:\Users\triage\AppData\Roaming\svchost.exe | Yes      │ 🔴
│   GoogleUpdateTask  | C:\Program Files\Google\Update\GoogleUpdate.exe | Yes  │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Task 6: Hunt for IOCs Across All Endpoints

Hunting is Velociraptor's superpower—query hundreds of endpoints simultaneously .

1. Go to **Hunts** → **New Hunt**
2. Select an artifact (e.g., `Windows.System.Pslist`)
3. Add a filter (optional):

   ```
   Process.Name =~ "powershell"
   ```
4. Select target clients or "All Clients"
5. Launch the hunt
6. Review results across all endpoints

![Hunt Results]

*[Screenshot: Hunt showing results from multiple clients]*

---

## Part 6: Investigation Scenario - Solara Health

Now you will apply these skills to investigate the Solara Health incident.

### The Incident

The SOC detected multiple endpoints with suspicious PowerShell execution. You've been asked to:

1. Identify all endpoints with malicious PowerShell activity
2. Determine the attacker's persistence mechanism
3. Identify C2 communication channels
4. Document findings for remediation

### Step 1: Hunt for Suspicious PowerShell Commands

**Hunt Configuration:**

| Field              | Value                                                                                                    |
| :----------------- | :------------------------------------------------------------------------------------------------------- |
| **Artifact** | `Windows.EventLogs.PowerShell`                                                                         |
| **Filter**   | `Message contains "-enc" OR Message contains "DownloadString" OR Message contains "Invoke-Expression"` |
| **Target**   | All Windows clients                                                                                      |

**Expected findings:**
Processes with encoded PowerShell commands (`-enc`), often used to obfuscate malicious code.

### Step 2: Hunt for C2 Communication

**Hunt Configuration:**

| Field              | Value                                                      |
| :----------------- | :--------------------------------------------------------- |
| **Artifact** | `Windows.Network.Netstat`                                |
| **Filter**   | `RemoteAddress != "127.0.0.1" AND RemoteAddress =~ "^(10\. |
| **Target**   | Clients with suspicious PowerShell activity                |

This hunts for external connections (not in private IP ranges).

### Step 3: Collect Full Forensic Artifacts

For compromised endpoints, perform a deep dive collection:

Select these artifacts:

- `Windows.System.Pslist` (processes)
- `Windows.Network.Netstat` (network)
- `Windows.Persistence.Autoruns` (persistence)
- `Windows.EventLogs.Security` (security events)
- `Windows.Forensics.Prefetch` (program execution history)

### Step 4: Generate Incident Report

1. Export collection as CSV:

   In the collection view, click **Export** → **CSV**
2. Download notebook:

   Velociraptor includes a **notebook** feature for collaborative analysis
3. Create summary of findings:

   ```
   SUMMARY OF FINDINGS
   ===================
   Date: 2025-04-07
   Investigator: [Your Name]

   AFFECTED SYSTEMS:
   - DESKTOP-SOLARA01 (PID 2844)
   - DESKTOP-FINANCE02 (PID 1278)

   MALICIOUS INDICATORS:
   - Process: powershell.exe spawning from svchost.exe
   - C2 IP: 185.130.5.253:443
   - Persistence: Suspicious service 'UpdateService'

   RECOMMENDATIONS:
   1. Isolate affected systems immediately
   2. Block C2 IP at firewall
   3. Remove malicious service
   4. Reset user credentials
   ```

---

## Part 7: Advanced Velociraptor Features

### Creating Custom VQL Artifacts

Velociraptor's power comes from VQL (Velociraptor Query Language) . Here's a simple custom artifact to find suspicious processes:

```yaml
name: Custom.Detection.SuspiciousProcesses
description: Hunt for processes with suspicious names or command lines

sources:
  - queries:
      - |
        SELECT Pid, Name, CommandLine, Exe, CreateTime
        FROM pslist()
        WHERE Name =~ 'powershell|cmd|wscript|cscript'
        AND CommandLine =~ '-enc|DownloadString|Invoke-Expression|Base64'
```

To add this artifact:

1. Go to **Artifacts** → **New Artifact**
2. Paste the YAML definition
3. Save

### Offline Collectors

For systems that cannot run the Velociraptor client service, you can create offline collectors :

```bash
# On the server, generate an offline collector binary
velociraptor --config server.config.yaml artifacts collect \
    --format executable \
    --artifacts Windows.System.Pslist,Windows.Network.Netstat \
    --output velociraptor_collector.exe
```

This creates a standalone executable that can be run on any Windows system. The output is an encrypted ZIP file that can be imported back into the Velociraptor GUI for analysis .

### Real-Time Monitoring

Velociraptor can monitor endpoints in real-time using Event Tracing for Windows (ETW) :

1. Go to **Monitoring** → **New Monitoring**
2. Select artifact `Windows.Detection.ProcFilter`
3. Choose client(s)
4. Click **Start Monitoring**

This will continuously send process creation events from the endpoint to the server—ideal for detecting malicious execution as it happens.

### Role-Based Access Control

Velociraptor supports RBAC for team collaboration :

| Role                    | Permissions                            |
| :---------------------- | :------------------------------------- |
| **Administrator** | Full access to all features            |
| **Investigator**  | Can collect artifacts and launch hunts |
| **Analyst**       | Read-only access to collections        |
| **Auditor**       | Can view logs only                     |

To assign roles: **User Management** → **Add User** → **Select Role**

---

## Part 8: Investigation Questions

Use Velociraptor to answer the following questions about the Solara Health incident:

| #  | Question                                                     | Answer |
| -- | ------------------------------------------------------------ | ------ |
| 1  | What is the hostname of the compromised Windows endpoint?    |        |
| 2  | What PID is running the malicious PowerShell process?        |        |
| 3  | What parent process spawned this PowerShell instance?        |        |
| 4  | What IP address and port is the C2 server using?             |        |
| 5  | What persistence mechanism did the attacker create?          |        |
| 6  | What command was executed via PowerShell?                    |        |
| 7  | How many endpoints are affected by this campaign?            |        |
| 8  | What user account is associated with the malicious activity? |        |
| 9  | What is the first time the malicious process was observed?   |        |
| 10 | What is your recommended remediation action?                 |        |

---

## Lab Completion Checklist

| Task                                                              | Completed |
| :---------------------------------------------------------------- | :-------- |
| **Part 1: Environment Setup**                               | ☐        |
| Ubuntu Server VM created                                          | ☐        |
| Windows 10 Client VM created                                      | ☐        |
| **Part 2: Velociraptor Server**                             | ☐        |
| Velociraptor binary downloaded and installed                      | ☐        |
| Server configuration generated                                    | ☐        |
| Server started successfully                                       | ☐        |
| Admin user created                                                | ☐        |
| Web GUI accessible at https://<server_ip>:8889                    | ☐        |
| **Part 3: Velociraptor Client**                             | ☐        |
| Client MSI generated                                              | ☐        |
| Client installed on Windows VM                                    | ☐        |
| Client shows as "Online" in GUI                                   | ☐        |
| **Part 4: Understanding**                                   | ☐        |
| Artifacts concept understood                                      | ☐        |
| VQL purpose understood                                            | ☐        |
| **Part 5: Core Tasks**                                      | ☐        |
| System information collected (`Windows.Sysinfo`)                | ☐        |
| Process list collected (`Windows.System.Pslist`)                | ☐        |
| Process tree analyzed (`Windows.System.Pstree`)                 | ☐        |
| Network connections analyzed (`Windows.Network.Netstat`)        | ☐        |
| Persistence mechanisms checked (`Windows.Persistence.Autoruns`) | ☐        |
| Hunt launched across endpoints                                    | ☐        |
| **Part 6: Investigation**                                   | ☐        |
| PowerShell hunting completed                                      | ☐        |
| C2 hunting completed                                              | ☐        |
| Full forensic collection completed                                | ☐        |
| Report generated                                                  | ☐        |
| **Part 7: Advanced (Optional)**                             | ☐        |
| Custom VQL artifact created                                       | ☐        |
| Offline collector tested                                          | ☐        |

---

## Screenshot Checklist

| Screenshot                  | Description                                     |
| :-------------------------- | :---------------------------------------------- |
| `velo_server_start.png`   | Velociraptor server startup screen              |
| `velo_gui_login.png`      | Velociraptor GUI login page                     |
| `clients_connected.png`   | Connected clients in the GUI                    |
| `artifact_collection.png` | Artifact selection screen                       |
| `pslist_results.png`      | Process list results showing suspicious process |
| `pstree_results.png`      | Process tree showing suspicious lineage         |
| `netstat_results.png`     | Network connections showing C2 IP               |
| `hunt_config.png`         | Hunt configuration screen                       |
| `hunt_results.png`        | Hunt results from multiple endpoints            |
| `report.png`              | Generated incident report                       |

---

## Troubleshooting Tips

| Issue                                     | Solution                                                                                                |
| :---------------------------------------- | :------------------------------------------------------------------------------------------------------ |
| **Client not connecting to server** | Verify network connectivity between VMs; check server's bind_address is 0.0.0.0; check Windows firewall |
| **HTTPS certificate warning**       | This is normal for self-signed certs; accept the warning or install a proper certificate for production |
| **Collections taking too long**     | Reduce the number of artifacts selected; use filters to limit data collected                            |
| **Client offline after reboot**     | Check that the Velociraptor service is set to auto-start; verify service is running                     |
| **Cannot access GUI on port 8889**  | Verify Ubuntu firewall allows port 8889:`sudo ufw allow 8889`                                         |
| **Hunt shows no results**           | Check that artifacts are correctly selected; verify filters are not too restrictive                     |

---

## Velociraptor Deployment Methods

| Method                              | Description                                   | Use Case                                          |
| :---------------------------------- | :-------------------------------------------- | :------------------------------------------------ |
| **Client-Server**             | Persistent agent installed on endpoints       | Continuous monitoring, IR readiness               |
| **Offline Collector**         | Standalone executable for one-time collection | Air-gapped systems, no agent installation allowed |
| **Interactive (Disk Images)** | Virtual client analyzing raw disk images      | Post-mortem analysis of acquired images           |

---

## Key Takeaways

| Concept                      | Description                                                                 |
| :--------------------------- | :-------------------------------------------------------------------------- |
| **Velociraptor**       | Open-source DFIR platform for endpoint monitoring and hunting               |
| **VQL**                | Velociraptor Query Language—customizable queries for artifact collection   |
| **Artifact**           | Pre-built VQL query for collecting specific forensic data                   |
| **Hunt**               | Scalable query across multiple endpoints simultaneously                     |
| **Offline Collector**  | Standalone binary for collecting data without agent installation            |
| **Push vs Pull Model** | Velociraptor clients phone home (pull), making deployment firewall-friendly |

---

## Real-World Application: IR Integration

In a real incident response scenario, Velociraptor integrates with other tools :

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    VELOCIRAPTOR IN INCIDENT RESPONSE                         │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   EDR Alert (CrowdStrike, SentinelOne, etc.)                                │
│              │                                                               │
│              ▼                                                               │
│   Velociraptor Hunt                                                         │
│   └── Identify full scope of compromise                                     │
│              │                                                               │
│              ▼                                                               │
│   Forensic Collection                                                       │
│   └── Collect memory, processes, network, registry                          │
│              │                                                               │
│              ▼                                                               │
│   Data Enrichment                                                           │
│   └── Export to Timesketch, Splunk, or Elastic                 │
│              │                                                               │
│              ▼                                                               │
│   Remediation at Scale                                                      │
│   └── Execute scripts via Velociraptor across affected systems              │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Test Your Knowledge

**Q1:** What is the purpose of VQL (Velociraptor Query Language)?

```
Your answer:
_________________________________________________________________________
```

**Q2:** How does the Velociraptor client-server model differ from traditional EDR agents?

```
Your answer:
_________________________________________________________________________
```

**Q3:** What artifact would you use to identify processes running on a Windows endpoint?

```
Your answer:
_________________________________________________________________________
```

**Q4:** What is a "hunt" in Velociraptor?

```
Your answer:
_________________________________________________________________________
```

**Q5:** When would you use an offline collector instead of the persistent client?

```
Your answer:
_________________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                                                                                                 |
| -- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1  | VQL is a powerful query language that allows customization of artifacts for collecting, querying, and monitoring endpoints                             |
| 2  | Velociraptor clients initiate the connection ("phone home") to the server, eliminating the need for inbound firewall ports on endpoints                |
| 3  | `Windows.System.Pslist`                                                                                                                              |
| 4  | A hunt is a Velociraptor feature that runs a query or artifact across multiple endpoints simultaneously to identify IOCs                               |
| 5  | Offline collectors are used when the Velociraptor client cannot be installed (air-gapped systems, compliance restrictions) or for one-time collections |

---

## Summary

In this lab, you have:

| Activity                                                  | Completed |
| :-------------------------------------------------------- | :-------- |
| Deployed Velociraptor server on Ubuntu                    | ☐        |
| Installed and enrolled a Windows Velociraptor client      | ☐        |
| Collected system information, processes, and network data | ☐        |
| Analyzed process lineage to detect malicious activity     | ☐        |
| Hunted for IOCs across endpoints                          | ☐        |
| Investigated a realistic data breach scenario             | ☐        |

These skills are essential for:

- Incident responders conducting enterprise-scale investigations
- Threat hunters searching for hidden adversaries
- DFIR analysts collecting forensic evidence remotely
- Security teams building proactive detection capabilities

---

## Additional Resources

| Resource                                                 | URL                                                             |
| :------------------------------------------------------- | :-------------------------------------------------------------- |
| **Velociraptor Documentation**                     | https://docs.velociraptor.app                                   |
| **Velociraptor GitHub**                            | https://github.com/Velocidex/velociraptor                       |
| **Velociraptor Artifacts**                         | https://github.com/Velocidex/velociraptor/tree/master/artifacts |
| **Digital Forensics and Incident Response (book)** | Includes Velociraptor coverage                                  |
| **SANS Velociraptor Resources**                    | https://www.sans.org                                            |

---

## Congratulations!

You have successfully completed the **Endpoint Forensics and Incident Response with Velociraptor** lab. You now know how to:

- Deploy Velociraptor in a client-server architecture
- Collect forensic artifacts from Windows endpoints
- Hunt for malicious activity across multiple systems
- Analyze process lineage, network connections, and persistence mechanisms
- Use Velociraptor for enterprise-scale incident response

These skills represent the modern approach to DFIR—scalable, efficient, and agent-based. Velociraptor has become the obvious choice for open-source DFIR at scale .

> "Velociraptor can revolutionize our IR capabilities, making it an essential tool for future threat hunting and rapid response." — BTLO Lab Participant
>

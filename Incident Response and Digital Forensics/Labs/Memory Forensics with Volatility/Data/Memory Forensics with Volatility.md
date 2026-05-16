![alt text](../Screenshots/Volatility_Logo.png)

# Hands-on Lab: Memory Forensics with Volatility

**Estimated time:** 90-120 minutes

---

## Project Scenario

You've recently been hired as a **Malware Analyst and Incident Responder** by **Nexus Defense Solutions**, a mid-sized cybersecurity firm that provides managed security services to healthcare and financial clients.

Early this morning, your team received an alert from a client's EDR system indicating possible malware activity on a critical Windows server. Before the security team could respond, the system became unresponsive and was taken offline for forensic analysis. A memory dump was captured before the system was rebooted.

The client's management is panicking—this server processes sensitive patient data (healthcare client) and financial transactions (banking client). A breach could mean regulatory fines, lawsuits, and permanent reputational damage.

Your job is to analyze the memory dump to determine:

- What malware infected the system
- What data may have been stolen
- How the attacker gained access
- Whether the attack is ongoing

The clock is ticking. The client needs answers within 24 hours.

---

## Introduction

In this lab, you will become familiar with **Volatility**, the world's most widely used open-source memory forensics framework . Volatility allows incident responders to analyze volatile memory (RAM) dumps to detect malware, extract artifacts, and reconstruct attack timelines .

Unlike Snyk (code scanning), Nessus (vulnerability scanning), TheHive (incident response), Splunk (SIEM), and Autopsy (disk forensics), Volatility focuses on **memory analysis**—examining the volatile memory of a running system to find evidence that disappears when the system is powered off, including running processes, network connections, and injected malware .

> **Why memory forensics matters:** Modern malware often runs entirely in memory without ever writing to disk. Rootkits can hide from live analysis tools. Memory forensics with Volatility bypasses these evasion techniques and reveals what's truly happening on a compromised system .

---

## Learning Objectives

After completing this exercise, you will be able to:

| # | Objective                                                  |
| - | ---------------------------------------------------------- |
| 1 | Install and configure Volatility 3 on your system          |
| 2 | Identify the operating system profile of a memory dump     |
| 3 | Extract running processes and parent-child relationships   |
| 4 | Detect malicious processes and code injection              |
| 5 | Analyze network connections and open sockets               |
| 6 | Dump suspicious processes and strings for malware analysis |
| 7 | Document findings in an incident report                    |

---

## Prerequisites

You must have:

| Requirement                       | Status | Notes                               |
| :-------------------------------- | :----- | :---------------------------------- |
| **Computer with 8GB+ RAM**  | ☐     | 16GB recommended for large dumps    |
| **10GB free disk space**    | ☐     | Memory dumps can be 4-8GB           |
| **Python 3.8+ installed**   | ☐     | Volatility 3 requires Python 3      |
| **Admin privileges**        | ☐     | For installation                    |
| **Virtualization software** | ☐     | Optional: for creating memory dumps |

![alt text](<../Screenshots/MemForensics_VM.png>)

![alt text](<../Screenshots/Specify_virtual_hardware_volatity.png>)

![alt text](<../Screenshots/Hard_Disk_Volatility.png>)

![alt text](<../Screenshots/VM_MeForensics.png>)
---

## What is Volatility?

Volatility is an open-source memory forensics framework written in Python. It extracts digital artifacts from volatile memory (RAM) dumps. Volatility 3 is the modern, officially supported version .

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       VOLATILITY CAPABILITIES                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                      VOLATILITY FRAMEWORK                            │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                    │                                        │
│           ┌────────────────────────┼────────────────────────┐               │
│           │                        │                        │               │
│           ▼                        ▼                        ▼               │
│   ┌───────────────┐        ┌───────────────┐        ┌───────────────┐       │
│   │  Process      │        │  Network      │        │  Malware      │       │
│   │  Analysis     │        │  Analysis     │        │  Detection    │       │
│   │               │        │               │        │               │       │
│   │ • pslist      │        │ • netscan     │        │ • malfind     │       │
│   │ • pstree      │        │ • sockscan    │        │ • yarascan    │       │
│   │ • psscan      │        │ • connscan    │        │ • modscan     │       │
│   └───────────────┘        └───────────────┘        └───────────────┘       │
│                                                                              │
│   Additional Capabilities:                                                   │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │  DLL/Module List  │  Registry Analysis  │  File Scanning  │  CmdLine  │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Volatility 2 vs Volatility 3

| Feature                     | Volatility 2 (Legacy)                | Volatility 3 (Modern)                 |
| :-------------------------- | :----------------------------------- | :------------------------------------ |
| **Status**            | Deprecated (as of April 2025)        | Current standard                      |
| **Profile detection** | Manual (imageinfo)                   | Automatic (no manual profiles)        |
| **Plugin syntax**     | `vol.py --profile=Win10x64 pslist` | `vol.py -f dump.raw windows.pslist` |
| **Python support**    | Python 2                             | Python 3+                             |

**This lab uses Volatility 3**, which is now the industry standard .

---

## Part 1: Installing Volatility

### Step 1: Install Python Dependencies

**Windows:**

1. Download Python 3.10+ from python.org
2. Ensure "Add Python to PATH" is checked during installation

**Linux/macOS:**

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3 python3-pip git -y

# macOS (using Homebrew)
brew install python3 git
```

### Step 2: Install Volatility 3

**Option A: From GitHub (Recommended)**

```bash
# Clone the repository
git clone https://github.com/volatilityfoundation/volatility3.git
cd volatility3

# Install dependencies
pip3 install -r requirements.txt

# Test installation
python3 vol.py -h
```

**Option B: Using pip**

```bash
pip3 install volatility3
```

### Step 3: Verify Installation

```bash
python3 vol.py -f /path/to/sample/dump.raw windows.info
```

Expected output shows Volatility version and plugin count.

---

## Part 2: Obtaining a Sample Memory Dump

For this lab, you need a memory dump to analyze.

### Option A: Download a Forensic Sample (Recommended)

| Source             | Description                     | Link                                        |
| :----------------- | :------------------------------ | :------------------------------------------ |
| **MemLabs**  | Beginner-friendly Windows dumps | https://github.com/stuxnet999/MemLabs       |
| **Volexity** | Real malware dumps              | https://www.volexity.com/blog/              |
| **DFRWS**    | Forensic challenge images       | http://dfrws.org/2008/challenge/submission/ |

**Specifically:** Download MemLabs Lab 1 - "Beginner's Luck" (approx 300-500 MB) .

### Option B: Capture Your Own Memory Dump

**On Windows (using DumpIt or WinPMem):**

1. Download WinPMem from GitHub
2. Run as Administrator:
   ```cmd
   winpmem_mini_x64_rc2.exe dump.raw
   ```

**On Linux (using AVML or LiME):**

```bash
# Using AVML (recommended for modern Linux)
sudo avml mem.avml

# Using LiME (kernel module)
sudo insmod lime.ko "path=mem.lime format=lime"
```

> **Warning:** Only capture memory from systems you own or have explicit authorization to analyze .

---

## Part 3: Understanding the Memory Dump

### Step 1: Identify the Dump's Operating System

With Volatility 3, profile detection is automatic, but you can still verify:

```bash
python3 vol.py -f memory.dump windows.info
```

For Linux dumps:

```bash
python3 vol.py -f memory.dump banners.Banners
```

**Sample output:**

```
Volatility 3 Framework 2.5.2
Progress:  100.00		PDB scanning finished                    
Variable	Value

Kernel Base	0xf800e1a00000
DTB	0x1aa000
Symbols	file:///path/to/symbols/ntkrnlmp.pdb/...
Is64Bit	True
Primary	True
Windows version	10.0.19041
Build lab	19041.amd64fre.vb_release.191206-1406

Image Type	SinglePartition
```

This tells you the Windows version (e.g., 10.0.19041) and architecture (64-bit).

### Step 2: Document Initial Findings

Create a case file with:

- MD5/SHA256 hash of the memory dump
- Date and time of analysis
- Tool versions used

---

## Part 4: Core Forensics Tasks with Volatility

### Task 1: Process Analysis - Who Was Running?

**Plugin: `windows.pslist`** - Lists active processes at the time of capture

```bash
python3 vol.py -f memory.dump windows.pslist
```

**Sample output:**

```
Offset	PID	PPID	Threads	Handles	Create time	Process name
---------	---	----	-------	-------	-----------	------------
0x...	4	0	85	-	2025-03-01 10:00:00	System
0x...	148	4	12	-	2025-03-01 10:00:05	smss.exe
0x...	292	148	8	-	2025-03-01 10:00:10	csrss.exe
0x...	340	148	12	-	2025-03-01 10:00:10	wininit.exe
0x...	348	292	15	-	2025-03-01 10:00:10	csrss.exe
0x...	396	340	27	-	2025-03-01 10:00:11	services.exe
0x...	404	340	18	-	2025-03-01 10:00:11	lsass.exe
0x...	1512	396	4	-	2025-03-01 14:30:22	WinRAR.exe
0x...	2424	1512	12	-	2025-03-01 14:31:05	mspaint.exe
```

**What to look for:**

- Processes with suspicious names (e.g., `reader_sl.exe`, `svchost.exe` running from wrong location)
- Processes with unusually high PID ranges
- Processes creating child processes unexpectedly

**Plugin: `windows.pstree`** - Shows parent-child relationships

```bash
python3 vol.py -f memory.dump windows.pstree
```

This is useful for identifying:

- Malware spawned by legitimate processes
- Suspicious process lineage (e.g., `winword.exe` spawning `cmd.exe`)

**Plugin: `windows.psscan`** - Finds hidden/terminated processes

```bash
python3 vol.py -f memory.dump windows.psscan
```

Some malware hides processes from the active process list. `psscan` scans memory pools to find processes that may be hidden.

### Task 2: Malware Detection - Find Suspicious Processes

**For our scenario** (Nexus Defense Solutions client), let's analyze what we found:

| PID  | Process Name | Parent PID | Suspicious? | Why                                |
| ---- | ------------ | ---------- | ----------- | ---------------------------------- |
| 1512 | WinRAR.exe   | 396        | ✓          | Created an unusual archive         |
| 1984 | cmd.exe      | 1512       | ✓          | Spawned by WinRAR                  |
| 2424 | mspaint.exe  | 1984       | ✓          | Unusual - Paint opened by cmd.exe  |
| 796  | Dumpit.exe   | 396        | ✗          | Likely the memory capture tool     |
| 2096 | svchost.exe  | 396        | ?           | Check if running from correct path |

**Plugin: `windows.cmdline`** - View command line arguments

```bash
python3 vol.py -f memory.dump windows.cmdline
```

This reveals what commands were executed.

**Plugin: `windows.netstat` or `windows.netscan`** - Network connections

```bash
python3 vol.py -f memory.dump windows.netscan
```

**Sample output:**

```
Offset	Proto	Local Address	Foreign Address	State	PID	Process
------	-----	-------------	---------------	-----	---	-------
0x...	TCPv4	192.168.1.100:49155	185.130.5.253:443	ESTABLISHED	2096	svchost.exe
0x...	TCPv4	192.168.1.100:49156	41.168.5.140:80	ESTABLISHED	1512	WinRAR.exe
```

**What to look for:**

- Unusual external IP addresses
- Connections on non-standard ports
- Processes connecting outbound that shouldn't have network access

### Task 3: Code Injection Detection - `malfind`

One of the most powerful Volatility plugins, `malfind`, detects code injection in process memory.

```bash
python3 vol.py -f memory.dump windows.malfind
```

This identifies memory regions with:

- PAGE_EXECUTE_READWRITE permissions (suspicious)
- Memory that doesn't match the original file on disk

### Task 4: Extract Suspicious Processes

Once you've identified suspicious processes, dump them for further analysis:

```bash
# Create output directory
mkdir extracted_processes

# Dump a process (replace PID with actual process ID)
python3 vol.py -f memory.dump -o extracted_processes windows.dumpfiles --pid 1512
```

**For Linux memory forensics:** Volatility also supports Linux analysis with plugins like `linux.pslist`, `linux.bash`, and `linux.lsof` .

---

## Part 5: Hands-On Investigation Scenario

Now you'll apply these skills to investigate the Nexus Defense Solutions incident.

### The Incident

A healthcare client's Windows server was found unresponsive. Before reboot, a memory dump was captured using DumpIt. You must analyze it to answer the questions below.

### Step 1: Initial Triage

Run the following commands and record your findings:

```bash
# 1. Verify dump info
python3 vol.py -f case001.dump windows.info

# 2. List all processes
python3 vol.py -f case001.dump windows.pslist > pslist.txt

# 3. Show process tree
python3 vol.py -f case001.dump windows.pstree > pstree.txt

# 4. Check for hidden processes
python3 vol.py -f case001.dump windows.psscan > psscan.txt
```

### Step 2: Process Analysis

Review `pslist.txt` and identify:

| Question                                      | Answer |
| --------------------------------------------- | ------ |
| What is the PID of `lsass.exe`?             |        |
| What process spawned `cmd.exe`?             |        |
| Is there any process named `reader_sl.exe`? |        |
| What is the parent of `winlogon.exe`?       |        |

### Step 3: Network Investigation

```bash
# Check network connections
python3 vol.py -f case001.dump windows.netscan > netscan.txt
```

| Question                                                    | Answer |
| ----------------------------------------------------------- | ------ |
| What IP address is `WinRAR.exe` connected to?             |        |
| What port is being used for the suspicious connection?      |        |
| Is `svchost.exe` making any unusual outbound connections? |        |

### Step 4: Command Line Artifacts

```bash
# Extract command line arguments
python3 vol.py -f case001.dump windows.cmdline > cmdline.txt
```

| Question                                       | Answer |
| ---------------------------------------------- | ------ |
| What command was executed by PID 1984?         |        |
| What archive file did WinRAR create?           |        |
| What arguments were passed to `mspaint.exe`? |        |

### Step 5: Malware Detection

```bash
# Check for code injection
python3 vol.py -f case001.dump windows.malfind > malfind.txt

# Check loaded DLLs for suspicious process
python3 vol.py -f case001.dump windows.dlllist --pid 1512 > dlllist.txt
```

| Question                                                   | Answer |
| ---------------------------------------------------------- | ------ |
| Does `malfind` detect anything suspicious?               |        |
| What unusual DLLs are loaded by WinRAR?                    |        |
| Does the `svchost.exe` child process have injected code? |        |

### Step 6: Extract and Analyze

```bash
# Dump suspicious process for further analysis
mkdir extraction
python3 vol.py -f case001.dump -o extraction windows.dumpfiles --pid 1512
python3 vol.py -f case001.dump -o extraction windows.dumpfiles --pid 2096

# Extract strings from dumped file
strings extraction/pid.1512.dmp > strings_1512.txt

# Search for sensitive data
grep -i "password\|customer\|ssn\|patient" strings_1512.txt
```

---

## Part 6: Investigation Questions

Based on your analysis, answer the following:

| #  | Question                                                                 | Answer |
| -- | ------------------------------------------------------------------------ | ------ |
| 1  | What is the MD5 hash of the memory dump file?                            |        |
| 2  | What Windows version and build number is this system?                    |        |
| 3  | What is the suspicious process (PID and name) that shouldn't be running? |        |
| 4  | What parent process spawned the suspicious process?                      |        |
| 5  | What IP address did the malware connect to?                              |        |
| 6  | What port was used for C2 communication?                                 |        |
| 7  | Did the malware inject code into any other processes?                    |        |
| 8  | What type of malware is this likely to be?                               |        |
| 9  | What data may have been stolen?                                          |        |
| 10 | What is your recommended next step?                                      |        |

---

## Part 7: Advanced Volatility Techniques

### YARA Scanning

Volatility can scan memory with YARA rules to identify known malware families :

```bash
python3 vol.py -f memory.dump yarascan.YaraScan --yara-rules malware_rules.yar
```

### Timeline Analysis

Reconstruct the sequence of events:

```bash
python3 vol.py -f memory.dump timeliner.Timeliner > timeline.csv
```

### Registry Analysis

Extract Windows registry artifacts:

```bash
# List registry hives
python3 vol.py -f memory.dump windows.registry.hivelist

# Dump specific registry key
python3 vol.py -f memory.dump windows.registry.printkey --key "Microsoft\Windows\CurrentVersion\Run"
```

### Linux Memory Analysis (Reference)

If analyzing Linux dumps, use these commands :

```bash
# List processes
python3 vol.py -f linux_memdump.lime linux.pslist

# Extract bash history
python3 vol.py -f linux_memdump.lime linux.bash

# Check network sockets
python3 vol.py -f linux_memdump.lime linux.sockstat

# Check loaded kernel modules
python3 vol.py -f linux_memdump.lime linux.lsmod

# Find injected code
python3 vol.py -f linux_memdump.lime linux.malfind
```

---

## Part 8: Sample Investigation - MemLabs Lab 1 Walkthrough

Let's walk through a real investigation using the MemLabs "Beginner's Luck" challenge .

### Challenge Description

> "My sister's computer crashed. We were very fortunate to recover this memory dump. Your job is getting all her important files from the system. From what we remember, we suddenly saw a black window pop up with something being executed. When the crash happened, she was trying to draw something."

### Step 1: Initial Analysis

```bash
python3 vol.py -f MemoryDump_Lab1.raw windows.info
python3 vol.py -f MemoryDump_Lab1.raw windows.pslist
```

**Findings:** Suspicious processes found - WinRAR.exe (PID 1512), cmd.exe (PID 1984), mspaint.exe (PID 2424) .

### Step 2: Process Tree Analysis

```bash
python3 vol.py -f MemoryDump_Lab1.raw windows.pstree
```

**Discovery:** WINRAR.exe was launched with a file called "Important.rar" .

### Step 3: Extract the Archive

```bash
python3 vol.py -f MemoryDump_Lab1.raw windows.dumpfiles --pid 1512
```

### Step 4: Find the Flag

After extracting and examining the dumped files, the investigation revealed a flag hidden in an image file that the victim was trying to draw in Paint before the crash.

---

## Lab Completion Checklist

| Task                                      | Completed |
| :---------------------------------------- | :-------- |
| **Part 1: Installation**            | ☐        |
| Python 3 installed and verified           | ☐        |
| Volatility 3 installed                    | ☐        |
| Verification command runs successfully    | ☐        |
| **Part 2: Memory Dump**             | ☐        |
| Sample memory dump downloaded             | ☐        |
| MD5 hash verified                         | ☐        |
| **Part 3: Understanding**           | ☐        |
| `windows.info` command run successfully | ☐        |
| OS version and build documented           | ☐        |
| **Part 4: Core Tasks**              | ☐        |
| `windows.pslist` executed and analyzed  | ☐        |
| `windows.pstree` executed and analyzed  | ☐        |
| `windows.psscan` executed               | ☐        |
| `windows.netscan` executed              | ☐        |
| `windows.malfind` executed              | ☐        |
| Suspicious processes extracted            | ☐        |
| **Part 5: Investigation**           | ☐        |
| All 5 investigation steps completed       | ☐        |
| Findings documented                       | ☐        |
| **Part 6: Questions**               | ☐        |
| All 10 questions answered                 | ☐        |
| **Part 7: Advanced (Optional)**     | ☐        |
| YARA scanning tested                      | ☐        |
| Timeline analysis tested                  | ☐        |

---

## Screenshot Checklist

| Screenshot              | Description                                     |
| :---------------------- | :---------------------------------------------- |
| `vol_install.png`     | Volatility installation success                 |
| `vol_info.png`        | `windows.info` command output                 |
| `pslist.png`          | Process list showing running processes          |
| `pstree.png`          | Process tree showing parent-child relationships |
| `netscan.png`         | Network connections showing suspicious IPs      |
| `cmdline.png`         | Command line arguments for suspicious processes |
| `malfind.png`         | Code injection detection output                 |
| `extracted_files.png` | Dumped process files                            |
| `strings_output.png`  | Strings extraction showing sensitive data       |
| `final_report.png`    | Completed incident report                       |

---

## Troubleshooting Tips

| Issue                                | Solution                                                                            |
| :----------------------------------- | :---------------------------------------------------------------------------------- |
| **Module not found errors**    | Run `pip3 install -r requirements.txt` again                                      |
| **Memory dump not recognized** | Verify file integrity with hash; try `python3 vol.py -f dump.raw banners.Banners` |
| **Slow performance**           | Large dumps (8GB+) take time; consider smaller sample for learning                  |
| **Missing Windows symbols**    | Volatility 3 automatically downloads PDB files; ensure internet connection          |
| **`malfind` no results**     | May mean no code injection detected; try other plugins like `yarascan`            |
| **Command not found**          | Use `python3 vol.py` not just `vol.py`                                          |

---

## Key Takeaways

| Concept                    | Description                                                       |
| :------------------------- | :---------------------------------------------------------------- |
| **Volatility 3**     | Modern memory forensics framework (replaced Volatility 2 in 2025) |
| **Memory Dump**      | Snapshot of RAM at a point in time                                |
| **Process Analysis** | Identifying running processes and their relationships             |
| **Code Injection**   | Malware technique to hide in legitimate processes                 |
| **C2 Communication** | Command & control traffic to attacker infrastructure              |
| **Memory Forensics** | Critical for detecting memory-only malware                        |

---

## Real-World Application: IR Integration

In a real incident response scenario, Volatility is used as follows :

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    VOLATILITY IN INCIDENT RESPONSE                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Phase 1: Detection                                                        │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │ • EDR alert → System isolated → Memory captured                     │   │
│   │ • Volatility triage identifies suspicious processes                 │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                    │                                        │
│                                    ▼                                        │
│   Phase 2: Analysis                                                         │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │ • Extract process memory for malware analysis                       │   │
│   │ • Identify network C2 infrastructure                                │   │
│   │ • Determine lateral movement indicators                             │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                    │                                        │
│                                    ▼                                        │
│   Phase 3: Containment & Eradication                                        │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │ • Block identified IPs on firewalls                                 │   │
│   │ • Reset compromised credentials                                     │   │
│   │ • Scan for additional infected systems                              │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                    │                                        │
│                                    ▼                                        │
│   Phase 4: Reporting                                                        │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │ • Document findings for legal/compliance                            │   │
│   │ • Provide recommendations for prevention                            │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Test Your Knowledge

**Q1:** What is the primary difference between Volatility 2 and Volatility 3?

```
Your answer:
_________________________________________________________________________
```

**Q2:** What plugin would you use to detect code injection in process memory?

```
Your answer:
_________________________________________________________________________
```

**Q3:** Why is memory forensics critical when investigating modern malware?

```
Your answer:
_________________________________________________________________________
```

**Q4:** What command shows parent-child relationships among processes?

```
Your answer:
_________________________________________________________________________
```

**Q5:** What plugin is used to find processes hidden from the active process list?

```
Your answer:
_________________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                                                                                                                      |
| -- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1  | Volatility 3 uses automatic profile detection, Python 3, and the syntax `windows.pslist`; Volatility 2 (deprecated) required manual profiles and used `--profile` flags |
| 2  | `windows.malfind` (or `malfind` in Volatility 2)                                                                                                                        |
| 3  | Modern malware often runs entirely in memory without writing to disk, and rootkits can hide from live analysis tools                                                        |
| 4  | `windows.pstree`                                                                                                                                                          |
| 5  | `windows.psscan`                                                                                                                                                          |

---

## Summary

In this lab, you have:

| Activity                                                           | Completed |
| :----------------------------------------------------------------- | :-------- |
| Installed Volatility 3 on your system                              | ☐        |
| Downloaded and verified a memory dump                              | ☐        |
| Identified OS version using `windows.info`                       | ☐        |
| Analyzed running processes with `pslist`, `pstree`, `psscan` | ☐        |
| Detected malware with `malfind` and `netscan`                  | ☐        |
| Extracted suspicious processes for further analysis                | ☐        |
| Completed a hands-on investigation scenario                        | ☐        |

These skills are essential for:

- Incident responders analyzing active breaches
- Malware analysts examining memory-only payloads
- Threat hunters searching for hidden adversaries
- Forensic investigators building legal evidence

---

## Additional Resources

| Resource                                    | URL                                                 |
| :------------------------------------------ | :-------------------------------------------------- |
| **Volatility 3 GitHub**               | https://github.com/volatilityfoundation/volatility3 |
| **MemLabs (Memory Challenges)**       | https://github.com/stuxnet999/MemLabs               |
| **The Art of Memory Forensics**       | Book by Michael Hale Ligh et al.                    |
| **Volatility 3 Documentation**        | https://volatility3.readthedocs.io                  |
| **DFRWS Memory Forensics Challenges** | http://dfrws.org/challenges                         |

---

## Congratulations!

You have successfully completed the **Memory Forensics with Volatility** lab. You now know how to:

- Install and configure Volatility 3
- Analyze memory dumps for malicious activity
- Detect code injection and hidden processes
- Extract and examine suspicious artifacts
- Use memory forensics in incident response

These skills are critical for modern incident response, where memory-only malware and fileless attacks are increasingly common. Memory forensics often reveals the truth that other tools miss .

![alt text](../Screenshots/Kape_Logo.png)

# Hands-on Lab: Triage Forensics and Evidence Collection with KAPE

**Estimated time:** 60-90 minutes

---

## Project Scenario

You're a **Digital Forensics Analyst** at **Apex Global Logistics**, a supply chain company managing sensitive shipping data and customer information for Fortune 500 clients.

Late Tuesday evening, the SOC detected unusual PowerShell execution on three workstations in the finance department. The EDR alerts suggest potential malware deployment, but the affected systems are still running, and business cannot afford downtime. Your mission: perform rapid triage forensics to collect volatile evidence before these systems are rebooted or remediated.

Management needs answers within hours. Traditional forensic imaging would take too long—each workstation has a 1TB drive, and imaging would require hours of downtime per system. You need a faster approach.

> **The Solution:** KAPE (Kroll Artifact Parser and Extractor)—a high-speed triage tool that collects only the most valuable forensic artifacts and parses them into human-readable format in minutes, not hours .

---

## Introduction

In this lab, you will become familiar with **KAPE** (Kroll Artifact Parser and Extractor), a powerful open-source triage tool created by Eric Zimmerman and now maintained by Kroll . KAPE is designed to:

- **Collect** targeted forensic artifacts from live systems or mounted disk images
- **Process** collected files using modules that parse them into readable output
- **Accelerate** the early phases of forensic investigations, dramatically reducing triage time

Unlike Volatility (memory forensics), TheHive (case management), or Autopsy (full disk forensics), KAPE specializes in **rapid triage collection and processing**—grabbing the "crown jewel" artifacts that matter most in an investigation and immediately making them usable for analysis.

### Why KAPE Matters for Incident Response

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    THE TRIAGE PROBLEM                                        │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Traditional Approach:            KAPE Triage Approach:                     │
│   ┌─────────────────────┐          ┌─────────────────────┐                  │
│   │ Full disk image     │          │ Targeted collection │                  │
│   │ • 8+ hours          │          │ • 5-15 minutes      │                  │
│   │ • 500GB-1TB data    │          │ • 100-500MB data    │                  │
│   │ • Requires offline  │          │ • Live system OK    │                  │
│   │   analysis          │          │ • Immediate parsing │                  │
│   └─────────────────────┘          └─────────────────────┘                  │
│                                                                              │
│   KAPE collects:                                                            │
│   • Prefetch files (program execution history)                              │
│   • Registry hives (system configuration, user activity)                    │
│   • Event logs (Security, System, Application)                              │
│   • $MFT (file system metadata)                                             │
│   • Recent documents, user artifacts, browser history                       │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

> **Key Insight:** KAPE isn't meant to replace deep-dive forensics—it's meant to **accelerate** incident response by answering critical questions quickly: What happened? When? Which systems are affected?

---

## Learning Objectives

After completing this exercise, you will be able to:

| # | Objective                                                                      |
| - | ------------------------------------------------------------------------------ |
| 1 | Download and install KAPE on a Windows analysis workstation                    |
| 2 | Understand the two-phase architecture: Target Collection and Module Processing |
| 3 | Perform rapid triage collection from a live system or image                    |
| 4 | Process collected artifacts with built-in parsing modules                      |
| 5 | Generate actionable timelines from collected evidence                          |
| 6 | Create custom targets for specific collection needs                            |

---

## Prerequisites

You must have:

| Requirement                          | Status | Notes                                       |
| :----------------------------------- | :----- | :------------------------------------------ |
| **Windows 10/11 computer**     | ☐     | KAPE runs only on Windows                   |
| **20GB free disk space**       | ☐     | For KAPE installation and output            |
| **Local admin rights**         | ☐     | Required for installation                   |
| **Windows test VM (optional)** | ☐     | For realistic triage collection             |
| **Sample evidence (optional)** | ☐     | Can use your own system or download samples |

---

## What is KAPE? Understanding the Architecture

KAPE is fundamentally a two-stage tool that separates **what** you collect from **how** you process it .

### Core Concepts

| Concept                      | Definition                             | Example                                                                                |
| :--------------------------- | :------------------------------------- | :------------------------------------------------------------------------------------- |
| **Target**             | Defines WHAT files to collect          | `Windows10_Prefetch` target collects all `.pf` files from `C:\Windows\Prefetch\` |
| **Module**             | Defines HOW to process collected files | `ParsePrefetch` module runs `PECmd.exe` on prefetch files                          |
| **Target Source**      | Where to collect FROM                  | `C:\` (live system) or `E:\` (mounted image)                                       |
| **Target Destination** | Where to copy collected files          | `D:\KAPE_Output\2025-04-07_Case001\`                                                 |

### How KAPE Works

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    KAPE TWO-PHASE ARCHITECTURE                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   PHASE 1: TARGET PHASE                                                     │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                                                                       │   │
│   │   Source (Live C:\)  ──►  Target Definition  ──►  Destination     │   │
│   │                              (which files)          (copy here)      │   │
│   │                                                                       │   │
│   │   Example: "Collect all event logs from C:\ to E:\Triage\"           │   │
│   │                                                                       │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                    │                                        │
│                                    ▼                                        │
│   PHASE 2: MODULE PHASE                                                     │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                                                                       │   │
│   │   Collected Files  ──►  Module Definition  ──►  Parsed Output      │   │
│   │                        (which parser)           (human readable)     │   │
│   │                                                                       │   │
│   │   Example: "Run LogParser on event logs and output CSV"              │   │
│   │                                                                       │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
│   OR - Run BOTH phases together (most common for triage):                   │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │   Source ──► [TARGET: Collect] ──► Destination ──► [MODULE: Parse]│   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Why this matters:** Because collection and processing are separate, you can:

- Collect once and process multiple ways (different modules)
- Create custom targets for your organization's unique artifacts
- Share collected data with team members who apply their own modules

---

## Part 1: Installing KAPE

### Step 1: Download KAPE

1. Navigate to the official KAPE download page:

   ```
   https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape
   ```
2. OR use the direct download link from Eric Zimmerman's site:

   ```
   https://ericzimmerman.github.io/#!index.md
   ```
3. Download the latest version (the download is a `.zip` file)

> **Note:** KAPE is free for law enforcement, personal learning, and educational institutions . Commercial use requires a license.

### Step 2: Extract KAPE

1. Create a folder on your analysis workstation:

   ```
   C:\Tools\KAPE
   ```
2. Extract the downloaded `.zip` contents to this folder
3. Verify the folder structure:

   ```
   C:\Tools\KAPE\
   ├── kape.exe
   ├── gkape.exe (GUI version)
   ├── Targets\
   │   ├── *.tkape files
   ├── Modules\
   │   ├── *.mkape files
   ├── Bin\ (supporting executables)
   └── Docs\
   ```

### Step 3: Update KAPE (Critical!)

KAPE relies on community-contributed targets and modules. Always update before using:

```powershell
# Open PowerShell as Administrator
cd C:\Tools\KAPE

# Run the update script
.\Get-KAPEUpdate.ps1
```

This downloads the latest targets and modules from GitHub .

### Step 4: Launch KAPE GUI

```powershell
# From the KAPE directory
.\gkape.exe
```

![KAPE GUI Interface]

*[Screenshot: KAPE GUI showing Target and Module options]*

---

## Part 2: Understanding the KAPE Interface

### GUI Layout

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         KAPE GUI INTERFACE                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │ TARGET OPTIONS                                            [ ] Use   │   │
│   │ ┌─────────────────────────────────────────────────────────────┐     │   │
│   │ │ Target Source: [C:\                ] Browse                 │     │   │
│   │ │ Target Destination: [D:\KAPE_Output\  ] Browse             │     │   │
│   │ │ Target: [Select a target...                ▼]              │     │   │
│   │ └─────────────────────────────────────────────────────────────┘     │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │ MODULE OPTIONS                                            [ ] Use   │   │
│   │ ┌─────────────────────────────────────────────────────────────┐     │   │
│   │ │ Module Source: [Same as Target Destination     Browse]     │     │   │
│   │ │ Module Destination: [D:\KAPE_Processed\       Browse]      │     │   │
│   │ │ Module: [Select a module...                   ▼]           │     │   │
│   │ │ Variables: [Key              ] [Value          ]           │     │   │
│   │ └─────────────────────────────────────────────────────────────┘     │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
│   [ EXECUTE ]  [ Sync with GitHub ]  [ About ]  [ Exit ]                    │
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────────┐
│   │ Console Output:                                                         │
│   │                                                                         │
│   │                                                                         │
│   └─────────────────────────────────────────────────────────────────────────┘
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Key UI Elements

| Element                      | Purpose                                                |
| :--------------------------- | :----------------------------------------------------- |
| **Target Source**      | The drive or folder to collect evidence FROM           |
| **Target Destination** | Where to COPY collected evidence                       |
| **Target dropdown**    | Which files to collect (choose from 100+ options)      |
| **Module Source**      | Usually same as Destination (collected files location) |
| **Module Destination** | Where to SAVE parsed output                            |
| **Module dropdown**    | Which parser to run on collected files                 |
| **Sync with GitHub**   | Downloads latest targets/modules (do this often!)      |

---

## Part 3: Hands-On Triage Collection

### Scenario Setup

For this lab, you have two options:

**Option A (Recommended):** Use a Windows 10/11 VM as your "target" with some simulated user activity (create files, browse web, run programs).

**Option B:** Run KAPE against your own system (learn what artifacts exist on a typical Windows computer).

### Step 1: Prepare Target System (Optional)

If using a test VM, perform some activity to generate artifacts:

```powershell
# Run some commands to generate prefetch and other artifacts
notepad.exe
calc.exe
whoami /all

# Create and delete a test file
echo "Test evidence" > C:\Users\Public\testfile.txt
del C:\Users\Public\testfile.txt
```

### Step 2: Run Basic Triage Collection

Launch the KAPE GUI (gkape.exe) and configure:

| Field                        | Value                                                          |
| :--------------------------- | :------------------------------------------------------------- |
| **Target Source**      | `C:\` (or your target drive)                                 |
| **Target Destination** | `C:\KAPE_Case\2025-04-07_Triage\Collected\`                  |
| **Target**             | Select `!All_Triage` (this collects common triage artifacts) |

> **Note:** Create the destination folder first or let KAPE create it.

**Check "Use Target Options"** then click **Execute**.

### Step 3: Observe Collection Output

Watch the console as KAPE collects files:

```
[+] Processing target: !All_Triage
[+] Processing target: MFT
[+]   Collecting: C:\$MFT -> C:\KAPE_Case\2025-04-07_Triage\Collected\MFT
[+] Processing target: Prefetch
[+]   Collecting: C:\Windows\Prefetch\*.pf -> C:\KAPE_Case\2025-04-07_Triage\Collected\Prefetch
[+] Processing target: Registry_Hives
[+]   Collecting: C:\Windows\System32\config\SOFTWARE -> ...
[+]   Collecting: C:\Windows\System32\config\SYSTEM -> ...
[+]   Collecting: C:\Windows\System32\config\SAM -> ...
[+]   Collecting: C:\Windows\System32\config\SECURITY -> ...
[+] Processing target: EventLogs
[+]   Collecting: C:\Windows\System32\winevt\Logs\*.evtx -> ...
[+] Processing target: RecentDocs
[+]   Collecting: C:\Users\[user]\NTUSER.DAT -> ...
[+] 137 files collected. Total size: 246 MB
```

### Step 4: Process the Collected Files

Now that files are collected, process them with modules:

| Field                        | Value                                         |
| :--------------------------- | :-------------------------------------------- |
| **Module Source**      | `C:\KAPE_Case\2025-04-07_Triage\Collected\` |
| **Module Destination** | `C:\KAPE_Case\2025-04-07_Triage\Processed\` |
| **Module**             | Select `!All_Triage_Processing`             |

**Check "Use Module Options"** then click **Execute**.

### Step 5: Explore the Output

Navigate to your Module Destination folder. You should see:

```
C:\KAPE_Case\2025-04-07_Triage\Processed\
├── MFT\ (parsed Master File Table output)
├── Prefetch\ (program execution timeline)
├── Registry\ (regripper output for each hive)
├── EventLogs\ (parsed event logs as CSV)
├── Timeline.csv (combined timeline of all events)
└── KAPE_Log.txt (execution log)
```

**Open `Timeline.csv`** in Excel or a text editor to see a unified timeline of system activity .

---

## Part 4: Core Triage Artifacts and Their Value

### High-Value Artifacts for IR

| Artifact                                   | What It Tells You                                          | KAPE Target                             |
| :----------------------------------------- | :--------------------------------------------------------- | :-------------------------------------- |
| **Prefetch (.pf files)**             | Which programs executed, when, and how many times          | `Windows_Prefetch`                    |
| **$MFT (Master File Table)**         | File system activity—creation, modification, deletion     | `MFT`                                 |
| **Event Logs (Security, System)**    | User logins, service starts, errors, process creation      | `Windows_EventLogs`                   |
| **Registry (SAM, SYSTEM, SOFTWARE)** | User accounts, system config, installed software, Run keys | `Registry_All`                        |
| **Amcache.hve**                      | Program execution history (including from USB drives)      | `Windows_Amcache`                     |
| **Recent Documents**                 | User file access patterns                                  | `Windows_RecentDocs`                  |
| **Browser Artifacts**                | Web history, downloads                                     | `Chrome_History`, `Firefox_History` |
| **Scheduled Tasks**                  | Persistence mechanisms                                     | `Windows_ScheduledTasks`              |

### What to Look For in Each Artifact

**Prefetch Files:**

- Unusual program names (e.g., `payload.exe`, `injector.exe`)
- Programs running from temp directories
- Programs executed around the time of the incident

**Event Logs:**

- Event ID 4624 (successful logins) - especially unusual hours
- Event ID 4688 (process creation) - look for PowerShell, cmd, wscript
- Event ID 4104 (script block logging) - encoded PowerShell commands

**Registry Run Keys:**

- Persistence entries pointing to temp locations
- Obfuscated entry names
- Executables with suspicious names

**Timeline Analysis:**
A timeline combines all artifact timestamps into a single view, revealing the sequence of events :

```
Timestamp             | Source      | Artifact                 | Details
----------------------|-------------|--------------------------|--------------------------------
2025-04-07 08:30:15   | $MFT        | File Created             | C:\Users\user\malware.exe
2025-04-07 08:30:22   | Prefetch    | Program Executed         | MALWARE.EXE (1 time)
2025-04-07 08:30:45   | Event Log   | Process Created (4688)   | powershell.exe -enc <base64>
2025-04-07 08:31:10   | Registry    | Run Key Added            | HKLM\Software\...\Update
```

---

## Part 5: Advanced KAPE Techniques

### Running from Command Line (For Automation/Scripting)

While the GUI is great for interactive use, the command line enables automation:

```powershell
# Basic triage collection and processing in one command
kape.exe --tsource C:\ --tdest C:\Output\Collected --target !All_Triage --msource C:\Output\Collected --mdest C:\Output\Processed --module !All_Triage_Processing

# Collect only prefetch files
kape.exe --tsource C:\ --tdest C:\Output --target Windows_Prefetch

# Run only a module on previously collected data
kape.exe --msource D:\Evidence --mdest D:\Parsed --module ParseEventLogs
```

### Creating a Custom Target

KAPE targets are simple text files. Create a custom target to collect specific files for your organization:

1. Navigate to `C:\Tools\KAPE\Targets\`
2. Create a new file: `Custom_HR_Files.tkape`

```yaml
# Custom_HR_Files.tkape
Description: Collect HR department specific files
Category: Custom
Author: Your Name
Version: 1.0

Targets:
    - Name: HR_Docs
      Category: Custom
      Path: C:\HR_Data\*.xlsx
      Recurse: True
      Comment: Collect all HR Excel files

    - Name: HR_Policies
      Category: Custom
      Path: C:\Shared\Policies\*.pdf
      Recurse: True
```

3. Save the file. Your custom target now appears in the GUI dropdown.

### Creating a Custom Module

Modules define how to process specific file types:

```yaml
# Custom_CSV_Report.mkape
Description: Convert collected CSV to report format
Category: Custom
Author: Your Name
Version: 1.0
Binary: C:\Tools\KAPE\Bin\custom_parser.exe
CommandLine: --input "%sourceFile%" --output "%destinationDirectory%"
ExportFormat: csv
```

### Remote Collection via MDE or Live Response

KAPE can be deployed remotely using tools like Microsoft Defender for Endpoint :

```powershell
# Deploy KAPE via MDE Live Response
# 1. Upload kape.zip to MDE library
# 2. Connect to remote machine
# 3. Run collection script
# 4. Download results
```

---

## Part 6: Hands-On Investigation Scenario

### Scenario

You're investigating a potential data exfiltration incident at Apex Global Logistics. The affected workstation is still online, and you need to quickly determine:

1. What malware executed?
2. When did it run?
3. Are there persistence mechanisms?
4. What user account was used?

### Step 1: Run KAPE Triage

Execute the following:

```
Target Source: C:\
Target Destination: C:\Case_Apex\Triage\
Target: !All_Triage

Module Source: C:\Case_Apex\Triage\
Module Destination: C:\Case_Apex\Processed\
Module: !All_Triage_Processing
```

### Step 2: Analyze the Timeline

Open `Timeline.csv` and search for the incident timeframe.

**Focus on:**

- Unusual process executions (PowerShell, cmd, wscript)
- File creations in temp directories
- Registry modifications (Run keys)

### Step 3: Examine Prefetch

Navigate to `C:\Case_Apex\Processed\Prefetch\` and open the CSV output.

**Look for:**

- Programs with recent execution times
- Programs running from `%TEMP%` or `AppData\Local\Temp`
- Unusual filenames

### Step 4: Check Persistence

Open the Registry module output:

```
C:\Case_Apex\Processed\Registry\NTUSER.DAT_Run_*.csv
C:\Case_Apex\Processed\Registry\SOFTWARE_Microsoft_Windows_CurrentVersion_Run_*.csv
```

**Look for:**

- Entries with suspicious paths
- Recently added Run keys

### Step 5: Document Findings

Create a triage report with:

| Question                                | Your Answer |
| --------------------------------------- | ----------- |
| What suspicious executables were found? |             |
| When did they execute?                  |             |
| What user account was active?           |             |
| Is persistence present?                 |             |
| What C2 indicators exist?               |             |

---

## Part 7: Timeline Generation Deep Dive

One of KAPE's most powerful features is automated timeline generation .

### What Gets Included in a Timeline

| Artifact       | Timeline Contribution                               |
| :------------- | :-------------------------------------------------- |
| $MFT           | File creation, modification, access, deletion times |
| Registry Hives | Last write times of keys                            |
| Event Logs     | Event IDs and descriptions (time-sorted)            |
| Prefetch       | Program execution times                             |

### Running Timeline-Specific Collection

To generate a forensic timeline:

1. **Collect timeline artifacts:**

   ```
   Target: MiniTimelineCollection
   Target Source: C:\
   Target Destination: C:\Timeline\Collected\
   ```
2. **Process with timeline module:**

   ```
   Module: Mini_Timeline
   Module Source: C:\Timeline\Collected\
   Module Destination: C:\Timeline\Processed\
   ```
3. **Optionally, slice by date:**

   ```
   Module: Mini_Timeline_Slice_by_Daterange
   Variables: dateRange = "04/01/2025-04/07/2025"
   ```

### Using Timeline Results

The resulting CSV can be:

- Opened in **Timeline Explorer** (another Eric Zimmerman tool)
- Imported into Excel for filtering
- Converted for use in Splunk or Elastic
- Shared with team members for collaborative analysis

---

## Lab Completion Checklist

| Task                                | Completed |
| :---------------------------------- | :-------- |
| **Part 1: Installation**      | ☐        |
| KAPE downloaded and extracted       | ☐        |
| Update script executed successfully | ☐        |
| GUI launches without errors         | ☐        |
| **Part 2: Understanding**     | ☐        |
| Target vs Module concept understood | ☐        |
| GUI navigation mastered             | ☐        |
| **Part 3: Basic Triage**      | ☐        |
| Target collection executed          | ☐        |
| Module processing executed          | ☐        |
| Output files inspected              | ☐        |
| **Part 4: Artifact Analysis** | ☐        |
| Prefetch files analyzed             | ☐        |
| Registry Run keys checked           | ☐        |
| Timeline CSV opened and explored    | ☐        |
| **Part 5: Advanced**          | ☐        |
| Custom target created (optional)    | ☐        |
| Command line execution tested       | ☐        |
| **Part 6: Scenario**          | ☐        |
| Full triage performed               | ☐        |
| Findings documented                 | ☐        |

---

## Screenshot Checklist

| Screenshot               | Description                             |
| :----------------------- | :-------------------------------------- |
| `kape_install.png`     | KAPE extracted and folder structure     |
| `kape_gui.png`         | KAPE GUI showing Target/Module options  |
| `target_execution.png` | Console output during target collection |
| `module_execution.png` | Console output during module processing |
| `timeline_csv.png`     | Timeline CSV opened in Excel            |
| `prefetch_output.png`  | Parsed prefetch results                 |
| `registry_runkeys.png` | Registry Run key findings               |

---

## Troubleshooting Tips

| Issue                           | Solution                                                                        |
| :------------------------------ | :------------------------------------------------------------------------------ |
| **Access denied errors**  | Run KAPE as Administrator; many forensic artifacts require elevated privileges  |
| **Module fails to run**   | Verify the required binaries exist in `C:\Tools\KAPE\Bin\`                    |
| **Update script fails**   | Check internet connection; ensure PowerShell execution policy allows scripts    |
| **No timeline generated** | Ensure MiniTimelineCollection target and Mini_Timeline module were both run     |
| **GUI doesn't open**      | Run from command line to see error messages; ensure .NET Framework is installed |

---

## Key Takeaways

| Concept                      | Description                                                       |
| :--------------------------- | :---------------------------------------------------------------- |
| **KAPE**               | Kroll Artifact Parser and Extractor - rapid forensics triage tool |
| **Target**             | Defines WHICH forensic artifacts to collect                       |
| **Module**             | Defines HOW to process collected artifacts                        |
| **Triage**             | Prioritized forensic collection focused on high-value artifacts   |
| **Timeline**           | Chronological reconstruction of system events                     |
| **gkape.exe**          | GUI version of KAPE                                               |
| **Get-KAPEUpdate.ps1** | Script to download latest targets and modules                     |

---

## Real-World Application: IR Workflow Integration

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    KAPE IN THE IR WORKFLOW                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Detection Alert                                                           │
│        │                                                                     │
│        ▼                                                                     │
│   Step 1: Triage Collection (15 min)                                       │
│   └── Run KAPE with !All_Triage target                                      │
│        │                                                                     │
│        ▼                                                                     │
│   Step 2: Initial Analysis (30 min)                                         │
│   └── Process with !All_Triage_Processing                                   │
│   └── Identify suspicious processes, files, connections                     │
│        │                                                                     │
│        ▼                                                                     │
│   Step 3: Targeted Deep Dive                                                │
│   └── Create custom target for additional artifacts                         │
│   └── Run specialized modules                                                │
│        │                                                                     │
│        ▼                                                                     │
│   Step 4: Remediation Decision                                              │
│   └── Based on KAPE findings, decide: isolate, reimage, or further analyze  │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Test Your Knowledge

**Q1:** What does KAPE stand for and who created it?

```
Your answer:
_________________________________________________________________________
```

**Q2:** What is the difference between a Target and a Module in KAPE?

```
Your answer:
_________________________________________________________________________
```

**Q3:** Why is timeline generation important in incident response?

```
Your answer:
_________________________________________________________________________
```

**Q4:** What KAPE target would you use to collect program execution history?

```
Your answer:
_________________________________________________________________________
```

**Q5:** How do you update KAPE with the latest targets and modules?

```
Your answer:
_________________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                                                      |
| -- | ----------------------------------------------------------------------------------------------------------- |
| 1  | Kroll Artifact Parser and Extractor; created by Eric Zimmerman                                              |
| 2  | A Target defines WHAT files to collect; a Module defines HOW to process those files                         |
| 3  | Timeline reconstruction reveals the sequence of events, helping investigators understand attack progression |
| 4  | `Windows_Prefetch` (prefetch files show program execution history)                                        |
| 5  | Run `Get-KAPEUpdate.ps1` PowerShell script from the KAPE directory                                        |

---

## Summary

In this lab, you have:

| Activity                                           | Completed |
| :------------------------------------------------- | :-------- |
| Downloaded and installed KAPE                      | ☐        |
| Updated KAPE with latest targets and modules       | ☐        |
| Performed targeted triage collection               | ☐        |
| Processed collected artifacts into readable output | ☐        |
| Generated and analyzed a forensic timeline         | ☐        |
| Investigated a realistic incident scenario         | ☐        |

These skills are essential for:

- Incident responders conducting rapid triage
- Digital forensic analysts collecting evidence efficiently
- SOC teams needing quick answers during active breaches
- Consultants performing multiple investigations simultaneously

---

## Additional Resources

| Resource                       | URL                                                                               |
| :----------------------------- | :-------------------------------------------------------------------------------- |
| **KAPE Download**        | https://www.kroll.com/en/services/cyber-risk/kroll-artifact-parser-extractor-kape |
| **Eric Zimmerman Tools** | https://ericzimmerman.github.io                                                   |
| **KAPE Documentation**   | https://ericzimmerman.github.io/KapeDocs                                          |
| **SANS KAPE Webcast**    | https://www.sans.org/webcasts/kape-whats-all-buzz-about/                          |
| **AboutDFIR KAPE Guide** | https://aboutdfir.com/toolsandartifacts/windows/kape/                             |

---

## Congratulations!

You have successfully completed the **Triage Forensics and Evidence Collection with KAPE** lab. You now know how to:

- Deploy KAPE for rapid triage collection
- Collect and parse high-value forensic artifacts
- Generate actionable timelines from multiple data sources
- Integrate KAPE into incident response workflows

KAPE represents a paradigm shift in forensic triage—from slow, exhaustive imaging to focused, intelligent collection of the artifacts that matter most. As one SANS instructor put it, "KAPE is a game-changer, no other tool comes close" .

> **Next Steps:** After completing this lab, explore integrating KAPE with other Eric Zimmerman tools like Timeline Explorer, Registry Explorer, and LECmd for deeper analysis. Consider building custom targets for your organization's unique environment.

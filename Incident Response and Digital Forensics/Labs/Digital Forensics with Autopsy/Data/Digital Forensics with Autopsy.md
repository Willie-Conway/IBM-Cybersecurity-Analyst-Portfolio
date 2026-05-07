![alt text](<../Screenshots/Autopsy_Digital_Forensics_Logo.png>)

# Hands-on Lab: Digital Forensics with Autopsy

**Estimated time:** 90-120 minutes

---

## Project Scenario

You've been hired as a **digital forensics investigator** by **CloudNine Marketing**, a fast-growing digital marketing agency that manages social media campaigns for Fortune 500 clients.

In the wake of recent industry breaches, management has become increasingly anxious about potential insider threats and data leaks. A senior marketing strategist, **Sarah Jenkins**, submitted her resignation unexpectedly last week. During her exit interview, several red flags were raised about potential client data exfiltration.

The security team has since seized Sarah's company-issued laptop and created a forensic image of the hard drive. The agency has now tasked you with **investigating potential data theft** and **identifying evidence of misconduct** that could violate client confidentiality agreements and NDAs.

---

## Introduction

In this lab, you will become familiar with **Autopsy**, an open-source digital forensics platform used for investigating disk images and recovering evidence from compromised systems. Autopsy is the graphical interface for The Sleuth Kit (TSK) and is widely used by forensic investigators, incident responders, and law enforcement to analyze file systems, recover deleted files, and uncover user activity.

Unlike Snyk (code scanning), Nessus (vulnerability scanning), TheHive (incident response), and Splunk (SIEM), Autopsy focuses on **dead analysis**—examining disk images from compromised systems without booting them, preserving evidence integrity.

---

## Learning Objectives

After completing this exercise, you will be able to:

| # | Objective                                                    |
| - | ------------------------------------------------------------ |
| 1 | Install Autopsy on Windows or Linux                          |
| 2 | Create a forensic case and import a disk image               |
| 3 | Navigate the Autopsy interface and run ingest modules        |
| 4 | Locate deleted files and recover them                        |
| 5 | Analyze file system metadata, web history, and user activity |
| 6 | Extract critical evidence for incident reporting             |

---

## Prerequisites

You must have:

| Requirement                                 | Status                |
| :------------------------------------------ | :-------------------- |
| **Computer with 8GB+ RAM**            | ☐ (16GB recommended) |
| **20GB free disk space**              | ☐                    |
| **Windows 10/11, macOS, or Linux**    | ☐                    |
| **Admin privileges for installation** | ☐                    |

---

## What is Autopsy?

Autopsy is a digital forensics platform that helps investigators analyze disk images without altering the original evidence.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         AUTOPSY CAPABILITIES                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                         AUTOPSY PLATFORM                             │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                    │                                        │
│           ┌────────────────────────┼────────────────────────┐               │
│           │                        │                        │               │
│           ▼                        ▼                        ▼               │
│   ┌───────────────┐        ┌───────────────┐        ┌───────────────┐       │
│   │  File System  │        │  Deleted File │        │  Timeline     │       │
│   │  Analysis     │        │  Recovery     │        │  Analysis     │       │
│   │               │        │               │        │               │       │
│   │ • Directory   │        │ • Carving     │        │ • Event       │       │
│   │   structure   │        │ • Unallocated │        │   sequencing  │       │
│   │ • Metadata    │        │   space       │        │ • Time-based  │       │
│   │ • Permissions │        │ • Orphan files│        │   filtering   │       │
│   └───────────────┘        └───────────────┘        └───────────────┘       │
│                                                                              │
│   Additional Modules:                                                        │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │  Keyword Search  │  Web History  │  Registry Analysis  │  Hash Lookup │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Dead Analysis vs. Live Analysis

| Type                    | Description                                 | Autopsy Use        |
| :---------------------- | :------------------------------------------ | :----------------- |
| **Dead Analysis** | Examining a powered-off system's disk image | ✓ Primary focus   |
| **Live Analysis** | Examining a running system                  | ✗ Not for Autopsy |

Autopsy performs **dead analysis**, meaning you analyze a copy of the drive (disk image) without altering the original evidence—critical for chain of custody.

---

## Part 1: Installing Autopsy

### Option A: Windows Installation (Recommended)

#### Step 1: Download Autopsy

1. Navigate to the official Autopsy download page:

   ```
   https://www.autopsy.com/download/
   ```
2. Click **Download Autopsy** (Windows installer)

#### Step 2: Run the Installer

1. Launch the downloaded `.exe` file
2. Accept the license agreement
3. Choose installation directory (default: `C:\Program Files\Autopsy`)
4. Select components to install (keep defaults)
5. Click **Install**

The installer includes:

- Autopsy GUI
- The Sleuth Kit (TSK) CLI tools
- Java Runtime Environment (if needed)

#### Step 3: Launch Autopsy

1. From the Start Menu, launch **Autopsy**
2. The main window will appear

### Option B: Linux Installation (Kali/Ubuntu)

For Kali Linux or Ubuntu systems:

```bash
# Update package list
sudo apt update

# Install Autopsy
sudo apt install autopsy -y

# Launch Autopsy
autopsy
```

After launching, access Autopsy in your browser at:

```
http://localhost:9999/autopsy
```

---

## Part 2: Obtaining a Sample Disk Image

For this lab, you need a disk image to analyze. You have several options:

### Option A: Download a Forensic Sample Image

Download a sample disk image from public forensic repositories:

| Source                    | URL                         | Description          |
| :------------------------ | :-------------------------- | :------------------- |
| **Digital Corpora** | https://digitalcorpora.org/ | Various drive images |
| **CFReDS**          | https://cfreds.nist.gov/    | NIST forensic images |

**Recommended:** Download a small `.dd` or `.E01` image (1-2 GB).

### Option B: Create Your Own Test Image

#### Step 1: Create a Small Disk Image

**Using FTK Imager (Windows):**

1. Download FTK Imager (free) from Exterro
2. Launch FTK Imager
3. **File → Create Disk Image**
4. Select **Physical Drive** or **Logical Drive**
5. Choose a small USB drive or create a RAM drive
6. Select **Raw (dd)** as image format
7. Save as `test_image.dd`

**Using dd (Linux/macOS):**

```bash
# Create a 100MB test image from /dev/zero
dd if=/dev/zero of=test_image.dd bs=1M count=100
```

### Option C: Use University Lab Materials

Some universities provide forensic lab images for educational purposes. Check your institution's resources.

---

## Part 3: Creating a New Forensic Case

### Step 1: Start a New Case

1. Launch Autopsy
2. Click **New Case**

### Step 2: Enter Case Information

| Field                    | Value                           | Description                     |
| :----------------------- | :------------------------------ | :------------------------------ |
| **Case Name**      | `CloudNine_Data_Exfiltration` | Case identifier                 |
| **Base Directory** | `C:\Cases\CloudNine`          | Where case files will be stored |
| **Case Number**    | `CN-IR-2024-042`              | Case tracking number            |
| **Examiner**       | `Your Name`                   | Investigator name               |

### Step 3: Add Data Source

1. Click **Add Data Source** or **Next**
2. Select **Disk Image or VM File** as the data source type
3. Browse to your disk image file
4. Select the image type:

   - **Disk Image** (`.dd`, `.raw`, `.img`, `.E01`)
   - **Partition Image**
   - **Logical File**
5. Click **Next**

### Step 4: Configure Ingest Modules

Select the ingest modules to run. For this lab, select:

| Module                            | Purpose                                |
| :-------------------------------- | :------------------------------------- |
| ✓**Recent Activity**       | Analyzes web history, recent documents |
| ✓**File System Analysis**  | Basic file system parsing              |
| ✓**Deleted File Recovery** | Finds and recovers deleted files       |
| ✓**Keyword Search**        | Searches for specific terms            |
| ✓**Hash Lookup**           | Identifies known files                 |

### Step 5: Run the Ingest

1. Click **Next** through the remaining screens
2. Click **Finish**
3. Wait for Autopsy to process the image

Processing time depends on image size and modules selected (5-20 minutes for a small image).

---

## Part 4: Navigating the Autopsy Interface

After the ingest completes, you'll see the main Autopsy interface:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         AUTOPSY MAIN INTERFACE                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │  Case: CloudNine_Data_Exfiltration                    [Search...] ☐  │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
│   ┌──────────────────┐  ┌──────────────────────────────────────────────┐   │
│   │  DATA SOURCES    │  │  RESULTS                                     │   │
│   │                  │  │                                              │   │
│   │  ▼ disk_image.dd │  │  Type: All Results ▼  Severity: All ▼       │   │
│   │    ├─ Partitions │  │  ┌────────────────────────────────────────┐ │   │
│   │    └─ Volumes    │  │  │ • Deleted Files (XX)                   │ │   │
│   │                  │  │  │ • Recent Documents (XX)                │ │   │
│   │  ANALYSIS       │  │  │ • Web History (XX)                      │ │   │
│   │  ───────────────  │  │  │ • Keyword Hits (X)                    │ │   │
│   │  • File Types    │  │  └────────────────────────────────────────┘ │   │
│   │  • Deleted Files │  │                                              │   │
│   │  • Directory Tree│  │  ┌────────────────────────────────────────┐ │   │
│   │  • Web History   │  │  │ Event Details                          │ │   │
│   │  • Timeline      │  │  │ ──────────────────────────────────────│ │   │
│   │                  │  │  │ File: client_campaign_data.xlsx        │ │   │
│   └──────────────────┘  │  │ Status: Deleted                        │ │   │
│                         │  │ Modified: 2024-05-01 14:23:11          │ │   │
│                         │  └────────────────────────────────────────┘ │   │
│                         │                                              │   │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Key Interface Areas

| Area                     | Description                                               |
| :----------------------- | :-------------------------------------------------------- |
| **Data Sources**   | Left panel showing disk structure and analysis categories |
| **Results**        | Main panel showing discovered artifacts                   |
| **Search Bar**     | Upper right for keyword searches                          |
| **Tagging System** | Mark artifacts as important for the investigation         |

---

## Part 5: Core Forensic Tasks

### Task 1: Locate Deleted Files

1. In the **Analysis** section, expand **File Types**
2. Click **Deleted Files**
3. Review the list of recoverable files

### Task 2: Recover a Deleted File

1. Right-click on a deleted file
2. Select **Extract File(s)**
3. Choose a destination folder (e.g., `C:\Cases\CloudNine\Recovered_Files\`)
4. Click **OK**

The recovered file is saved to your chosen location.

### Task 3: Analyze Web History

1. In the **Analysis** section, expand **Web History**
2. View:
   - **Visited URLs**
   - **Search Terms**
   - **Downloaded Files**
   - **Cookies**

This reveals user browsing activity, which is critical for incident investigations.

### Task 4: Perform Keyword Search

1. Click the **Keyword Search** button in the upper right
2. Enter search terms such as:

   - `confidential`
   - `client list`
   - `campaign data`
   - `password`
   - `NDA`
3. Review the search results

### Task 5: Timeline Analysis

1. In the **Analysis** section, click **Timeline**
2. Select a time range for analysis
3. View events chronologically

The timeline helps reconstruct the sequence of user actions:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         TIMELINE ANALYSIS                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   2024-05-01 08:30:15 - System boot                                         │
│   2024-05-01 09:02:44 - File created: q2_campaign_metrics.xlsx              │
│   2024-05-01 09:15:22 - USB device connected                                │
│   2024-05-01 09:18:07 - File copied: q2_campaign_metrics.xlsx → E:\         │
│   2024-05-01 09:20:33 - USB device removed                                  │
│   2024-05-01 14:23:11 - File deleted: q2_campaign_metrics.xlsx              │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Part 6: Investigation Questions

Using Autopsy, answer the following questions about the CloudNine Marketing incident:

| # | Question                                                                            |
| - | ----------------------------------------------------------------------------------- |
| 1 | What is the filename of the deleted Excel document containing client campaign data? |
| 2 | What USB device was connected to the system (Vendor and Product)?                   |
| 3 | What files were copied to the USB device?                                           |
| 4 | What web searches did Sarah perform related to competitors or job searching?        |
| 5 | What was the most recently accessed file before the USB was connected?              |
| 6 | What email address appears in the deleted browser history?                          |
| 7 | What keyword search term revealed the most sensitive findings?                      |

---

## Part 7: Advanced Features

### Registry Analysis

For Windows disk images, Autopsy can analyze the Windows Registry:

1. Expand **Data Artifacts** → **Registry**
2. View:
   - Recently opened documents
   - USB device history
   - User accounts
   - Autostart locations

### Hash Lookup

1. Navigate to **Results** → **Hash Set Hits**
2. See which files match known hash databases (NSRL, custom sets)

### Tagging Evidence

1. Right-click on any artifact
2. Select **Tag**
3. Choose tag type:
   - **Bookmark** (for important evidence)
   - **Notable** (significant finding)
   - **Custom tag**

### Generating Reports

1. Click **Generate Report** (upper right)
2. Select report format:

   - HTML (for browser viewing)
   - CSV (for data analysis)
   - Excel (for spreadsheets)
   - PDF (for formal reports)
3. Choose what to include:

   - All results
   - Tagged items only
   - Specific sections
4. Click **Generate**

---

## Lab Completion Checklist

| Task                                       | Completed |
| :----------------------------------------- | :-------- |
| **Part 1: Installation**             | ☐        |
| Downloaded and installed Autopsy           | ☐        |
| Launched Autopsy successfully              | ☐        |
| **Part 2: Disk Image**               | ☐        |
| Obtained or created a disk image           | ☐        |
| **Part 3: Case Creation**            | ☐        |
| Created case "CloudNine_Data_Exfiltration" | ☐        |
| Added disk image as data source            | ☐        |
| Selected appropriate ingest modules        | ☐        |
| Completed ingest processing                | ☐        |
| **Part 4: Navigation**               | ☐        |
| Located Data Sources panel                 | ☐        |
| Viewed Results and Event Details           | ☐        |
| **Part 5: Core Tasks**               | ☐        |
| Located deleted files                      | ☐        |
| Recovered a deleted file                   | ☐        |
| Analyzed web history                       | ☐        |
| Performed keyword search                   | ☐        |
| Used timeline analysis                     | ☐        |
| **Part 6: Investigation**            | ☐        |
| Answered all 7 investigation questions     | ☐        |
| **Part 7: Advanced**                 | ☐        |
| Tagged evidence                            | ☐        |
| Generated a report                         | ☐        |

---

## Screenshot Checklist

| Screenshot              | Description                        |
| :---------------------- | :--------------------------------- |
| `autopsy_install.png` | Autopsy installation process       |
| `case_creation.png`   | Creating a new case                |
| `ingest_modules.png`  | Select ingest modules              |
| `deleted_files.png`   | Deleted files section with results |
| `web_history.png`     | Web history analysis               |
| `keyword_search.png`  | Keyword search results             |
| `recovered_file.png`  | Recovered file saved to disk       |
| `timeline.png`        | Timeline analysis view             |
| `report.png`          | Generated forensic report          |

---

## Troubleshooting Tips

| Issue                                 | Solution                                                       |
| :------------------------------------ | :------------------------------------------------------------- |
| **Autopsy won't start**         | Ensure Java is installed; run as administrator                 |
| **Ingest takes too long**       | Reduce selected modules; use a smaller image                   |
| **Can't find disk image**       | Verify file path; ensure image is not corrupted                |
| **Keyword search no results**   | Check case sensitivity; try different terms                    |
| **Deleted files not appearing** | Ensure Deleted File Recovery module was selected during ingest |
| **Web history empty**           | Image may not contain browser data; try different image        |

---

## Key Takeaways

| Concept                         | Description                                              |
| :------------------------------ | :------------------------------------------------------- |
| **Autopsy**               | Open-source digital forensics platform                   |
| **Dead Analysis**         | Examining a powered-off system's disk image              |
| **The Sleuth Kit (TSK)**  | Command-line forensics tools underlying Autopsy          |
| **Ingest Modules**        | Processing modules that extract different artifact types |
| **Deleted File Recovery** | Finding files no longer visible in the file system       |
| **Timeline Analysis**     | Chronological reconstruction of system events            |
| **Keyword Search**        | Finding specific text across all files                   |

---

## Test Your Knowledge

**Q1:** What is the difference between dead analysis and live analysis?

```
Your answer:
_________________________________________________________________________
```

**Q2:** What ingest module is required to recover deleted files?

```
Your answer:
_________________________________________________________________________
```

**Q3:** Where would you look in Autopsy to find a user's browsing history?

```
Your answer:
_________________________________________________________________________
```

**Q4:** What is The Sleuth Kit and how does it relate to Autopsy?

```
Your answer:
_________________________________________________________________________
```

**Q5:** Why is it important to verify the hash of a disk image before analysis?

```
Your answer:
_________________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                                                                     |
| -- | -------------------------------------------------------------------------------------------------------------------------- |
| 1  | Dead analysis examines a powered-off system's disk image; live analysis examines a running system                          |
| 2  | Deleted File Recovery / Data Carving module                                                                                |
| 3  | Analysis section → Web History (or Data Artifacts → Web History)                                                         |
| 4  | The Sleuth Kit (TSK) is the command-line forensics toolkit; Autopsy is the GUI front-end for TSK                           |
| 5  | Hash verification ensures the disk image is an exact, unaltered copy of the original evidence, preserving chain of custody |

---

## Summary

In this lab, you have:

| Activity                                            | Completed |
| :-------------------------------------------------- | :-------- |
| Installed Autopsy on your system                    | ☐        |
| Created a forensic case for CloudNine Marketing     | ☐        |
| Imported and processed a disk image                 | ☐        |
| Located and recovered deleted files                 | ☐        |
| Analyzed web history and performed keyword searches | ☐        |
| Used timeline analysis to reconstruct events        | ☐        |
| Answered investigation questions                    | ☐        |
| Generated a forensic report                         | ☐        |

These skills are essential for:

- Digital forensic investigators
- Incident response team members
- Corporate security teams
- HR investigators handling employee misconduct cases

---

## Congratulations!

You have successfully completed the **Digital Forensics with Autopsy** lab. You now know how to investigate potential data theft and insider threats using industry-standard forensic tools.

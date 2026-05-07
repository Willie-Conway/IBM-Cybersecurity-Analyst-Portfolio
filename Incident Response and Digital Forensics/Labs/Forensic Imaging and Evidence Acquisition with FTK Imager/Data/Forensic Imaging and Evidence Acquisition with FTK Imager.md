
![alt text](<../Screenshots/FTK_Imager.png>)

# Hands-on Lab: Forensic Imaging and Evidence Acquisition with FTK Imager

**Estimated time:** 60-90 minutes

---

## Project Scenario

Imagine you're a **Digital Forensic Investigator** at **Horizon Financial Services**, a regional bank with over 500,000 customers.

This morning, a suspicious transaction alert was triggered from a terminal in the wealth management division. A junior analyst, Michael Chen, downloaded an encrypted client portfolio containing high-net-worth customer data just before resigning last week. When contacted, Michael claimed he was "just backing up personal files." But HR confirmed he never used a personal USB drive on company equipment before.

The terminal has been seized and powered off. Before sending it to your lab for full forensic imaging, you need to:

1. **Create a forensically sound image** of the USB drive Michael was seen using
2. **Verify the integrity** of that image with cryptographic hashes
3. **Preview the evidence** to determine if client data was actually exfiltrated

The legal team needs an answer within 24 hours. If data was stolen, they must notify affected clients. If not, they can close this investigation quickly.

> **Why FTK Imager?** FTK Imager is the industry-standard free tool for forensic imaging and evidence preview . It creates bit-for-bit copies of storage devices without altering the original evidence—critical for chain of custody .

---

## Introduction

In this lab, you will become familiar with **FTK Imager**, a free data preview and imaging tool used to acquire electronic evidence in a forensically sound manner . FTK Imager allows investigators to create forensic images of hard drives, USB devices, memory cards, and CDs/DVDs without making changes to the original evidence .

Unlike Volatility (memory forensics), KAPE (triage collection), or Autopsy (disk forensics analysis), FTK Imager specializes in **forensic acquisition**—the critical first step of creating a verified, admissible copy of digital evidence .

### Why FTK Imager Matters for Incident Response

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    THE FORENSIC IMAGING IMPERATIVE                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Original Evidence                  Forensic Image                          │
│   ┌─────────────────────┐            ┌─────────────────────┐                │
│   │ USB Drive (suspect)  │            │ .E01 or .DD file    │                │
│   │ • Evidence can be    │    ──►     │ • Bit-for-bit copy   │                │
│   │   modified/tampered  │            │ • Cryptographically  │                │
│   │ • Chain of custody   │            │   verified           │                │
│   │   risk if examined   │            │ • Safe to analyze    │                │
│   │   directly           │            │ • Legally admissible │                │
│   └─────────────────────┘            └─────────────────────┘                │
│                                                                              │
│   Key Insight: You NEVER work on the original evidence. FTK Imager creates  │
│   a verifiable copy that preserves the original's forensic integrity.       │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

After completing this exercise, you will be able to:

| # | Objective                                                               |
| - | ----------------------------------------------------------------------- |
| 1 | Download and install FTK Imager on a Windows analysis workstation       |
| 2 | Navigate the FTK Imager interface and understand its core components    |
| 3 | Create a physical forensic image of a USB drive or other storage device |
| 4 | Create a logical forensic image of specific files and folders           |
| 5 | Verify image integrity using MD5 and SHA1 hash values                   |
| 6 | Mount and preview forensic images to examine evidence                   |
| 7 | Capture volatile memory (RAM) from a live system                        |

---

## Prerequisites

You must have:

| Requirement                      | Status | Notes                                  |
| :------------------------------- | :----- | :------------------------------------- |
| **Windows 10/11 computer** | ☐     | FTK Imager runs only on Windows        |
| **5GB free disk space**    | ☐     | For installation and test images       |
| **Local admin rights**     | ☐     | Required for installation              |
| **USB drive (any size)**   | ☐     | 1GB or larger - for imaging practice   |
| **Test files on USB**      | ☐     | Create sample documents before the lab |

---

## What is FTK Imager? Understanding the Tool

FTK Imager is a Windows-based forensic tool from AccessData (now Exterro) that serves two primary purposes :

### Core Capabilities

| Capability                  | Description                                   | IR Use Case                               |
| :-------------------------- | :-------------------------------------------- | :---------------------------------------- |
| **Forensic Imaging**  | Creates bit-for-bit copies of storage devices | Preserve evidence without modification    |
| **Evidence Preview**  | Browse contents of drives and images          | Quick triage before full analysis         |
| **Image Mounting**    | Mount images as read-only drives              | Analyze using other tools                 |
| **Memory Capture**    | Dump RAM from live systems                    | Capture volatile evidence before shutdown |
| **Hash Verification** | Generate/verify MD5 and SHA1 hashes           | Prove evidence integrity                  |

> **Note:** FTK Imager creates **forensic images** (bit-for-bit copies), not just file backups. This includes deleted files, unallocated space, and file system metadata that normal copy operations miss .

### Physical vs. Logical Imaging

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    PHYSICAL vs LOGICAL IMAGING                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   PHYSICAL IMAGE                         LOGICAL IMAGE                       │
│   ┌─────────────────────────┐            ┌─────────────────────────┐         │
│   │ Entire drive:            │            │ Specific files/folders:  │         │
│   │ ┌─────────────────────┐ │            │ ┌─────────────────────┐ │         │
│   │ │ Partition Table     │ │            │ │ C:\Users\john\      │ │         │
│   │ ├─────────────────────┤ │            │ │   Documents\*       │ │         │
│   │ │ C:\ (Active files)  │ │            │ └─────────────────────┘ │         │
│   │ ├─────────────────────┤ │            │                         │         │
│   │ │ Unallocated space   │ │            │ Does NOT capture:       │         │
│   │ ├─────────────────────┤ │            │ • Deleted files         │         │
│   │ │ Deleted files       │ │            │ • Unallocated space     │         │
│   │ └─────────────────────┘ │            │ • File system metadata  │         │
│   └─────────────────────────┘            └─────────────────────────┘         │
│                                                                              │
│   Best for: Complete investigation      Best for: Targeted collection       │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Part 1: Installing FTK Imager

### Step 1: Download FTK Imager

1. Navigate to the official Exterro download page:

   ```
   https://www.exterro.com/ftk-imager
   ```
2. OR search for "FTK Imager download" from trusted sources
3. Look for the file: `FTK Imager <version>.exe`

> **Note:** FTK Imager is **free** for forensic and educational use .

### Step 2: Install the Software

1. Run the downloaded installer as Administrator
2. Accept the license agreement
3. Choose installation directory (default: `C:\Program Files\AccessData\FTK Imager\`)
4. Complete the installation wizard
5. **Launch FTK Imager** from the desktop shortcut or Start Menu

![FTK Imager Installation]

*[Screenshot: FTK Imager installer welcome screen]*

### Step 3: Verify Installation

You should see the FTK Imager main window:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    FTK IMAGER MAIN INTERFACE                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│  File  View  Tools  Help                                                     │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │ Evidence Tree (Left Pane)      │  File List (Top Right)            │    │
│  │                                │                                   │    │
│  │ (Empty - no evidence loaded)   │ (Empty - no selection)            │    │
│  │                                │                                   │    │
│  │                                │                                   │    │
│  ├────────────────────────────────┼───────────────────────────────────┤    │
│  │ Properties (Bottom Left)       │  View Pane (Bottom Right)         │    │
│  │                                │                                   │    │
│  │ No item selected               │ File content preview              │    │
│  │                                │                                   │    │
│  └────────────────────────────────┴───────────────────────────────────┘    │
│                                                                              │
│  Status: Ready                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Understanding the Interface Panels

| Panel                   | Location     | Function                                       |
| :---------------------- | :----------- | :--------------------------------------------- |
| **Evidence Tree** | Top-Left     | Displays evidence items in hierarchical format |
| **File List**     | Top-Right    | Shows files/folders selected in Evidence Tree  |
| **Properties**    | Bottom-Left  | Shows metadata about selected item             |
| **View Pane**     | Bottom-Right | Displays contents of selected files            |

---

## Part 2: Preparing Your Lab Environment

### Step 1: Create a Test USB Drive

For this lab, you need a USB drive to image. **Do NOT use a drive with real evidence**:

1. Insert a USB drive (any size - 1GB or larger)
2. Create sample files on the drive:

```
USB Drive (E:\) 
├── sample_document.docx (with text: "Confidential client data")
├── financial_report.xlsx
├── employee_list.csv
├── vacation_photo.jpg
└── deleted_folder\
    └── credentials.txt (then delete this folder)
```

3. After creating files, **delete some** to practice recovery (though FTK Imager images will capture them)

### Step 2: Prepare Working Directories

Create folders for your lab:

```powershell
mkdir C:\Forensics_Lab
mkdir C:\Forensics_Lab\Images
mkdir C:\Forensics_Lab\Reports
mkdir C:\Forensics_Lab\Logs
```

---

## Part 3: Creating a Forensic Image

### Step 1: Launch the Imaging Wizard

1. In FTK Imager, click **File** → **Create Disk Image** (or click the disk icon in toolbar)
2. The "Create Image" wizard opens

![Create Image Wizard]

*[Screenshot: Create Image wizard showing source type selection]*

### Step 2: Select Source Type

Select the source you want to image:

| Option                         | Description                          | When to Use                   |
| :----------------------------- | :----------------------------------- | :---------------------------- |
| **Physical Drive**       | Entire physical disk                 | Complete forensic examination |
| **Logical Drive**        | Single partition (e.g., E:\)         | Targeted collection           |
| **Image File**           | Convert existing image to new format | Format conversion             |
| **Contents of a Folder** | Specific files/folders               | Logical evidence collection   |

**For this lab:** Select **Logical Drive** (safer for learning, faster imaging)

**For real investigations:** Select **Physical Drive** for complete preservation

### Step 3: Select Your USB Drive

1. From the drop-down menu, select your USB drive (look for size matching your drive)
2. You can identify it by:

   - Drive letter (e.g., E:\)
   - Size (matches your USB capacity)
   - File system (FAT32, NTFS, exFAT)
3. Click **Finish**

![Select Source Drive]

*[Screenshot: Selecting the USB drive from the source list]*

### Step 4: Add Image Destination

The "Create Image" window appears:

1. Click **Add** to configure image destination
2. Select **Image Type**:

| Image Type             | Description                   | Best For                     |
| :--------------------- | :---------------------------- | :--------------------------- |
| **Raw (dd)**     | Simple, widely compatible     | Cross-platform compatibility |
| **E01 (Encase)** | Compressed, includes metadata | Standard forensic format     |
| **AFF**          | Advanced Forensic Format      | Open-source tools            |

**For this lab:** Select **Raw (dd)** or **E01** (E01 recommended for practice)

3. Click **Next**

### Step 5: Fill Evidence Information

Complete the evidence metadata :

| Field                     | Value (Example)                                          | Purpose                         |
| :------------------------ | :------------------------------------------------------- | :------------------------------ |
| **Case Number**     | `HFS-2025-042`                                         | Your case tracking ID           |
| **Evidence Number** | `USB-001`                                              | Unique identifier for this item |
| **Description**     | `Michael Chen's USB drive - 16GB SanDisk`              | Physical description            |
| **Examiner Name**   | `Your Name`                                            | Who created the image           |
| **Notes**           | `Seized from wealth management department, 2025-04-07` | Context information             |

**For real investigations:** These fields become part of the evidence chain of custody .

![Evidence Information]

*[Screenshot: Evidence information entry screen with sample data]*

### Step 6: Set Image Destination

1. **Image Destination Folder:** Browse to `C:\Forensics_Lab\Images\`
2. **Image Filename:** Enter `USB_Michael_Chen` (no extension needed)
3. **Image Fragment Size:** Leave as `0` (no splitting)
4. **Compression:** Leave as `0` or select `Fast` for E01
5. Click **Finish**

### Step 7: Start the Imaging Process

1. **Verify "Verify images after they are created" is CHECKED**

   > **Critical:** Hash verification ensures your image is an exact match to the original. Without this, the evidence may be inadmissible .
   >
2. Click **Start**

![Imaging Progress]

*[Screenshot: Imaging progress bar showing completion percentage]*

### Step 8: Monitor Progress

The imaging process may take 2-10 minutes depending on:

- Drive size
- Drive speed (USB 2.0 vs 3.0)
- Data amount

### Step 9: Verify Image Completion

When complete, FTK Imager displays:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    DRIVE/IMAGE VERIFY RESULTS                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Original MD5:     a1b2c3d4e5f6789012345678901234567                       │
│   Verified MD5:     a1b2c3d4e5f6789012345678901234567                       │
│                                                                              │
│   Original SHA1:    1234567890abcdef1234567890abcdef12345678                 │
│   Verified SHA1:    1234567890abcdef1234567890abcdef12345678                 │
│                                                                              │
│   Result: MATCH ✓                                                            │
│                                                                              │
│   [The image file(s) are identical to the original]                          │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

> **If hashes don't match:** DO NOT use the image. Something went wrong. Re-image the source .

---

## Part 4: Creating a Logical Image (Files and Folders)

Logical imaging captures specific files and folders instead of an entire drive .

### Step 1: Start Logical Imaging

1. **File** → **Create Disk Image**
2. Select **Contents of a Folder**
3. Click **Next**

### Step 2: Select Folders to Image

1. Browse to and select folders (e.g., `C:\Users\[YourName]\Documents\`)
2. You can select multiple folders
3. Click **Next**

### Step 3: Configure Destination (Same as physical imaging)

1. Add destination
2. Set image type (Raw or E01)
3. Fill evidence information
4. Choose destination folder
5. Start imaging

### Logical Image Use Cases

| Scenario              | Why Logical Imaging                                |
| :-------------------- | :------------------------------------------------- |
| Targeted collection   | HR says: "Get all files from this specific folder" |
| Cloud data            | Download specific folders from cloud storage       |
| Time constraints      | Only need active files, not unallocated space      |
| Partial investigation | Initial triage before full imaging                 |

---

## Part 5: Previewing Evidence

### Step 1: Add Evidence Item

1. **File** → **Add Evidence Item**
2. Select source type:

| Option                         | Description                                         |
| :----------------------------- | :-------------------------------------------------- |
| **Logical Drive**        | Live drive (C:\, D:\, etc.)                         |
| **Image File**           | Previously created forensic image (.E01, .dd, .raw) |
| **Physical Drive**       | Entire physical disk                                |
| **Contents of a Folder** | Directory on disk                                   |

3. Click **Next**
4. Browse to your image file (`C:\Forensics_Lab\Images\USB_Michael_Chen.E01`)
5. Click **Finish**

### Step 2: Browse the Evidence Tree

The Evidence Tree now shows your image contents:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    EVIDENCE TREE (EXPANDED)                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ▼ USB_Michael_Chen (E01)                                                  │
│       ▼ [root]                                                              │
│           ├── sample_document.docx                                           │
│           ├── financial_report.xlsx                                          │
│           ├── employee_list.csv                                              │
│           ├── vacation_photo.jpg                                             │
│           ├── [Orphan Files] (Deleted files area)  ← Evidence!              │
│           └── [Unallocated Space]                                            │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Step 3: Preview File Contents

1. Select any file in the Evidence Tree
2. The File List pane shows all items
3. The View Pane (bottom-right) displays the file's contents

![File Preview]

*[Screenshot: Preview of a text file showing its contents in the View Pane]*

### Step 4: Export a File

1. Right-click any file
2. Select **Export Files**
3. Choose destination folder
4. Click **OK**

> **Reminder:** You're previewing the image, not the original evidence. This is forensically sound.

---

## Part 6: Capturing Memory (RAM)

### Why Capture Memory?

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    WHY CAPTURE RAM?                                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   RAM contains evidence that disappears when powered off:                   │
│   • Running processes (including malware)                                   │
│   • Network connections                                                      │
│   • Decrypted data (passwords, encryption keys)                             │
│   • Command history                                                          │
│   • Unencrypted chat messages                                                │
│                                                                              │
│   Volatility Rule: The moment you power off a system, volatile evidence     │
│   is lost forever. Capture memory FIRST before shutting down.               │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Step 1: Capture Memory

FTK Imager can capture RAM from the live system :

1. **File** → **Capture Memory**
2. Select destination folder: `C:\Forensics_Lab\Images\`
3. Enter filename: `HFS-2025-042_Memory_Dump`
4. Select options (for this lab, keep defaults)
5. Click **Capture**

![Memory Capture]

*[Screenshot: Memory capture dialog with destination selected]*

### Step 2: Capture Complete

FTK Imager creates two files:

- `.mem` or `.raw` (the actual memory dump)
- `.txt` (metadata including MD5 hash)

> **Best Practice:** In a real investigation, capture memory BEFORE performing any other actions on a live system .

---

## Part 7: Mounting a Forensic Image

Mounting allows you to browse an image as if it were a physical drive .

### Step 1: Mount the Image

1. **File** → **Image Mounting**
2. Click **Add** and browse to your image
3. Select mount options:

| Option                 | Selection               | Why                   |
| :--------------------- | :---------------------- | :-------------------- |
| **Mount Type**   | Logical                 | Standard browsing     |
| **Mount Method** | File System / Read Only | Prevents modification |
| **Drive Letter** | Auto-assign or manual   | Access point          |

4. Click **Mount**

### Step 2: Verify the Mount

The image now appears as a drive in Windows Explorer (e.g., `F:\`) .

You can use other forensic tools to analyze the mounted image.

### Step 3: Unmount When Done

When finished analyzing:

1. **File** → **Image Mounting**
2. Select the mounted image
3. Click **Unmount**

---

## Part 8: Generating Reports

### Step 1: Generate Hash Report

1. **File** → **Generate Hash Report**
2. Select hash algorithm: MD5 and SHA1
3. Select destination: `C:\Forensics_Lab\Reports\`
4. Click **Generate**

### Step 2: Export Directory Listing

You can export a full file listing :

1. **File** → **Export Directory Listing**
2. Choose destination
3. Save as CSV or text file

### Sample Hash Report Output

```
FTK Imager Hash Report
========================
Image File: USB_Michael_Chen.E01
Case Number: HFS-2025-042

File Path                              MD5 Hash
------------------------------------------------------------------------
/USB_Michael_Chen/sample_document.docx  5d41402abc4b2a76b9719d911017c592
/USB_Michael_Chen/financial_report.xlsx f5a7924e621e84c9480a9fb6f2d2b42f
/USB_Michael_Chen/employee_list.csv     f2c7f31e42d134c8b5d0c3fae7c54b1e
```

---

## Part 9: Investigation Scenario

Now apply your skills to the Horizon Financial Services case.

### The Situation

Michael Chen's USB drive has been imaged. You need to determine:

1. **Was client data copied to the drive?**
2. **When was the data copied?** (file timestamps)
3. **What other suspicious files exist?**
4. **Were there attempts to delete evidence?**

### Step 1: Open Your USB Image

```
File → Add Evidence Item → Image File → Browse to your .E01 file
```

### Step 2: Search for Sensitive Terms

In FTK Imager, you can search within the Evidence Tree:

1. Right-click the evidence item
2. Select **Find**
3. Search for terms like:
   - `confidential`
   - `client`
   - `portfolio`
   - `SSN`
   - `account`
   - `password`

### Step 3: Check for Deleted Files

Navigate to **Orphan Files** (deleted files section) - look for recently deleted items.

### Step 4: Document Your Findings

Create an initial triage report:

| Question                                | Your Answer |
| --------------------------------------- | ----------- |
| What sensitive files were found?        |             |
| What are their creation/modified dates? |             |
| Are there deleted files of interest?    |             |
| Is there evidence of data exfiltration? |             |

### Step 5: Generate Hash Report

1. **File** → **Generate Hash Report**
2. Save as `HFS-2025-042_Hashes.txt`
3. These hashes will be used to verify evidence integrity

---

## Lab Completion Checklist

| Task                                      | Completed |
| :---------------------------------------- | :-------- |
| **Part 1: Installation**            | ☐        |
| FTK Imager downloaded and installed       | ☐        |
| FTK Imager launches without errors        | ☐        |
| Interface panels identified               | ☐        |
| **Part 2: Lab Setup**               | ☐        |
| Test USB drive prepared with sample files | ☐        |
| Working directories created               | ☐        |
| **Part 3: Forensic Imaging**        | ☐        |
| Physical or logical image created         | ☐        |
| Evidence information filled accurately    | ☐        |
| Hash verification confirmed "Match"       | ☐        |
| Image saved to working directory          | ☐        |
| **Part 4: Logical Imaging**         | ☐        |
| Logical image created                     | ☐        |
| **Part 5: Evidence Preview**        | ☐        |
| Image added as evidence item              | ☐        |
| Evidence tree browsed                     | ☐        |
| File previewed in View Pane               | ☐        |
| File exported from image                  | ☐        |
| **Part 6: Memory Capture**          | ☐        |
| Memory captured successfully              | ☐        |
| Memory dump file created                  | ☐        |
| **Part 7: Image Mounting**          | ☐        |
| Image mounted as read-only drive          | ☐        |
| Mounted drive accessed in Explorer        | ☐        |
| Image unmounted                           | ☐        |
| **Part 8: Reporting**               | ☐        |
| Hash report generated                     | ☐        |
| Directory listing exported                | ☐        |
| **Part 9: Scenario**                | ☐        |
| Sensitive keywords searched               | ☐        |
| Deleted files examined                    | ☐        |
| Triage findings documented                | ☐        |

---

## Screenshot Checklist

| Screenshot                  | Description                          |
| :-------------------------- | :----------------------------------- |
| `ftkimager_main.png`      | Main FTK Imager interface            |
| `create_image_wizard.png` | Create Image wizard source selection |
| `evidence_info.png`       | Evidence information entry           |
| `imaging_progress.png`    | Imaging progress bar                 |
| `hash_verification.png`   | Hash verification results (Match)    |
| `evidence_tree.png`       | Evidence tree showing image contents |
| `file_preview.png`        | File preview in View Pane            |
| `memory_capture.png`      | Memory capture dialog                |
| `mounting_config.png`     | Image mounting configuration         |
| `hash_report.png`         | Generated hash report                |

---

## Troubleshooting Tips

| Issue                                        | Solution                                         |
| :------------------------------------------- | :----------------------------------------------- |
| **FTK Imager won't install**           | Run as Administrator; ensure Windows is updated  |
| **USB drive not detected**             | Try different USB port; check Disk Management    |
| **Image creation fails**               | Check destination folder has space; run as Admin |
| **Hash verification shows "No Match"** | Source drive changed during imaging; re-image    |
| **Can't mount image**                  | Ensure "File System / Read Only" is selected     |
| **Memory capture grayed out**          | Need to run FTK Imager as Administrator          |
| **Large image file**                   | Use E01 format with compression                  |

---

## Best Practices for Forensic Imaging

| Practice                                                 | Why It Matters                           |
| :------------------------------------------------------- | :--------------------------------------- |
| **Always verify hashes**                           | Proves image matches original            |
| **Work from images, not originals**                | Preserves chain of custody               |
| **Document everything**                            | Evidence handling must be provable       |
| **Use write-blockers**                             | Prevents accidental modification         |
| **Capture memory first**                           | Volatile evidence disappears on shutdown |
| **Never image a live system** without proper tools | Can alter evidence                       |
| **Store images securely**                          | Evidence must be protected               |

---

## Key Takeaways

| Concept                     | Description                                                      |
| :-------------------------- | :--------------------------------------------------------------- |
| **FTK Imager**        | Free forensic imaging and preview tool from AccessData/Exterro   |
| **Forensic Image**    | Bit-for-bit copy including unallocated space and deleted files   |
| **Hash Verification** | Cryptographic proof (MD5/SHA1) that image matches original       |
| **Physical Image**    | Complete disk capture including partitions and unallocated space |
| **Logical Image**     | Selected files/folders only                                      |
| **E01 Format**        | Compressed Encase format with embedded metadata                  |
| **Write-Blocker**     | Hardware preventing writes to evidence drives                    |

---

## Real-World Application: The Forensic Workflow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    FORENSIC WORKFLOW WITH FTK IMAGER                         │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   1. SEIZE           2. IMAGE            3. VERIFY          4. ANALYZE      │
│   ┌────────┐        ┌────────┐          ┌────────┐         ┌────────┐       │
│   │ Power  │        │ FTK    │          │ Hash   │         │ Autopsy│       │
│   │ off    │ ────►  │ Imager │ ────►    │ Match? │ ────►   │ Volatility│    │
│   │ system │        │        │          │   ✓    │         │ KAPE   │       │
│   └────────┘        └────────┘          └────────┘         └────────┘       │
│       │                  │                   │                  │           │
│       ▼                  ▼                   ▼                  ▼           │
│   Forensically      Creates .E01        Cryptographic       Deep dive       │
│   sound seizure      forensic image      integrity          analysis        │
│                                                                              │
│   FTK Imager is the GATEWAY tool - it gets evidence into a safe,           │
│   analyzable format. All other tools work from the IMAGE.                   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Test Your Knowledge

**Q1:** What is the difference between a physical image and a logical image?

```
Your answer:
_________________________________________________________________________
```

**Q2:** Why is hash verification critical in forensic imaging?

```
Your answer:
_________________________________________________________________________
```

**Q3:** What evidence formats does FTK Imager support for image creation?

```
Your answer:
_________________________________________________________________________
```

**Q4:** Why should you capture memory before shutting down a live system?

```
Your answer:
_________________________________________________________________________
```

**Q5:** What is the purpose of a write-blocker?

```
Your answer:
_________________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                                                                                      |
| -- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| 1  | Physical image captures the entire disk (partitions, unallocated space, deleted files). Logical image captures only specified files/folders |
| 2  | Hash verification proves the forensic image is an exact, unaltered copy of the original evidence, making it admissible in court             |
| 3  | Raw (dd), E01 (Encase), and AFF                                                                                                             |
| 4  | RAM contains volatile evidence (running processes, network connections, decrypted data) that is lost immediately when power is removed      |
| 5  | A write-blocker prevents any writes to the evidence drive, ensuring the original evidence cannot be accidentally modified                   |

---

## Summary

In this lab, you have:

| Activity                                          | Completed |
| :------------------------------------------------ | :-------- |
| Installed FTK Imager on a Windows workstation     | ☐        |
| Created verified forensic images of a USB drive   | ☐        |
| Previewed evidence without altering original data | ☐        |
| Captured volatile memory from a live system       | ☐        |
| Mounted forensic images for analysis              | ☐        |
| Generated hash reports and directory listings     | ☐        |

These skills are essential for:

- Digital forensic investigators acquiring evidence
- Incident responders preserving volatile data
- Legal teams preparing admissible evidence
- Security professionals building forensic readiness

---

## Additional Resources

| Resource                            | URL                                     |
| :---------------------------------- | :-------------------------------------- |
| **FTK Imager Download**       | https://www.exterro.com/ftk-imager      |
| **Exterro Documentation**     | https://kb.digital-detective.net/       |
| **MIT FTK Imager Guide**      | https://wikis.mit.edu/.../FTKImager     |
| **Smithsonian Imaging Guide** | https://confluence.si.edu/              |
| **AboutDFIR FTK Imager**      | https://aboutdfir.com/tools/ftk-imager/ |

---

## Congratulations!

You have successfully completed the **Forensic Imaging and Evidence Acquisition with FTK Imager** lab. You now know how to:

- Install and configure FTK Imager
- Create verified physical and logical forensic images
- Preview evidence without altering original data
- Capture volatile memory from live systems
- Mount images for analysis with other tools
- Generate forensic reports and hash verification

These skills form the foundation of any digital forensic investigation. FTK Imager is often the very first tool used in the forensic workflow—the gateway that transforms raw storage devices into admissible, analyzable evidence.

> **Next Steps:** After completing this lab, use your forensic images with other tools you've learned: analyze them with Autopsy, hunt for IOCs with KAPE, or examine memory with Volatility. Each tool plays a specific role in the complete forensic investigation workflow.
>

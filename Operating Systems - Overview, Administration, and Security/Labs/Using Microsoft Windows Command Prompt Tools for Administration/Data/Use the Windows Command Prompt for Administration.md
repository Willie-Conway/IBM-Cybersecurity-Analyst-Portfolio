![alt text](<../Screenshots/Windows Defender.png>)

# Hands-on Lab: Use the Windows Command Prompt for Administration

**Estimated time needed:** 45 minutes

---

## About This Lab

In this lab we will use Microsoft Windows command prompt tools for various administrative tasks.

---

## Learning Objectives

In this hands-on lab, you will:

- Obtain system information using the command line
- Manage directories using the command line
- Perform system maintenance using the command line

---

## Important Information About Lab Instructions and Solutions

In case you try to use your physical keyboard in the lab environment, it might not produce any visible results. To avoid this issue, please use the **On-Screen Keyboard** (you can find it by searching for "On-Screen Keyboard" in the search bar at the bottom of your screen). If search functionality doesn't work, you can also click on the Windows icon, scroll down to find **Windows Ease of Access**, click on it, and then select **On-Screen Keyboard**.

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About the Lab Instructions and Solutions

Microsoft Windows operating system features can vary based on the Windows edition. If completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Exercise 1: Obtain System Information Using the Command Line

In this exercise we will obtain information about the system and network using command line tools.

### Step 1: Open Command Prompt

1. Type **Command Prompt** in the search bar at the bottom of your screen
2. Click on **Command Prompt** from the search results

![alt text](<../Screenshots/Search bar with - Command Prompt - typed and highlighted.png>)

### Step 2: Display the Computer Name

1. At the command prompt, type the following command:

```cmd
hostname
```

2. Press **Enter**
3. The command will display the name of your computer


![alt text](<../Screenshots/Command Prompt showing hostname command and result.png>)


**What this command does:** The `hostname` command displays the name of the current computer on the network. This is useful for identifying which system you're working on, especially when managing multiple computers remotely.

### Step 3: Display Basic Network Configuration

1. Type the following command:

```cmd
ipconfig
```

2. Press **Enter**
3. You will see several network identifications for the local system including:

   - **IPv4 Address** - The IP address of your computer
   - **Subnet Mask** - Defines the network segment
   - **Default Gateway** - The router that connects to other networks


![alt text](<../Screenshots/Command Prompt showing ipconfig results with IP address, subnet mask, and gateway highlighted.png>)

### Step 4: Display Detailed Network Information

1. Type the following command to see more detailed network information:

```cmd
ipconfig /all
```

2. Press **Enter**
3. This displays comprehensive network configuration including:

   - **Host Name** - Your computer's name
   - **DNS Servers** - Domain Name System servers in use
   - **DHCP Enabled** - Whether IP is assigned automatically
   - **Physical Address** - MAC address of network adapters
   - **Lease Obtained/Expires** - DHCP lease information



![alt text](<../Screenshots/Command Prompt showing ipconfig - all detailed results.png>)

**Key information in ipconfig /all:**

| Field                        | Description                              |
| :--------------------------- | :--------------------------------------- |
| **Host Name**          | Your computer's network name             |
| **Primary DNS Suffix** | Domain name (if joined to a domain)      |
| **Node Type**          | How name resolution is performed         |
| **IP Routing Enabled** | Whether the system acts as a router      |
| **WINS Proxy Enabled** | Whether WINS proxy is active             |
| **DNS Servers**        | IP addresses of DNS servers              |
| **Physical Address**   | MAC address (unique hardware identifier) |

### Step 5: Clear the Command Prompt Window

1. Type the following command to clear the screen:

```cmd
cls
```

2. Press **Enter**
3. The command prompt window will now be empty, with only the prompt visible at the top

![alt text](<../Screenshots/Command Prompt after cls command showing clean screen.png>)


**What this command does:** `cls` (clear screen) removes all previous commands and output from the window, giving you a fresh workspace.

### Step 6: Test Network Connectivity

1. Type the following command to test connectivity to a remote server:

```cmd
ping google.com
```

2. Press **Enter**
3. You will see results showing:

   - **Reply from** - Confirmation of successful connection
   - **Time** - Round-trip time in milliseconds
   - **TTL** - Time to Live (packet lifetime)

![Command Prompt showing ping results]

**Understanding ping results:**

| Result                                 | Meaning                                          |
| :------------------------------------- | :----------------------------------------------- |
| **Reply from...**                | The destination responded successfully           |
| **Request timed out**            | No response received (firewall or network issue) |
| **Destination host unreachable** | Network path doesn't exist                       |
| **Time=<1ms**                    | Very fast connection (local network)             |
| **Time=100ms+**                  | Slower connection (internet distance)            |

### Step 7: Trace Network Route

1. Type the following command to see the path packets take to reach a destination:

```cmd
tracert google.com
```

2. Press **Enter**
3. This shows each hop (router) along the path, with response times for each

![Command Prompt showing tracert results]

**What this command does:** `tracert` (trace route) shows every router your data passes through to reach the destination, helping identify where network delays or failures occur.

### Step 8: Display Network Statistics

1. Type the following command to show active network connections:

```cmd
netstat -a
```

2. Press **Enter**
3. This displays all active TCP and UDP connections, listening ports, and their states

![Command Prompt showing netstat -a results]

**Common netstat options:**

| Option | Description                                   |
| :----- | :-------------------------------------------- |
| `-a` | Display all connections and listening ports   |
| `-b` | Show the executable involved (requires admin) |
| `-n` | Display addresses and ports numerically       |
| `-o` | Show the process ID (PID) for each connection |

---

## Exercise 2: Manage Directories Using the Command Line

In this exercise, you will learn to navigate and manage directories (folders) using command line commands.

### Step 1: Clear the Screen and Display Current Directory

1. Clear the screen:

```cmd
cls
```

2. Display your current directory location:

```cmd
cd
```

3. Press **Enter**
4. This shows your current working directory (likely `C:\Users\YourUsername`)


![alt text](<../Screenshots/Command Prompt showing cd command result.png>)

**What this command does:** `cd` (change directory) without parameters displays the current directory path.

### Step 2: List Directory Contents

1. Type the following command to list files and folders:

```cmd
dir
```

2. Press **Enter**
3. This displays:

   - List of files and subdirectories
   - File sizes
   - Date and time of last modification
   - Number of files and free space


![alt text](<../Screenshots/Command Prompt showing dir command results.png>)

**Understanding dir output:**

| Symbol       | Meaning              |
| :----------- | :------------------- |
| `<DIR>`    | A directory (folder) |
| No `<DIR>` | A file               |
| `.`        | Current directory    |
| `..`       | Parent directory     |

### Step 3: Create a New Directory

1. Create a new directory called "LabFiles":

```cmd
mkdir LabFiles
```

2. Press **Enter**
3. No message appears if successful (this means it worked!)

**Alternative command:** You can also use `md LabFiles` (make directory)

### Step 4: Verify Directory Creation

1. List contents again to see your new directory:

```cmd
dir
```

2. Press **Enter**
3. You should now see `LabFiles` listed with `<DIR>` indicator



![alt text](<../Screenshots/Command Prompt showing dir with new LabFiles directory.png>)

### Step 5: Navigate to the New Directory

1. Change to the LabFiles directory:

```cmd
cd LabFiles
```

2. Press **Enter**
3. The prompt should change to show you're now in `C:\Users\YourUsername\LabFiles>`


![alt text](<../Screenshots/delete the newly created directory - type rmdir comedy.png>)

### Step 6: Create Nested Directories

1. Create multiple directories at once:

```cmd
mkdir Projects\Project1 Documents\Work
```

2. Press **Enter**
3. This creates:

   - A `Projects` folder with a `Project1` subfolder inside it
   - A `Documents` folder with a `Work` subfolder inside it

**What this command does:** The backslash (`\`) creates a directory structure in one command.

![alt text](<../Screenshots/To verify that the directory has been removed - type dir.png>)

### Step 7: Verify Nested Directories

1. List contents of LabFiles:

```cmd
dir
```

2. You should see `Projects` and `Documents` folders
3. Check the Project1 folder:

```cmd
dir Projects
```

4. You should see `Project1` listed inside

![alt text](<../Screenshots/return to the previous directory.png>)

### Step 8: Create a Directory with Spaces

1. Create a directory with a space in the name:

```cmd
mkdir "My Lab Files"
```

2. Press **Enter**

**Important:** Use quotes around directory names that contain spaces

### Step 9: Display Directory Tree Structure

1. Return to the parent directory:

```cmd
cd ..
```

2. Press **Enter**
3. Now display the entire directory structure:

```cmd
tree LabFiles
```

4. Press **Enter**
5. This shows a graphical tree of all subdirectories under LabFiles

![Command Prompt showing tree command results]

**What this command does:** `tree` displays a graphical representation of the folder structure.

### Step 10: Remove a Directory

1. First, navigate to LabFiles:

```cmd
cd LabFiles
```

2. Remove the "My Lab Files" directory:

```cmd
rmdir "My Lab Files"
```

3. Press **Enter**

**Note:** `rmdir` only removes empty directories. To remove a directory with contents, use `rmdir /s "directory name"`

### Step 11: Verify Removal

1. List contents to confirm removal:

```cmd
dir
```

2. "My Lab Files" should no longer appear

---

## Exercise 3: Perform System Maintenance Using the Command Line

In this exercise, you will use command-line tools for system maintenance tasks.

### Step 1: Check System File Integrity

1. Open Command Prompt as **Administrator** (important for this command):
   - Type **Command Prompt** in search
   - Right-click on **Command Prompt**
   - Select **Run as administrator**

![Right-click menu showing Run as administrator]

2. Run the System File Checker:

```cmd
sfc /scannow
```

3. Press **Enter**
4. This will scan all protected system files and replace corrupted versions


![alt text](<../Screenshots/Command Prompt running sfc - scannow.png>)

**What this command does:** `sfc /scannow` verifies the integrity of all protected system files and repairs them if necessary.

**Possible results:**

| Result                                                                         | Meaning                  |
| :----------------------------------------------------------------------------- | :----------------------- |
| Windows Resource Protection did not find any integrity violations              | System files are healthy |
| Windows Resource Protection found corrupt files and successfully repaired them | Corrupt files were fixed |
| Windows Resource Protection found corrupt files but was unable to fix some     | Manual repair needed     |

### Step 2: Check Disk for Errors

1. Check the C: drive for errors:

```cmd
chkdsk C:
```

2. Press **Enter**
3. This displays the disk status without making changes

![alt text](<../Screenshots/Command Prompt showing chkdsk results.png>)


**For a more thorough check with repair:**

```cmd
chkdsk C: /f
```

**Note:** The `/f` parameter fixes errors on the disk. If the drive is in use, you'll be prompted to schedule the check for next reboot.

### Step 3: View System Information

1. Display comprehensive system information:

```cmd
systeminfo
```

2. Press **Enter**
3. This displays detailed information including:

   - OS Name and Version
   - System Manufacturer
   - System Model
   - Processor(s)
   - BIOS Version
   - Total Physical Memory
   - Network Card(s)

![Command Prompt showing systeminfo results]

### Step 4: View Running Processes

1. Display all running processes:

```cmd
tasklist
```

2. Press **Enter**
3. This shows:

   - Process Name
   - Process ID (PID)
   - Session Name
   - Session Number
   - Memory Usage

![Command Prompt showing tasklist results]

### Step 5: Kill a Process (Optional - Use Carefully)

If you need to terminate a process, you can use:

```cmd
taskkill /PID [process_id] /F
```

Replace `[process_id]` with the actual PID from tasklist.

**Example:** `taskkill /PID 1234 /F`

**Warning:** Only terminate processes you understand. Terminating system processes can cause instability.

### Step 6: View Disk Usage

1. View disk space information:

```cmd
wmic logicaldisk get deviceid, volumename, size, freespace
```

2. Press **Enter**
3. This displays:

   - Drive letter
   - Volume name
   - Total size (in bytes)
   - Free space (in bytes)

![Command Prompt showing wmic disk information]

### Step 7: Create a Batch File (Simple Script)

1. Create a new text file:

```cmd
notepad system_check.bat
```

2. Press **Enter**
3. When Notepad opens, type:

```batch
@echo off
echo ========================================
echo     SYSTEM INFORMATION REPORT
echo ========================================
echo.
echo Computer Name: %computername%
echo.
echo Date: %date%
echo Time: %time%
echo.
echo ========================================
echo     DISK SPACE INFORMATION
echo ========================================
wmic logicaldisk get deviceid, volumename, size, freespace
echo.
echo ========================================
echo     NETWORK CONFIGURATION
echo ========================================
ipconfig | findstr /i "IPv4 Address"
echo.
pause
```

4. Save the file (Ctrl+S) and close Notepad
5. Run the batch file:

```cmd
system_check.bat
```

6. Press **Enter**

![Batch file running]

### Step 8: Schedule a Task Using Command Line

1. Create a scheduled task to run a system check daily:

```cmd
schtasks /create /tn "SystemCheck" /tr "system_check.bat" /sc daily /st 09:00
```

2. Press **Enter**
3. This creates a scheduled task named "SystemCheck" that runs daily at 9:00 AM

**Understanding the command:**

| Parameter   | Meaning                             |
| :---------- | :---------------------------------- |
| `/create` | Create a new task                   |
| `/tn`     | Task name                           |
| `/tr`     | Task to run                         |
| `/sc`     | Schedule type (daily, weekly, etc.) |
| `/st`     | Start time                          |

### Step 9: View Scheduled Tasks

1. List all scheduled tasks:

```cmd
schtasks /query
```

2. Press **Enter**
3. This shows all scheduled tasks on the system

### Step 10: Delete the Scheduled Task (Cleanup)

1. Remove the task we created:

```cmd
schtasks /delete /tn "SystemCheck" /f
```

2. Press **Enter**
3. The `/f` parameter forces deletion without confirmation

---

## Exercise 4: Advanced Command Line Techniques

In this exercise, you will learn advanced command-line techniques for efficient administration.

### Step 1: Command Redirection

1. Save command output to a file:

```cmd
ipconfig /all > network_info.txt
```

2. Press **Enter**
3. This creates a file called `network_info.txt` containing the ipconfig output
4. View the file:

```cmd
type network_info.txt
```

### Step 2: Append to a File

1. Add more information to the same file:

```cmd
systeminfo >> network_info.txt
```

2. Press **Enter**
3. The `>>` operator appends output to the file instead of overwriting

### Step 3: Using Pipes

1. Pipe output to find specific information:

```cmd
ipconfig | findstr "IPv4"
```

2. Press **Enter**
3. This shows only lines containing "IPv4" (your IP addresses)

### Step 4: Command History

1. View command history:

```cmd
doskey /history
```

2. Press **Enter**
3. This shows all commands you've typed in the current session

### Step 5: Create a Directory and File Structure for Practice

1. Create a complete lab practice structure:

```cmd
cd %userprofile%
mkdir LabPractice
cd LabPractice
mkdir Documents Spreadsheets Presentations Archives
echo This is a test document > Documents\test.txt
echo Project notes > Documents\notes.txt
echo Q1 Sales Data > Spreadsheets\sales.csv
echo Budget 2026 > Spreadsheets\budget.xlsx
echo Board Meeting > Presentations\meeting.pptx
echo Strategy Overview > Presentations\strategy.pptx
echo Archived files > Archives\old_data.txt
```

### Step 6: Search for Files

1. Search for all .txt files:

```cmd
dir *.txt /s
```

2. Press **Enter**
3. The `/s` parameter searches subdirectories

### Step 7: Copy Files

1. Copy all text files to a backup folder:

```cmd
mkdir Backup
copy *.txt Backup\
```

2. Press **Enter**

### Step 8: Move Files

1. Move files between directories:

```cmd
move Documents\notes.txt Presentations\
```

2. Press **Enter**

### Step 9: Delete Files

1. Delete specific files:

```cmd
del Presentations\notes.txt
```

2. Press **Enter**

### Step 10: Remove Directory Structure (Cleanup)

1. Navigate up and remove the entire LabPractice structure:

```cmd
cd ..
rmdir /s LabPractice
```

2. Press **Enter**
3. Type `Y` when prompted to confirm

---

## Exercise 5: Command Reference Guide Creation

In this exercise, you will create your own command reference guide.

### Step 1: Create a Reference File

```cmd
notepad command_reference.txt
```

### Step 2: Document Commands You've Learned

Type the following in Notepad:

```
WINDOWS COMMAND PROMPT REFERENCE GUIDE
=======================================

SYSTEM INFORMATION COMMANDS
---------------------------
hostname                 - Display computer name
ipconfig                 - Show basic network configuration
ipconfig /all           - Show detailed network configuration
systeminfo              - Display comprehensive system information
tasklist                - List running processes
wmic logicaldisk        - Show disk information

NETWORK COMMANDS
----------------
ping [host]             - Test connectivity to host
tracert [host]          - Trace route to host
netstat -a              - Show all network connections
nslookup [domain]       - Query DNS information

DIRECTORY COMMANDS
------------------
cd                      - Show current directory
cd [folder]             - Change to folder
cd ..                   - Go up one level
dir                     - List directory contents
mkdir [name]            - Create new directory
rmdir [name]            - Remove empty directory
rmdir /s [name]         - Remove directory with contents
tree                    - Show directory structure

FILE COMMANDS
-------------
type [file]             - Display file contents
copy [source] [dest]    - Copy files
move [source] [dest]    - Move files
del [file]              - Delete file
ren [old] [new]         - Rename file

MAINTENANCE COMMANDS
--------------------
sfc /scannow            - Check system file integrity
chkdsk C:               - Check disk for errors
chkdsk C: /f            - Check and fix disk errors
schtasks /query         - List scheduled tasks

BATCH FILE TECHNIQUES
---------------------
@echo off               - Hide commands in batch file
echo [text]             - Display text
%computername%          - System variable for computer name
%date%                  - Current date
%time%                  - Current time
> [file]                - Redirect output to file (overwrite)
>> [file]               - Append output to file
| [command]             - Pipe output to another command

Created by: [Your Name]
Date: [Current Date]
```

### Step 3: Save and Close

1. Press **Ctrl+S** to save
2. Close Notepad

---

## Summary

In this hands-on lab, you have:

| Activity                                                        | Completed |
| :-------------------------------------------------------------- | :-------- |
| Opened Command Prompt                                           | ✓        |
| Used `hostname` to display computer name                      | ✓        |
| Used `ipconfig` and `ipconfig /all` for network information | ✓        |
| Used `cls` to clear the screen                                | ✓        |
| Used `ping` to test network connectivity                      | ✓        |
| Used `tracert` to trace network routes                        | ✓        |
| Used `netstat` to view network connections                    | ✓        |
| Used `cd` to navigate directories                             | ✓        |
| Used `dir` to list directory contents                         | ✓        |
| Used `mkdir` to create directories                            | ✓        |
| Created nested directories with a single command                | ✓        |
| Used `rmdir` to remove directories                            | ✓        |
| Used `tree` to display directory structure                    | ✓        |
| Used `sfc /scannow` for system file checking                  | ✓        |
| Used `chkdsk` for disk checking                               | ✓        |
| Used `systeminfo` for system details                          | ✓        |
| Used `tasklist` to view processes                             | ✓        |
| Used `wmic` for disk space information                        | ✓        |
| Created and ran a batch file                                    | ✓        |
| Used `schtasks` to schedule and manage tasks                  | ✓        |
| Used redirection (`>`, `>>`) and pipes (`\|`)              | ✓        |
| Created a personal command reference guide                      | ✓        |

---

<video controls src="Use the Windows Command Prompt for Administration.mp4" title="Use the Windows Command Prompt for Administration"></video>


## Key Takeaways

### Essential Commands by Category

| Category                  | Key Commands                                               |
| :------------------------ | :--------------------------------------------------------- |
| **Navigation**      | `cd`, `dir`, `tree`                                  |
| **File Management** | `mkdir`, `rmdir`, `copy`, `move`, `del`, `ren` |
| **System Info**     | `hostname`, `systeminfo`, `tasklist`                 |
| **Network**         | `ipconfig`, `ping`, `tracert`, `netstat`           |
| **Maintenance**     | `sfc`, `chkdsk`, `schtasks`                          |

### Best Practices

1. **Run as Administrator** when making system changes
2. **Use quotes** around paths with spaces
3. **Test commands** with non-destructive parameters first
4. **Document complex commands** for future reference
5. **Use redirection** to save output for analysis
6. **Create batch files** for repetitive tasks

### Common Pitfalls to Avoid

- Forgetting to use quotes with spaces in filenames
- Using `rmdir` on non-empty directories without `/s`
- Making system changes without administrator privileges
- Not understanding what a command does before running it
- Forgetting that lab sessions are temporary

---

## Additional Practice Ideas

1. Create a batch file that backs up important documents
2. Use `findstr` to search for specific text in multiple files
3. Create a script that logs system information daily
4. Use `schtasks` to automate regular maintenance
5. Practice using `for` loops in batch files for repetitive tasks

---

## Troubleshooting Tips

| Issue                                 | Solution                                            |
| :------------------------------------ | :-------------------------------------------------- |
| **'command' is not recognized** | Command doesn't exist or path issue; check spelling |
| **Access denied**               | Run Command Prompt as Administrator                 |
| **File in use**                 | Close the program using the file                    |
| **Path not found**              | Check for typos; use quotes for spaces              |
| **Directory not empty**         | Use `rmdir /s` for directories with contents      |

---

## Congratulations!

You have successfully completed the **Use the Windows Command Prompt for Administration** lab. You now have practical experience with:

- Gathering system and network information
- Navigating and managing the file system
- Performing system maintenance tasks
- Creating batch files for automation
- Scheduling tasks for regular maintenance
- Using advanced techniques like redirection and piping

These command-line skills are essential for efficient Windows system administration and will serve as a foundation for more advanced scripting and automation tasks.

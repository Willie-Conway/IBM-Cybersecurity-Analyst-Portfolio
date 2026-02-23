
![alt text](<../Screenshots/Windows Defender.png>)



# Hands-on Lab: Windows Defender Antivirus

**Estimated time needed:** 20 minutes

---

## Objectives

By completing this lab, you will develop a comprehensive understanding of how to secure a Windows operating system using the functionality of real-time protection provided by Windows Defender.

In this hands-on lab, you will explore typical settings to enable protection:

- **Exercise 1:** Review Windows Security Virus & threat protection
- **Exercise 2:** Update threat definitions
- **Exercise 3:** Run Windows Defender Antivirus quick scan
- **Exercise 4:** Run Windows Defender Antivirus custom scan

Further in this hands-on lab, you will also explore typical use cases:

- **Scenario 1:** Schedule a weekly full scan using Windows Defender Antivirus
- **Scenario 2:** Simulate downloading a test malware file and activate Windows Defender Antivirus to block and quarantine the file

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About the Lab Instructions and Solutions

Microsoft Windows operating system features can vary based on the Windows edition. If completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Configuration of Windows Defender Antivirus

### Exercise 1: Review Windows Security Virus & Threat Protection

In this exercise, you'll access and review Windows Security Virus & threat protection. Let's begin with locating and opening Windows Security Virus & threat protection.

#### Step 1: Open Windows Settings

1. Click the **Windows Start** button
2. Select **Settings** (the gear icon)


![alt text](<../Screenshots/Configuration of Windows Defender Antivirus/Exercise 1 - Review Windows Security Virus & threat protection/Review Windows Security Virus & threat protection.png>)

#### Step 2: Navigate to Update & Security

1. On the Windows Settings page, select **Update & Security**

![alt text](<../Screenshots/Configuration of Windows Defender Antivirus/Exercise 1 - Review Windows Security Virus & threat protection/On the Windows Settings page, select Update & Security.png>)

#### Step 3: Access Windows Security

1. Under Update & Security, select **Windows Security**
2. Select **Virus & threat protection**

![alt text](<../Screenshots/Configuration of Windows Defender Antivirus/Exercise 1 - Review Windows Security Virus & threat protection/Under Update & Security, select Windows Security. Here, select Virus and threat protection.png>)

#### Step 4: Review Virus & Threat Protection Features

On this screen, you'll see the following features (scroll down to discover all the features):

| Feature                                      | Description                                                                                                                                                                                                      |
| :------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Current threats**                    | View any threats detected on your device. See when the last scan occurred, how long the scan took, and how many files were scanned. Click to start a quick scan or access scan options for full or custom scans. |
| **Virus & threat protection settings** | Access options for managing protection settings. Customize protection level, opt to send sample files to Microsoft, exclude files or folders from scans, or temporarily stop protection.                         |
| **Virus & threat protection updates**  | View when virus definitions were last updated. Manually check for updates as needed.                                                                                                                             |
| **Ransomware protection**              | Enable controlled folder access to protect memory, files, and folders from unauthorized changes.                                                                                                                 |


![alt text](<../Screenshots/Configuration of Windows Defender Antivirus/Exercise 1 - Review Windows Security Virus & threat protection/Virus & threat protection settings.png>)

---

### Exercise 2: Update Threat Definitions

Windows Security uses **security intelligence**, also known as definitions, to identify known threats. These definitions include information about known threats and are updated automatically. However, if you suspect a problem with your system, you should ensure threat definitions are up-to-date before running a scan.

#### Step 1: Access Update Section

![alt text](<../Screenshots/Configuration of Windows Defender Antivirus/Exercise 2 - Update Threat Definitions/Update Threat Definitions.png>)

1. Under **Virus & threat protection updates**, select **Check for updates**

#### Step 2: Check for Updates

1. View details for the most recent update to your threat definitions
2. Select **Check for updates** (this process may take a few minutes)
3. When the update completes, the Check for updates button will return
4. Notice that the last update time and date have changed
5. Select the **back button** to return to the Virus & threat protection screen

![alt text](<../Screenshots/Configuration of Windows Defender Antivirus/Exercise 2 - Update Threat Definitions/Return to the Virus & threat protection screen.png>)

---

### Exercise 3: Run Antivirus Quick Scan

#### Step 1: Initiate Quick Scan

![alt text](<../Screenshots/Configuration of Windows Defender Antivirus/Exercise 3 - Run Antivirus Quick Scan/Run Antivirus Quick Scan.png>)

1. Click the **Quick scan** button on the Virus & threat protection screen
2. The scan will take several minutes to run
3. When complete, the Quick scan button will reappear

#### Step 2: Review Scan Results

1. Click **Protection history** to view any recent findings
2. This page shows:
   - Files identified as threats and quarantined (prevented from damaging your device)
   - Files identified as potential threats but allowed to continue running

![alt text](<../Screenshots/Configuration of Windows Defender Antivirus/Exercise 3 - Run Antivirus Quick Scan/This page shows you the results of the last scan.png>)

---

### Exercise 4: Run Antivirus Custom Scan

In this exercise, you will run a custom scan that only scans the files in the Downloads folder.

#### Step 1: Access Scan Options

1. From the Virus & threat protection screen, click **Scan options** (under Current threats)

#### Step 2: Select Custom Scan

1. Select **Custom scan**
2. Click the **Scan now** button

#### Step 3: Choose Folder to Scan

1. Browse to select the **Downloads** folder
2. Click **Select Folder**

#### Step 4: Run the Scan

1. The custom scan will begin scanning only the selected folder
2. Review results when complete

![alt text](<../Screenshots/Configuration of Windows Defender Antivirus/Exercise 4 - Run Antivirus Custom Scan/Run the Scan.png>)

<details>
<summary><strong>Click here for a hint</strong></summary>
The Downloads folder is typically located at C:\Users\[YourUsername]\Downloads
</details>

<details>
<summary><strong>Click here for the solution</strong></summary>
1. From Virus & threat protection, click Scan options
2. Select Custom scan
3. Click Scan now
4. Navigate to C:\Users\[YourUsername]\Downloads
5. Click Select Folder
6. Wait for scan to complete
7. Review results
</details>

---

## Typical Use Cases of Windows Defender Antivirus

### Scenario 1: Schedule a Weekly Full Scan

**Background:** Roshan is an employee working from home and needs to access company resources securely while ensuring his personal computer remains protected from potential threats. He wants to enable Windows Defender Antivirus and set up scheduled scans to automatically scan his system fully each week.

The steps below will help you schedule a weekly full scan using Windows Defender Antivirus via Task Scheduler.

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 1/Enable Virus & Threat Protection.png>)

#### Step 1: Enable Antivirus Protection

1. Open Virus & threat protection (follow steps from Exercise 1)
2. Under **Virus & threat protection settings**, click **Manage settings**
3. Ensure the following are enabled (toggled **On**):
   - Real-time protection
   - Cloud-delivered protection
   - Automatic sample submission

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 1/Turn On Real-time Protection.png>)


#### Step 2: Open Task Scheduler

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 1/Open Task Scheduler.png>)

1. Click the **Windows Start** button
2. Type **Task Scheduler** in the search box
3. Click **Task Scheduler** from the search results

#### Step 3: Create a New Task

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 1/Create a New Task.png>)

1. In Task Scheduler, click **Create Task** (from the Actions panel on the right)

#### Step 4: Configure General Settings


1. **Name:** Enter "Weekly Windows Defender Full Scan"
2. **Description:** Enter "Runs a full system scan every week"
3. Check **Run whether user is logged on or not**
4. Check **Run with highest privileges**

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 1/Configure General Settings.png>)

#### Step 5: Configure Trigger

1. Click the **Triggers** tab
2. Click **New**
3. Configure:
   - **Begin the task:** On a schedule
   - **Settings:** Weekly
   - **Start:** Set desired date and time (e.g., Sunday at 2:00 AM)
   - **Recur every:** 1 week
4. Click **OK**

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 1/Configure Triggers.png>)

#### Step 6: Configure Action

1. Click the **Actions** tab
2. Click **New**
3. Configure:
   - **Action:** Start a program
   - **Program/script:** `C:\Program Files\Windows Defender\MpCmdRun.exe`
   - **Add arguments:** `-Scan -ScanType 2`
4. Click **OK**

*Note: ScanType 2 specifies a full system scan*

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 1/Configure Actions.png>)

#### Step 7: Configure Conditions

1. Click the **Conditions** tab
2. Review and adjust settings as needed:
   - Uncheck **Start the task only if the computer is on AC power** (if laptop may run on battery)
   - Adjust other conditions based on preferences

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 1/Configure Conditions.png>)

#### Step 8: Finish Task Creation

1. Click **OK** to create the task
2. Enter your Windows password when prompted

#### Step 9: Verify Task

1. In Task Scheduler Library, locate your new task
2. Right-click and select **Run** to test immediately
3. The command prompt window will open showing scan progress
4. After completion, check the Windows Defender history to confirm the scan occurred
   
![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 1/Verify task.png>)

---

### Scenario 2: Simulate Malware Detection

**Background:** In this scenario, you will simulate downloading a test malware file to verify that Windows Defender Antivirus properly blocks and quarantines threats.

#### Step 1: Ensure Real-Time Protection is Enabled

1. Open Virus & threat protection
2. Click **Manage settings** (under Virus & threat protection settings)
3. Verify **Real-time protection** is turned **On**

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 2/Ensure Real-Time Protection is Enabled.png>)

#### Step 2: Download EICAR Test File

The **EICAR test file** is a standard test string developed by the European Institute for Computer Antivirus Research. It is not actually malicious but is recognized by antivirus software as a threat for testing purposes.

1. Open a web browser
2. Navigate to: `https://www.eicar.org/download-anti-malware-testfile/`
3. Click the **Download** button for the test file
4. Choose a location (Downloads folder is fine)

    ![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 2/Download EICAR Test File.png>)

#### Step 3: Observe Windows Defender Response

When the download completes, Windows Defender Antivirus will:

1. **Immediately detect** the test file as a threat
2. **Block** the file from executing
3. **Display a notification** in the system tray
4. **Quarantine** the file automatically

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 2/Observe Windows Defender Response.png>)

#### Step 4: Review Protection History

1. Open Virus & threat protection
2. Click **Protection history**
3. Locate the EICAR test file in the list of quarantined items
4. Review details including:
   - Threat name (typically "Virus:DOS/EICAR_Test_File")
   - Date and time of detection
   - Status (Quarantined)
   - Recommended actions

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 2/Review Protection History.png>)

#### Step 5: Manage Quarantined Item (Optional)

To remove the test file from quarantine:

1. Click on the quarantined item
2. Review available actions:
   - **Remove:** Permanently delete the file
   - **Restore:** Return the file to its original location (not recommended for test files)
3. Click **Remove** to delete the quarantined file

#### Step 6: Verify Cleanup

1. Navigate to the Downloads folder
2. Confirm the test file is no longer present
3. This confirms Windows Defender successfully removed the threat

![alt text](<../Screenshots/Typical Use cases of Windows Defender Antivirus/Scenario 2/Reviewing Alerts and Logs.png>)

---

## Troubleshooting Tips

| Issue                                       | Possible Solution                                                            |
| :------------------------------------------ | :--------------------------------------------------------------------------- |
| **Cannot access Windows Security**    | Run Windows Update; ensure Windows is activated                              |
| **Updates fail to download**          | Check internet connection; run Windows Update Troubleshooter                 |
| **Scan takes too long**               | Full scans on large drives may take several hours; schedule during off-hours |
| **Real-time protection won't enable** | Check for group policy restrictions; may be managed by organization          |
| **EICAR file not detected**           | Ensure real-time protection is enabled; check if file was excluded           |

---

## Summary

In this hands-on lab, you have:

| Task                                                | Completed |
| :-------------------------------------------------- | :-------- |
| Reviewed Windows Security Virus & threat protection | ✓        |
| Updated threat definitions                          | ✓        |
| Ran a quick scan                                    | ✓        |
| Ran a custom scan                                   | ✓        |
| Scheduled a weekly full scan using Task Scheduler   | ✓        |
| Simulated malware detection with EICAR test file    | ✓        |
| Reviewed protection history and quarantine          | ✓        |


<video controls src="Windows Defender Antivirus.mp4" title="Windows Defender Antivirus"></video>


### Key Takeaways

- **Real-time protection** continuously monitors for threats
- **Threat definitions** must be kept current for effective protection
- **Different scan types** serve different purposes (quick, full, custom)
- **Scheduled scans** ensure regular system checks without manual intervention
- **Quarantine** safely isolates threats for review or removal
- **EICAR test file** provides safe method to verify antivirus functionality

---

## Next Steps

After completing this lab, you should be comfortable with:

- Navigating Windows Security interface
- Managing virus and threat protection settings
- Running different types of scans
- Scheduling automated scans
- Responding to detected threats
- Verifying antivirus functionality with test files

Continue to the next lab to explore additional Windows security features.

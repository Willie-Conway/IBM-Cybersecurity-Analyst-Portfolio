

![alt text](<../Screenshots/Windows Defender.png>)

# Hands-on Lab: Windows Update

**Estimated time needed:** 30 minutes

---

## About This Lab

Operating system updates include patches that are designed to:

- Address known vulnerabilities
- Fix bugs
- Protect against new attack types
- Add new features

Because these patches address security risks, it is important to perform system updates as soon as possible. In this lab, we will work with **Windows Update**, the tool that is used for downloading, installing, and configuring Windows updates.

---

## Objectives

In this hands-on lab, you will:

- Review Windows Update
- Check for Windows updates
- Configure update settings

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About the Lab Instructions and Solutions

Microsoft Windows operating system features can vary based on the Windows edition. If completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Exercise 1: Review Windows Update




In this exercise, we will review the features available with Windows Update.

### Step-by-Step Instructions

#### Step 1: Open Windows Settings

![alt text](<../Screenshots/Review Windows Update.png>)

1. Click the **Windows Start** button (located at the bottom-left corner of the screen)
2. Click **Settings** (the gear icon) on the Start menu

   ![Windows Start Menu with Settings highlighted]

#### Step 2: Navigate to Update & Security

![alt text](<../Screenshots/Update & Security.png>)

1. In the Windows Settings window, locate and click **Update & Security**

   ![Windows Settings window with Update & Security highlighted]

#### Step 3: Review Windows Update Options

![alt text](<../Screenshots/Check for Windows Updates.png>)

Once you are in the Update & Security section, you will see the options for Windows Update. At the top of the right pane, you will find:

| Element                            | Description                                                                                                                                                                                                                        |
| :--------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Update Status**            | A notification regarding the current update status – whether update policies are up-to-date. In this instance, there is an alert indicating that Windows Update is not up-to-date and that the last update was several years ago. |
| **Check for updates button** | This button checks with Microsoft to see what updates are available for this system. Clicking this button will automatically download and install the updates that are found.                                                      |
| **Change active hours**      | This option allows you to specify when you typically use your computer so that updates do not interrupt your work.                                                                                                                 |

![Windows Update screen showing status, Check for updates button, and Change active hours link]

---

## Exercise 2: Check for Windows Updates

![alt text](<../Screenshots/Check for updates.png>)

In this exercise, we will check for and install available Windows updates.

### Step-by-Step Instructions

#### Step 1: Check for Updates

1. From the Windows Update screen, click the **Check for updates** button
2. Windows will connect to Microsoft servers and search for available updates for your system

   ![Checking for updates progress indicator]

#### Step 2: Review Available Updates

![alt text](<../Screenshots/Status updates.png>)

Once the scan completes, Windows will display:

- **Quality updates:** Security patches, bug fixes, and reliability improvements
- **Feature updates:** Major new features and functionality (if available)
- **Optional updates:** Driver updates and other non-critical items (if available)

#### Step 3: Download and Install Updates

![alt text](<../Screenshots/Download and Install Updates.png>)


1. If updates are found, click **Download and install** (or **Install now**)
2. The download progress will be displayed
3. Some updates may require a system restart to complete installation

#### Step 4: Restart if Required

If a restart is required:

1. Save any open work
2. Click **Restart now** to complete the update installation
3. The system will restart and apply updates during the shutdown/startup process

---

## Exercise 3: Configure Active Hours

![alt text](<../Screenshots/Cancel active hours.png>)

In this exercise, we will configure active hours to prevent updates from restarting your computer during work hours.

### Step-by-Step Instructions

#### Step 1: Access Active Hours Settings

1. From the Windows Update screen, click **Change active hours**

#### Step 2: Configure Active Hours

You have two options:

**Option A: Automatically adjust active hours**

- Windows learns your usage patterns and adjusts active hours automatically

**Option B: Manually set active hours**

1. Toggle **Automatically adjust active hours for this device based on activity** to **Off**
2. Click the drop-down menus to set your **Start time** and **End time**
3. Choose times when you typically use your computer
4. Click **Save**

![Active hours configuration screen]

---

## Exercise 4: Advanced Options

![alt text](<../Screenshots/Advanced Options.png>)

In this exercise, we will explore advanced Windows Update settings.

### Step-by-Step Instructions

#### Step 1: Access Advanced Options

1. From the Windows Update screen, click **Advanced options**

#### Step 2: Review Advanced Settings

![alt text](<../Screenshots/Windows Update.png>)

The Advanced options screen includes:

| Setting                                                           | Description                                                                |
| :---------------------------------------------------------------- | :------------------------------------------------------------------------- |
| **Update notifications**                                    | Control when and how you receive update notifications                      |
| **Download updates over metered connections**               | Allow or block updates when using metered networks (like cellular data)    |
| **Give me updates for other Microsoft products**            | Enable this to receive updates for Office and other Microsoft applications |
| **Download and install updates automatically**              | Control automatic update behavior                                          |
| **Restart this device as soon as possible**                 | Allow Windows to restart sooner to complete updates                        |
| **Show a notification when your device requires a restart** | Receive alerts when a restart is needed                                    |
| **Delivery Optimization**                                   | Configure how updates are downloaded from other PCs (peer-to-peer)         |

#### Step 3: Configure Optional Updates (if available)

1. Click **Optional updates** (if visible)
2. Review available driver updates and other optional items
3. Select any desired updates
4. Click **Download and install**

---

## Exercise 5: View Update History

![alt text](<../Screenshots/View update history.png>)

In this exercise, we will review the history of installed updates.

### Step-by-Step Instructions

#### Step 1: Access Update History

1. From the Windows Update screen, click **View update history**

#### Step 2: Review Installed Updates

The update history screen displays:

| Section                      | Description                                            |
| :--------------------------- | :----------------------------------------------------- |
| **Feature Updates**    | Major Windows version upgrades                         |
| **Quality Updates**    | Security and reliability patches                       |
| **Definition Updates** | Antivirus and security intelligence updates            |
| **Other Updates**      | Driver and other non-security updates                  |
| **Update History**     | Chronological list of all installed updates with dates |

#### Step 3: Uninstall Updates (if needed)

**Warning**: Uninstalling updates may affect system stability. Only proceed if instructed by IT support.

![alt text](<../Screenshots/Uninstall update.png>)

1. Click **Uninstall updates** (at the top of the screen)
2. This opens the Control Panel with a list of installed updates
3. Select an update and click **Uninstall** to remove it (use caution—this may affect system stability)

---

## Summary

In this hands-on lab, you have:

| Task                                 | Completed |
| :----------------------------------- | :-------- |
| Navigated to Windows Update settings | ✓        |
| Reviewed current update status       | ✓        |
| Checked for available updates        | ✓        |
| Downloaded and installed updates     | ✓        |
| Configured active hours              | ✓        |
| Explored advanced options            | ✓        |
| Viewed update history                | ✓        |

### Key Takeaways

<video controls src="Windows Updates.mp4" title="Windows Update"></video>

- **Regular updates are essential** for maintaining system security
- **Windows Update** provides a centralized interface for managing updates
- **Active hours** prevent disruptive restarts during work time
- **Update history** helps track which patches have been installed
- **Advanced options** provide fine-grained control over update behavior

---

## Troubleshooting Tips

| Issue                          | Possible Solution                                            |
| :----------------------------- | :----------------------------------------------------------- |
| Updates fail to download       | Check internet connection; run Windows Update Troubleshooter |
| Updates fail to install        | Restart computer and try again; check disk space             |
| System is slow after updates   | Updates may be configuring in background; wait 30-60 minutes |
| Update settings are grayed out | May be managed by organization policy; contact IT support    |

---

## Next Steps

After completing this lab, you should be comfortable with:

- Checking for and installing Windows updates
- Configuring update settings to minimize disruption
- Reviewing update history to verify patch installation
- Understanding the importance of regular updates for security

Continue to the next hands-on lab to explore additional Windows security features.

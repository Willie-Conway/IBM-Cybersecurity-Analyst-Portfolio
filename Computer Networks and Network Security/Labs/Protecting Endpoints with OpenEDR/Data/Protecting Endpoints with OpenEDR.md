![alt text](../Screenshots/Xcitium.jpg)


# Lab: Protecting Endpoints with OpenEDR

**Estimated Time:** 45 minutes

Welcome to the Protecting Endpoints with Xcitium OpenEDR lab!

---

## Introduction

**Xcitium OpenEDR** is a free, open-source endpoint protection and response (EDR) system that follows a client-server model. A centrally managed server hosts a security program, and an accompanying client program runs on each endpoint. The client sends information to the server, and the server administrator uses a server EDR program to analyze this information and defend endpoints from malware and additional threats.

In this lab, you will learn to manage and protect endpoints using Xcitium OpenEDR, manage endpoints, and explore the cloud manager.

---

## Before You Begin

This lab requires the download and installation of no-cost software. Before you begin this lab, you need to be logged in as the administrator, or have administrative rights, to install the required software.

---

## Learning Objectives

After completing this lab, you will be able to:

- Set up the Xcitium Cloud Manager
- Add an endpoint device to the OpenEDR system
- Locate endpoint data in the Xcitium Cloud Manager
- Manage endpoint patches from the Xcitium Cloud Manager
- Scan an endpoint for malware and find the results in the Xcitium Cloud Manager

---

## Prerequisites

For this lab, you need to have:

### Authenticator App

A smartphone with an authenticator application installed. Common authenticator applications include:

| App                               | Available On |
| :-------------------------------- | :----------- |
| **Google Authenticator**    | iOS, Android |
| **Microsoft Authenticator** | iOS, Android |
| **LastPass Authenticator**  | iOS, Android |
| **2FAS**                    | iOS, Android |

### Endpoint Devices

One or more devices to use as endpoints. You can use internet-enabled computers, tablets, or smartphones with one of the following operating systems:

| OS                | Support |
| :---------------- | :------ |
| **Windows** | ✅      |
| **macOS**   | ✅      |
| **Linux**   | ✅      |
| **iOS**     | ✅      |
| **Android** | ✅      |

**Note:** You can set up endpoint protection on the same device you're using to explore the cloud manager.

---

## Task 1: Set Up Open Source Version of Xcitium Cloud Manager

In this task, you will create a free OpenEDR account and configure multifactor authentication.

### Step 1: Access OpenEDR Website

1. Open your web browser (Chrome, Firefox, Edge, etc.)
2. Navigate to: **https://openedr.com/**

![OpenEDR homepage]

![alt text](<../Screenshots/OpenEDR homepage_2.png>)

### Step 2: Create Free Account

1. Click **Get Started for Free** (or **Sign Up**)

![Get Started for Free button]

![alt text](<../Screenshots/Get Started for Free button.jpg>)

2. Enter your information to create a free account:

| Field                      | Information                                                               |
| :------------------------- | :------------------------------------------------------------------------ |
| **First Name**       | Enter your first name                                                     |
| **Last Name**        | Enter your last name                                                      |
| **Email Address**    | Enter a valid email address                                               |
| **Password**         | Create a strong password (12+ characters, mix of cases, numbers, symbols) |
| **Confirm Password** | Re-enter your password                                                    |

![Account creation form]

![alt text](<../Screenshots/Account creation form_2.png>)

3. Click **Create Account** or **Sign Up**

### Step 3: Set Up Multifactor Authentication (MFA)

After creating your account, Xcitium will prompt you to set up multifactor authentication (MFA) using the authenticator app on your mobile device.

1. Open your authenticator app on your smartphone
2. Scan the on-screen **QR barcode** to add the account
3. The authenticator app will generate a six-digit verification code

![MFA setup QR code]

4. Type or enter this code in the **Enter Verification Code** field on your browser window
5. Click **Pair Authenticator**

![MFA verification code entry]

**Note:** You might see an optional **Set Secret Questions** window. This lab does not require that you complete this task. Select **Skip** to bypass this task.

### Step 4: Complete Welcome Setup

1. The **Welcome** screen opens
2. Click **Next** to continue

![Welcome screen]

### Step 5: Take Screenshot

Take a screenshot showing:

- The OpenEDR dashboard after successful login

Save the file as `OpenEDR_Dashboard.png`

---

## Task 2: Add an Endpoint Device to the OpenEDR System

In this task, you will download and install the OpenEDR agent on an endpoint device and register it with the cloud manager.

### Step 1: Navigate to Endpoint Management

1. From the OpenEDR dashboard, locate and click **Endpoint Management** or **Add Endpoint**

![Endpoint Management option]

### Step 2: Select Operating System

1. Choose the operating system of the device you want to protect:

| OS                | Selection                               |
| :---------------- | :-------------------------------------- |
| **Windows** | Download Windows installer (.exe)       |
| **macOS**   | Download macOS installer (.dmg)         |
| **Linux**   | Download Linux installer (.deb or .rpm) |
| **Android** | Download from Google Play               |
| **iOS**     | Download from Apple App Store           |

![OS selection screen]

### Step 3: Download the Agent

1. Click **Download** to download the appropriate installer for your device
2. Save the file to your computer

### Step 4: Install the OpenEDR Agent

**For Windows:**

1. Locate the downloaded installer file (e.g., `OpenEDR_Setup.exe`)
2. Right-click and select **Run as Administrator**
3. Follow the installation wizard prompts
4. Accept the license agreement
5. Click **Install**

![Windows installer]

**For macOS:**

1. Open the downloaded `.dmg` file
2. Drag the OpenEDR application to the Applications folder
3. Open the application (may require allowing in Security & Privacy settings)

**For Linux (Ubuntu/Debian):**

```bash
# Navigate to the download folder
cd ~/Downloads

# Install the package
sudo dpkg -i openedr_*.deb

# Fix dependencies if needed
sudo apt-get install -f
```

### Step 5: Register the Endpoint

During installation, you may be prompted to register the endpoint:

1. The agent may automatically register with your cloud account
2. If prompted, enter your OpenEDR account credentials
3. The endpoint will appear in the cloud manager within a few minutes

### Step 6: Verify Endpoint Registration

1. Return to the OpenEDR Cloud Manager in your browser
2. Navigate to **Endpoints** or **Endpoint Management**
3. You should see your newly added endpoint listed

![Endpoint list showing registered device]

### Step 7: Take Screenshot

Take a screenshot showing:

- The endpoint list with your device showing as online/connected

Save the file as `OpenEDR_Endpoint_Added.png`

---

## Task 3: Locate Endpoint Data in the Xcitium Cloud Manager

In this task, you will explore the various data views available for your endpoints.

### Step 1: Navigate to Endpoint Details

1. From the **Endpoints** list, click on your endpoint name or ID
2. This opens the detailed view for that endpoint

### Step 2: Review Endpoint Information

The endpoint details page typically shows:

| Section                   | Information Displayed                           |
| :------------------------ | :---------------------------------------------- |
| **General Info**    | Hostname, OS, IP address, last seen time        |
| **Status**          | Protection status, last scan, connection status |
| **Hardware**        | CPU, RAM, disk space                            |
| **Software**        | Installed applications, running processes       |
| **Security Events** | Alerts, detections, blocked threats             |

![Endpoint details page]

### Step 3: Explore Security Events

1. Click on **Security Events** or **Alerts** tab
2. Review any events recorded for this endpoint
3. Note that a new endpoint may have few or no events initially

### Step 4: Explore Running Processes

1. Click on **Processes** or **Applications** tab
2. View the list of currently running processes on the endpoint
3. This data is collected by the agent and sent to the cloud

![Process list]

### Step 5: Take Screenshot

Take a screenshot showing:

- The endpoint details page with at least one section expanded

Save the file as `OpenEDR_Endpoint_Data.png`

---

## Task 4: Manage Endpoint Patches from the Xcitium Cloud Manager

In this task, you will view and manage software patches for your endpoints.

### Step 1: Navigate to Patch Management

1. From the main dashboard, click **Patch Management** or **Software Updates**

![Patch Management option]

### Step 2: View Missing Patches

1. The patch management dashboard shows:

   - Number of endpoints
   - Number of missing patches
   - Critical vs. non-critical updates
2. Review the list of **Missing Patches** for your endpoint

![Missing patches list]

### Step 3: Review Patch Details

1. Click on a specific patch to view details:
   - Patch name and KB number (for Windows)
   - Severity (Critical, Important, Moderate)
   - Description of what the patch addresses
   - Applicable endpoints

![Patch details]

### Step 4: Approve or Deploy Patches

1. Select patches you want to deploy
2. Click **Approve** or **Deploy**
3. The cloud manager will instruct the endpoint agent to install the selected patches

![Deploy patches button]

### Step 5: Monitor Patch Status

1. After deployment, monitor the **Patch Status** column
2. Status will change from "Missing" to "Installed" or "Pending Reboot"

### Step 6: Take Screenshot

Take a screenshot showing:

- The patch management dashboard with at least one missing patch

Save the file as `OpenEDR_Patch_Management.png`

---

## Task 5: Scan an Endpoint for Malware and Find Results

In this task, you will initiate a malware scan from the cloud manager and view the results.

### Step 1: Navigate to Antivirus/Scan

1. From the endpoint details page, click **Antivirus** or **Scan**

![Scan option]

### Step 2: Select Scan Type

Choose the type of scan:

| Scan Type             | Description                            |
| :-------------------- | :------------------------------------- |
| **Quick Scan**  | Scans common malware locations (fast)  |
| **Full Scan**   | Scans entire system (thorough, slower) |
| **Custom Scan** | Scan specific files or folders         |

For this lab, select **Quick Scan**

![Scan type selection]

### Step 3: Initiate the Scan

1. Click **Start Scan** or **Run Now**
2. The scan command is sent to the endpoint agent

### Step 4: Monitor Scan Progress

1. The scan status will update in the cloud manager
2. Status will show:
   - **Queued** – Waiting to run
   - **In Progress** – Currently scanning
   - **Completed** – Scan finished

![Scan progress]

### Step 5: View Scan Results

1. After the scan completes, click **View Results**
2. The results will show:

| Result                | Meaning                    |
| :-------------------- | :------------------------- |
| **Clean**       | No threats detected        |
| **Quarantined** | Threats found and isolated |
| **Removed**     | Threats found and deleted  |
| **Failed**      | Scan encountered errors    |

![Scan results]

### Step 6: Review Threat Details

If any threats were detected:

1. Click on the threat to view details:
   - Threat name
   - File location
   - Severity
   - Action taken

![Threat details]

### Step 7: Take Screenshot

Take a screenshot showing:

- The scan results (clean or showing any detected threats)

Save the file as `OpenEDR_Scan_Results.png`

---

## Task 6: Explore Additional OpenEDR Features (Optional)

### Real-Time Protection

1. Navigate to **Policies** to view real-time protection settings
2. Check that real-time protection is enabled
3. This feature continuously monitors for threats

### Device Control

1. Explore **Device Control** to manage USB and peripheral access
2. Configure which devices can connect to endpoints

### Reporting

1. Click **Reports** to generate security reports
2. Select report type and date range
3. Export or view reports

---

## Lab Completion Checklist

| Task                                       | Completed |
| :----------------------------------------- | :-------- |
| Created OpenEDR account                    | ☐        |
| Set up MFA with authenticator app          | ☐        |
| Completed welcome setup                    | ☐        |
| Downloaded OpenEDR agent                   | ☐        |
| Installed agent on endpoint device         | ☐        |
| Verified endpoint appears in cloud manager | ☐        |
| Located endpoint details and data          | ☐        |
| Navigated to patch management              | ☐        |
| Viewed missing patches                     | ☐        |
| Initiated malware scan from cloud manager  | ☐        |
| Monitored scan progress                    | ☐        |
| Viewed scan results                        | ☐        |

---

## Screenshot Checklist

| Screenshot       | File Name                        | Description                       |
| :--------------- | :------------------------------- | :-------------------------------- |
| Dashboard        | `OpenEDR_Dashboard.png`        | OpenEDR dashboard after login     |
| Endpoint Added   | `OpenEDR_Endpoint_Added.png`   | Endpoint list showing your device |
| Endpoint Data    | `OpenEDR_Endpoint_Data.png`    | Endpoint details page             |
| Patch Management | `OpenEDR_Patch_Management.png` | Missing patches list              |
| Scan Results     | `OpenEDR_Scan_Results.png`     | Malware scan results              |

---

## Troubleshooting Tips

| Issue                              | Solution                                                         |
| :--------------------------------- | :--------------------------------------------------------------- |
| **Endpoint not appearing**   | Wait 2-3 minutes; refresh page; check agent installation         |
| **MFA code not working**     | Ensure authenticator app time is synced; try re-scanning QR code |
| **Agent installation fails** | Run installer as administrator; check antivirus blocking         |
| **Scan not completing**      | Check endpoint connectivity; ensure agent is running             |
| **Patches not deploying**    | Verify endpoint is online; check patch approval status           |

---

## Key Takeaways

| Concept                        | Description                                              |
| :----------------------------- | :------------------------------------------------------- |
| **OpenEDR**              | Free, open-source Endpoint Detection and Response system |
| **Client-Server Model**  | Server manages; client agents report to server           |
| **MFA**                  | Required for account security during setup               |
| **Endpoint Management**  | View and manage devices from cloud console               |
| **Patch Management**     | Deploy software updates to endpoints remotely            |
| **On-Demand Scanning**   | Initiate malware scans from cloud manager                |
| **Real-Time Protection** | Continuous monitoring for threats                        |

---

## Summary

In this hands-on lab, you have:

| Activity                               | Completed |
| :------------------------------------- | :-------- |
| Created Xcitium OpenEDR account        | ✓        |
| Set up MFA with authenticator app      | ✓        |
| Downloaded and installed OpenEDR agent | ✓        |
| Registered endpoint with cloud manager | ✓        |
| Located endpoint data in cloud console | ✓        |
| Viewed and managed missing patches     | ✓        |
| Initiated malware scan from cloud      | ✓        |
| Viewed scan results                    | ✓        |
| Explored additional features           | ✓        |

---

## Congratulations!

You have successfully completed the **Protecting Endpoints with OpenEDR** lab. You now know how to:

- Set up an OpenEDR cloud account with MFA
- Add endpoint devices to the OpenEDR system
- Locate and review endpoint data
- Manage patches remotely
- Initiate and review malware scans

These skills are essential for modern endpoint protection and security management in both home and enterprise environments.

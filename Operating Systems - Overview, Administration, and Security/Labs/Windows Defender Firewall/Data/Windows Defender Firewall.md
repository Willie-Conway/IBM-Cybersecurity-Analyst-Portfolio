![alt text](<../Screenshots/Windows Defender.png>)

# Hands-on Lab: Windows Defender Firewall

**Estimated time needed:** 25 minutes

---

## Learning Objectives

In this lab, you will learn to:

- Configure the Windows Defender Firewall using the basic user interface
- Understand the different types of network profiles: Domain, Private, and Public
- Enable or disable the firewall for each network profile
- Manage incoming connections to improve the security of your Windows system

---

## Important Information About Lab Instructions and Solutions

In case you try to use your physical keyboard in the lab environment, it might not produce any visible results. To avoid this issue, please use the **On-Screen Keyboard** (you can find it by searching for "On-Screen Keyboard" in the search bar at the bottom of your screen). If search functionality doesn't work, you can also click on the Windows icon, scroll down to find **Windows Ease of Access**, click on it, and then select **On-Screen Keyboard**.

Microsoft Windows operating system features can vary based on the Windows edition. If completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About the Lab Instructions and Solutions

Microsoft Windows operating system features can vary based on the Windows edition. If completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Introduction

Windows Defender Firewall acts as a barrier between your computer and potential threats from the network or internet. It monitors incoming and outgoing traffic and blocks or allows data packets based on a set of security rules. Understanding how to configure the firewall is essential for maintaining system security.

---

## Exercise 1: Access Windows Security and Firewall Settings

In this exercise, you will navigate to the Windows Security center and access firewall configuration options.

### Step 1: Open Windows Security

1. Click the Windows **Start** button (bottom-left corner of your screen)




![alt text](<../Screenshots/Windows Start button highlighted.png>)


1. Scroll down through the applications list or type **Windows Security** in the search bar
2. Click on **Windows Security** to open the application

![Windows Start menu with Windows Security selected]

### Step 2: Navigate to Firewall & Network Protection

1. In the Windows Security dashboard, click on **Firewall & network protection**



![alt text](<../Screenshots/Security at a glance window with Firewall & network protection highlighted.png>)

### Step 3: Understand Network Profiles

The Firewall & network protection screen displays the status for three different network profiles:

| Profile                   | Description                                                                 | When Used                                                          |
| :------------------------ | :-------------------------------------------------------------------------- | :----------------------------------------------------------------- |
| **Domain network**  | Networks where an Active Directory domain controller authenticates accounts | Corporate networks, school networks, any domain-joined environment |
| **Private network** | Trusted networks where your device should be discoverable by other devices  | Home networks, small office networks, trusted Wi-Fi                |
| **Public network**  | Untrusted networks where your device should be hidden from others           | Coffee shops, airports, hotels, libraries, any public Wi-Fi        |



![alt text](<../Screenshots/Firewall & network protection window showing three network profiles.png>)

---

## Exercise 2: Configure Domain Network Firewall Settings

In this exercise, you will examine and configure firewall settings for the Domain network profile.

### Step 1: Select Domain Network

1. Click on **Domain network** from the three profile options



![alt text](<../Screenshots/Domain network highlighted on Firewall & network protection window.png>)

### Step 2: Review Domain Network Settings

The Domain network settings screen displays:

- **Current status** - Whether the firewall is on or off for this profile
- **Incoming connections** - Settings for blocking or allowing incoming traffic
- **Active Domain networks** - Lists the domain networks your device is connected to



![alt text](<../Screenshots/Domain network details screen.png>)

### Step 3: Verify Firewall Status

1. Verify that the **Windows Defender Firewall** toggle is set to **On**

   - If it's off, click the toggle to turn it on
2. Observe the **Incoming connections** section which has the option:

   - **Block all incoming connections, including those in the list of allowed apps**

![Domain network with firewall toggle On]

**Understanding Incoming Connections:**

| Setting                       | Effect                                                                                                  |
| :---------------------------- | :------------------------------------------------------------------------------------------------------ |
| **Default (unchecked)** | Allows incoming connections that match allowed app rules                                                |
| **Checked**             | Blocks all unsolicited incoming connections; your computer will be essentially invisible on the network |

**Note:** You do not need to enable the "Block all incoming connections" option for this lab, but it's important to understand what it does.

### Step 4: Return to Main Firewall Screen

1. Click the **back arrow** button (top-left corner) to return to the main Firewall & network protection window

---

## Exercise 3: Configure Private Network Firewall Settings

In this exercise, you will examine and configure firewall settings for the Private network profile.

### Step 1: Select Private Network

1. From the main Firewall & network protection window, click on **Private network**

![Private network highlighted on Firewall & network protection window]

### Step 2: Review Private Network Settings

The Private network settings screen displays similar options to the Domain network:

- Firewall status toggle
- Incoming connections blocking option
- Active private networks list

### Step 3: Verify Firewall Status

1. Verify that the **Windows Defender Firewall** toggle is set to **On**
   - If it's off, click the toggle to turn it on



![alt text](<../Screenshots/Private network highlighted on Firewall & network protection window.png>)

### Step 4: Return to Main Firewall Screen

1. Click the **back arrow** button to return to the main Firewall & network protection window


![alt text](<../Screenshots/Private network with firewall toggle On.png>)
---

## Exercise 4: Configure Public Network Firewall Settings

In this exercise, you will examine and configure firewall settings for the Public network profile.

### Step 1: Select Public Network

1. From the main Firewall & network protection window, click on **Public network**

![alt text](<../Screenshots/Public network highlighted on Firewall & network protection window.png>)


### Step 2: Review Public Network Settings

The Public network settings screen displays the same options as the other profiles.

### Step 3: Verify Firewall Status

1. Verify that the **Windows Defender Firewall** toggle is set to **On**
   - If it's off, click the toggle to turn it on


![alt text](<../Screenshots/Public network with firewall toggle On.png>)

### Step 4: Return to Main Firewall Screen

1. Click the **back arrow** button to return to the main Firewall & network protection window
   
![alt text](<../Screenshots/Firewall and network protection screen.png>)

---

## Exercise 5: Allow an App Through the Firewall

In this exercise, you will learn how to allow specific applications to communicate through the firewall.

### Step 1: Access Allowed Apps

1. From the main Firewall & network protection window, click on **Allow an app through firewall**

![Allow an app through firewall highlighted on Firewall & network protection window]

### Step 2: Review Allowed Apps List

The "Allowed apps" window displays:

- A list of applications that have firewall rules
- Checkboxes indicating which network profiles each app is allowed on
- **Private** column - Allows app on private networks
- **Public** column - Allows app on public networks

![Allowed apps list showing various applications with checkboxes]

### Step 3: Locate an Application

1. Scroll through the list to find an application like **Google Chrome** or **Microsoft Edge**
2. Observe the current configuration - note which networks the app is currently allowed on

### Step 4: Modify App Permissions (Optional)

If you want to allow an app on a different network profile:

1. Click the **Change settings** button (requires administrator privileges)
2. Find the application you want to modify
3. Check or uncheck the boxes under **Private** or **Public** as desired
4. Click **OK** to save changes

![Changing app permissions with checkboxes]

**Example:** To allow Firefox on the public network:

- Locate Firefox in the list
- Click the **Public** checkbox to add a checkmark
- Click **OK**

### Step 5: Add a New App (Optional)

If an application isn't listed, you can add it:

1. Click **Allow another app**
2. Click **Browse** to find the application's executable file
3. Select the app and click **Add**
4. Choose which network profiles to allow it on

![Allow another app dialog]

### Step 6: Return to Main Firewall Screen

1. Click **OK** to close the Allowed apps window
2. You'll return to the Firewall & network protection main screen

---

## Exercise 6: Advanced Firewall Settings Overview

In this exercise, you will be introduced to the advanced firewall configuration interface.

### Step 1: Open Advanced Settings

1. From the main Firewall & network protection window, click on **Advanced settings** in the left navigation pane

![Advanced settings link in left pane]

### Step 2: Explore Windows Defender Firewall with Advanced Security

This opens the **Windows Defender Firewall with Advanced Security** console, which provides more detailed configuration options.

![Windows Defender Firewall with Advanced Security window]

### Step 3: Understand the Interface

The advanced console is organized into three main sections:

| Section                             | Description                                            |
| :---------------------------------- | :----------------------------------------------------- |
| **Inbound Rules**             | Rules that control traffic coming INTO your computer   |
| **Outbound Rules**            | Rules that control traffic leaving your computer       |
| **Connection Security Rules** | Rules for secure connections between computers (IPsec) |
| **Monitoring**                | View current firewall activity and settings            |

### Step 4: View Inbound Rules

1. Click on **Inbound Rules** in the left pane
2. The center pane displays all inbound rules with:
   - Name
   - Group
   - Profile (Domain, Private, Public)
   - Enabled status
   - Action (Allow/Block)
   - Protocol and ports

![Inbound rules list]

### Step 5: Examine a Rule

1. Double-click on any rule to open its properties
2. Explore the different tabs:
   - **General** - Rule name, description, enabled status, action
   - **Programs and Services** - Which program the rule applies to
   - **Protocols and Ports** - Which protocols and ports are affected
   - **Scope** - Which IP addresses are affected
   - **Advanced** - Which profiles the rule applies to

![Rule properties window]

3. Click **Cancel** to close without making changes

### Step 6: Close Advanced Security

1. Click the **X** in the top-right corner to close the Advanced Security window
2. You'll return to the main Firewall & network protection screen

---

## Exercise 7: Restore Default Firewall Settings (Optional)

In this exercise, you will learn how to restore firewall settings to their default configuration.

### Step 1: Navigate to Restore Defaults

1. From the main Firewall & network protection window, scroll down and click on **Restore firewalls to default**

![Restore firewalls to default link]

### Step 2: Understand the Impact

The restore defaults screen explains that this will:

- Reset all firewall settings to their original installation state
- Remove all custom rules you've created
- Reset all network profiles to default settings

![Restore defaults confirmation screen]

### Step 3: Restore Defaults (Optional)

If you want to restore defaults:

1. Click the **Restore defaults** button
2. Click **Yes** when prompted to confirm

**Note:** For this lab, you do NOT need to restore defaults. This information is provided for future reference.

---

## Exercise 8: Firewall Best Practices Review

In this exercise, you will review best practices for firewall configuration.

### Step 1: Create a Best Practices Reference

Open Notepad and create a file called **`firewall-best-practices.txt`** :

```
WINDOWS DEFENDER FIREWALL BEST PRACTICES
=========================================

GENERAL PRINCIPLES
------------------
1. Keep the firewall enabled on all profiles
2. Only allow necessary applications through the firewall
3. Use the principle of least privilege - grant minimum necessary access
4. Regularly review allowed apps and remove unused ones
5. Understand the network profile before connecting

NETWORK PROFILE RECOMMENDATIONS
--------------------------------

PUBLIC NETWORKS (Coffee shops, airports, hotels)
• Firewall: MUST be enabled
• Incoming connections: Block all
• App permissions: Only absolutely necessary apps
• Device discoverability: Turned OFF
• Risk level: High - treat as untrusted

PRIVATE NETWORKS (Home, trusted office)
• Firewall: Enabled
• Incoming connections: Allow as needed
• App permissions: Can be more permissive
• Device discoverability: Can be ON for file/printer sharing
• Risk level: Medium - trusted but still protected

DOMAIN NETWORKS (Corporate, managed)
• Firewall: Enabled (managed by group policy)
• Incoming connections: Managed centrally
• App permissions: Often managed by IT
• Device discoverability: As configured by domain policies
• Risk level: Low - professionally managed

WHEN TO BLOCK ALL INCOMING CONNECTIONS
---------------------------------------
• When using public Wi-Fi
• When troubleshooting security issues
• When maximum privacy is needed
• When you don't need file/printer sharing

APP PERMISSION GUIDELINES
-------------------------
Allow through firewall only if:
• The app needs to receive incoming connections
• You trust the application completely
• The app requires network access to function

Consider blocking if:
• The app doesn't need incoming connections
• The app is rarely used
• You're on a public network

REGULAR MAINTENANCE TASKS
-------------------------
□ Review allowed apps list monthly
□ Check for unknown or suspicious rules
□ Verify firewall is enabled on all profiles
□ Monitor firewall logs for blocked attempts
□ Keep Windows updated for latest firewall rules

TROUBLESHOOTING TIPS
--------------------
If an app can't connect:
1. Check if firewall is blocking it
2. Temporarily disable firewall to test (re-enable immediately)
3. Add app to allowed list if needed
4. Check both inbound and outbound rules

If you can't connect to the internet:
1. Verify firewall isn't blocking all traffic
2. Check if public network profile is too restrictive
3. Look for recently changed rules
4. Consider restoring defaults as last resort

Remember: The firewall is your first line of defense - 
configure it carefully and review it regularly!
```

### Step 2: Save the File

1. Save the file to your desktop or documents folder
2. Name it **`firewall-best-practices.txt`**

---

## Exercise 9: Lab Completion Checklist

### Step 1: Verify All Tasks Completed

Use this checklist to ensure you've completed all lab activities:

| Task                                       | Completed |
| :----------------------------------------- | :-------- |
| Opened Windows Security                    | ☐        |
| Navigated to Firewall & network protection | ☐        |
| Viewed Domain network settings             | ☐        |
| Verified Domain network firewall is On     | ☐        |
| Viewed Private network settings            | ☐        |
| Verified Private network firewall is On    | ☐        |
| Viewed Public network settings             | ☐        |
| Verified Public network firewall is On     | ☐        |
| Explored "Allow an app through firewall"   | ☐        |
| Located an application in the allowed list | ☐        |
| Opened Advanced settings                   | ☐        |
| Viewed Inbound Rules in Advanced Security  | ☐        |
| Examined a rule's properties               | ☐        |
| Located Restore defaults option            | ☐        |
| Created firewall best practices reference  | ☐        |

### Step 2: Answer Review Questions

1. **What are the three network profiles in Windows Defender Firewall and when would you use each?**

   ```
   _________________________________________________________________
   _________________________________________________________________
   _________________________________________________________________
   ```
2. **Why is it important to have the firewall enabled on public networks?**

   ```
   _________________________________________________________________
   _________________________________________________________________
   ```
3. **What is the difference between allowing an app on Private vs. Public networks?**

   ```
   _________________________________________________________________
   _________________________________________________________________
   ```
4. **When might you want to block all incoming connections?**

   ```
   _________________________________________________________________
   _________________________________________________________________
   ```
5. **What information can you find in the Windows Defender Firewall with Advanced Security console?**

   ```
   _________________________________________________________________
   _________________________________________________________________
   ```

---

## Summary of Key Concepts

| Concept                      | Description                                           |
| :--------------------------- | :---------------------------------------------------- |
| **Domain Network**     | Corporate/managed networks with domain authentication |
| **Private Network**    | Trusted home or small office networks                 |
| **Public Network**     | Untrusted networks like coffee shops, airports        |
| **Inbound Rules**      | Control traffic coming INTO your computer             |
| **Outbound Rules**     | Control traffic leaving your computer                 |
| **Allowed Apps**       | Applications permitted through the firewall           |
| **Block All Incoming** | Makes your computer invisible on the network          |

---

## Summary

In this hands-on lab, you have:

| Activity                                                | Completed |
| :------------------------------------------------------ | :-------- |
| Opened Windows Security from the Start menu             | ✓        |
| Navigated to Firewall & network protection              | ✓        |
| Reviewed Domain network profile settings                | ✓        |
| Reviewed Private network profile settings               | ✓        |
| Reviewed Public network profile settings                | ✓        |
| Verified firewall is enabled on all profiles            | ✓        |
| Explored the "Allow an app through firewall" interface  | ✓        |
| Located applications in the allowed apps list           | ✓        |
| Opened Windows Defender Firewall with Advanced Security | ✓        |
| Viewed Inbound Rules in the advanced console            | ✓        |
| Examined properties of a firewall rule                  | ✓        |
| Located the Restore defaults option                     | ✓        |
| Created a firewall best practices reference guide       | ✓        |
| Reviewed key firewall concepts and terminology          | ✓        |

---

<video controls src="Windows Defender Firewall.mp4" title="Windows Defender Firewall"></video>


## Key Takeaways

- **Firewall is essential** - Keep it enabled on all network profiles
- **Different networks, different risks** - Public networks require stricter settings
- **App permissions matter** - Only allow necessary applications through the firewall
- **Inbound vs. Outbound** - Both directions of traffic can be controlled
- **Advanced settings** - Provide granular control for complex scenarios
- **Regular review** - Periodically check allowed apps and rules

---

## Additional Practice Ideas

1. Create a custom inbound rule to block a specific port
2. Create an outbound rule to prevent an application from accessing the internet
3. Review firewall logs to see what's being blocked
4. Export your firewall rules as a backup
5. Research how Group Policy can manage firewall settings in domain environments

---

## Troubleshooting Tips

| Issue                                              | Solution                                                       |
| :------------------------------------------------- | :------------------------------------------------------------- |
| **Can't access Windows Security**            | Search for it in Start menu; check for Windows updates         |
| **Firewall settings are grayed out**         | You need administrator privileges; contact your IT admin       |
| **App still blocked after allowing**         | Check both inbound and outbound rules; verify correct app path |
| **Accidentally blocked something important** | Review recently changed rules; restore defaults if needed      |
| **Can't find Advanced settings**             | Look in left navigation pane of Firewall & network protection  |

---

## Congratulations!

You have successfully completed the **Windows Defender Firewall** lab. You now understand:

- The three network profiles and when to use each
- How to verify firewall status for each profile
- How to manage allowed applications
- How to access advanced firewall configuration
- Best practices for firewall security

These firewall management skills are essential for maintaining the security of any Windows system in today's networked environment.

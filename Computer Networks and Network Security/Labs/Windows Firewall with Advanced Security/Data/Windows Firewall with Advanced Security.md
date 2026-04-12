
![alt text](<../Screenshots/Windows Defender.png>)

# Hands-on Lab: Windows Firewall with Advanced Security

**Estimated time needed:** 45 minutes

---

## Learning Objectives

By completing this lab, users will develop a comprehensive understanding of how to secure a Windows operating system using the real-time protection provided by Windows Firewall.

In this hands-on lab, you will review settings to enable firewall:

- **Exercise 1:** Configure Firewall Rules Using Windows Defender Firewall
- **Exercise 2:** Configure Firewall Rules Using Windows Defender Firewall with Advanced Security

Further in this hands-on lab, you will also explore few typical use cases:

| Scenario             | Type           | Description                                         |
| :------------------- | :------------- | :-------------------------------------------------- |
| **Scenario 1** | Inbound Rules  | Block Remote Desktop on the Public Network          |
| **Scenario 2** | Outbound Rules | Block Outbound Traffic for Specified Applications   |
| **Scenario 3** | Inbound Rules  | Block Web Server (HTTP) Traffic on a Public Network |
| **Scenario 4** | Inbound Rules  | Allow KMS on Domain/Private, Deny on Public         |

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About the Lab Instructions and Solutions

Microsoft Windows operating system features can vary based on the Windows edition. If completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Exercise 1: Enable Firewall on Different Network Profiles

In this exercise we will review Windows Defender Firewall configuration.

### Step 1: Open Windows Security

1. Click the Windows **Start** button
2. Select **Windows Security** from the menu

![Windows Start menu with Windows Security selected]

![alt text](<../Screenshots/Windows Start menu with Windows Security selected.png>)

### Step 2: Access Firewall & Network Protection

1. Click **Firewall & network protection**

![Security at a glance window with Firewall & network protection selected]

![alt text](<../Screenshots/Security at a glance window with Firewall & network protection selected.png>)

### Step 3: Understand Network Profiles

Here you will see the firewall status for three network profiles:

| Profile                   | Description                                                                                                              |
| :------------------------ | :----------------------------------------------------------------------------------------------------------------------- |
| **Domain network**  | Workplace networks. A computer must be part of a domain to communicate with other computers on that network.             |
| **Private network** | Discoverable networks where devices can see each other. Home networks are a good example.                                |
| **Public network**  | Non-discoverable networks where your device cannot be discovered by others. Coffee shops or libraries are good examples. |

![Firewall & network protection window showing three network profiles]

![alt text](<../Screenshots/Firewall & network protection window showing three network profiles.png>)

### Step 4: Review Domain Network Settings

1. Click **Domain network**

![Domain network highlighted]

![alt text](<../Screenshots/Domain network highlighted.png>)

2. Verify that **Windows Defender Firewall** is toggled to **On**
3. Observe the option **Incoming connections**. If you need to block all incoming domain network traffic, including traffic that is typically allowed, you can activate this option.

**Note:** You do not need to enable this option for this lab.

**Note:** If you have installed a 3rd Party anti-virus software, this option will be disabled. In this case, you can control the firewall settings only through the anti-virus software.

4. Click the **back arrow** button to return to the Firewall and network protection window

![Domain network details with firewall toggle On]

![alt text](<../Screenshots/Domain network details with firewall toggle On.png>)

### Step 5: Review Private Network Settings

1. Click **Private network**

![Private network highlighted]

![alt text](<../Screenshots/Private network highlighted.png>)

2. Verify that **Windows Defender Firewall** is toggled to **On**
3. Click the **back arrow** button to return

![Private network details]

![alt text](<../Screenshots/Private network details.png>)

### Step 6: Review Public Network Settings

1. Click **Public network**

![Public network highlighted]

![alt text](<../Screenshots/Public network highlighted.png>)

2. Verify that **Windows Defender Firewall** is toggled to **On**
3. Click the **back arrow** button to return

![Public network details]

![alt text](<../Screenshots/Public network details.png>)

### Step 7: Allow an App Through Firewall

1. Click **Allow an app through firewall**

![Allow an app through firewall highlighted]

![alt text](<../Screenshots/Allow an app through firewall highlighted.png>)

2. Scroll to locate **Google Chrome** or **Mozilla Firefox**
3. Observe the current configuration – note which networks each app is allowed on

![Allowed apps list showing Firefox permitted on Private network only]

![alt text](<../Screenshots/Allowed apps list showing Firefox permitted on Private network only.png>)

4. To allow an app on the Public network, click the **Public** box next to the app to add a checkmark
5. Click **OK** to save changes

![Allowing Mozilla Firefox on public network]

![alt text](<../Screenshots/Allowing Mozilla Firefox on public network.png>)

---

## Exercise 2: Configure Firewall Rules Using Windows Defender Firewall with Advanced Security

The first exercise used the consumer-friendly version of Windows Defender Firewall. In this exercise, we will explore **Windows Defender Firewall with Advanced Security**, which provides more in-depth configuration options.

### Step 1: Open Advanced Security

1. From the **Firewall & network protection** window, click **Advanced settings** in the left pane

![Advanced settings highlighted]

![alt text](<../Screenshots/Advanced settings highlighted.png>)

2. This opens the **Windows Defender Firewall with Advanced Security** window

### Step 2: Understand the Interface

The console is organized into three main sections:

| Section                             | Description                                                  |
| :---------------------------------- | :----------------------------------------------------------- |
| **Inbound rules**             | Determine what traffic is allowed to enter the computer      |
| **Outbound rules**            | Determine what traffic is allowed to leave the computer      |
| **Connection security rules** | Define how and when computers use IPsec to secure traffic    |
| **Monitoring**                | Track and analyze traffic allowed or blocked by the firewall |

![Windows Defender Firewall with Advanced Security interface]

![alt text](<../Screenshots/Windows Defender Firewall with Advanced Security interface.png>)

**Note:** Rules with a green checkmark are enabled; rules with a red circle indicate blocking rules.

---

## Scenario 1: Block Remote Desktop on Public Network (Inbound Rules)

Remote Desktop allows remote connection and control of a computer. Blocking it on public networks enhances security by preventing unauthorized access.

### Step 1: Create New Inbound Rule

1. In the left pane, click **Inbound Rules**
2. In the right Actions pane, click **New Rule…**

![Inbound Rules with New Rule option]

![alt text](<../Screenshots/Inbound Rules with New Rule option.png>)

### Step 2: Select Rule Type

1. Select **Port**
2. Click **Next**

![Select Rule Type - Port selected]

![alt text](<../Screenshots/Select Rule Type - Port selected.png>)

### Step 3: Specify Port

1. Select **TCP**
2. In **Specific local ports**, enter **3389** (default RDP port)
3. Click **Next**

![Specify Port - TCP port 3389]

![alt text](<../Screenshots/Specify Port - TCP port 3389.png>)

### Step 4: Specify Action

1. Select **Block the connection**
2. Click **Next**

![Action - Block the connection selected]

![alt text](<../Screenshots/Action - Block the connection selected.png>)

### Step 5: Select Profile

1. Select only **Public**
2. Deselect **Domain** and **Private**
3. Click **Next**

![Profile - Only Public selected]

![alt text](<../Screenshots/Profile - Only Public selected.png>)

### Step 6: Name the Rule

1. Enter a name: **Block Remote Desktop on Public Network**
2. Add an optional description
3. Click **Finish**

![Name the rule - Block Remote Desktop on Public Network]

![alt text](<../Screenshots/Name the rule - Block Remote Desktop on Public Network.png>)

### Step 7: Verify the Rule

1. Click **Inbound Rules**
2. Verify the new rule is enabled (red circle indicates blocking rule)

![New rule displayed in Inbound Rules list with red circle]

![alt text](<../Screenshots/New rule displayed in Inbound Rules list with red circle.png>)

---

## Scenario 2: Block Outbound Traffic for Specified Applications (Outbound Rules)

Creating outbound rules to restrict applications from sending data over the internet enhances security and controls network traffic.

### Step 1: Select Outbound Rules

1. In the left pane, click **Outbound Rules**
2. In the right Actions pane, click **New Rule…**

![Outbound Rules with New Rule option]

![alt text](<../Screenshots/Outbound Rules with New Rule option.png>)

### Step 2: Choose Rule Type

1. Select **Program**
2. Click **Next**

![Rule Type - Program selected]

![alt text](<../Screenshots/Rule Type - Program selected.png>)

### Step 3: Specify Program Path

1. Select **This program path:**
2. Browse to the application executable

**Example to block Google Chrome:**

- Navigate to `C:\Program Files (x86)\Google\Chrome\Application\`
- Select `chrome.exe`
- Click **Open**

![Program path selection for Chrome]

![alt text](<../Screenshots/Program path selection for Chrome.png>)

3. Click **Next**

### Step 4: Select Action

1. Select **Block the connection**
2. Click **Next**

### Step 5: Specify Profile

1. Check all profiles (**Domain, Private, and Public**) to apply in all scenarios
2. Click **Next**

### Step 6: Name the Rule

1. Enter a name: **Block Chrome Internet Access**
2. Add an optional description
3. Click **Finish**

![Name the rule - Block Chrome Internet Access]

![alt text](<../Screenshots/Name the rule - Block Chrome Internet Access.png>)

### Step 7: Verify the Rule

1. Open the blocked application and try to access the internet
2. You should not be able to connect (confirms rule is working)
3. To disable: return to Outbound Rules, right-click the rule, and select **Disable Rule**

---

## Scenario 3: Block Web Server (HTTP) Traffic on Public Network (Inbound Rules)

Blocking HTTP traffic when connected to a public network ensures web server services are not exposed to potential threats.

### Step 1: Create New Inbound Rule

1. In the left pane, click **Inbound Rules**
2. In the right Actions pane, click **New Rule…**

### Step 2: Select Rule Type

1. Select **Port**
2. Click **Next**

### Step 3: Specify Port

1. Select **TCP**
2. In **Specific local ports**, enter **80** (default HTTP port)
3. Click **Next**

![Specify Port - TCP port 80]

![alt text](<../Screenshots/Specify Port - TCP port 80.png>)

### Step 4: Specify Action

1. Select **Block the connection**
2. Click **Next**

### Step 5: Select Profile

1. Check only **Public**
2. Uncheck **Domain** and **Private**
3. Click **Next**

![Profile - Only Public selected]

![alt text](<../Screenshots/Profile - Only Public selected.png>)




### Step 6: Name the Rule

1. Enter a name: **Block HTTP on Public Network**
2. Add an optional description
3. Click **Finish**

---

## Scenario 4: Configure Key Management Service Rules (Inbound Rules)

KMS (Key Management Service) is used to activate Microsoft products within organizations. We'll configure it to allow on Domain/Private networks but deny on Public networks.

### Step 1: Locate KMS Rule

1. In **Inbound Rules**, scroll to find **Key Management Service (TCP-In)**
2. Note the current status (Enabled column may say "No," Action column says "Allow")

![Key Management Service inbound rule in list]

![alt text](<../Screenshots/Key Management Service inbound rule in list.png>)

### Step 2: Examine KMS Rule Properties

1. Double-click the **Key Management Service (TCP-In)** rule
2. Review the **General** tab (name, description, action)

![Key Management Service Properties - General tab]

![alt text](<../Screenshots/Key Management Service Properties - General tab.png>)

### Step 3: Modify Profile Settings

1. Click the **Advanced** tab
2. Note that **Domain, Private, and Public** are all selected

![Advanced tab showing all three profiles selected]

![alt text](<../Screenshots/Advanced tab showing all three profiles selected.png>)

3. Click **Public** to remove the checkmark
4. Click **Apply**, then **OK**

![Public profile removed - only Domain and Private selected]



### Step 4: Create Blocking Rule for Public Network

1. Right-click the **Key Management Service (TCP-In)** rule
2. Select **Copy**
3. Press **Ctrl+V** to paste (creates duplicate rule)

![Copy and paste to create new rule]

![alt text](<../Screenshots/Copy and paste to create new rule.png>)

### Step 5: Configure the New Rule to Block

1. Double-click the new **Key Management Service (TCP-In)** rule
2. On **General** tab, select **Block the connection**
3. Click **Apply**

![New rule - Block the connection selected]

![alt text](<../Screenshots/New rule - Block the connection selected.png>)

### Step 6: Set Profile for Blocking Rule

1. Click the **Advanced** tab
2. Click **Domain** and **Private** to remove checkmarks
3. Click **Public** to add a checkmark
4. Click **OK**

![Advanced tab - Only Public selected for blocking rule]



### Step 7: Enable Both Rules

1. Right-click the first KMS rule (Allow - Domain/Private)
2. Select **Enable Rule**
3. Right-click the second KMS rule (Block - Public)
4. Select **Enable Rule**

### Step 8: Verify Configuration

Observe the rule status indicators:

- **Green checkmark**: Allow rule enabled (Domain/Private)
- **Red circle with line**: Block rule enabled (Public)

![Both KMS rules enabled with proper indicators]

---

## Summary of Scenarios

| Scenario    | Rule Type | Port/Program    | Action      | Profile                                    | Purpose                                      |
| :---------- | :-------- | :-------------- | :---------- | :----------------------------------------- | :------------------------------------------- |
| **1** | Inbound   | Port 3389 (RDP) | Block       | Public only                                | Prevent remote desktop on untrusted networks |
| **2** | Outbound  | Chrome.exe      | Block       | All                                        | Prevent specific app from accessing internet |
| **3** | Inbound   | Port 80 (HTTP)  | Block       | Public only                                | Block web server exposure on public networks |
| **4** | Inbound   | KMS service     | Allow/Block | Allow: Domain/Private`<br>`Block: Public | Control activation service by network type   |

---

## Key Takeaways

| Principle                       | Description                                                                |
| :------------------------------ | :------------------------------------------------------------------------- |
| **Least Privilege**       | Only allow necessary traffic; block everything else                        |
| **Profile Awareness**     | Apply stricter rules on Public networks, more permissive on Domain/Private |
| **Specific over General** | Create specific rules rather than broad ones whenever possible             |
| **Documentation**         | Use descriptive names and descriptions for all rules                       |

---

## Troubleshooting Tips

| Issue                                     | Possible Solution                                                                    |
| :---------------------------------------- | :----------------------------------------------------------------------------------- |
| **Application can't connect**       | Check if outbound rule is blocking; verify rule order (block takes precedence)       |
| **Rule not applying**               | Run `gpupdate /force` from command prompt; verify profile matches network location |
| **Can't create rule**               | Ensure you have administrator privileges                                             |
| **Multiple rules conflicting**      | Review rule order; most specific rule typically applies                              |
| **Remote Desktop still accessible** | Verify port 3389 is correct; check if rule is enabled                                |

---

## Summary

In this hands-on lab, you have:

| Activity                                                            | Completed |
| :------------------------------------------------------------------ | :-------- |
| Reviewed firewall settings for Domain, Private, and Public networks | ✓        |
| Configured app permissions through firewall                         | ✓        |
| Navigated Windows Defender Firewall with Advanced Security          | ✓        |
| Created inbound rule to block RDP on public networks                | ✓        |
| Created outbound rule to block application internet access          | ✓        |
| Created inbound rule to block HTTP on public networks               | ✓        |
| Modified existing KMS rule for profile-specific access              | ✓        |
| Created complementary blocking rule for KMS                         | ✓        |
| Enabled and verified rule functionality                             | ✓        |

---

## Congratulations!

You have successfully completed the **Windows Firewall with Advanced Security** lab. You now know how to:

- Configure Windows Firewall for different network profiles
- Create inbound and outbound rules
- Implement profile-specific security controls
- Manage application and port-based rules
- Create complementary allow/block rules for the same service

These firewall management skills are essential for securing Windows systems in both home and enterprise environments.

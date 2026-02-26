
![alt text](<../Screenshots/Windows Defender.png>)

# Hands-on Lab: Windows Firewall with Advanced Security

**Estimated time needed:** 45 minutes

---

## About This Lab

In this lab, we will explore how to secure a Windows operating system using the real-time protection provided by Windows Firewall. You will learn to configure firewall rules for different network profiles and implement security controls for various real-world scenarios.

In this hands-on lab, you will:

- Review firewall settings for different network profiles
- Configure inbound and outbound firewall rules
- Implement security controls for specific applications and services
- Apply profile-specific firewall configurations

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About the Lab Instructions and Solutions

Microsoft Windows operating system features can vary based on the Windows edition. If completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Exercise 1: Enable Firewall on Different Network Profiles

In this exercise, we will review Windows Defender Firewall configuration and understand the three network profile types.

### Step 1: Open Windows Security

1. Click the Windows **Start** button
2. Select **Windows Security** from the menu

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Windows Security selected from the Start menu.png>)

### Step 2: Access Firewall & Network Protection

1. Click **Firewall & network protection**

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Security at a glance window with Firewall & network protection selected.png>)

### Step 3: Understand Network Profiles

Here you will see the firewall status for three network profiles:

| Profile                   | Description                                                                                             |
| :------------------------ | :------------------------------------------------------------------------------------------------------ |
| **Domain network**  | Workplace networks where a computer must be part of the domain to communicate with other computers      |
| **Private network** | Discoverable networks where only devices on that network can discover each other (e.g., home networks)  |
| **Public network**  | Non-discoverable networks where your device cannot be discovered by others (e.g., coffee shop, library) |

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Firewall & network protection window showing three network profiles.png>)

### Step 4: Review Domain Network Settings

1. Click **Domain network**
2. Verify that **Windows Defender Firewall** is toggled to **On**
3. Observe the **Incoming connections** option (note: this blocks all incoming traffic if enabled)
4. Click the back arrow to return

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Domain network details with firewall toggle On.png>)

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Domain network details with firewall toggle On back.png>)

### Step 5: Review Private Network Settings

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Private network details with firewall toggle On.png>)

1. Click **Private network**
2. Verify that **Windows Defender Firewall** is toggled to **On**
3. Click the back arrow to return

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Windows Defender Firewall is toggled to On.png>)

### Step 6: Review Public Network Settings

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Public network details with firewall toggle On.png>)

1. Click **Public network**
2. Verify that **Windows Defender Firewall** is toggled to **On**
3. Click the back arrow to return

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Public network details with firewall toggle On back.png>)

### Step 7: Allow an App Through Firewall

1. Click **Allow an app through firewall**

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Allow an app through firewall highlighted.png>)

2. Scroll to locate **Google Chrome** or **Mozilla Firefox**
3. Observe the current configuration (note which networks each app is allowed on)

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Allowed apps list showing Firefox permitted on Private network only.png>)

4. Click the **Public** box next to Firefox to add a checkmark
5. Click **OK** to save changes

*Users will now be able to use Mozilla Firefox on the public network*

![alt text](<../Screenshots/Exercise 1 - Enable Firewall on different Network Profiles/Allowing Mozilla Firefox on public network.png>)

---

## Exercise 2: Windows Firewall with Advanced Security

The first exercise used the consumer-friendly version of Windows Defender Firewall. In this exercise, we will explore **Windows Defender Firewall with Advanced Security**, which provides more in-depth configuration options.

![alt text](<../Screenshots/Exercise 2 - Windows Firewall with Advanced Security/Inbound rules list with New Rule option.png>)

### Step 1: Open Advanced Security

![alt text](<../Screenshots/Exercise 2 - Windows Firewall with Advanced Security/Click Firewall & network protection.png>)

1. From the **Firewall & network protection** window, click **Advanced settings** in the left pane

![alt text](<../Screenshots/Exercise 2 - Windows Firewall with Advanced Security/Advanced settings highlighted in left pane.png>)

2. This opens the **Windows Defender Firewall with Advanced Security** window

### Step 2: Understand the Interface

The console is organized into three main sections:

| Section                             | Description                                                  |
| :---------------------------------- | :----------------------------------------------------------- |
| **Inbound rules**             | Determine what traffic is allowed to enter the computer      |
| **Outbound rules**            | Determine what traffic is allowed to leave the computer      |
| **Connection security rules** | Define how and when computers use IPsec to secure traffic    |
| **Monitoring**                | Track and analyze traffic allowed or blocked by the firewall |

![Windows Defender Firewall with Advanced Security main interface]

*Note: Rules with a green checkmark are enabled; rules without a checkmark are available but not enabled*

---

## Scenario 1: Block Remote Desktop on Public Network (Inbound Rules)

The Remote Desktop feature allows remote connection and control of a computer. Blocking it on public networks enhances security by preventing unauthorized access.

### Step 1: Create New Inbound Rule

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 1 - Block Remote Desktop on the Public Network Using Windows Firewall (Inbound Rules)/Opens the Windows Defender Firewall with Advanced Security window.png>)

1. In the left pane, click **Inbound Rules**
2. In the right pane, click **New Rule…**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 1 - Block Remote Desktop on the Public Network Using Windows Firewall (Inbound Rules)/Create New Inbound Rule.png>)

### Step 2: Select Rule Type

1. Select **Port**
2. Click **Next**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 1 - Block Remote Desktop on the Public Network Using Windows Firewall (Inbound Rules)/Select Rule Type - Port selected.png>)

### Step 3: Specify Port

1. Select **TCP**
2. In **Specific local ports**, enter **3389** (default RDP port)
3. Click **Next**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 1 - Block Remote Desktop on the Public Network Using Windows Firewall (Inbound Rules)/Specify Port - TCP port 3389.png>)

### Step 4: Specify Action

1. Select **Block the connection**
2. Click **Next**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 1 - Block Remote Desktop on the Public Network Using Windows Firewall (Inbound Rules)/Action - Block the connection selected.png>)

### Step 5: Select Profile

1. Select only **Public**
2. Deselect **Domain** and **Private**
3. Click **Next**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 1 - Block Remote Desktop on the Public Network Using Windows Firewall (Inbound Rules)/Profile - Only Public selected.png>)

### Step 6: Name the Rule

1. Enter a name: **Block Remote Desktop on Public Network**
2. Add an optional description
3. Click **Finish**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 1 - Block Remote Desktop on the Public Network Using Windows Firewall (Inbound Rules)/Name the rule - Block Remote Desktop on Public Network.png>)

### Step 7: Verify the Rule

1. Click **Inbound Rules**
2. Verify the new rule is enabled (red circle indicates blocking rule)

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 1 - Block Remote Desktop on the Public Network Using Windows Firewall (Inbound Rules)/New rule displayed in Inbound Rules list with red circle.png>)

---

## Scenario 2: Block Outbound Traffic for Specified Applications (Outbound Rules)

Creating outbound rules to restrict applications from sending data over the internet enhances security and controls network traffic.

### Step 1: Select Outbound Rules

1. In the left pane, click **Outbound Rules**
2. In the right pane, click **New Rule…**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 2 - Block Outbound Traffic for Specified Applications (Outbound Rules)/Outbound Rules with New Rule option.png>)

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 2 - Block Outbound Traffic for Specified Applications (Outbound Rules)/New Rule…..png>)

### Step 2: Choose Rule Type

1. Select **Program**
2. Click **Next**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 2 - Block Outbound Traffic for Specified Applications (Outbound Rules)/Rule Type - Program selected.png>)

### Step 3: Specify Program Path

1. Select **This program path:**
2. Browse to the application executable

*For example, to block Google Chrome:*

- Navigate to `C:\Program Files (x86)\Google\Chrome\Application\`
- Select `chrome.exe`
- Click **Open**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 2 - Block Outbound Traffic for Specified Applications (Outbound Rules)/Program path selection for Chrome.png>)

1. Click **Next**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 2 - Block Outbound Traffic for Specified Applications (Outbound Rules)/Click Next.png>)

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

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 2 - Block Outbound Traffic for Specified Applications (Outbound Rules)/Name the rule - Block Chrome Internet Access.png>)

### Step 7: Verify the Rule

1. Open Chrome browser and try to access the internet
2. You should not be able to connect (confirms rule is working)
3. To disable: return to Outbound Rules, right-click the rule, and select **Disable Rule**

---

## Scenario 3: Block Web Server (HTTP) Traffic on Public Network (Inbound Rules)

Blocking HTTP traffic when connected to a public network ensures web server services are not exposed to potential threats.

### Step 1: Create New Inbound Rule

1. In the left pane, click **Inbound Rules**
2. In the right pane, click **New Rule…**

### Step 2: Select Rule Type

1. Select **Port**
2. Click **Next**

### Step 3: Specify Port

1. Select **TCP**
2. In **Specific local ports**, enter **80** (default HTTP port)
3. Click **Next**

### Step 4: Specify Action

1. Select **Block the connection**
2. Click **Next**

### Step 5: Select Profile

1. Check only **Public**
2. Uncheck **Domain** and **Private**
3. Click **Next**

### Step 6: Name the Rule

1. Enter a name: **Block HTTP on Public Network**
2. Add an optional description
3. Click **Finish**

---

## Scenario 4: Configure Key Management Service Rules (Inbound Rules)

KMS (Key Management Service) is used to activate Microsoft products within organizations. We'll configure it to allow on Domain/Private networks but deny on Public networks.

### Step 1: Locate KMS Rule

1. In **Inbound Rules**, scroll to find **Key Management Service (TCP-In)**
2. Note the current status (Enabled column says "No," Action column says "Allow")

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 4 (Inbound Rules) - Allow Key Management Service on the Domain and Private network, and deny the connection on the Public network/Key Management Service inbound rule in list.png>)

### Step 2: Examine KMS Rule Properties

1. Double-click the **Key Management Service (TCP-In)** rule
2. Review the **General** tab (name, description, action)

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 4 (Inbound Rules) - Allow Key Management Service on the Domain and Private network, and deny the connection on the Public network/Key Management Service Properties - General tab.png>)

### Step 3: Modify Profile Settings

1. Click the **Advanced** tab
2. Note that **Domain, Private, and Public** are all selected

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 4 (Inbound Rules) - Allow Key Management Service on the Domain and Private network, and deny the connection on the Public network/Advanced tab showing all three profiles selected.png>)

3. Click **Public** to remove the checkmark
4. Click **Apply**, then **OK**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 4 (Inbound Rules) - Allow Key Management Service on the Domain and Private network, and deny the connection on the Public network/Public profile removed - only Domain and Private selected.png>)

### Step 4: Create Blocking Rule for Public Network

1. Right-click the **Key Management Service (TCP-In)** rule
2. Select **Copy**
3. Press **Ctrl+V** to paste (creates duplicate rule)

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 4 (Inbound Rules) - Allow Key Management Service on the Domain and Private network, and deny the connection on the Public network/Copy and paste to create new rule.png>)

### Step 5: Configure the New Rule to Block

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 4 (Inbound Rules) - Allow Key Management Service on the Domain and Private network, and deny the connection on the Public network/Key Management Service (TCP-In) inbound rule.png>)

1. Double-click the new **Key Management Service (TCP-In)** rule
2. On **General** tab, select **Block the connection**
3. Click **Apply**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 4 (Inbound Rules) - Allow Key Management Service on the Domain and Private network, and deny the connection on the Public network/New rule - Block the connection selected.png>)

### Step 6: Set Profile for Blocking Rule

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 4 (Inbound Rules) - Allow Key Management Service on the Domain and Private network, and deny the connection on the Public network/Advanced tab - Only Public selected for blocking rule.png>)

1. Click the **Advanced** tab
2. Click **Domain** and **Private** to remove checkmarks
3. Click **Public** to add a checkmark
4. Click **OK**

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 4 (Inbound Rules) - Allow Key Management Service on the Domain and Private network, and deny the connection on the Public network/Click the Domain and Private boxes to remove the checkmarks.png>)

### Step 7: Enable Both Rules

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 4 (Inbound Rules) - Allow Key Management Service on the Domain and Private network, and deny the connection on the Public network/Right-click each Key Management Service (TCP-In) rule and click Enable rule.png>)

1. Right-click the first KMS rule (Allow - Domain/Private)
2. Select **Enable Rule**
3. Right-click the second KMS rule (Block - Public)
4. Select **Enable Rule**

### Step 8: Verify Configuration

Observe the rule status indicators:

- **Green checkmark**: Allow rule enabled (Domain/Private)
- **Red circle with line**: Block rule enabled (Public)

![alt text](<../Screenshots/Typical use cases with Windows Firewall Advanced Security options/Scenario 4 (Inbound Rules) - Allow Key Management Service on the Domain and Private network, and deny the connection on the Public network/Both KMS rules enabled with proper indicators.png>)

---

## Summary of Scenarios

| Scenario | Rule Type | Port/Program    | Action      | Profile                             | Purpose                                      |
| :------- | :-------- | :-------------- | :---------- | :---------------------------------- | :------------------------------------------- |
| 1        | Inbound   | Port 3389 (RDP) | Block       | Public only                         | Prevent remote desktop on untrusted networks |
| 2        | Outbound  | Chrome.exe      | Block       | All                                 | Prevent specific app from accessing internet |
| 3        | Inbound   | Port 80 (HTTP)  | Block       | Public only                         | Block web server exposure on public networks |
| 4        | Inbound   | KMS service     | Allow/Block | Allow: Domain/Private Block: Public | Control activation service by network type   |

---

## Best Practices for Firewall Configuration

### Rule Design Principles

| Principle                       | Description                                                                |
| :------------------------------ | :------------------------------------------------------------------------- |
| **Least Privilege**       | Only allow necessary traffic; block everything else                        |
| **Profile Awareness**     | Apply stricter rules on Public networks, more permissive on Domain/Private |
| **Specific over General** | Create specific rules rather than broad ones whenever possible             |
| **Documentation**         | Use descriptive names and descriptions for all rules                       |

### Rule Management Tips

| Tip                         | Benefit                                        |
| :-------------------------- | :--------------------------------------------- |
| Group related rules         | Easier management and troubleshooting          |
| Test before full deployment | Prevents unintended access issues              |
| Regular rule audits         | Removes obsolete rules, reduces attack surface |
| Monitor firewall logs       | Detects blocked attack attempts                |

---

## Troubleshooting Common Issues

| Issue                                     | Possible Solution                                                                    |
| :---------------------------------------- | :----------------------------------------------------------------------------------- |
| **Application can't connect**       | Check if outbound rule is blocking; verify rule order (block takes precedence)       |
| **Rule not applying**               | Run `gpupdate /force` from command prompt; verify profile matches network location |
| **Can't create rule**               | Ensure you have administrator privileges                                             |
| **Multiple rules conflicting**      | Review rule order; most specific rule typically applies                              |
| **Remote Desktop still accessible** | Verify port 3389 is correct; check if rule is enabled                                |

---

## Verification Commands

Use these commands to verify firewall configuration:

```cmd
# View all firewall rules
netsh advfirewall firewall show rule name=all

# View specific rule
netsh advfirewall firewall show rule name="Block Remote Desktop on Public Network"

# View firewall status for all profiles
netsh advfirewall show allprofiles

# Reset firewall to defaults
netsh advfirewall reset
```

---

## Congratulations

In this hands-on lab, you have:

| Task                                                                | Completed |
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

<video controls src="Windows Firewall with Advanced Security.mp4" title="Windows Firewall with Advanced Security"></video>

### Key Takeaways

- **Network profiles matter** – Apply different security rules based on network trust level
- **Inbound vs. Outbound** – Control both incoming and outgoing traffic
- **Port-based rules** – Effective for blocking specific services
- **Program-based rules** – Useful for controlling application behavior
- **Rule copying** – Efficient way to create complementary rules
- **Testing is essential** – Always verify rules work as intended

---

## Next Steps

After completing this lab, you should be comfortable with:

- Configuring Windows Firewall for different network profiles
- Creating inbound and outbound rules
- Implementing profile-specific security controls
- Managing application and port-based rules

Continue to the next lab to explore additional Windows security features.

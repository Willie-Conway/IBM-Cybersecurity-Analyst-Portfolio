![alt text](<../Screenshots/Windows Defender.png>)


# Lab: Configuring Firewalls in Microsoft Windows

**Estimated time needed:** 20 minutes

---

## Introduction

After you complete this hands-on lab, you will be able to create an outbound rule within a Microsoft Windows Firewall. You will know how to block specific IP addresses, using the example of blocking the IP address of the website Jharkhand State Cricket Association (https://www.cricjharkhand.org/). Understanding how to configure outbound rules in Windows Firewall is essential for managing and securing your network traffic effectively.

**Note:** If trying these lab instructions on your own computer, your screens might look slightly different than what you see here. Also, remember to disable or remove any rules you create after completing the lab.

---

## Learning Objectives

By the end of this session, you will be able to:

- Open and navigate the Windows Firewall interface
- Create a new outbound rule in Windows Firewall
- Configure custom settings for outbound rules
- Block specific IP addresses using outbound rules
- Verify the functionality of the newly created rule
- Enable and disable firewall rules

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About the Lab Instructions and Solutions

Microsoft Windows operating system features can vary based on the Windows edition. If completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Understanding Outbound Rules

| Rule Type                | Description                                                |
| :----------------------- | :--------------------------------------------------------- |
| **Inbound Rules**  | Control traffic coming INTO your computer from the network |
| **Outbound Rules** | Control traffic leaving your computer to the network       |

**Why block specific IP addresses?**

- Prevent access to malicious websites
- Block known command and control (C2) servers
- Enforce corporate internet usage policies
- Prevent data exfiltration to unauthorized destinations

---

## Task 1: Open and Navigate the Windows Firewall Interface

### Step 1: Open Control Panel

There are two ways to open Control Panel:

**Method 1: Run dialog**

1. Press **Win + R** on your keyboard
2. Type `control panel` and press **Enter**

**Method 2: Start menu**

1. Click the **Start** button
2. Type **Control Panel** in the search bar
3. Click on **Control Panel**

![Control Panel in Start menu]

### Step 2: Navigate to Windows Defender Firewall

1. In Control Panel, click **System and Security**

![System and Security in Control Panel]

2. Click **Windows Defender Firewall**

![Windows Defender Firewall in System and Security]

---

## Task 2: Create a New Outbound Rule in Windows Firewall

### Step 3: Open Advanced Settings

1. In the left pane of Windows Defender Firewall, click **Advanced settings**

![Windows Defender Firewall with Advanced settings highlighted]

![alt text](<../Screenshots/Windows Defender Firewall with Advanced settings highlighted.jpg>)

### Step 4: Select Outbound Rules

1. In the left navigation pane, click **Outbound Rules**

![Outbound Rules selected]

![alt text](<../Screenshots/Outbound Rules selected.jpg>)

### Step 5: Start New Rule Wizard

1. In the right Actions pane, click **New Rule...**

![New Rule option in Actions pane]

![alt text](<../Screenshots/New Rule option in Actions pane.jpg>)

---

## Task 3: Configure Custom Settings

### Step 6: Select Custom Rule Type

1. Select **Custom** as the rule type
2. Click **Next**

![Rule Type - Custom selected]

![alt text](<../Screenshots/Rule Type - Custom selected.jpg>)

### Step 7: Select All Programs

1. Select **All programs**
2. Click **Next**

![Program selection - All programs]

![alt text](<../Screenshots/Program selection - All programs.jpg>)

### Step 8: Configure Protocol and Ports

1. Keep the default onscreen parameters (protocol type: Any)
2. Click **Next**

![Protocol and Ports - default settings]

![alt text](<../Screenshots/Protocol and Ports - default settings.jpg>)

**Explanation:** We're leaving protocol and ports as "Any" because we want to block all traffic to the specific IP address, regardless of protocol or port.

---

## Task 4: Configure Scope to Block Specific IP Address

### Step 9: Locate the IP Address to Block

Before creating the rule, you need to find the IP address of the website you want to block.

**Finding the IP address of cricjharkhand.org:**

1. Open Command Prompt (search for `cmd`)

```cmd
nslookup www.cricjharkhand.org
```

Or use ping:

```cmd
ping www.cricjharkhand.org
```

**Example output:**

```
Non-authoritative answer:
Name:    www.cricjharkhand.org
Address:  103.xxx.xxx.xxx
```

Note the IP address(es) returned. Websites may have multiple IP addresses.

### Step 10: Configure Scope

1. In the **Which remote IP addresses does this rule apply to?** section
2. Select **These IP addresses**

![Scope configuration with These IP addresses selected]

![alt text](<../Screenshots/Scope configuration with These IP addresses selected.jpg>)

3. Click **Add** to add the IP address

![Add IP address button]


1. In the **IP Address** dialog:
   - Select **This IP address or subnet**
   - Enter the IP address of the website (e.g., `103.xxx.xxx.xxx`)
   - Click **OK**

![Add IP address dialog]

![alt text](<../Screenshots/Add IP address dialog.jpg>)


5. If the website has multiple IP addresses, add them all
6. Click **Next**

![IP addresses added to scope]

![alt text](<../Screenshots/IP addresses added to scope.jpg>)

### Step 11: Specify Action

1. Select **Block the connection**
2. Click **Next**

![Action - Block the connection]

![alt text](<../Screenshots/Action - Block the connection.jpg>)

### Step 12: Specify Profile

1. Select all three profiles:
   - ☑ **Domain** (when connected to domain network)
   - ☑ **Private** (when connected to home/private network)
   - ☑ **Public** (when connected to public/untrusted network)
2. Click **Next**

![Profile selection with all three profiles checked]

![alt text](<../Screenshots/Profile selection with all three profiles checked.jpg>)

### Step 13: Name the Rule

1. Enter a name for the rule: **Block CricJharkhand Website**
2. (Optional) Enter a description: **Blocks all outbound traffic to www.cricjharkhand.org IP addresses**
3. Click **Finish**

![Rule naming - Block CricJharkhand Website]

![alt text](<../Screenshots/Rule naming - Block CricJharkhand Website.jpg>)

---

## Task 5: Verify the New Outbound Rule

### Step 14: Locate the New Rule

1. In the Outbound Rules list, scroll to find your new rule: **Block CricJharkhand Website**

![Outbound Rules list showing new rule]

![alt text](<../Screenshots/Outbound Rules list showing new rule.jpg>)

### Step 15: Verify Rule Properties

Verify that the rule shows:

| Column            | Expected Value              |
| :---------------- | :-------------------------- |
| **Name**    | Block CricJharkhand Website |
| **Enabled** | Yes (green checkmark)       |
| **Action**  | Block                       |
| **Profile** | Domain, Private, Public     |

### Step 16: Test the Rule

1. Open a web browser
2. Try to visit the blocked website: **https://www.cricjharkhand.org/**

**Expected result:** The browser will fail to load the website (may show "This site can't be reached" or connection timeout)

![Browser showing blocked website]

![alt text](<../Screenshots/Browser showing blocked website.jpg>)

3. If the website loads, verify that:
   - The IP address was correct
   - The rule is enabled
   - The profile matches your current network type

### Step 17: Verify with Command Prompt

Test connectivity to the blocked IP address:

```cmd
ping www.cricjharkhand.org
```

**Expected result:** The ping will fail (Request timed out or Destination host unreachable)

![Ping failing to blocked IP]

![alt text](<../Screenshots/Ping failing to blocked IP.jpg>)

---

## Task 6: Enable and Disable Firewall Rules

### Step 18: Disable the Rule

1. In Windows Defender Firewall with Advanced Security
2. Locate the **Block CricJharkhand Website** rule
3. Right-click on the rule
4. Select **Disable Rule**

![Disable Rule option]

![alt text](<../Screenshots/Disable Rule option.jpg>)

The rule will remain in the list but will show a gray icon, indicating it is disabled.

![Disabled rule showing gray icon]

### Step 19: Test with Rule Disabled

1. Refresh the website in your browser
2. The website should now load (if the IP address was correct and the site is accessible)

### Step 20: Re-enable the Rule

1. Right-click on the rule again
2. Select **Enable Rule**

### Step 21: Delete the Rule (Cleanup)

To completely remove the rule:

1. Right-click on the rule
2. Select **Delete**
3. Confirm deletion when prompted

![Delete Rule option]

---

## Alternative Method: Block by Domain Name (Using Hosts File)

While the firewall method blocks by IP address, another approach is using the Windows hosts file:

1. Open Notepad as Administrator
2. Open `C:\Windows\System32\drivers\etc\hosts`
3. Add the line: `127.0.0.1 www.cricjharkhand.org`
4. Save the file

This method blocks by domain name but is system-wide and doesn't require firewall rules.

---

## Common IP Address Ranges to Block

| Purpose                         | IP Range                                      |
| :------------------------------ | :-------------------------------------------- |
| **Localhost**             | 127.0.0.0/8                                   |
| **Private Networks**      | 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16     |
| **Multicast**             | 224.0.0.0/4                                   |
| **Documentation/Example** | 192.0.2.0/24, 198.51.100.0/24, 203.0.113.0/24 |

---

## Lab Completion Checklist

| Task                                          | Completed |
| :-------------------------------------------- | :-------- |
| Opened Control Panel                          | ☐        |
| Navigated to Windows Defender Firewall        | ☐        |
| Opened Advanced Settings                      | ☐        |
| Selected Outbound Rules                       | ☐        |
| Created new custom outbound rule              | ☐        |
| Selected All programs                         | ☐        |
| Configured scope with specific IP addresses   | ☐        |
| Selected Block the connection                 | ☐        |
| Selected all profiles                         | ☐        |
| Named rule "Block CricJharkhand Website"      | ☐        |
| Verified rule appears in Outbound Rules list  | ☐        |
| Tested rule by attempting to access website   | ☐        |
| Disabled rule and verified website accessible | ☐        |
| Re-enabled or deleted rule for cleanup        | ☐        |

---

## Screenshot Checklist

| Screenshot      | File Name                        | Description                     |
| :-------------- | :------------------------------- | :------------------------------ |
| New Rule        | `FW_Outbound_Rule_Created.png` | New outbound rule in list       |
| Rule Properties | `FW_Rule_Properties.png`       | Scope showing IP addresses      |
| Rule Test       | `FW_Block_Test.png`            | Browser showing blocked website |
| Rule Disabled   | `FW_Rule_Disabled.png`         | Disabled rule showing gray icon |

---

## Troubleshooting Tips

| Issue                            | Solution                                                                    |
| :------------------------------- | :-------------------------------------------------------------------------- |
| **Website still loads**    | Verify IP address is correct; website may use multiple IPs; flush DNS cache |
| **Rule not blocking**      | Check rule is enabled; verify profile matches current network               |
| **Cannot find IP address** | Use `nslookup` or `ping` from Command Prompt                            |
| **Rule doesn't appear**    | Ensure you selected Outbound Rules (not Inbound)                            |
| **Cannot create rule**     | Ensure you have administrator privileges                                    |

---

## Key Takeaways

| Concept                       | Description                                            |
| :---------------------------- | :----------------------------------------------------- |
| **Outbound Rules**      | Control traffic leaving your computer                  |
| **Custom Rule Type**    | Allows advanced configuration including IP blocking    |
| **Scope Configuration** | Specify which remote IP addresses are affected         |
| **IP Blocking**         | Prevents communication with specific IP addresses      |
| **Profile Selection**   | Apply rules to Domain, Private, and/or Public networks |
| **Rule Management**     | Enable, disable, or delete rules as needed             |

---

## Summary

In this hands-on lab, you have:

| Activity                                                | Completed |
| :------------------------------------------------------ | :-------- |
| Opened Windows Defender Firewall with Advanced Security | ✓        |
| Navigated to Outbound Rules                             | ✓        |
| Created a new custom outbound rule                      | ✓        |
| Configured rule to block specific IP addresses          | ✓        |
| Found the IP address of a website using nslookup        | ✓        |
| Set scope to block specific remote IP addresses         | ✓        |
| Named and saved the rule                                | ✓        |
| Verified the rule blocks access to the website          | ✓        |
| Disabled and re-enabled the rule                        | ✓        |
| Deleted the rule for cleanup                            | ✓        |

---

## Congratulations!

You have successfully completed the **Configuring Firewalls in Microsoft Windows** lab. You now know how to:

- Open and navigate Windows Defender Firewall
- Create custom outbound rules
- Block specific IP addresses using firewall rules
- Test and verify firewall rule functionality
- Enable, disable, and delete firewall rules

These skills are essential for network security professionals who need to control outbound traffic, block malicious destinations, and enforce security policies.

![alt text](<../Screenshots/Windows Defender.png>)

# Lab: DNS Filtering

**Estimated time:** 15 minutes

---

## Important Note

All steps must be completed in a single session. Once the virtual instance is closed, all configurations will be lost.

---

## Introduction

In this hands-on lab, you will learn how to create an outbound rule in Windows Firewall to strengthen network security by restricting DNS requests. By completing this lab, you will gain valuable skills in managing firewall rules and controlling network traffic.

**Note:** If you try these instructions on your computer, your screens might look slightly different than what you see in this lab. Also, remember to disable or remove the outbound rule after completing the lab.

---

## Learning Objectives

After completing this lab, you will be able to:

- Locate and access the Microsoft Windows Firewall interface
- Create a new outbound rule in Windows Firewall interface to block DNS traffic
- Verify the existence and effectiveness of the new outbound rule

---

## What is DNS Filtering?

**DNS (Domain Name System)** is often called the "phonebook of the internet" – it translates human-readable domain names (like www.google.com) into IP addresses that computers use to communicate.

**DNS filtering** is a security technique that blocks access to certain websites by preventing DNS resolution. By blocking DNS requests, you can:

| Benefit                         | Description                                                  |
| :------------------------------ | :----------------------------------------------------------- |
| **Block malicious sites** | Prevent access to known phishing or malware sites            |
| **Content filtering**     | Restrict access to inappropriate or non-work-related content |
| **Security enforcement**  | Prevent DNS-based data exfiltration                          |
| **Network control**       | Enforce acceptable use policies                              |

---

## Understanding DNS Ports

| Protocol                       | Port | Purpose                            |
| :----------------------------- | :--- | :--------------------------------- |
| **DNS over UDP**         | 53   | Standard DNS queries (default)     |
| **DNS over TCP**         | 53   | Zone transfers and large responses |
| **DNS over TLS (DoT)**   | 853  | Encrypted DNS queries              |
| **DNS over HTTPS (DoH)** | 443  | DNS queries over HTTPS             |

In this lab, we will block standard DNS traffic on **UDP port 53**.

---

## Task 1: Navigate to the Microsoft Windows Firewall Interface

### Step 1: Open Control Panel

1. Click the **Windows Icon** (Start button) on the taskbar
2. Type **Control Panel** in the search bar
3. Click on **Control Panel** from the search results

![Start menu with Control Panel highlighted]

![alt text](<../Screenshots/Start menu with Control Panel highlighted.jpg>)

### Step 2: Access System and Security

1. In Control Panel, click on **System and Security**

![Control Panel with System and Security highlighted]

![alt text](<../Screenshots/Control Panel with System and Security highlighted.jpg>)

### Step 3: Open Windows Defender Firewall

1. Click on **Windows Defender Firewall**

![System and Security with Windows Defender Firewall highlighted]

![alt text](<../Screenshots/System and Security with Windows Defender Firewall highlighted.jpg>)

---

## Task 2: Create a New Outbound Rule

### Step 4: Open Advanced Settings

1. In the left pane of Windows Defender Firewall, click **Advanced settings**

![Windows Defender Firewall with Advanced settings highlighted]

![alt text](<../Screenshots/Windows Defender Firewall with Advanced settings highlighted.jpg>)

This opens the **Windows Defender Firewall with Advanced Security** console.

![Windows Defender Firewall with Advanced Security window]

![alt text](<../Screenshots/Windows Defender Firewall with Advanced Security window.jpg>)

### Step 5: Select Outbound Rules

1. In the left navigation pane, click on **Outbound Rules**

![Outbound Rules selected in left pane]

![alt text](<../Screenshots/Outbound Rules selected in left pane.jpg>)

### Step 6: Start New Rule Wizard

1. In the right Actions pane, click **New Rule...**

![New Rule option in Actions pane]

![alt text](<../Screenshots/New Rule option in Actions pane.jpg>)

### Step 7: Select Rule Type

1. Select **Port** as the rule type
2. Click **Next**

![New Outbound Rule Wizard - Rule Type selection with Port selected]

![alt text](<../Screenshots/New Outbound Rule Wizard - Rule Type selection with Port selected.jpg>)

### Step 8: Configure Protocol and Ports

1. Select **UDP** as the protocol
2. Select **Specific remote ports**
3. Enter **53** in the port field
4. Click **Next**

![Protocol and Ports configuration - UDP port 53]

![alt text](<../Screenshots/Protocol and Ports configuration - UDP port 53.jpg>)

**Explanation:** DNS primarily uses UDP port 53 for standard queries. By blocking outbound traffic on this port, we prevent DNS resolution.

### Step 9: Specify Action

1. Select **Block the connection**
2. Click **Next**

![Action selection - Block the connection]

![alt text](<../Screenshots/Action selection - Block the connection.jpg>)

### Step 10: Specify Profile

1. Ensure all three profiles are selected:
   - ☑ **Domain** (when connected to domain network)
   - ☑ **Private** (when connected to private/home network)
   - ☑ **Public** (when connected to public/untrusted network)
2. Click **Next**

![Profile selection with all three profiles checked]

![alt text](<../Screenshots/Profile selection with all three profiles checked.jpg>)

**Profile Explanation:**

| Profile           | When Applied                                                           |
| :---------------- | :--------------------------------------------------------------------- |
| **Domain**  | When computer is connected to a domain network (corporate)             |
| **Private** | When computer is connected to a trusted home or private network        |
| **Public**  | When computer is connected to public networks (coffee shops, airports) |

### Step 11: Name the Rule

1. Enter a name for the rule: **Block DNS Traffic**
2. (Optional) Enter a description: **Blocks all outbound DNS requests on UDP port 53**
3. Click **Finish**

![Rule naming - Block DNS Traffic]

![alt text](<../Screenshots/Rule naming - Block DNS Traffic.jpg>)

---

## Task 3: Verify the New Outbound Rule

### Step 12: Locate the New Rule

1. In the Outbound Rules list, scroll to find your new rule: **Block DNS Traffic**

![Outbound Rules list showing Block DNS Traffic rule]

![alt text](<../Screenshots/Outbound Rules list showing Block DNS Traffic rule.jpg>)

### Step 13: Verify Rule Properties

Verify that the rule shows:

| Column                | Expected Value          |
| :-------------------- | :---------------------- |
| **Name**        | Block DNS Traffic       |
| **Enabled**     | Yes (green checkmark)   |
| **Action**      | Block                   |
| **Profile**     | Domain, Private, Public |
| **Protocol**    | UDP                     |
| **Local Port**  | Any                     |
| **Remote Port** | 53                      |

### Step 14: Test the Rule (Verify Effectiveness)

To verify that the rule is working:

**Method 1: Using Command Prompt**

1. Open Command Prompt (search for `cmd`)
2. Run the following command to attempt a DNS lookup:

```cmd
nslookup google.com
```

3. **Expected result without rule:** Returns IP addresses for google.com
4. **Expected result with rule active:** The command will time out or fail to resolve

![nslookup failing after rule applied]

**Method 2: Using Web Browser**

1. Open a web browser
2. Try to visit any website (e.g., www.google.com)
3. **Expected result:** The browser will fail to load because it cannot resolve the domain name

**Note:** You may need to flush your DNS cache for immediate effect:

```cmd
ipconfig /flushdns
```

---

## Task 4: Disable or Remove the Rule (Cleanup)

Since blocking DNS traffic will prevent internet access, it's important to disable or remove the rule after testing.

### Option 1: Disable the Rule

1. In Windows Defender Firewall with Advanced Security
2. Locate the **Block DNS Traffic** rule in Outbound Rules
3. Right-click on the rule
4. Select **Disable Rule**

![Disable Rule option]

The rule will remain in the list but will show a gray icon, indicating it is disabled.

![Disabled rule showing gray icon]

### Option 2: Delete the Rule

1. Right-click on the **Block DNS Traffic** rule
2. Select **Delete**
3. Confirm deletion when prompted

### Step 15: Verify Internet Access is Restored

1. After disabling or deleting the rule, test internet access:

```cmd
nslookup google.com
```

2. The DNS lookup should succeed, returning IP addresses

![nslookup working after rule disabled]

---

## Understanding DNS Resolution Process

```
┌─────────┐     ┌─────────┐     ┌─────────┐     ┌─────────┐
│ Browser │────▶│ DNS     │────▶│ DNS     │────▶│ Website │
│         │     │ Request │     │ Response│     │         │
└─────────┘     └─────────┘     └─────────┘     └─────────┘
                    │
                    ▼
              ┌─────────────┐
              │ DNS Server  │
              │ (Port 53)   │
              └─────────────┘

When outbound rule blocks UDP port 53:
┌─────────┐     ┌─────────┐
│ Browser │────▶│ Firewall│
│         │     │ BLOCKS  │ ✗ No DNS response
└─────────┘     └─────────┘
```

---

## Advanced DNS Filtering Scenarios

| Scenario                                 | Rule Configuration                                                   |
| :--------------------------------------- | :------------------------------------------------------------------- |
| **Block specific DNS server**      | Create rule for remote port 53 AND specific remote IP address        |
| **Allow internal DNS only**        | Create block rule, but add exception for your internal DNS server IP |
| **Block encrypted DNS**            | Create additional rules for ports 853 (DoT) and 443 (DoH)            |
| **Allow DNS but restrict queries** | Use DNS filtering services (OpenDNS, Cisco Umbrella)                 |

---

## Lab Completion Checklist

| Task                                            | Completed |
| :---------------------------------------------- | :-------- |
| Opened Control Panel                            | ☐        |
| Navigated to Windows Defender Firewall          | ☐        |
| Opened Advanced Settings                        | ☐        |
| Selected Outbound Rules                         | ☐        |
| Created new outbound rule                       | ☐        |
| Selected Port rule type                         | ☐        |
| Selected UDP protocol                           | ☐        |
| Entered remote port 53                          | ☐        |
| Selected Block the connection                   | ☐        |
| Selected all profiles (Domain, Private, Public) | ☐        |
| Named rule "Block DNS Traffic"                  | ☐        |
| Verified rule appears in Outbound Rules list    | ☐        |
| Tested rule effectiveness with nslookup         | ☐        |
| Disabled or deleted the rule                    | ☐        |
| Verified internet access restored               | ☐        |

---

## Screenshot Checklist

| Screenshot    | File Name                 | Description                               |
| :------------ | :------------------------ | :---------------------------------------- |
| New Rule      | `DNS_Rule_Created.png`  | Outbound rule "Block DNS Traffic" in list |
| Rule Test     | `DNS_Block_Test.png`    | nslookup failing after rule applied       |
| Rule Disabled | `DNS_Rule_Disabled.png` | Rule disabled or deleted                  |
| Restored Test | `DNS_Restored.png`      | nslookup working after cleanup            |

---

## Troubleshooting Tips

| Issue                                     | Solution                                                              |
| :---------------------------------------- | :-------------------------------------------------------------------- |
| **Rule not blocking DNS**           | Verify rule is enabled; check protocol (UDP, not TCP); verify port 53 |
| **Can't find rule**                 | Sort by Name; filter by Action (Block)                                |
| **nslookup still works**            | Flush DNS cache:`ipconfig /flushdns`                                |
| **Cannot disable rule**             | Ensure you have administrator privileges                              |
| **Internet still works after rule** | Browser may use DoH (DNS over HTTPS) – block port 443 as well        |

---

## Key Takeaways

| Concept                     | Description                                            |
| :-------------------------- | :----------------------------------------------------- |
| **DNS Port**          | Standard DNS uses UDP port 53                          |
| **Outbound Rule**     | Controls traffic leaving your computer                 |
| **Block Action**      | Prevents matching traffic from being sent              |
| **DNS Filtering**     | Blocks DNS resolution to control website access        |
| **Profile Selection** | Apply rules to Domain, Private, and/or Public networks |
| **Cleanup Required**  | Always disable test rules to restore normal function   |

---

## Summary

In this hands-on lab, you have:

| Activity                                     | Completed |
| :------------------------------------------- | :-------- |
| Navigated to Windows Defender Firewall       | ✓        |
| Opened Advanced Settings console             | ✓        |
| Selected Outbound Rules                      | ✓        |
| Created a new port-based outbound rule       | ✓        |
| Configured rule to block UDP port 53         | ✓        |
| Applied rule to all network profiles         | ✓        |
| Named and saved the rule                     | ✓        |
| Verified rule appears in Outbound Rules list | ✓        |
| Tested rule effectiveness with nslookup      | ✓        |
| Disabled or deleted the rule                 | ✓        |
| Verified DNS resolution restored             | ✓        |

---

## Congratulations!

You have successfully completed the **DNS Filtering** lab. You now know how to:

- Navigate to Windows Defender Firewall with Advanced Security
- Create a new outbound rule to block DNS traffic
- Configure port-based rules for network traffic filtering
- Test and verify firewall rule effectiveness
- Properly disable or remove test rules after completion

These skills are essential for network security professionals who need to control network traffic, enforce security policies, and protect against DNS-based attacks.

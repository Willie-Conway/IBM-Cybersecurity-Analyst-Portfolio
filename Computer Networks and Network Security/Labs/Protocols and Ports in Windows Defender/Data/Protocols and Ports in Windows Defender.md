
![alt text](<../Screenshots/Windows Defender.png>)

# Lab: Protocols and Ports in Windows Defender

**Estimated time needed:** 10 minutes

---

## Learning Objectives

In this hands-on lab, you will:

- Determine the protocols and ports associated with various rules used in Windows Defender

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About the Lab Instructions and Solutions

In case you try to use your physical keyboard in the lab environment, it might not produce any visible results. To avoid this issue, please use the **On-Screen Keyboard** (you can find it by searching for "On-Screen Keyboard" in the search bar at the bottom of your screen).

If search functionality doesn't work, you can also click on the Windows icon, scroll down to find **Windows Ease of Access**, click on it, and then select **On-Screen Keyboard**.

Microsoft Windows operating system features can vary based on the Windows edition. If you are completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Introduction to Protocols and Ports

Understanding protocols and ports is essential for network security:

| Protocol      | Description                                                    | Common Use                                      |
| :------------ | :------------------------------------------------------------- | :---------------------------------------------- |
| **TCP** | Transmission Control Protocol – reliable, connection-oriented | Web browsing (HTTP/HTTPS), email, file transfer |
| **UDP** | User Datagram Protocol – faster, connectionless               | Streaming, DNS, VoIP, gaming                    |

| Port Range            | Description                        |
| :-------------------- | :--------------------------------- |
| **0-1023**      | Well-known ports (system services) |
| **1024-49151**  | Registered ports (applications)    |
| **49152-65535** | Dynamic/private ports (temporary)  |

---

## Exercise: Determine Protocols and Ports for Various Inbound Rules

### Step 1: Open Windows Defender Firewall with Advanced Security

1. Click the **Search** icon (magnifying glass) on the taskbar

![Search icon on taskbar]

![alt text](<../Screenshots/Search icon on taskbar.png>)

2. Type the word **defender** in the search bar

![Search bar with "defender" typed]

![alt text](<../Screenshots/Search bar with defender typed.png>)

3. Select **Windows Defender Firewall with Advanced Security** from the search results

![Windows Defender Firewall with Advanced Security selected]

![alt text](<../Screenshots/Windows Defender Firewall with Advanced Security selected.png>)

### Step 2: Explore the Interface

The **Windows Defender Firewall with Advanced Security** window opens. Notice the key sections:

| Section               | Purpose                                         |
| :-------------------- | :---------------------------------------------- |
| **Left pane**   | Navigation: Inbound Rules, Outbound Rules, etc. |
| **Center pane** | List of rules with details                      |
| **Right pane**  | Actions available for selected item             |

![Windows Defender Firewall with Advanced Security window]

![alt text](<../Screenshots/Windows Defender Firewall with Advanced Security window.png>)

### Step 3: Select Inbound Rules

1. In the left navigation pane, click **Inbound Rules**

![Inbound Rules selected]

![alt text](<../Screenshots/Inbound Rules selected.png>)

The center pane now displays a list of all inbound firewall rules on your system.

### Step 4: Locate Firefox Rule

1. Scroll through the list of inbound rules
2. Locate an entry for **Firefox** (or another browser like Microsoft Edge or Google Chrome)
3. If multiple Firefox rules exist, select the first one

![Firefox rule in Inbound Rules list]



### Step 5: Open Rule Properties

1. Double-click the Firefox rule (or right-click and select **Properties**)

![Rule properties option]

### Step 6: View Protocols and Ports Tab

1. In the properties window, select the **Protocols and Ports** tab

![Protocols and Ports tab]

![alt text](<../Screenshots/Protocols and Ports tab.png>)

### Step 7: Examine Protocol Type

On the Protocols and Ports tab, you will see:

| Field                   | Value | Explanation            |
| :---------------------- | :---- | :--------------------- |
| **Protocol type** | UDP   | User Datagram Protocol |

**Why UDP for Firefox?**

- **UDP** is faster than TCP
- **UDP** is connectionless, meaning it doesn't establish a persistent connection
- UDP is commonly used for streaming media, video calls, and real-time applications
- Firefox uses UDP for WebRTC (Real-Time Communication) for video/audio calls and streaming

![Protocol type set to UDP]

![alt text](<../Screenshots/Protocol type set to UDP.png>)

### Step 8: Examine Local Port Setting

Look at the **Local port** field:

| Field                | Value     | Explanation                         |
| :------------------- | :-------- | :---------------------------------- |
| **Local port** | All Ports | The rule applies to all local ports |

**Why "All Ports"?**

- Firefox can communicate on any available local port
- The firewall rule allows incoming UDP traffic on any port
- This ensures Firefox can receive UDP data for WebRTC and other real-time features

![Local port set to All Ports]

### Step 9: Examine Remote Port Setting

Look at the **Remote port** field:

| Field                 | Value     | Explanation                          |
| :-------------------- | :-------- | :----------------------------------- |
| **Remote port** | All Ports | The rule applies to all remote ports |

### Step 10: Close the Properties Window

1. Click the **X** in the top-right corner of the properties window to close it

### Step 11: Examine Other Rules (Optional)

Explore other inbound rules to see different protocol and port configurations:

| Rule                                             | Protocol | Local Port | Purpose                   |
| :----------------------------------------------- | :------- | :--------- | :------------------------ |
| **File and Printer Sharing (SMB-In)**      | TCP      | 445        | File sharing              |
| **Remote Desktop (RDP-In)**                | TCP      | 3389       | Remote desktop access     |
| **World Wide Web Services (HTTP)**         | TCP      | 80         | Web server traffic        |
| **Secure World Wide Web Services (HTTPS)** | TCP      | 443        | Secure web server traffic |
| **Core Networking - DNS (UDP-In)**         | UDP      | 53         | DNS server traffic        |

### Step 12: Close Windows Defender Firewall

1. Click the **X** in the top-right corner to close Windows Defender Firewall with Advanced Security

---

## Additional Exploration: Outbound Rules

### Step 1: Select Outbound Rules

1. Reopen Windows Defender Firewall with Advanced Security (if closed)
2. Click **Outbound Rules** in the left pane

### Step 2: Find Firefox Outbound Rule

1. Locate a Firefox outbound rule
2. Double-click to view properties
3. Select the **Protocols and Ports** tab

**Observation:** Outbound rules often have different configurations than inbound rules, controlling traffic leaving your computer.

---

## Common Protocols and Ports Reference

| Service         | Protocol | Port   | Direction            |
| :-------------- | :------- | :----- | :------------------- |
| **HTTP**  | TCP      | 80     | Inbound/Outbound     |
| **HTTPS** | TCP      | 443    | Inbound/Outbound     |
| **DNS**   | UDP      | 53     | Outbound (typically) |
| **DHCP**  | UDP      | 67, 68 | Outbound/Inbound     |
| **FTP**   | TCP      | 21     | Inbound/Outbound     |
| **SSH**   | TCP      | 22     | Outbound (client)    |
| **RDP**   | TCP      | 3389   | Inbound (server)     |
| **SMB**   | TCP      | 445    | Inbound              |
| **SMTP**  | TCP      | 25     | Outbound             |
| **IMAP**  | TCP      | 143    | Outbound             |
| **POP3**  | TCP      | 110    | Outbound             |

---

## Lab Completion Checklist

| Task                                                    | Completed |
| :------------------------------------------------------ | :-------- |
| Opened Windows Defender Firewall with Advanced Security | ☐        |
| Selected Inbound Rules in left pane                     | ☐        |
| Located Firefox rule in the list                        | ☐        |
| Double-clicked to open rule properties                  | ☐        |
| Selected Protocols and Ports tab                        | ☐        |
| Identified Protocol type (UDP)                          | ☐        |
| Identified Local port setting (All Ports)               | ☐        |
| Closed properties window                                | ☐        |
| Explored additional inbound rules (optional)            | ☐        |
| Explored outbound rules (optional)                      | ☐        |
| Closed Windows Defender Firewall                        | ☐        |

---

## Screenshot Checklist

| Screenshot              | File Name                   | Description                                       |
| :---------------------- | :-------------------------- | :------------------------------------------------ |
| Protocols and Ports Tab | `WDF_Protocols_Ports.png` | Firefox rule properties showing UDP and All Ports |

---

## Key Takeaways

| Concept                  | Key Point                                                         |
| :----------------------- | :---------------------------------------------------------------- |
| **UDP Protocol**   | Faster, connectionless; used for streaming, WebRTC, DNS           |
| **TCP Protocol**   | Reliable, connection-oriented; used for web, email, file transfer |
| **Local Port**     | Port on your computer that receives traffic                       |
| **Remote Port**    | Port on the remote computer sending traffic                       |
| **All Ports**      | Rule applies regardless of which port is used                     |
| **Inbound Rules**  | Control traffic coming INTO your computer                         |
| **Outbound Rules** | Control traffic leaving your computer                             |

---

## Summary

In this hands-on lab, you have:

| Activity                                                | Completed |
| :------------------------------------------------------ | :-------- |
| Opened Windows Defender Firewall with Advanced Security | ✓        |
| Navigated to Inbound Rules                              | ✓        |
| Located a Firefox inbound rule                          | ✓        |
| Opened rule properties                                  | ✓        |
| Viewed Protocols and Ports tab                          | ✓        |
| Identified protocol type (UDP)                          | ✓        |
| Identified local port setting (All Ports)               | ✓        |
| Examined other inbound rules                            | ✓        |
| Explored outbound rules                                 | ✓        |

---

## Congratulations!

You have successfully completed the **Protocols and Ports in Windows Defender** lab. You now know how to:

- Open Windows Defender Firewall with Advanced Security
- Navigate to Inbound Rules and Outbound Rules
- Locate and examine rule properties
- Identify the protocol type (TCP vs. UDP) used by specific applications
- Identify the port configurations associated with firewall rules

These skills are essential for network security professionals who need to understand how applications communicate and how firewall rules control network traffic.

![alt text](<../Screenshots/Windows Defender.png>)

# Lab: Exploring Networking Ports and Protocols

**Estimated time needed:** 20 minutes

---

## Learning Objectives

In this hands-on lab, you will:

- Identify the protocols used by the default web browser
- Identify the protocol used when visiting a website
- Determine the computer's public IP address
- Determine the computer's private IP address

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About the Lab Instructions and Solutions

In case you try to use your physical keyboard in the lab environment, it might not produce any visible results. To avoid this issue, please use the **On-Screen Keyboard** (you can find it by searching for "On-Screen Keyboard" in the search bar at the bottom of your screen).

If search functionality doesn't work, you can also click on the Windows icon, scroll down to find **Windows Ease of Access**, click on it, and then select **On-Screen Keyboard**.

Microsoft Windows operating system features can vary based on the Windows edition. If completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Introduction

Understanding networking ports and protocols is essential for network security. This lab explores:

- **HTTP (Hypertext Transfer Protocol)** - Port 80, used for unencrypted web traffic
- **HTTPS (HTTP Secure)** - Port 443, used for encrypted web traffic
- **LDAP (Lightweight Directory Access Protocol)** - Port 389, used for directory services
- **Public vs. Private IP addresses**

---

## Exercise 1: Identify the Default Applications Used for HTTP and HTTPS Protocols

In this exercise, you will identify which applications are configured to handle HTTP and HTTPS protocols on your Windows system.

### Step 1: Open Protocol Settings

1. Click on the **Search** icon (magnifying glass) on the taskbar

![Search icon on taskbar]

![alt text](<../Screenshots/Search icon on taskbar.png>)

1. Type **protocol** in the search bar

![Search bar with "protocol" typed]

![alt text](<../Screenshots/Search bar with protocol typed.png>)

1. Select **Choose a default app for each protocol** from the search results

![Choose a default app for each protocol selected]

![alt text](<../Screenshots/Choose a default app for each protocol selected.png>)

### Step 2: Locate HTTP and HTTPS Protocols

1. Scroll through the list of protocols to find **HTTP** and **HTTPS**

![Protocol list showing HTTP and HTTPS]

2. Identify the default application for each protocol

| Protocol        | Default Application                              |
| :-------------- | :----------------------------------------------- |
| **HTTP**  | Google Chrome (or your system's default browser) |
| **HTTPS** | Google Chrome (or your system's default browser) |

### Step 3: Take Screenshot

1. Take a screenshot showing HTTP and HTTPS with their default applications
2. Save the file as `Protocols_HTTP_HTTPS.png`

**Screenshot should show:**

- The "Choose default apps by protocol" window
- HTTP protocol with its associated app
- HTTPS protocol with its associated app

![Default apps window showing HTTP and HTTPS with Chrome selected]

---

## Practice Exercise: Determine the Default Application for LDAP

**Problem:** Determine the default application for LDAP (Lightweight Directory Access Protocol).

### Solution

Follow the same steps as above:

1. In the **Choose default apps by protocol** window
2. Scroll down to find **LDAP** in the list of protocols
3. Note the default application associated with LDAP

| Protocol       | Default Application                                                  |
| :------------- | :------------------------------------------------------------------- |
| **LDAP** | Microsoft Active Directory (or your system's configured LDAP client) |

**Note:** LDAP is used for directory services like Active Directory, email client address books, and other authentication services. It typically uses port 389 for unencrypted connections and port 636 for encrypted (LDAPS) connections.

![alt text](<../Screenshots/Determine the Default Application for LDAP.png>)

---

## Exercise 2: Identify the Protocol Used When Visiting a Website

In this exercise, you will determine which protocol is used when visiting a website (www.ibm.com).

### Step 1: Open Google Chrome

1. Locate the **Google Chrome** application
2. Double-click the application to open it

![Google Chrome icon]

![alt text](<../Screenshots/Google Chrome icon.png>)

### Step 2: Navigate to a Website

1. In the address bar (search bar), type: **www.ibm.com**
2. Press **Enter**

![Chrome address bar with www.ibm.com]

![alt text](<../Screenshots/Chrome address bar with www.ibm.com.png>)

**Note:** If you get any notification while opening the website, scroll down and choose "No Thanks" and proceed.

### Step 3: View Site Information

1. Once the website loads, look for the **Site Information icon** (or lock icon) to the left of the URL in the address bar

![Site Information icon (or lock icon) in address bar]

![alt text](<../Screenshots/Site Information icon (or lock icon) in address bar.png>)

1. Click on the **Site Information icon** (or **Lock icon**)

### Step 4: Identify the Protocol

Clicking the icon reveals information about the website connection:

- A **lock icon** indicates the site is using **HTTPS** (secure, encrypted connection)
- A **"Not secure"** warning indicates **HTTP** (unencrypted connection)

For www.ibm.com, you should see:

- **Connection is secure** message
- **Certificate information** (valid, issued by a Certificate Authority)
- **Cookies** and **Site settings**

![Site information panel showing secure connection]

![alt text](<../Screenshots/Site information panel showing secure connection.png>)

### Step 5: View Certificate Details

1. Click **Connection is secure** (or similar text)
2. Click **Certificate is valid** (or similar)
3. The certificate details will appear, showing:
   - **Issued to:** www.ibm.com
   - **Issued by:** Certificate Authority
   - **Valid from:** [Date]
   - **Valid to:** [Date]

![Certificate information window]

![alt text](<../Screenshots/Certificate information window.png>)

![alt text](<../Screenshots/Locate the Google Chrome application and double-click to open.png>)

### Step 6: Take Screenshot

1. Take a screenshot showing the site information panel and protocol indicator
2. Save the file as `Website_Protocol.png`

**Screenshot should show:**

- The IBM website loaded in Chrome
- The lock icon in the address bar
- The site information panel (or certificate details)

---

## Exercise 3: Determine Your Computer's Public IP Address

In this exercise, you will find your computer's public IP address (the address visible to the internet).

### Step 1: Open a Web Browser

![alt text](<../Screenshots/Open Google Chrome (or any web browser).png>)

1. Open Google Chrome (or any web browser)

### Step 2: Search for "What is my IP"

1. In the address bar, type: **what is my ip**
2. Press **Enter**

![What is my IP search results]

![alt text](<../Screenshots/What is my IP search results.png>)

### Step 3: Use an IP Lookup Website

Alternatively, you can visit an IP lookup website:

1. Type **www.whatismyip.com** in the address bar
2. Press **Enter**

![Whatismyip.com website]

![alt text](<../Screenshots/Whatismyip.com website.png>)

### Step 4: Record Your Public IP Address

The website will display your public IP address. It should look something like:

```
Your Public IP Address: 203.0.113.45
```

**Note:** Your IP address is unique to your internet connection at this moment. It may change depending on your network location.

### Step 5: Take Screenshot

1. Take a screenshot showing your public IP address
2. Save the file as `Public_IP.png`

**Screenshot should show:**

- The whatismyip.com website (or search results)
- Your public IP address clearly visible

---

## Exercise 4: Determine Your Computer's Private IP Address

In this exercise, you will find your computer's private IP address (the address used within your local network).

### Step 1: Open Command Prompt

1. Click the **Search** icon on the taskbar
2. Type **cmd** or **Command Prompt**
3. Click **Command Prompt** from the search results

![Command Prompt in search results]

![alt text](<../Screenshots/Command Prompt in search results.png>)

![alt text](<../Screenshots/Command Prompt in search results_2.png>)

### Step 2: Run ipconfig Command

1. In the Command Prompt window, type:

```cmd
ipconfig
```

2. Press **Enter**

![ipconfig command output]

![alt text](<../Screenshots/ipconfig command output.png>)

![alt text](<../Screenshots/ipconfig command output_2.png>)

### Step 3: Locate Your Private IP Address

Scroll through the output to find your active network adapter. Look for:

| Adapter Type               | Look For                                  |
| :------------------------- | :---------------------------------------- |
| **Ethernet (wired)** | Ethernet adapter or Local Area Connection |
| **Wi-Fi (wireless)** | Wireless LAN adapter Wi-Fi                |
| **VPN**              | Any adapter showing VPN connection        |

Under your active adapter, locate:

- **IPv4 Address** or **IPv4 Address.** - This is your private IP address
- Typical private IP ranges:
  - **192.168.x.x** (most common)
  - **10.x.x.x**
  - **172.16.x.x - 172.31.x.x**

**Example output:**

```
Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  . : home.local
   IPv4 Address. . . . . . . . . . . : 192.168.1.105
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.1.1
```

### Step 4: Take Screenshot

1. Take a screenshot showing the ipconfig output with your private IP address
2. Save the file as `Private_IP.png`

**Screenshot should show:**

- Command Prompt window
- `ipconfig` command and output
- IPv4 Address clearly visible

---

## Alternative: Find Private IP via Settings (Windows 10/11)

1. Open **Settings** (Windows key + I)
2. Click **Network & Internet**
3. Click **Status** (left menu)
4. Click **Properties** under your active network connection
5. Look for **IPv4 address** under **Properties**

![Network settings showing IP address]

---

## Exercise 5: Common Ports and Protocols Reference

For your reference, review these common port assignments:

| Port  | Protocol | Service                               | Description                     |
| :---- | :------- | :------------------------------------ | :------------------------------ |
| 20,21 | FTP      | File Transfer Protocol                | File transfer (control & data)  |
| 22    | SSH      | Secure Shell                          | Secure remote administration    |
| 23    | Telnet   | Telnet                                | Unsecured remote administration |
| 25    | SMTP     | Simple Mail Transfer Protocol         | Email sending                   |
| 53    | DNS      | Domain Name System                    | Domain name resolution          |
| 80    | HTTP     | Hypertext Transfer Protocol           | Unsecured web traffic           |
| 110   | POP3     | Post Office Protocol                  | Email retrieval                 |
| 123   | NTP      | Network Time Protocol                 | Time synchronization            |
| 143   | IMAP     | Internet Message Access Protocol      | Email retrieval                 |
| 389   | LDAP     | Lightweight Directory Access Protocol | Directory services              |
| 443   | HTTPS    | HTTP Secure                           | Encrypted web traffic           |
| 445   | SMB      | Server Message Block                  | File sharing                    |
| 636   | LDAPS    | LDAP over SSL                         | Encrypted directory services    |
| 3389  | RDP      | Remote Desktop Protocol               | Remote desktop access           |

---

## Summary

In this hands-on lab, you have:

| Activity                                                     | Completed |
| :----------------------------------------------------------- | :-------- |
| Located default applications for HTTP and HTTPS protocols    | ☐        |
| Found the default application for LDAP (practice exercise)   | ☐        |
| Visited www.ibm.com and identified the protocol used (HTTPS) | ☐        |
| Viewed site information and certificate details              | ☐        |
| Determined your computer's public IP address                 | ☐        |
| Determined your computer's private IP address using ipconfig | ☐        |
| Reviewed common ports and protocols                          | ☐        |

---

## Screenshot Checklist

| Screenshot       | File Name                    | Description                          |
| :--------------- | :--------------------------- | :----------------------------------- |
| Default Apps     | `Protocols_HTTP_HTTPS.png` | HTTP and HTTPS default applications  |
| Website Protocol | `Website_Protocol.png`     | IBM.com with lock icon showing HTTPS |
| Public IP        | `Public_IP.png`            | Your public IP address               |
| Private IP       | `Private_IP.png`           | Your private IP from ipconfig        |

---

<video controls src="Exploring Networking Ports and Protocols.mp4" title="Exploring Networking Ports and Protocols"></video>


## Key Takeaways

| Concept                     | Description                                                  |
| :-------------------------- | :----------------------------------------------------------- |
| **HTTP vs HTTPS**     | HTTP is unencrypted (port 80); HTTPS is encrypted (port 443) |
| **Lock Icon**         | Indicates secure HTTPS connection with valid certificate     |
| **Public IP**         | Unique internet-facing address assigned by ISP               |
| **Private IP**        | Local network address (192.168.x.x, 10.x.x.x, 172.16-31.x.x) |
| **Default Protocols** | Applications can be assigned to handle specific protocols    |
| **LDAP**              | Port 389, used for directory services and authentication     |

---

## Troubleshooting Tips

| Issue                                               | Solution                                                                       |
| :-------------------------------------------------- | :----------------------------------------------------------------------------- |
| Can't find "Choose a default app for each protocol" | Search for "default apps" and scroll down to "Choose default apps by protocol" |
| Lock icon not showing                               | Site may be using HTTP; check URL starts with https://                         |
| ipconfig shows multiple adapters                    | Look for adapter with "Default Gateway" or active connection                   |
| Whatismyip.com blocked                              | Try:`https://ipinfo.io` or `https://checkip.amazonaws.com`                 |

---

## Additional Practice

1. Check the default applications for other protocols:

   - FTP
   - SMTP
   - Telnet
2. Visit different websites and observe which use HTTP vs HTTPS
3. Check your IP address at different times to see if it changes
4. Compare your private IP to your public IP (they should be different)

---

## Congratulations!

You have successfully completed the **Exploring Networking Ports and Protocols** lab. You now know how to:

- Identify default applications for network protocols
- Determine which protocol a website is using
- Find both public and private IP addresses
- Understand the difference between HTTP and HTTPS
- Locate common port assignments for network services

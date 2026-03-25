
![alt text](../Screenshots/Linksys.jpg)

# Lab: Securing a SOHO Network

**Estimated time needed:** 20 minutes

---

## Learning Objectives

- Change the default administrator password of the SOHO router to enhance security
- Change the SOHO router's default Service Set Identifier (SSID) for improved wireless security
- Enable the WPA3 Personal security protocol with a strong passphrase for the SOHO router's 2.4 GHz and 5 GHz frequencies

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### Lab Environment

This lab uses the **Cisco Linksys E7350 router emulator** – a simulated router interface that allows you to practice security configurations without affecting real network equipment.

---

## Introduction to SOHO Network Security

**SOHO** stands for **Small Office / Home Office**. Securing a SOHO network involves:

| Security Measure                        | Purpose                                            |
| :-------------------------------------- | :------------------------------------------------- |
| **Change default admin password** | Prevents unauthorized access to router settings    |
| **Change default SSID**           | Hides router brand/model; reduces targeted attacks |
| **Enable WPA3 encryption**        | Provides strongest wireless security protocol      |
| **Use strong passphrase**         | Prevents unauthorized Wi-Fi access                 |

---

## Exercise 1: Change the Administrator Router Password

In this exercise, you will change the administrator password on a router. The default password is a well-known security vulnerability that attackers can exploit to gain control of your network.

### Step 1: Access the Router Emulator

1. Open your web browser (Google Chrome, Firefox, etc.)
2. Navigate to: **https://ui.linksys.com/ExpertFamily/E7350/**

![Linksys E7350 emulator login screen]



### Step 2: Login to the Router

1. Click **Login** on the emulator screen
2. You do not need to enter a password for this emulator

![Login button highlighted]

![alt text](<../Screenshots/Linksys E7350 emulator login screen.png>)


### Step 3: Access the Configuration Tab

1. After logging in, click the **Configuration** tab at the top of the screen

![Configuration tab highlighted]

![alt text](<../Screenshots/Configuration tab highlighted.png>)


### Step 4: Navigate to Administration Settings

1. In the left panel, click **Administration**

![Administration menu option]

![alt text](<../Screenshots/Administration menu option.png>)


### Step 5: Select Password Settings

1. In the Administration sub-panel, select **Password**

![Password option in Administration sub-panel]

![alt text](<../Screenshots/Password option in Administration sub-panel.png>)

### Step 6: Create a Strong Administrator Password

Enter a strong password following these guidelines:

| Requirement                  | Description                 |
| :--------------------------- | :-------------------------- |
| **Minimum length**     | At least 12 characters      |
| **Uppercase letters**  | A-Z                         |
| **Lowercase letters**  | a-z                         |
| **Numbers**            | 0-9                         |
| **Special characters** | ! @ # $ % ^ & * ( ) - _ + = |

**Example Password:** `Klb2!79100@1`

**Fields to complete:**

| Field                         | Value                             |
| :---------------------------- | :-------------------------------- |
| **Router password**     | Enter your chosen strong password |
| **Re-enter to confirm** | Enter the same password again     |

![Password fields with example password]

![alt text](<../Screenshots/Password fields with example password.png>)

### Step 7: Save the Password

1. After entering and confirming the password
2. Click **Save** or **Apply** to save the changes

![Save button]

![alt text](<../Screenshots/Save button.png>)

### Step 8: Take Screenshot

Take a screenshot showing:

- The Administration → Password page
- Password fields filled (you may obscure the actual password if desired)
- The "Save" option

Save the file as `SOHO_Admin_Password.png`

---

## Exercise 2: Change the Default SSID

In this exercise, you will change the router's default Service Set Identifier (SSID) – the name of your Wi-Fi network.

### Why Change the Default SSID?

| Reason                            | Explanation                                                               |
| :-------------------------------- | :------------------------------------------------------------------------ |
| **Hide router brand**       | Default SSIDs often include the router brand (e.g., "Linksys", "Netgear") |
| **Reduce targeted attacks** | Attackers may use known vulnerabilities for specific router models        |
| **Avoid confusion**         | Multiple networks with default names can cause connection issues          |
| **Professional appearance** | Custom SSID looks more professional in business settings                  |

### Step 1: Navigate to Wireless Settings

1. In the left panel, click **Wireless**

![Wireless menu option]

![alt text](<../Screenshots/Wireless menu option.png>)

### Step 2: Select Basic Wireless Settings

1. In the Wireless sub-panel, select **Basic Wireless Settings**

![Basic Wireless Settings option]

![alt text](<../Screenshots/Basic Wireless Settings option.png>)

### Step 3: View Current SSID

You will see the current network names (SSIDs) for:

| Frequency         | Typical Default SSID |
| :---------------- | :------------------- |
| **2.4 GHz** | LinksysXXXXX         |
| **5 GHz**   | LinksysXXXXX_5GHz    |

![Current SSID fields]

![alt text](<../Screenshots/Current SSID fields.png>)

### Step 4: Create a New SSID

Create a new SSID following these guidelines:

| Guideline                            | Example                                         |
| :----------------------------------- | :---------------------------------------------- |
| **Avoid personal information** | Don't use your name, address, or birth year     |
| **Avoid router brand**         | Don't use "Linksys", "Netgear", etc.            |
| **Make it unique**             | Create something memorable but not identifiable |
| **No offensive language**      | Keep it professional                            |

**Example SSID:** `SecureHomeNetwork` or `CyberSecureWiFi`

### Step 5: Update SSID for Both Frequencies

1. In the **Network Name (SSID)** field for 2.4 GHz, enter your new SSID
2. In the **Network Name (SSID)** field for 5 GHz, enter your new SSID (can be same or different)

![SSID fields updated]

![alt text](<../Screenshots/SSID fields updated.png>)

### Step 6: Save the Changes

1. Click **Save** or **Apply** to save the SSID changes

### Step 7: Take Screenshot

Take a screenshot showing:

- Wireless → Basic Wireless Settings page
- The new SSID(s) you created

Save the file as `SOHO_SSID.png`

---

## Exercise 3: Enable WPA3 Personal Security Protocol

In this exercise, you will enable the strongest wireless security protocol – WPA3 Personal – and set a strong passphrase.

### Understanding Wi-Fi Security Protocols

| Protocol       | Status             | Description                                    |
| :------------- | :----------------- | :--------------------------------------------- |
| **WEP**  | Deprecated (1999)  | Broken, easily cracked – never use            |
| **WPA**  | Deprecated (2003)  | Vulnerable to KRACK attack – avoid            |
| **WPA2** | Current but aging  | Still used widely, but WPA3 is stronger        |
| **WPA3** | Recommended (2018) | Strongest available; mandatory for new devices |

### Step 1: Navigate to Wireless Security Settings

1. In the left panel, click **Wireless**
2. Select **Wireless Security** from the sub-panel

![Wireless Security option]

![alt text](<../Screenshots/Wireless Security option.png>)

### Step 2: Select Security Mode for 2.4 GHz

1. In the **2.4 GHz** section, locate **Security Mode**
2. From the dropdown menu, select **WPA3 Personal**

![Security Mode dropdown with WPA3 Personal selected]

![alt text](<../Screenshots/Security Mode dropdown with WPA3 Personal selected.png>)

### Step 3: Select Security Mode for 5 GHz

1. In the **5 GHz** section, locate **Security Mode**
2. From the dropdown menu, select **WPA3 Personal**

![5 GHz security 
mode with WPA3 Personal]

![alt text](<../Screenshots/5 GHz security mode with WPA3 Personal.png>)

### Step 4: Create a Strong Passphrase

Create a strong Wi-Fi passphrase following these guidelines:

| Requirement                      | Description                                                  |
| :------------------------------- | :----------------------------------------------------------- |
| **Minimum length**         | At least 12-16 characters (WPA3 supports up to 63)           |
| **Complexity**             | Mix of uppercase, lowercase, numbers, and special characters |
| **Avoid dictionary words** | Don't use common words or phrases                            |
| **Avoid personal info**    | Don't use names, birthdays, addresses                        |

**Example Passphrase:** `BlueSky$2026!Forest#Lake`

### Step 5: Enter the Passphrase

1. In the **2.4 GHz** section, enter your strong passphrase in the **Password** field
2. In the **5 GHz** section, enter the same passphrase in the **Password** field

![WPA3 passphrase fields]

![alt text](<../Screenshots/WPA3 passphrase fields.png>)

### Step 6: Save the Changes

1. Click **Save** or **Apply** to save the security settings

### Step 7: Take Screenshot

Take a screenshot showing:

- Wireless → Wireless Security page
- Security Mode set to WPA3 Personal for both frequencies
- The strong passphrase (you may obscure the actual passphrase if desired)

Save the file as `SOHO_WPA3.png`

---

## Exercise 4: Additional SOHO Security Best Practices (Optional)

While not required for this lab, consider these additional security measures:

### Additional Security Settings

| Setting                                  | Recommended Configuration                              |
| :--------------------------------------- | :----------------------------------------------------- |
| **Remote Management**              | Disabled (prevents external access to router settings) |
| **UPnP (Universal Plug and Play)** | Disabled (security risk; enable only if needed)        |
| **Guest Network**                  | Enable with separate SSID and password for visitors    |
| **Firmware Updates**               | Enable automatic updates or check regularly            |
| **Router Firewall**                | Enabled (usually enabled by default)                   |
| **MAC Address Filtering**          | Optional (adds layer but not foolproof)                |
| **Logging**                        | Enable to monitor network activity                     |

### How to Disable Remote Management

1. Navigate to **Configuration → Administration → Remote Management**
2. Uncheck **Allow remote access**
3. Click **Save**

![Remote Management disabled]

---

## Lab Completion Checklist

| Task                                                     | Completed |
| :------------------------------------------------------- | :-------- |
| Accessed Cisco Linksys E7350 emulator                    | ☐        |
| Logged into router (no password needed)                  | ☐        |
| Navigated to Configuration → Administration → Password | ☐        |
| Changed administrator password to a strong password      | ☐        |
| Took screenshot of password settings                     | ☐        |
| Navigated to Wireless → Basic Wireless Settings         | ☐        |
| Changed default SSID to a custom name                    | ☐        |
| Took screenshot of new SSID                              | ☐        |
| Navigated to Wireless → Wireless Security               | ☐        |
| Enabled WPA3 Personal for both 2.4 GHz and 5 GHz         | ☐        |
| Created and entered a strong Wi-Fi passphrase            | ☐        |
| Took screenshot of WPA3 settings                         | ☐        |

---

## Screenshot Checklist

| Screenshot               | File Name                   | Description                                  |
| :----------------------- | :-------------------------- | :------------------------------------------- |
| **Admin Password** | `SOHO_Admin_Password.png` | Administration password settings             |
| **SSID Settings**  | `SOHO_SSID.png`           | Basic Wireless Settings with new SSID        |
| **WPA3 Security**  | `SOHO_WPA3.png`           | Wireless Security with WPA3 Personal enabled |

---
<video controls src="Securing a SOHO Network.mp4" title="Securing a SOHO Network"></video>


## Key Takeaways

| Concept                      | Key Point                                                                       |
| :--------------------------- | :------------------------------------------------------------------------------ |
| **Default Passwords**  | Never leave default admin password; always change to a strong password          |
| **SSID Customization** | Change default SSID to hide router brand and reduce targeted attacks            |
| **WPA3 Protocol**      | Use WPA3 Personal for strongest wireless security                               |
| **Strong Passphrases** | Use 12+ characters with mix of character types                                  |
| **2.4 GHz vs 5 GHz**   | Configure both frequencies with same security settings                          |
| **SOHO Security**      | Small office/home office networks require same security diligence as enterprise |

---

## Strong Password Guidelines

| Do                                    | Don't                                      |
| :------------------------------------ | :----------------------------------------- |
| Use 12-16+ characters                 | Use dictionary words                       |
| Mix uppercase and lowercase           | Use personal information (name, birthdate) |
| Include numbers                       | Use sequential numbers (12345)             |
| Include special characters (!@#$%^&*) | Use keyboard patterns (qwerty)             |
| Use passphrases (multiple words)      | Reuse passwords across devices             |

---

## Troubleshooting Tips

| Issue                            | Solution                                                                      |
| :------------------------------- | :---------------------------------------------------------------------------- |
| **Emulator doesn't load**  | Check internet connection; refresh page; try different browser                |
| **Can't find WPA3 option** | Ensure you're in Wireless Security section; look under Security Mode dropdown |
| **Password not saving**    | Ensure both password fields match; check for any validation errors            |
| **SSID not changing**      | Click Save/Apply; may need to reboot router for changes to take effect        |

---

## Summary

In this hands-on lab, you have:

| Activity                                                        | Completed |
| :-------------------------------------------------------------- | :-------- |
| Accessed the Cisco Linksys E7350 router emulator                | ✓        |
| Changed the default administrator password to a strong password | ✓        |
| Changed the default SSID to a custom network name               | ✓        |
| Enabled WPA3 Personal security protocol for 2.4 GHz             | ✓        |
| Enabled WPA3 Personal security protocol for 5 GHz               | ✓        |
| Created and applied a strong Wi-Fi passphrase                   | ✓        |
| Documented security changes with screenshots                    | ✓        |

---

## Congratulations!

You have successfully completed the **Securing a SOHO Network** lab. You now know how to:

- Change the default administrator password on a router
- Change the default SSID to improve wireless security
- Enable WPA3 Personal encryption for both 2.4 GHz and 5 GHz frequencies
- Create and apply strong passphrases for Wi-Fi security

These skills are essential for securing small office and home office networks against unauthorized access and cyber threats.

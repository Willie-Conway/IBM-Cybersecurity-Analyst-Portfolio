# Hands-on Lab: Review Security Threat Reports using X-Force Threat Exchange

**Estimated time needed:** 15 minutes

---

## Overview

X-Force Threat Exchange is a cloud-based, collaborative platform developed by IBM. Its primary function is facilitating user sharing of security-related information and threat intelligence.

With X-Force, you have access to real-time feeds of threat intelligence shared by other users. You can also contribute data about potential threats, vulnerabilities, and risky IP addresses. The ability to exchange information allows everyone to enhance their cybersecurity measures, stay up-to-date about the latest threats, and take proactive steps to protect their systems and networks.

---

## Learning Objectives

After completing this lab, you will be able to:

| Objective          | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| **Navigate** | Navigate the X-Force Exchange Dashboard                      |
| **Review**   | Review available reports and threat intelligence information |

---

## Tools Needed

| Requirement                   | Details                                           |
| ----------------------------- | ------------------------------------------------- |
| **Web Browser**         | Chrome, Firefox, Edge, or Safari (latest version) |
| **Internet Connection** | Active connection to access IBM X-Force Exchange  |
| **IBM ID**              | Optional (Guest access is available for this lab) |

---

## Exercise 1: Get Started with X-Force Exchange Dashboard

In this exercise, you will launch the X-Force Exchange website and take a tour of the Dashboard.

### Step 1: Launch X-Force Exchange

1. Open your web browser
2. Navigate to the IBM X-Force Exchange website:

   ```
   https://exchange.xforce.ibmcloud.com/
   ```

![X-Force Exchange landing page]

### Step 2: Authentication Options

The first time you log in to the site, you will be prompted with three options:

| Option                           | Description                                          |
| -------------------------------- | ---------------------------------------------------- |
| **Create IBM ID**          | Register for a free IBM account                      |
| **Login with Credentials** | Use existing IBM ID                                  |
| **Enter as Guest**         | Access without an account (recommended for this lab) |

### Step 3: Guest Access

For this demonstration:

1. ✅ Select the **Terms of Service** checkbox
2. Click **Enter as Guest**

![Guest access selection screen]

### Step 4: Dashboard Tour

The X-Force Exchange Dashboard is displayed. The first time you enter the X-Force Exchange Dashboard, a tour of the Dashboard will automatically launch.

You have two options:

| Action                    | Description                   |
| ------------------------- | ----------------------------- |
| **Click Next**      | Continue with the guided tour |
| **Click Skip tour** | Go directly to the Dashboard  |

### Step 5: Explore the Dashboard

Take a few minutes to familiarize yourself with the layout and functionalities by:

- Taking the guided tour (recommended for first-time users)
- Or manually exploring the Dashboard sections

### Step 6: Dashboard Overview

The Dashboard provides a high-level overview of all shared threat intelligence, including:

| Dashboard Section              | Content                                                   |
| ------------------------------ | --------------------------------------------------------- |
| **Recent Activity**      | Latest threat reports and updates                         |
| **Top Indicators**       | Most frequently reported malicious IPs, domains, and URLs |
| **Threat Maps**          | Geographic visualization of threat activity               |
| **Popular Collections**  | Curated threat intelligence sets                          |
| **Recent Contributions** | Latest user-submitted threat data                         |

---

## Exercise 2: Explore Threat Reports

### Step 1: Navigate to Reports

1. From the Dashboard, locate the top navigation menu
2. Click on **Reports** or search for specific threat reports

### Step 2: Review Available Reports

Common report types available on X-Force Exchange:

| Report Type                     | Description                                   | Example Use                               |
| ------------------------------- | --------------------------------------------- | ----------------------------------------- |
| **IP Reports**            | Information about malicious IP addresses      | Check if an IP is associated with malware |
| **Domain Reports**        | Domain reputation and associated threats      | Investigate suspicious domain names       |
| **URL Reports**           | URL safety and threat categorization          | Verify if a link is safe to click         |
| **Malware Reports**       | Malware family information and behavior       | Research specific malware variants        |
| **Vulnerability Reports** | CVE details and exposure information          | Assess software vulnerabilities           |
| **APT Reports**           | Advanced Persistent Threat group intelligence | Track nation-state actor activities       |

### Step 3: Search for Specific Threats

Use the search bar at the top of the page to look for:

```
Example searches:
- "Emotet"
- "Log4j" or "CVE-2021-44228"
- "Ransomware"
- Specific IP address (e.g., "8.8.8.8")
- Domain name (e.g., "malicious-domain.com")
```

### Step 4: Examine a Threat Report

1. Click on any report of interest
2. Review the following sections:

| Section              | Information Provided                                   |
| -------------------- | ------------------------------------------------------ |
| **Summary**    | Overview of the threat                                 |
| **Risk Score** | Severity rating (Low/Medium/High/Critical)             |
| **Indicators** | IOCs (IPs, domains, hashes) associated with the threat |
| **Tags**       | Categorization labels (e.g., #Malware #Phishing)       |
| **References** | External links and sources                             |
| **Timeline**   | When the threat was first and last seen                |

---

## Exercise 3: Explore Threat Collections

### Step 1: Navigate to Collections

1. Click on **Collections** in the top navigation menu
2. Review available public collections

### Step 2: Collection Types

| Collection Type               | Description                                                         |
| ----------------------------- | ------------------------------------------------------------------- |
| **IBM X-Force Curated** | Official threat intelligence from IBM                               |
| **Community Shared**    | Threat data shared by other users                                   |
| **Sector-Specific**     | Threats relevant to specific industries (finance, healthcare, etc.) |
| **Geographic**          | Threats targeting specific regions                                  |

### Step 3: View Collection Details

Click on any collection to view:

- List of indicators in the collection
- Collection description and purpose
- Contributor information
- Last update date

---

## Exercise 4: Understand Threat Scores

### X-Force Threat Scores

X-Force uses a scoring system to indicate threat levels:

| Score Range    | Risk Level | Color Indicator | Recommended Action        |
| -------------- | ---------- | --------------- | ------------------------- |
| **0-1**  | Very Low   | 🟢 Green        | Monitor                   |
| **2-3**  | Low        | 🟢 Green        | Review periodically       |
| **4-6**  | Medium     | 🟡 Yellow       | Investigate               |
| **7-8**  | High       | 🟠 Orange       | Prioritize investigation  |
| **9-10** | Critical   | 🔴 Red          | Immediate action required |

### Score Factors

Threat scores are calculated based on:

| Factor               | Description                             |
| -------------------- | --------------------------------------- |
| **Confidence** | How certain X-Force is about the threat |
| **Severity**   | Potential impact of the threat          |
| **Recency**    | When the threat was last observed       |
| **Prevalence** | How widespread the threat is            |
| **Activity**   | Frequency of threat behavior            |

---

## Exercise 5: Key Dashboard Features

### Top Navigation Menu

| Menu Item                 | Purpose                                                 |
| ------------------------- | ------------------------------------------------------- |
| **Dashboard**       | Main overview of threat intelligence                    |
| **Search**          | Find specific threats, IPs, domains, or vulnerabilities |
| **Reports**         | Browse detailed threat reports                          |
| **Collections**     | View curated threat intelligence sets                   |
| **Indicators**      | Search for specific IOCs                                |
| **Vulnerabilities** | Browse CVE database                                     |
| **Contribute**      | Submit your own threat intelligence                     |

### Dashboard Widgets

| Widget                             | Information Displayed              |
| ---------------------------------- | ---------------------------------- |
| **Recent Indicators**        | Latest malicious IPs/domains added |
| **Top Malware Families**     | Most active malware by volume      |
| **Trending Vulnerabilities** | CVEs being discussed/exploited     |
| **Activity Map**             | Global threat visualization        |
| **Recent Collections**       | Newly shared threat collections    |

---

## Lab Completion Checklist

| Task                                          | Completed | Notes                                 |
| --------------------------------------------- | --------- | ------------------------------------- |
| Launch X-Force Exchange website               | ☐        | https://exchange.xforce.ibmcloud.com/ |
| Accept Terms of Service                       | ☐        |                                       |
| Login as Guest                                | ☐        | No IBM ID required                    |
| Take Dashboard tour                           | ☐        | Optional but recommended              |
| Navigate to Reports section                   | ☐        |                                       |
| Review at least 3 threat reports              | ☐        |                                       |
| Search for a specific threat (e.g., "Emotet") | ☐        |                                       |
| Navigate to Collections section               | ☐        |                                       |
| Review 2 different collections                | ☐        |                                       |
| Understand threat scoring system              | ☐        | 0-10 scale                            |
| Identify high-risk vs low-risk threats        | ☐        |                                       |

---

## X-Force Exchange Features Summary

| Feature                          | Description                                               |
| -------------------------------- | --------------------------------------------------------- |
| **Free Access**            | No subscription required for basic features               |
| **Guest Access**           | Use without creating an account                           |
| **Real-Time Intelligence** | Up-to-date threat information                             |
| **Community Driven**       | Shared intelligence from security professionals worldwide |
| **IBM Curated Content**    | Verified threat intelligence from IBM X-Force research    |
| **CVE Integration**        | Comprehensive vulnerability database                      |
| **API Access**             | Programmatic access for automation (requires IBM ID)      |

---

## Common Use Cases

| Use Case                           | How X-Force Helps                                    |
| ---------------------------------- | ---------------------------------------------------- |
| **Incident Response**        | Look up suspicious IPs/domains during investigations |
| **Threat Hunting**           | Search for IOCs across shared intelligence           |
| **Vulnerability Management** | Check CVE details and exploit status                 |
| **Security Monitoring**      | Enrich alerts with threat intelligence               |
| **Threat Research**          | Study malware families and attack patterns           |
| **Report Writing**           | Gather threat data for security assessments          |

---

## Troubleshooting Tips

| Issue                                              | Solution                                            |
| -------------------------------------------------- | --------------------------------------------------- |
| **Website not loading**                      | Check internet connection; try refreshing           |
| **Guest access not available**               | Clear browser cache and cookies; try incognito mode |
| **Tour not launching**                       | Manually explore dashboard or refresh the page      |
| **Search returning no results**              | Try broader search terms or check spelling          |
| **Terms of Service checkbox not selectable** | Zoom out or scroll to see full page                 |

---

## Key Takeaways

| Concept                     | Description                                      |
| --------------------------- | ------------------------------------------------ |
| **X-Force Exchange**  | IBM's collaborative threat intelligence platform |
| **Guest Access**      | Use without account creation for basic features  |
| **Threat Reports**    | Detailed information about specific threats      |
| **Collections**       | Curated sets of threat indicators                |
| **Risk Scores**       | 0-10 scale indicating threat severity            |
| **IOCs**              | Indicators of Compromise (IPs, domains, hashes)  |
| **Community Sharing** | Security professionals sharing threat data       |

---

## Additional Resources

| Resource                            | URL                                   |
| ----------------------------------- | ------------------------------------- |
| **X-Force Exchange**          | https://exchange.xforce.ibmcloud.com/ |
| **IBM Security Intelligence** | https://securityintelligence.com/     |
| **X-Force Research**          | https://www.ibm.com/security/xforce   |
| **CVE Database**              | https://cve.mitre.org/                |

---

## Summary

In this hands-on lab, you have:

| Activity                                   | Completed |
| ------------------------------------------ | --------- |
| Accessed IBM X-Force Exchange as a guest   | ☐        |
| Navigated the Dashboard interface          | ☐        |
| Reviewed available threat reports          | ☐        |
| Explored threat collections                | ☐        |
| Understood the threat scoring system       | ☐        |
| Learned key X-Force features and use cases | ☐        |

---

## Congratulations!

You have successfully completed the **Review Security Threat Reports using X-Force Threat Exchange** lab. You now know how to:

- Navigate the IBM X-Force Exchange Dashboard
- Access and review threat reports as a guest user
- Search for specific threats, IPs, and domains
- Understand X-Force threat scoring (0-10 scale)
- Browse curated threat collections
- Use X-Force for security investigations and research

These skills are essential for:

- Security analysts investigating potential threats
- Incident response teams needing rapid IOC lookups
- Security professionals staying updated on latest threats
- Organizations improving their threat intelligence capabilities


![alt text](<../Screenshots/Google Chrome.png>)

# Hands-on Lab: Managing Browser Security and Privacy Settings

## Overview

In this hands-on lab, you will explore key privacy and security settings in the Google Chrome browser. You will learn how to perform a safety check, manage browsing data, configure privacy settings, and understand the limitations of Incognito mode.

## Exercise 1: Identify How to Perform a Safety Check within a Google Chrome Browser

The Safety Check tool in Chrome reviews your browser's security and privacy settings to identify potential issues.

**Steps:**

1. Open Google Chrome.

![alt text](<../Screenshots/Exercise 1 - Identify How to Perform a Safety Check within a Google Chrome Browser/Google Chrome browser.png>)

2. Click on the three vertical dots (Customize and control Google Chrome) in the top-right corner.
3. Navigate to **Settings**.

![alt text](<../Screenshots/Exercise 1 - Identify How to Perform a Safety Check within a Google Chrome Browser/Click the three dots.png>)

4. In the left-hand menu, select **Privacy and security**.
   
 ![alt text](<../Screenshots/Exercise 1 - Identify How to Perform a Safety Check within a Google Chrome Browser/Click on Safety check.png>)

5. Click on **Safety check**. Chrome will automatically run a check and review:
   - Compromised passwords
   - Safe Browsing status
   - Available updates
   - Unwanted software or extensions


 ![alt text](<../Screenshots/Exercise 1 - Identify How to Perform a Safety Check within a Google Chrome Browser/Once the safety check completes.png>)

## Exercise 2: Identify Options for Clearing Google Chrome Browsing Data

Clearing your browsing data helps protect your privacy by removing local records of your online activity.

**Steps:**

1. In Chrome, click the three vertical dots and go to **Settings** > **Privacy and security**.

![alt text](<../Screenshots/Exercise 2 - Identify Options for Clearing Google Chrome Browsing Data/Go to Settings then Privacy and security.png>)

2. Click on **Clear browsing data**.

![alt text](<../Screenshots/Exercise 2 - Identify Options for Clearing Google Chrome Browsing Data/Click on Clear browsing data.png>)

3. A dialog box will appear with two main tabs:
   - **Basic:** Allows you to clear browsing history, cookies, and cached images and files. You can select the time range (e.g., Last hour, All time).
   - **Advanced:** Provides more granular options, including clearing download history, passwords, autofill form data, and site settings.
4. Select the desired data types and time range, then click **Clear data**.

![alt text](<../Screenshots/Exercise 2 - Identify Options for Clearing Google Chrome Browsing Data/Then click Clear data.png>)

## Exercise 3: Identify How to Check and Clear Google Chrome Browsing History

Viewing and managing your browsing history is a fundamental privacy task.

**Steps:**

1. To view your browsing history, you can either:
   - Press `Ctrl+H` (Windows/Linux) or `Cmd+Y` (Mac).
   - Type `chrome://history` into the address bar and press Enter.
2. You will see a list of websites you have visited, organized by date and time.
3. To clear your history from this view, click "Clear browsing data" on the left-hand side, which will take you to the menu described in Exercise 2.

## Exercise 4: Identify and Configure Settings in Google Chrome Browser for Privacy and Security

This exercise guides you through configuring key privacy settings and understanding the role of Incognito mode.

**Steps:**

1. **Navigate to Privacy and Security Settings:**

   - Go to **Settings** > **Privacy and security**.
2. **Review Cookies and Site Data:**

   - Click on **Third-party cookies**.
   - You will see options to block third-party cookies in different scenarios.
3. **Understanding Incognito Mode and Cookies:**

   - **Note:** When a browser is in Incognito mode (also known as Private browsing), your browsing history is not saved locally on your device. However, it is important to understand that your activity is not invisible to everyone.
     - **Example:** If you log into your social media account in an Incognito window, the website itself can still track your activity on *their own site* during that session using its own first-party cookies.
   - Your internet service provider (ISP), employer (if on a work network), and the websites you visit can still see your activity.
4. **Configure Cookie Settings:**

   - Select the option **Block all third-party cookies**.
   - **Note:** Be aware that selecting this option may cause some features on certain websites to stop working.
     - **Example:** An e-commerce site like Amazon might use third-party cookies to show you personalized product recommendations or to keep items in your shopping cart if you leave the site. Blocking all third-party cookies could break these features.
   - After reviewing, ensure **Block all third-party cookies** is selected, then proceed.
5. **Complete the Privacy Guide (if applicable):**

   - This completes the review of privacy settings. Next, you will verify that the settings are enabled.
6. **Verify Safe Browsing Settings:**

   - Open a new tab and visit `chrome://safe-browsing`.
   - Once on the site, scroll down to view **Preferences**.
   - You should notice that `safebrowsing.enabled` is set to **true** (enabled), along with the other settings configured previously under safe browsing protection.

---

## Practice Exercises

### Problem 1: Does Incognito browsing mode in a browser record browsing history?

**Click here for a hint.**
Follow the steps mentioned in Exercise 3. First, view the history and go to `chrome://history`. If there is browser history, clear it. Then, open a new incognito browser tab, browse to `ibm.com` or conduct a Google search to create activity. Once searches or browsing is complete within an incognito browser, go back to review `chrome://history`.

**Click here for the solution.**
No, browsing history is **not recorded** on your device while in incognito mode.

**Step-by-step solution with visual aids:**

| Step | Action                                                                                                                                                                                                           | Screenshot (Placeholder)        |
| :--- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------ |
| 1    | **Open a new incognito window.** Click the three dots and select "New Incognito Window".                                                                                                                   | New Incognito window            |
| 2    | **Create browsing activity.** In the incognito window, navigate to a website like `ibm.com` or perform a Google search.                                                                                  | New browser activity at ibm.com |
| 3    | **Review browsing history.** Close the incognito window and open a regular Chrome window. Go to `chrome://history`. You will see that the sites you visited in incognito mode do not appear in the list. | New browsing history            |

### Problem 2: How can third-party cookies in Chrome Browser be blocked while in incognito mode?

**Click here for a hint.**
Follow the steps mentioned in Exercise 3 and browse to "Cookies and other site data".

**Click here for the solution.**
To block third-party cookies in Chrome, especially while in incognito mode:

1. Open Google Chrome Browser.
2. Click on the three dots and go to **Settings**.
3. Under the **Privacy and security** section on the left, click **Third-party cookies**.
4. In the "General settings" section, you will see different options:
   - **Block third-party cookies in Incognito:** This is the default setting. It allows third-party cookies in regular browsing but blocks them in incognito windows.
   - **Block all third-party cookies:** This setting blocks them globally, in both regular and incognito windows.
5. To specifically block them in incognito while keeping them on for regular browsing, ensure the **"Block third-party cookies in Incognito"** option is selected.

| Action                            | Setting Location                                                                          |
| :-------------------------------- | :---------------------------------------------------------------------------------------- |
| Navigate to cookie settings       | Settings > Privacy and security > Third-party cookies                                     |
| Select the desired blocking level | Choose either "Block third-party cookies in Incognito" or "Block all third-party cookies" |

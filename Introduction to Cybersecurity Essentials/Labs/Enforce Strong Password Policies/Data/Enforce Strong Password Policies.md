![alt text](<../Screenshots/Kaspersky Password Manager.png>)

# Hands-on Lab: Enforce Strong Password Policies

**Estimated time needed:** 30 minutes

---

## About This Lab

In this lab, we will use Kaspersky's password checker to learn how vulnerable our passwords are. Using the Local Group Policy Editor, we will also learn how to enforce strong password policies within the Microsoft Windows operating system.

In this hands-on lab, you will:

- Check password strength
- Review Windows Local Group Policy Editor
- Configure password policies

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About the Lab Instructions and Solutions

Microsoft Windows operating system features can vary based on the Windows edition. If completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Exercise 1: Check Password Strength

![alt text](<../Screenshots/Exercise 1 - Check Password Strength/Check Password Strength.png>)

In this exercise, we will use **Kaspersky's password checker** to test password strength. This tool will show you how safe a password is. It considers how long it would take an attacker to brute-force your password. It also compares your password to a database of leaked passwords that any attacker could have access to.

### Step 1: Open Kaspersky Password Checker

1. Click the **Chrome** icon to open the Chrome browser
2. Type **`password.kaspersky.com`** into the address bar and press Enter

![alt text](<../Screenshots/Exercise 1 - Check Password Strength/Test your password box and type fido1973.png>)

### Step 2: Test a Simple Password

1. A user created a password using letters and numbers. They used their pet's name and year of birth so they could remember it.
2. Click the **Test your password** box and type: **`fido1973`**
3. Press **Enter**

**Observe the results:**

Kaspersky will provide feedback on the strength of the tested password, including:

- Whether the password has been leaked
- Estimated time to crack
- Overall strength rating

![alt text](<../Screenshots/Exercise 1 - Check Password Strength/Press Enter.png>)

### Step 3: Test a More Complex Password

1. A user was required to create an 8-character password using a capital letter, at least one number, and at least one symbol
2. Click the **Test your password** box and type: **`Fido1973!`**
3. Press **Enter**

**Observe the results:**

Compare these results with the previous password. Note any improvements in:

- Estimated crack time
- Overall strength rating

### Step 4: Test a Strong Password Using a Phrase

![alt text](<../Screenshots/Exercise 1 - Check Password Strength/Test your password box and type Mh1llifwwas!.png>)

1. A user was required to create a 12-character password using a capital letter, at least one number, and at least one symbol
2. Instead of using common words, they used the first letter of each word in a memorable phrase: **"Mary had 1 little lamb it's fleece was white as snow !"**
3. Click the **Test your password** box and type: **`Mh1llifwwas!`**
4. Press **Enter**

**Observe the results:**

Note the significant improvement in:

- Estimated crack time (should be millions of years)
- Strength rating (should be "Strong")
- No matches in leaked password databases

### Password Test Results Comparison

| Password         | Length | Composition                   | Estimated Crack Time | Strength Rating |
| :--------------- | :----- | :---------------------------- | :------------------- | :-------------- |
| `fido1973`     | 8      | Lowercase + numbers           | Instant - minutes    | Very Weak       |
| `Fido1973!`    | 9      | Mixed case + numbers + symbol | Hours - months       | Moderate        |
| `Mh1llifwwas!` | 12     | Mixed case + numbers + symbol | Millions of years    | Strong          |

---

## Exercise 2: Review Windows Local Group Policy Editor

Now we will learn how to enforce strong password policies for Windows users using the **Local Group Policy Editor**. The Local Group Policy Editor is a Microsoft Management Console (MMC) snap-in used to configure and monitor Group Policies and user settings.

### Step 1: Open Command Prompt

![alt text](<../Screenshots/Exercise 2 - Review Windows Local Group Policy Editor/Command Prompt.png>)

1. Type **Command Prompt** in the Windows search bar
2. Click on **Command Prompt** from the search results

### Step 2: Launch Local Group Policy Editor

![alt text](<../Screenshots/Exercise 2 - Review Windows Local Group Policy Editor/Type gpedit and press Enter.png>)

1. At the command prompt, type: **`gpedit`**
2. Press **Enter**

*Note: On some systems, you may need to type `gpedit.msc`*

### Step 3: Navigate the Local Group Policy Editor

![alt text](<../Screenshots/Exercise 2 - Review Windows Local Group Policy Editor/Open the Local Group Policy Editor.png>)

This will open the **Local Group Policy Editor**. Here you will see that the **Local Computer Policy** is broken into two main configurations:

| Configuration                    | Description                                                               |
| :------------------------------- | :------------------------------------------------------------------------ |
| **Computer Configuration** | Holds settings that are applied to the computer when it is started        |
| **User Configuration**     | Holds settings that are applied to users when they sign into the computer |

### Step 4: Navigate to Security Settings

![alt text](<../Screenshots/Exercise 2 - Review Windows Local Group Policy Editor/Navigate to Security Settings.png>)

1. Click **Computer Configuration** to expand it
2. Click **Windows Settings** to expand it
3. Select **Security Settings**

On the right panel, you will see several policy types along with a description of the types of policies included in that section.

### Step 5: Access Account Policies

1. Click the **Account Policies** folder to expand it

### Step 6: Access Password Policy

1. Under the Account Policies folder, click the **Password Policy** folder
2. On the right pane, you will see several configurable password policies

### Step 7: Review Password Policies

| Policy                                               | Description                                                                                                             | Default Setting                 |
| :--------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------- | :------------------------------ |
| **Enforce password history**                   | Determines how many unique passwords need to be used before an old password can be reused                               | 24 passwords remembered         |
| **Maximum password age**                       | Determines how many days a password can be used before the system requires a password change                            | 42 days                         |
| **Minimum password age**                       | Determines how many days a password must be used before the system requires a change                                    | 0 days (can change immediately) |
| **Minimum password length**                    | Determines the fewest number of characters required in a password                                                       | 0 characters (no minimum)       |
| **Minimum password length audit**              | Designed for organizations who want to track user password length (newer systems)                                       | Not configured                  |
| **Password must meet complexity requirements** | Requires passwords to include characters from at least three of four categories: uppercase, lowercase, numbers, symbols | Disabled                        |

---

## Exercise 3: Configure Password Policies

In this exercise, we will configure strong password policies to enhance system security.

### Step 1: Configure Enforce Password History

![alt text](<../Screenshots/Exercise 3 - Configure Password Policies/Configure Enforce Password History.png>)

1. Double-click **Enforce password history** policy
2. Microsoft recommends this be set to **24**
3. Type **24** into the box
4. Click **OK**
   
![alt text](<../Screenshots/Exercise 3 - Configure Password Policies/Microsoft recommends that Enforce password history be set to 24.png>)

### Step 2: Configure Maximum Password Age

![alt text](<../Screenshots/Exercise 3 - Configure Password Policies/Configure Maximum Password Age.png>)

1. Double-click **Maximum password age** policy
2. Microsoft recommends passwords expire between 30 and 90 days
3. Type **60** into the box
4. Click **OK**

![alt text](<../Screenshots/Exercise 3 - Configure Password Policies/Microsoft recommends that passwords should be set to expire somewhere between 30 and 90 days.png>)


### Step 3: Configure Minimum Password Age

![alt text](<../Screenshots/Exercise 3 - Configure Password Policies/Configure Minimum Password Age.png>)

1. Double-click **Minimum password age** policy
2. Microsoft recommends users wait at least one day before changing passwords
3. Type **1** into the box
4. Click **OK**

*Note: Minimum password age should be less than Maximum password age*

![alt text](<../Screenshots/Exercise 3 - Configure Password Policies/Microsoft recommends that users should be required to wait at least one day before they can change their password.png>)

### Step 4: Configure Minimum Password Length

![alt text](<../Screenshots/Exercise 3 - Configure Password Policies/Configure Minimum Password Length.png>)

1. Double-click **Minimum password length** policy
2. Microsoft recommends passwords be at least 8 characters and no more than 14 characters
3. Type **12** into the box
4. Click **OK**

![alt text](<../Screenshots/Exercise 3 - Configure Password Policies/Microsoft recommends that passwords be at least 8 characters and no more than 14 characters.png>)

### Step 5: Enable Password Complexity Requirements

![alt text](<../Screenshots/Exercise 3 - Configure Password Policies/Enable Password Complexity Requirements.png>)

1. Double-click **Password must meet complexity requirements** policy
2. Select **Enabled**
3. Click **OK**

**Complexity requirements mean passwords must contain characters from at least three of the following categories:**

- Uppercase letters (A-Z)
- Lowercase letters (a-z)
- Numbers (0-9)
- Special characters (!, @, #, $, etc.)

### Step 6: Review Configured Policies

![alt text](<../Screenshots/Exercise 3 - Configure Password Policies/Review Configured Policies.png>)

After configuration, your password policies should look similar to this:

| Policy                                     | Configured Setting      |
| :----------------------------------------- | :---------------------- |
| Enforce password history                   | 24 passwords remembered |
| Maximum password age                       | 60 days                 |
| Minimum password age                       | 1 day                   |
| Minimum password length                    | 12 characters           |
| Password must meet complexity requirements | Enabled                 |

---

## Exercise 4: Apply and Test Policies (Optional)

### Step 1: Close Local Group Policy Editor

1. Click the **X** in the top-right corner to close the Local Group Policy Editor

### Step 2: Update Group Policy

1. Open **Command Prompt** as administrator
2. Type: **`gpupdate /force`**
3. Press **Enter**
4. Wait for the update to complete (may take a minute or two)

### Step 3: Test Password Policy (Optional)

To test that policies are working:

1. Press **Ctrl + Alt + Del**
2. Select **Change a password**
3. Attempt to change to a weak password that doesn't meet requirements
4. Observe that Windows will reject the password with a message about requirements

---

## Practice Exercises

### Problem 1: Create a Complex Password

You have been asked to create a password for a new account. The website requires that your password have at least:

- Eight characters
- One capital letter
- One number

Create a password that you can remember that will take at least one week to crack. Use the Kaspersky Password Checker at `password.kaspersky.com` to ensure password strength.

<details>
<summary><strong>Click here for a hint</strong></summary>

Visit password.kaspersky.com. Type a chosen password into the Test your password box. View the length of time that it would take to crack the password. Ensure that the chosen password would take at least one week to crack. Increase the complexity of the password as needed to meet the requirement.

</details>

<details>
<summary><strong>Click here for the solution</strong></summary>

1. Open Chrome and navigate to `password.kaspersky.com`
2. Create a memorable password that meets requirements, such as:
   - `Summer2024!` (uses season, year, and symbol)
   - `MyDog$5Calls` (uses phrase with substitutions)
   - `IL0veC@ts!` (uses "I love cats" with number/symbol substitutions)
3. Type your password in the test box
4. Verify the estimated crack time is at least one week
5. If not, increase length or complexity until the target is met

Example solution: `SunnyBeach$2024` - This password would take centuries to crack while being memorable.

</details>

---

### Problem 2: Enable Password Complexity Requirements

If other, more complex policies are not set, Microsoft recommends that **Password must meet complexity requirements** is set to **Enabled**. Open the Password must meet complexity requirements policy. Enable the policy. View the **Explain** tab to see which requirements are set when this is enabled.

<details>
<summary><strong>Click here for a hint</strong></summary>

Follow the instructions in Exercise 2 to navigate to the Password Policy folder.

</details>

<details>
<summary><strong>Click here for the solution</strong></summary>

1. Open the **Local Group Policy Editor** (follow steps in Exercise 2)
2. Navigate to: Computer Configuration → Windows Settings → Security Settings → Account Policies → Password Policy
3. On the right panel, double-click **Password must meet complexity requirements**
4. Select **Enabled**
5. Click the **Explain** tab to review the policy description

The Explain tab shows that when enabled, passwords must:

- Not contain the user's account name or parts of their full name
- Be at least six characters in length (though minimum length policy may set higher)
- Contain characters from at least three of the following four categories:
  - English uppercase characters (A through Z)
  - English lowercase characters (a through z)
  - Base 10 digits (0 through 9)
  - Non-alphabetic characters (special characters like !, $, #, %)

6. Click **OK** to apply the setting

</details>

---

## Best Practices for Password Policies

### Recommended Settings

| Setting                           | Recommendation   | Rationale                                              |
| :-------------------------------- | :--------------- | :----------------------------------------------------- |
| **Minimum Password Length** | 12-16 characters | Longer passwords are exponentially harder to crack     |
| **Complexity Requirements** | Enabled          | Forces use of multiple character types                 |
| **Password History**        | 12-24 passwords  | Prevents password reuse                                |
| **Maximum Password Age**    | 60-90 days       | Limits window of opportunity for compromised passwords |
| **Minimum Password Age**    | 1-3 days         | Prevents rapid cycling through password history        |

### Additional Security Measures

| Measure                                       | Description                                                  |
| :-------------------------------------------- | :----------------------------------------------------------- |
| **Multi-Factor Authentication (MFA)**   | Adds second verification layer beyond passwords              |
| **Account Lockout Policies**            | Locks account after multiple failed attempts                 |
| **Regular Security Awareness Training** | Educates users on creating strong passwords                  |
| **Password Managers**                   | Encourages use of unique, complex passwords for each service |

---

## Password Creation Tips

| Do                                    | Don't                                       |
| :------------------------------------ | :------------------------------------------ |
| Use passphrases (multiple words)      | Use dictionary words alone                  |
| Include numbers and symbols           | Use sequential numbers (12345)              |
| Make it at least 12 characters        | Use personal information (birthdays, names) |
| Use unique passwords for each account | Reuse passwords across services             |
| Consider a password manager           | Write passwords on sticky notes             |

---

## Summary

In this hands-on lab, you have:

| Task                                                      | Completed |
| :-------------------------------------------------------- | :-------- |
| Tested password strength using Kaspersky password checker | ✓        |
| Compared weak, moderate, and strong passwords             | ✓        |
| Opened Local Group Policy Editor                          | ✓        |
| Navigated to Password Policy settings                     | ✓        |
| Reviewed available password policies                      | ✓        |
| Configured enforce password history                       | ✓        |
| Configured maximum password age                           | ✓        |
| Configured minimum password age                           | ✓        |
| Configured minimum password length                        | ✓        |
| Enabled password complexity requirements                  | ✓        |
| Completed practice exercises                              | ✓        |


<video controls src="Enforce Strong Password Policies.mp4" title="Enforce Strong Password Policies"></video>

### Key Takeaways

- **Password strength matters** – Weak passwords can be cracked instantly
- **Length is more important than complexity** – A long passphrase is harder to crack than a short complex password
- **Policy enforcement** – Technical controls ensure users follow security requirements
- **History prevents reuse** – Users should not recycle old passwords
- **Complexity defeats brute force** – Mixing character types dramatically increases password entropy
- **Education is essential** – Users need to understand why strong passwords matter

---

## Troubleshooting Tips

| Issue                                         | Possible Solution                                                        |
| :-------------------------------------------- | :----------------------------------------------------------------------- |
| **gpedit command not found**            | Local Group Policy Editor not available on Windows Home edition          |
| **Policies not applying**               | Run `gpupdate /force` from command prompt                              |
| **Users cannot change passwords**       | Check minimum password age setting                                       |
| **Complexity causing user frustration** | Balance security with usability; provide training on passphrases         |
| **Password history not working**        | Ensure value is set to at least 12; verify with `net accounts` command |

---

## Password Policy Best Practices

- **Enforce minimum password length** (12+ characters)
- **Enable password complexity** (uppercase, lowercase, numbers, symbols)
- **Set maximum password age** (90 days or less)
- **Implement password history** (prevents reuse of previous passwords)
- **Set minimum password age** (1 day to prevent immediate password changes)
- **Regularly audit password policies** (quarterly reviews recommended)

## Next Steps

After completing this lab, you should be comfortable with:

- Testing password strength using online tools
- Navigating Local Group Policy Editor
- Configuring password policies
- Understanding the impact of different policy settings

Continue to the next lab to explore additional Windows security features.

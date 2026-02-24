

![alt text](<Password Management.png>)

# Reading: Password Management

**Estimated time: 5 min**

## Learning objectives

*At the end of this reading, you will be able to:*

- Apply best practices for creating, managing, and securing strong passwords
- Recognize the risks of password reuse, sharing, and default credentials
- Use password managers and secure reset processes effectively

## Overview

Password management is a critical component of cybersecurity that involves creating, storing, and maintaining secure passwords across all your digital accounts.

## What makes a password strong and secure?

**Password length and complexity**
Strong passwords should be at least 12-16 characters long. Length is more important than complexity, as longer passwords are exponentially harder to crack. However, effective passwords should include a combination of uppercase letters, lowercase letters, numbers, and special characters. Avoid predictable patterns such as "Password123!" or keyboard walks such as "qwerty123." **For example, a password like "MyBlueDog-Runs@2024!" is both long (19 characters) and uses a mix of character types, making it far more secure than a shorter, complex one like "P@ssw0rd".**

## Why is password reuse and expiration risky?

**Password history and reuse**
Never reuse passwords across multiple sites or accounts. If one account is compromised, reused passwords put all other accounts at risk. **For instance, if you use the same password for your email and an online forum that gets hacked, attackers can use that email/password combination to access your email account, potentially resetting passwords for your bank and other sensitive services.** Maintain a password history to ensure that you don't accidentally reuse old passwords. Many systems enforce password history requirements, preventing users from cycling back to recently used passwords.

**Password expiration policies**
While traditional wisdom suggested regular password changes, current best practices recommend changing passwords only when there's evidence of compromise or when required by organizational policy. Frequent mandatory changes often lead to weaker passwords and predictable patterns. **For example, forced 90-day password changes often lead users to create simple variations like "Summer2024!" becoming "Fall2024!", which are easy for attackers to guess if the original is known.**

## How to keep password private and secure?

**Password privacy**
Keep passwords completely private, never share them with colleagues, friends, or family members. Be cautious when entering passwords in public spaces where shoulder surfing might occur. Use privacy screens when working in open environments, and always ensure you're on a secure, trusted network when entering credentials. **A common example of a privacy breach is typing a password into a video conferencing call while screen sharing, inadvertently exposing it to all meeting participants.**

**Password reset processes**
Understand and utilize secure password reset mechanisms. Legitimate password resets typically involve email verification or security questions. Be wary of unsolicited password reset emails, as these are common phishing tactics. Always initiate password resets directly from the official website rather than clicking links in emails. **For example, a phishing email might claim "Your Netflix account will be suspended" and include a link to a fake login page designed to steal your credentials, rather than directing you to the real Netflix site.**

**Default credentials management**
One of the most critical security practices is changing default usernames and passwords immediately after device installation or software setup. Default credentials are publicly available and represent a major security vulnerability. This applies to:

- Network equipment (routers, switches, access points)
- IoT devices (cameras, smart home devices)
- Software applications and databases
- Administrative accounts on new systems

**For example, a home security camera left with the default username "admin" and password "1234" can be easily found and accessed by anyone using a simple online search for exposed devices.**

Always enable password protection on accounts that don't have it by default, particularly on local user accounts and administrative interfaces.

## Password managers

Password managers are essential tools for implementing proper password hygiene. They generate strong, unique passwords for every account and store them securely behind a single master password. Key benefits include:

- Automatic generation of complex, unique passwords
- Secure storage using encryption
- Auto-fill capabilities that reduce typing errors and phishing risks
- Cross-platform synchronization across devices
- Breach monitoring that alerts you to compromised accounts

**For example, instead of trying to remember "J*8k#mP2!qR9$zL1" for your email and a different equally complex password for your banking site, a password manager like Bitwarden remembers them for you, so you only need to remember one strong master password.**

Popular password managers include built-in browser tools, dedicated applications such as Bitwarden or 1Password, and enterprise solutions for organizations.

## Authentication beyond passwords

- **Single sign-on (SSO)**
  Single sign-on allows users to authenticate once and access multiple applications without re-entering credentials. While convenient, SSO requires careful implementation to ensure security, as compromising the SSO account affects all connected services. **For instance, a company using Google Workspace might set up SSO so employees can access their CRM (like Salesforce) and project management tools (like Asana) just by logging into their company Google account.**
- **Multifactor authentication (MFA)**
  Implement multifactor authentication whenever possible. MFA combines something you know (password) with something you have (phone, token) or something you are (biometric). This significantly improves security even if passwords are compromised. **For example, even if a hacker steals your Instagram password, they cannot log in without the one-time code sent to your phone's authenticator app (something you have).**
- Single-factor authentication relies solely on passwords, making accounts vulnerable if credentials are stolen.
- Multifactor authentication provides additional security layers, making unauthorized access much more difficult even with compromised passwords.

## How to manage admin and user account privileges?

Understand the principle of least privilege when managing account permissions. Administrative accounts should have elevated privileges only when necessary for specific tasks. Regular user accounts should have minimal permissions needed for daily work. This separation limits potential damage from compromised credentials.

| **Administrator accounts** | **User accounts**                              |
| -------------------------------- | ---------------------------------------------------- |
| Install and configure software   | Personal files and applications                      |
| Modify system settings           | Specific business applications needed for their role |
| Access all files and folders     | Limited system modification capabilities             |
| Manage other user accounts       |                                                      |

**For example, if a receptionist's regular user account is compromised by a phishing email, the attacker's access is limited to their files and email. However, if the receptionist habitually logged in with a local administrator account, the attacker could potentially install malware or ransomware on the entire system.**

## Implementation tips

Create a password policy that balances security with usability. Educate users about password security without creating such complex requirements that they resort to insecure workarounds. Regularly audit password practices and provide training on recognizing and avoiding phishing attempts that target credentials.

## Summary

Password management is essential for protecting digital accounts. Strong passwords should be long, unique, and private. Avoid password reuse and change default credentials immediately. Use secure password reset processes and leverage password managers for safe storage and generation. Enhance security with multifactor authentication and manage access through proper account privileges. A balanced password policy and user awareness are key to reducing credential-related risks.

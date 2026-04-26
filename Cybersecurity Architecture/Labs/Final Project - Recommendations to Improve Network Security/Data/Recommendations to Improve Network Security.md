# Final Project: Recommendations to Improve Network Security

**Estimated time needed:** 40 minutes

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective                                                                          |
| - | ---------------------------------------------------------------------------------- |
| 1 | Propose security enhancements based on the infrastructure evaluation               |
| 2 | Identify common web application security vulnerabilities based on OWASP guidelines |
| 3 | Recommend solutions to address basic OWASP security concerns                       |

---

## Project Structure

The final project is divided into **two parts**:

| Part             | Description                                                                               |
| ---------------- | ----------------------------------------------------------------------------------------- |
| **Part 1** | Evaluate the existing infrastructure and recommend security enhancements for the scenario |
| **Part 2** | Answer questions related to the scenario and recommendations (graded quiz)                |

---

## Scenario: Jackson Corporation

Jackson Corporation is experiencing a surge in cyberthreats. The company has hired you to evaluate its existing infrastructure and recommend security enhancements.

After reviewing the existing network and processes, you have identified various concerns. The table summarizes these concerns by component.

---

## Findings Summary

| #           | Network Component                                   | Findings                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------- | --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | **Firewall**                                  | Currently, Jackson Corporation has only one firewall that indiscriminately filters both external traffic from the internet and internal traffic from within the organization. This setup poses a potential risk as it does not allow for targeted security protocols based on the traffic source.                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **2** | **Web Servers**                               | Jackson Corporation's web server is located internally within the organization's primary network. This setup means that the server, a crucial and sensitive asset, is exposed to the same potential risks as the rest of the internal network. In terms of security, a basic firewall is the only mechanism in place for protecting the web server. This singular firewall is tasked with filtering both incoming external traffic and internal traffic within the network, creating a potential vulnerability.                                                                                                                                                                                                            |
| **3** | **Network Monitoring**                        | Jackson Corporation's network infrastructure currently consists of wired and wireless networks. All devices, including employee workstations, servers, and other digital assets, are interconnected within this network. There is no comprehensive system to centrally monitor, log, and analyze security events across the entire network. While this interconnected setup allows for operational efficiency, it also opens potential vulnerabilities that internal or external threats can exploit. Currently, there is no comprehensive system in place. This limitation makes threat detection and incident response slower and less efficient, leaving the corporation at increased risk.                             |
| **4** | **Breach Detection**                          | As it currently stands, Jackson Corporation primarily relies on a basic network monitoring system. This system monitors traffic and network performance but lacks an advanced threat detection mechanism. The current setup involves regular checks on network health, performance statistics, and traffic volume. However, it does not provide detailed analysis or real-time alerts about potential security threats, anomalies, or suspicious activities. While this setup allows for maintaining basic network performance, it falls short in proactively identifying and mitigating potential security threats. As a result, the company might not be able to detect a cyberthreat until after a breach has occurred. |
| **5** | **Remote Work**                               | As Jackson Corporation expands globally, its workforce becomes increasingly remote and mobile. Employees frequently travel or work from home, needing to access the corporation's internal resources from different parts of the world. Users are currently accessing shared resources using web-based tools. However, accessing these resources over public or unsecured networks poses significant security risks. The data exchanged could be intercepted and compromised by malicious entities. The absence of a secure remote access solution could potentially limit productivity and efficiency while also exposing internal resources to unnecessary security risks.                                               |
| **6** | **Software Development**                      | Jackson Corporation currently follows a traditional waterfall approach to software development. Developers code in isolation, focusing primarily on software functionality, with little consideration for potential security vulnerabilities. Code reviews are not a regular practice and are typically only conducted on an ad hoc basis when a problem arises. The final product is then passed to a separate team for testing before deployment. The current process creates gaps in understanding and practicing secure coding principles. Without focusing on security from the outset and regular code reviews, vulnerabilities could be overlooked and make their way into deployed software.                       |
| **7** | **Web Application Security (OWASP Concerns)** | During the security audit, several common web application vulnerabilities were discovered in Jackson Corporation's customer portal and internal web applications. These issues align with common OWASP security risks.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

---

## OWASP Issues Details

| Issue             | Description                                                                                                                                                                                                                                                                                                    |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Issue A** | **Weak password policy** - The system allows users to create simple passwords like "password123" or "12345678". There are no requirements for password complexity (uppercase letters, numbers, or special characters), and there is no minimum length requirement beyond 6 characters.                   |
| **Issue B** | **Unencrypted sensitive data** - Customer credit card information and social security numbers are stored in the database in plain text format (not encrypted). If an attacker gains access to the database, they can easily read all this sensitive information.                                         |
| **Issue C** | **No input validation** - The search box and contact forms on the website accept any type of input without checking or cleaning it. Users can type special characters and code into these fields, which could allow attackers to inject malicious code into the system.                                  |
| **Issue D** | **Detailed error messages** - When something goes wrong on the website, error messages display detailed technical information including database names, file paths, and system configuration details. This information could help attackers understand how the system works and find ways to exploit it. |

---

# Part 1: Recommendations

Based on the findings listed in the scenario, provide your recommended solutions to improve network security.

---

## Recommendation 1: Firewall

### Current Problem

Jackson Corporation has only **one firewall** that indiscriminately filters both external and internal traffic, lacking targeted security protocols based on traffic source.

### Recommended Solution

| Recommendation                                   | Details                                                            |
| ------------------------------------------------ | ------------------------------------------------------------------ |
| **Implement a Dual Firewall Architecture** | Deploy two separate firewalls instead of one                       |
| **External Firewall**                      | Place at the network perimeter to filter incoming internet traffic |
| **Internal Firewall**                      | Place between DMZ and internal network to filter internal traffic  |
| **Separate Rulesets**                      | Create different rules for external vs internal traffic            |

### Specific Recommendations

```
┌─────────────────────────────────────────────────────────────────┐
│                   RECOMMENDED FIREWALL ARCHITECTURE              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   INTERNET ──► [External Firewall] ──► DMZ ──► [Internal Firewall] ──► Internal Network
│                                                                  │
│   External Firewall Rules:                                       │
│   • Allow only HTTPS (443) and VPN traffic from internet         │
│   • Block all other inbound traffic                              │
│   • Enable DDoS protection                                       │
│                                                                  │
│   Internal Firewall Rules:                                       │
│   • Allow only necessary communication between DMZ and Internal  │
│   • Restrict database access to application servers only         │
│   • Log all traffic for audit purposes                           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Recommendation 2: Web Servers

### Current Problem

The web server is located **internally** within the primary network, exposing it to the same risks as the rest of the internal network.

### Recommended Solution

| Recommendation                        | Details                                                 |
| ------------------------------------- | ------------------------------------------------------- |
| **Relocate Web Server to DMZ**  | Move the web server to a Demilitarized Zone (DMZ)       |
| **Create Network Segmentation** | Separate public-facing servers from internal assets     |
| **Implement Defense-in-Depth**  | Add multiple layers of protection around the web server |

### Specific Recommendations

```
┌─────────────────────────────────────────────────────────────────┐
│                   RECOMMENDED WEB SERVER ARCHITECTURE            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   BEFORE (Current):                                              │
│   INTERNET ──► Firewall ──► Internal Network [Web Server]        │
│                                                                  │
│   AFTER (Recommended):                                           │
│   INTERNET ──► External FW ──► DMZ [Web Server] ──► Internal FW ──► Internal Network
│                                                                  │
│   Additional Protections:                                        │
│   • Add WAF (Web Application Firewall) in front of web server    │
│   • Implement SSL/TLS encryption for all web traffic             │
│   • Regular security patching and vulnerability scanning         │
│   • Harden web server configuration (disable unnecessary services)│
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Recommendation 3: Network Monitoring

### Current Problem

No comprehensive system to centrally monitor, log, and analyze security events across the entire network.

### Recommended Solution

| Recommendation                 | Details                                                          |
| ------------------------------ | ---------------------------------------------------------------- |
| **Deploy SIEM System**   | Implement Security Information and Event Management (SIEM)       |
| **Centralized Logging**  | Collect logs from all network devices, servers, and applications |
| **Real-time Monitoring** | Enable continuous monitoring of network activity                 |

### Specific Recommendations

```
┌─────────────────────────────────────────────────────────────────┐
│                   RECOMMENDED MONITORING ARCHITECTURE            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   Components to Deploy:                                          │
│                                                                  │
│   1. SIEM Platform (e.g., Splunk, IBM QRadar, ELK Stack)         │
│      • Centralized log collection                                │
│      • Log correlation and analysis                              │
│      • Automated alerting                                        │
│                                                                  │
│   2. Log Sources to Monitor:                                     │
│      • Firewalls (external and internal)                         │
│      • Web servers and application servers                       │
│      • Database servers                                          │
│      • Employee workstations                                     │
│      • Network devices (routers, switches)                       │
│                                                                  │
│   3. Monitoring Capabilities:                                    │
│      • Real-time dashboards                                      │
│      • Anomaly detection                                         │
│      • Compliance reporting                                      │
│      • Incident response workflows                               │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Recommendation 4: Breach Detection

### Current Problem

Basic network monitoring lacks advanced threat detection mechanisms, real-time alerts, and proactive identification of security threats.

### Recommended Solution

| Recommendation                          | Details                                                     |
| --------------------------------------- | ----------------------------------------------------------- |
| **Deploy IDS/IPS**                | Implement Intrusion Detection and Prevention Systems        |
| **Add Advanced Threat Detection** | Use behavior-based and signature-based detection            |
| **Enable Real-time Alerting**     | Configure immediate notifications for suspicious activities |

### Specific Recommendations

```
┌─────────────────────────────────────────────────────────────────┐
│                  RECOMMENDED BREACH DETECTION                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   Intrusion Detection System (IDS):                              │
│   • Deploy at key network segments                               │
│   • Monitor for known attack patterns (signature-based)          │
│   • Detect anomalous behavior (behavior-based)                   │
│   • Generate alerts without blocking traffic                     │
│                                                                  │
│   Intrusion Prevention System (IPS):                             │
│   • Deploy inline at critical boundaries                         │
│   • Automatically block malicious traffic                        │
│   • Integrate with firewall for dynamic blocking                 │
│                                                                  │
│   Endpoint Detection and Response (EDR):                         │
│   • Install on all endpoints (workstations, servers)             │
│   • Detect ransomware and malware                                │
│   • Enable forensic investigation capabilities                   │
│                                                                  │
│   Alerting Configuration:                                        │
│   • Real-time email/SMS alerts for critical threats              │
│   • Integration with SIEM for correlation                        │
│   • 24/7 security monitoring                                     │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Recommendation 5: Remote Work

### Current Problem

No secure remote access solution exists. Employees access internal resources over public/unsecured networks, risking data interception.

### Recommended Solution

| Recommendation                 | Details                                                          |
| ------------------------------ | ---------------------------------------------------------------- |
| **Deploy VPN Solution**  | Implement Virtual Private Network (VPN) for secure remote access |
| **Implement Zero Trust** | Adopt Zero Trust Network Access (ZTNA) principles                |
| **Enable MFA**           | Require multi-factor authentication for all remote access        |

### Specific Recommendations

```
┌─────────────────────────────────────────────────────────────────┐
│                 RECOMMENDED REMOTE ACCESS SOLUTION               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   VPN Gateway:                                                   │
│   • Deploy SSL/TLS VPN for remote access                         │
│   • Encrypt all traffic between remote users and corporate network│
│   • Require VPN for all remote connections                       │
│                                                                  │
│   Multi-Factor Authentication (MFA):                             │
│   • Require MFA for all remote access                            │
│   • Options: SMS codes, authenticator app, hardware tokens       │
│   • Never rely on password alone                                 │
│                                                                  │
│   Access Controls:                                               │
│   • Implement least privilege access                             │
│   • Restrict remote access to only necessary resources           │
│   • Segment remote users from sensitive internal systems         │
│                                                                  │
│   Additional Security Measures:                                  │
│   • Require endpoint compliance checks (patch level, antivirus)  │
│   • Implement session timeouts                                   │
│   • Log and monitor all remote access attempts                   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Recommendation 6: Software Development

### Current Problem

Traditional waterfall approach with isolated coding, ad hoc code reviews, separate testing team, and no focus on security from the outset.

### Recommended Solution

| Recommendation                  | Details                                           |
| ------------------------------- | ------------------------------------------------- |
| **Adopt DevSecOps**       | Integrate security into the development lifecycle |
| **Implement Secure SDLC** | Add security checks at every phase of development |
| **Regular Code Reviews**  | Mandatory peer reviews for all code changes       |

### Specific Recommendations

```
┌─────────────────────────────────────────────────────────────────┐
│              RECOMMENDED SOFTWARE DEVELOPMENT PROCESS            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   Phase 1: Requirements & Design                                │
│   • Conduct threat modeling                                      │
│   • Define security requirements                                 │
│   • Perform security design reviews                              │
│                                                                  │
│   Phase 2: Development                                           │
│   • Secure coding training for all developers                    │
│   • Use static code analysis tools (SAST)                        │
│   • Mandatory peer code reviews for every commit                 │
│                                                                  │
│   Phase 3: Testing                                               │
│   • Dynamic application security testing (DAST)                  │
│   • Penetration testing before release                           │
│   • Automated vulnerability scanning                             │
│                                                                  │
│   Phase 4: Deployment & Maintenance                              │
│   • Continuous integration/continuous deployment (CI/CD)         │
│   • Regular security patches                                     │
│   • Bug bounty program (optional)                                │
│                                                                  │
│   Recommended Tools:                                             │
│   • SAST: SonarQube, Checkmarx, Fortify                          │
│   • DAST: OWASP ZAP, Burp Suite                                  │
│   • CI/CD: Jenkins, GitLab CI, GitHub Actions                    │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Recommendation 7: Web Application Security (OWASP Concerns)

### Issue A: Weak Password Policy

| Current Problem                                    | Recommended Solution                                        |
| -------------------------------------------------- | ----------------------------------------------------------- |
| Passwords like "password123" or "12345678" allowed | Implement strong password policy                            |
| No complexity requirements                         | Require complexity (uppercase, lowercase, numbers, symbols) |
| Only 6-character minimum                           | Increase minimum length                                     |

#### Specific Recommendations

```
┌─────────────────────────────────────────────────────────────────┐
│                   RECOMMENDED PASSWORD POLICY                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   Password Complexity Requirements:                              │
│   • Minimum length: 12 characters                                │
│   • At least 1 uppercase letter (A-Z)                            │
│   • At least 1 lowercase letter (a-z)                            │
│   • At least 1 number (0-9)                                      │
│   • At least 1 special character (!@#$%^&*)                      │
│                                                                  │
│   Additional Security Measures:                                  │
│   • Implement Multi-Factor Authentication (MFA)                  │
│   • Block common passwords (e.g., haveibeenpwned database)       │
│   • Prevent password reuse (remember last 10 passwords)          │
│   • Enforce password changes every 90 days                       │
│   • Lock account after 5 failed attempts                         │
│                                                                  │
│   Example of a strong password:                                  │
│   "MySecureP@ssw0rd2024!"                                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

### Issue B: Unencrypted Sensitive Data

| Current Problem                               | Recommended Solution                       |
| --------------------------------------------- | ------------------------------------------ |
| Credit card numbers stored in plain text      | Encrypt sensitive data at rest             |
| Social security numbers unencrypted           | Use strong encryption algorithms           |
| Anyone with database access can read all data | Implement data masking and access controls |

#### Specific Recommendations

```
┌─────────────────────────────────────────────────────────────────┐
│              RECOMMENDED DATA PROTECTION STRATEGY                │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   Encryption at Rest:                                            │
│   • Use AES-256 encryption for stored sensitive data             │
│   • Encrypt credit card numbers, SSNs, and PII                   │
│   • Use transparent data encryption (TDE) for databases          │
│                                                                  │
│   Encryption in Transit:                                         │
│   • Use TLS 1.2+ for all data transmission                       │
│   • Encrypt database connections                                 │
│   • Use HTTPS for all web traffic                                │
│                                                                  │
│   Key Management:                                                │
│   • Use a Hardware Security Module (HSM) or key management service│
│   • Rotate encryption keys regularly                             │
│   • Never hardcode keys in source code                           │
│                                                                  │
│   Additional Protections:                                        │
│   • Tokenize credit card numbers (replace with tokens)           │
│   • Implement data masking for non-production environments       │
│   • Apply least privilege database access                        │
│   • Log all access to sensitive data                             │
│                                                                  │
│   Compliance Note: PCI DSS requires encryption for cardholder data│
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

### Issue C: No Input Validation

| Current Problem                                  | Recommended Solution                       |
| ------------------------------------------------ | ------------------------------------------ |
| Search box accepts any input                     | Validate all user inputs before processing |
| Contact forms accept special characters and code | Sanitize and escape special characters     |
| Potential for SQL injection and XSS attacks      | Use parameterized queries                  |

#### Specific Recommendations

```
┌─────────────────────────────────────────────────────────────────┐
│              RECOMMENDED INPUT VALIDATION STRATEGY               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   Input Validation Approaches:                                   │
│                                                                  │
│   1. Whitelist Validation (Allowlisting):                        │
│      • Define exactly what is allowed                            │
│      • Reject anything not on the list                           │
│      • Most secure approach                                      │
│                                                                  │
│   2. Blacklist Validation (Blocklisting):                        │
│      • Block known malicious patterns                            │
│      • Less secure (attackers can bypass)                        │
│                                                                  │
│   Specific Input Handling:                                       │
│                                                                  │
│   • Search Box: Limit to alphanumeric + spaces only              │
│   • Name Fields: Allow letters, spaces, hyphens, apostrophes     │
│   • Email Fields: Validate RFC 5322 email format                 │
│   • Phone Numbers: Allow only digits and basic separators        │
│   • Numeric Fields: Only accept digits 0-9                       │
│                                                                  │
│   Output Encoding (for prevention):                              │
│   • HTML Encode: Convert < to <, > to >                    │
│   • JavaScript Encode: Escape special characters                 │
│   • SQL Encode: Use parameterized queries                        │
│                                                                  │
│   Parameterized Queries (SQL Injection Prevention):              │
│                                                                  │
│   // Instead of:                                                │
│   String query = "SELECT * FROM users WHERE name = '" + name + "'";│
│                                                                  │
│   // Use:                                                       │
│   PreparedStatement stmt = conn.prepareStatement(                │
│       "SELECT * FROM users WHERE name = ?");                     │
│   stmt.setString(1, name);                                       │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

### Issue D: Detailed Error Messages

| Current Problem                             | Recommended Solution                       |
| ------------------------------------------- | ------------------------------------------ |
| Error messages show database names          | Show generic, user-friendly error messages |
| File paths and system configuration exposed | Log detailed errors internally only        |
| Attackers gain system information           | Never expose technical details to users    |

#### Specific Recommendations

```
┌─────────────────────────────────────────────────────────────────┐
│              RECOMMENDED ERROR HANDLING STRATEGY                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   User-Facing Error Messages (What users see):                   │
│                                                                  │
│   ✅ GOOD Examples:                                              │
│   • "Something went wrong. Please try again later."              │
│   • "Invalid login credentials. Please try again."               │
│   • "The page you requested cannot be found."                    │
│   • "An unexpected error occurred. Our team has been notified."  │
│                                                                  │
│   ❌ BAD Examples (Current):                                     │
│   • "SQL Error: Table 'customers.orders' doesn't exist"          │
│   • "Warning: Failed to connect to database at 192.168.1.100"    │
│   • "Fatal error: Uncaught exception in /var/www/html/includes/  │
│      database.php on line 42"                                    │
│                                                                  │
│   Internal Logging (What developers see):                        │
│                                                                  │
│   • Log full error details to centralized logging system (SIEM)  │
│   • Include: timestamp, error type, stack trace, user ID         │
│   • Store in secure, access-restricted location                  │
│   • Never include sensitive data (passwords, tokens) in logs     │
│                                                                  │
│   Implementation Guidelines:                                     │
│                                                                  │
│   1. Set production environment to "production mode"             │
│      - display_errors = Off                                      │
│      - log_errors = On                                           │
│                                                                  │
│   2. Use custom error pages (404, 500, 403)                      │
│                                                                  │
│   3. Implement proper exception handling                         │
│      try { ... } catch (Exception $e) {                          │
│          log_error($e->getMessage());                            │
│          show_generic_error_page();                              │
│      }                                                           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

# Recommendation Summary Table

| Component                              | Key Recommendations                                                               |
| -------------------------------------- | --------------------------------------------------------------------------------- |
| **1. Firewall**                  | Implement dual firewall architecture (external + internal) with separate rulesets |
| **2. Web Servers**               | Relocate web server to DMZ; add WAF; implement defense-in-depth                   |
| **3. Network Monitoring**        | Deploy SIEM for centralized logging and real-time monitoring                      |
| **4. Breach Detection**          | Implement IDS/IPS, EDR, and real-time alerting                                    |
| **5. Remote Work**               | Deploy VPN with MFA; implement Zero Trust principles                              |
| **6. Software Development**      | Adopt DevSecOps; implement Secure SDLC; regular code reviews                      |
| **7a. OWASP - Passwords**        | 12-character minimum; complexity requirements; MFA                                |
| **7b. OWASP - Encryption**       | AES-256 encryption for sensitive data at rest and in transit                      |
| **7c. OWASP - Input Validation** | Whitelist validation; parameterized queries; output encoding                      |
| **7d. OWASP - Error Messages**   | Generic user messages; detailed internal logging only                             |

---

# Part 2: Quiz Questions

Use your recommendations above to answer the following questions. These will be part of a graded quiz.

---

## Question 1: Firewall Architecture

**What is the primary problem with Jackson Corporation's current single firewall setup?**

A. The firewall is too expensive to maintain
B. The firewall cannot filter both external and internal traffic effectively
C. The firewall indiscriminately filters both external and internal traffic without targeted security protocols
D. The firewall blocks all legitimate traffic

**Answer:** _______

---

## Question 2: Web Server Placement

**Where should Jackson Corporation relocate its web server to improve security?**

A. Outside the network perimeter
B. In a cloud environment only
C. In a Demilitarized Zone (DMZ) between external and internal firewalls
D. On employee workstations

**Answer:** _______

---

## Question 3: Network Monitoring Solution

**What system should Jackson Corporation deploy to centrally monitor, log, and analyze security events?**

A. A basic network monitoring system
B. A SIEM (Security Information and Event Management) system
C. A spreadsheet for manual log review
D. A single firewall

**Answer:** _______

---

## Question 4: Breach Detection

**Which of the following should be deployed for advanced threat detection and real-time alerts?**

A. Only a basic network monitor
B. IDS/IPS (Intrusion Detection/Prevention System)
C. Additional workstations
D. More web servers

**Answer:** _______

---

## Question 5: Remote Work Security

**What is the recommended solution for secure remote access to internal resources?**

A. Allow employees to use any public Wi-Fi without restrictions
B. Deploy a VPN with Multi-Factor Authentication (MFA)
C. Disable remote access completely
D. Use only web-based tools without encryption

**Answer:** _______

---

## Question 6: Software Development Process

**What approach should Jackson Corporation adopt to integrate security into the development lifecycle?**

A. Continue using isolated waterfall development
B. Adopt DevSecOps with security at every phase
C. Eliminate all code reviews
D. Skip security testing to save time

**Answer:** _______

---

## Question 7: Password Policy (OWASP Issue A)

**What minimum length should Jackson Corporation require for passwords?**

A. 6 characters
B. 8 characters
C. 12 characters
D. No minimum

**Answer:** _______

---

## Question 8: Password Complexity (OWASP Issue A)

**Which of the following should be required in passwords? (Select all that apply)**

☐ Uppercase letters (A-Z)
☐ Lowercase letters (a-z)
☐ Numbers (0-9)
☐ Special characters (!@#$%^&*)

---

## Question 9: Data Encryption (OWASP Issue B)

**How should sensitive data like credit card numbers and SSNs be stored in the database?**

A. In plain text for easy access
B. Encrypted using AES-256
C. In a separate spreadsheet
D. Only in email attachments

**Answer:** _______

---

## Question 10: Input Validation (OWASP Issue C)

**What is the most secure approach to input validation?**

A. Blacklist validation (blocking known bad patterns)
B. No validation at all
C. Whitelist validation (allowing only known good input)
D. Accepting all input as-is

**Answer:** _______

---

## Question 11: SQL Injection Prevention (OWASP Issue C)

**What technique prevents SQL injection attacks?**

A. Using string concatenation in SQL queries
B. Parameterized queries (prepared statements)
C. Disabling all security features
D. Storing passwords in plain text

**Answer:** _______

---

## Question 12: Error Messages (OWASP Issue D)

**What should error messages show to users?**

A. Detailed database names and file paths
B. System configuration details
C. Generic, user-friendly error messages (e.g., "Something went wrong")
D. Full stack traces

**Answer:** _______

---

## Question 13: Error Logging (OWASP Issue D)

**Where should detailed error information be stored?**

A. Displayed on the user's screen
B. In an internal, secure logging system (SIEM)
C. Never logged at all
D. Emailed to all employees

**Answer:** _______

---

## Question 14: Additional Authentication (OWASP Issue A)

**What additional security measure should be implemented alongside strong passwords?**

A. Allow "password123" as an exception
B. Multi-Factor Authentication (MFA)
C. No additional measures needed
D. Store passwords in plain text for recovery

**Answer:** _______

---

## Question 15: Secure Coding Practice

**What should developers do before integrating new code?**

A. Skip code reviews to save time
B. Always require peer code reviews
C. Only review code when problems arise
D. Never review code

**Answer:** _______

---

## Question 16: Remote Access Authentication

**What should be required for all remote access connections?**

A. Only a username
B. Multi-Factor Authentication (MFA)
C. No authentication required
D. Only a simple password

**Answer:** _______

---

## Question 17: Encryption in Transit

**What protocol should be used to encrypt web traffic?**

A. HTTP (no encryption)
B. FTP
C. TLS (HTTPS)
D. Telnet

**Answer:** _______

---

## Question 18: Web Application Firewall (WAF)

**What additional control should be added in front of the web server?**

A. Another database server
B. Web Application Firewall (WAF)
C. More employee workstations
D. Remove all security controls

**Answer:** _______

---

# Answer Key

| Q# | Answer                                                     |
| -- | ---------------------------------------------------------- |
| 1  | C                                                          |
| 2  | C                                                          |
| 3  | B                                                          |
| 4  | B                                                          |
| 5  | B                                                          |
| 6  | B                                                          |
| 7  | C                                                          |
| 8  | All ☐ (Uppercase, Lowercase, Numbers, Special characters) |
| 9  | B                                                          |
| 10 | C                                                          |
| 11 | B                                                          |
| 12 | C                                                          |
| 13 | B                                                          |
| 14 | B                                                          |
| 15 | B                                                          |
| 16 | B                                                          |
| 17 | C                                                          |
| 18 | B                                                          |

---

## OWASP Top 10 Reference for This Lab

| OWASP Risk                                                      | Issue in Lab                      | Solution                                      |
| --------------------------------------------------------------- | --------------------------------- | --------------------------------------------- |
| **A01:2021 - Broken Access Control**                      | Not directly addressed            | Implement proper access controls              |
| **A02:2021 - Cryptographic Failures**                     | Issue B (unencrypted data)        | Encrypt sensitive data at rest and in transit |
| **A03:2021 - Injection**                                  | Issue C (no input validation)     | Input validation + parameterized queries      |
| **A04:2021 - Insecure Design**                            | Issue D (detailed errors)         | Proper error handling design                  |
| **A05:2021 - Security Misconfiguration**                  | Issue D (detailed error exposure) | Disable verbose error messages in production  |
| **A07:2021 - Identification and Authentication Failures** | Issue A (weak passwords)          | Strong password policy + MFA                  |

---

## Submission Checklist

| Item                                                | Completed |
| --------------------------------------------------- | --------- |
| Recommendation 1: Firewall                          | ☐        |
| Recommendation 2: Web Servers                       | ☐        |
| Recommendation 3: Network Monitoring                | ☐        |
| Recommendation 4: Breach Detection                  | ☐        |
| Recommendation 5: Remote Work                       | ☐        |
| Recommendation 6: Software Development              | ☐        |
| Recommendation 7a: OWASP Issue A (Passwords)        | ☐        |
| Recommendation 7b: OWASP Issue B (Encryption)       | ☐        |
| Recommendation 7c: OWASP Issue C (Input Validation) | ☐        |
| Recommendation 7d: OWASP Issue D (Error Messages)   | ☐        |
| Quiz Questions Completed                            | ☐        |

---

## Summary

Congratulations! You have completed the **Final Project: Recommendations to Improve Network Security**. You have:

| Achievement                                                | Completed |
| ---------------------------------------------------------- | --------- |
| Evaluated existing infrastructure vulnerabilities          | ☐        |
| Proposed security enhancements for 7 key areas             | ☐        |
| Addressed 4 specific OWASP web application security issues | ☐        |
| Provided practical, actionable recommendations             | ☐        |
| Prepared for the graded quiz                               | ☐        |

These skills are essential for:

- Security consultants assessing organizational risk
- Network administrators implementing security improvements
- Security architects designing secure infrastructures
- Compliance officers ensuring security best practices

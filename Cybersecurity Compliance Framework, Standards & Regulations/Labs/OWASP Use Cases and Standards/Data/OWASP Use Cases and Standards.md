![alt text](<../Screenshots/OWASP.png>)

# Hands-on Lab: OWASP Use Cases and Standards

**Estimated time needed:** 45 minutes

---

## Overview

The Open Web Application Security Project (OWASP) is a nonprofit organization focused on making software more secure. It started on December 1, 2001, and became an official nonprofit in the U.S. on April 21, 2004. OWASP works by offering free resources like code, guides, and standards to help with safe software creation and use.

In this hands-on lab, you will explore OWASP standards, understand their purposes, and apply them to real-world use cases.

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective                                                   |
| - | ----------------------------------------------------------- |
| 1 | List the major OWASP standards and resources                |
| 2 | Describe the purpose of each OWASP standard                 |
| 3 | Apply OWASP standards to real-world security scenarios      |
| 4 | Identify appropriate OWASP resources for specific use cases |
| 5 | Create a security program using OWASP frameworks            |

---

## Prerequisites

| Requirement     | Description                                     |
| --------------- | ----------------------------------------------- |
| Internet access | For accessing OWASP resources and documentation |
| Web browser     | For research                                    |
| Word processor  | For documentation                               |

---

## Background: OWASP Standards Overview

OWASP has established various standards and resources to improve the security of software and web applications. Among these, the most recognized include:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         OWASP STANDARDS & RESOURCES                          │
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                         OWASP TOP 10                                 │   │
│   │              Top 10 Critical Web Application Security Risks          │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
│   ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐            │
│   │      ASVS       │  │     MASVS       │  │      SAMM       │            │
│   │ Application     │  │   Mobile App    │  │   Software      │            │
│   │ Security        │  │   Security      │  │   Assurance     │            │
│   │ Verification    │  │   Verification  │  │   Maturity      │            │
│   │ Standard        │  │   Standard      │  │   Model         │            │
│   └─────────────────┘  └─────────────────┘  └─────────────────┘            │
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                    OWASP TESTING GUIDE                               │   │
│   │         Framework for Security Testing of Web Applications           │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                    OWASP CHEAT SHEET SERIES                          │   │
│   │         Concise, High-Value Security Guidance Documents              │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Exercise 1: OWASP Top 10

### Overview

The OWASP Top 10 is a widely recognized document that outlines the ten most critical web application security risks, serving as a guideline for developers and security professionals to understand and mitigate prevalent vulnerabilities.

### Step 1: Research the OWASP Top 10 (2021)

Navigate to the OWASP Top 10 page: <https://owasp.org/Top10/>

**Complete the table with the latest OWASP Top 10 risks:**

| Rank | Risk Category | Description | Example |
| ---- | ------------- | ----------- | ------- |
| A01  |               |             |         |
| A02  |               |             |         |
| A03  |               |             |         |
| A04  |               |             |         |
| A05  |               |             |         |
| A06  |               |             |         |
| A07  |               |             |         |
| A08  |               |             |         |
| A09  |               |             |         |
| A10  |               |             |         |

### Step 2: OWASP Top 10 Use Case Scenario

**Scenario:** A small e-commerce company has just been informed by a security researcher that their website may have multiple security vulnerabilities. The development team is unsure where to start.

**Your Task:** Based on the OWASP Top 10, which risks should they prioritize and why?

```
Top 3 risks to prioritize:
1. _________________________________________________________________________
   Why: ____________________________________________________________________

2. _________________________________________________________________________
   Why: ____________________________________________________________________

3. _________________________________________________________________________
   Why: ____________________________________________________________________
```

### Step 3: Mitigation Mapping

For each of the top 3 risks above, identify at least one mitigation strategy:

| Risk | Mitigation Strategy |
| ---- | ------------------- |
| 1    |                     |
| 2    |                     |
| 3    |                     |

---

## Exercise 2: OWASP ASVS (Application Security Verification Standard)

### Overview

The OWASP Application Security Verification Standard (ASVS) is a framework for assessing the security of web applications and services. It provides comprehensive security requirements and controls that guide developers and organizations in creating and maintaining secure applications.

### Step 1: ASVS Levels

ASVS categorizes requirements into different levels of assurance:

| Level   | Description | Target Applications |
| ------- | ----------- | ------------------- |
| Level 1 |             |                     |
| Level 2 |             |                     |
| Level 3 |             |                     |

**Your Task:** Research and complete the table above.

### Step 2: ASVS Use Case Scenario

**Scenario:** A healthcare startup is developing a patient portal that will store sensitive medical records and personally identifiable information (PII). The application must comply with HIPAA regulations.

**Your Task:**

1. Which ASVS level should they target? _______________
2. Why? ________________________________________________
3. What are three key verification requirements they should focus on?

| Requirement Area | Specific Verification Requirement |
| ---------------- | --------------------------------- |
| 1                |                                   |
| 2                |                                   |
| 3                |                                   |

### Step 3: ASVS Verification Mapping

Match the following ASVS categories with their descriptions:

| Category                                  | Description                                               |
| ----------------------------------------- | --------------------------------------------------------- |
| V1: Architecture, Design, Threat Modeling | A. Verify that user identities are properly managed       |
| V2: Authentication                        | B. Verify that cryptographic functions are used correctly |
| V3: Session Management                    | C. Verify security controls are designed and documented   |
| V4: Access Control                        | D. Verify that session tokens are secure                  |
| V5: Validation, Sanitization, Encoding    | E. Verify that users cannot act outside their permissions |
| V6: Cryptography                          | F. Verify that input is validated and output is encoded   |

**Answers:**
V1-****, V2-****, V3-****, V4-****, V5-****, V6-****

---

## Exercise 3: OWASP MASVS (Mobile Application Security Verification Standard)

### Overview

The OWASP Mobile Application Security Verification Standard (MASVS) is a framework to establish a security baseline for mobile applications. It provides a comprehensive set of security requirements that developers and testers can follow to ensure their mobile applications are secure.

### Step 1: MASVS Levels

| Level    | Description | Target Applications |
| -------- | ----------- | ------------------- |
| MASVS-L1 |             |                     |
| MASVS-L2 |             |                     |
| MASVS-R  |             |                     |

**Your Task:** Research and complete the table above.

### Step 2: MASVS Use Case Scenario

**Scenario:** A financial technology (FinTech) company is developing a mobile banking app that will handle money transfers, account management, and sensitive customer financial data. The app will be available on both iOS and Android.

**Your Task:**

1. Which MASVS level should they target? _______________
2. Why? ________________________________________________

### Step 3: Mobile-Specific Security Requirements

Identify 5 mobile-specific security requirements from MASVS:

| # | Requirement | Why Important for Mobile |
| - | ----------- | ------------------------ |
| 1 |             |                          |
| 2 |             |                          |
| 3 |             |                          |
| 4 |             |                          |
| 5 |             |                          |

---

## Exercise 4: OWASP SAMM (Software Assurance Maturity Model)

### Overview

The OWASP Software Assurance Maturity Model (SAMM) is an open framework designed to help organizations formulate and implement a strategy for software security that integrates easily into their existing Software Development Lifecycle (SDLC).

### Step 1: SAMM Business Functions

SAMM is structured around business functions. Identify each function and its objectives:

| Business Function | Description | Key Security Practices |
| ----------------- | ----------- | ---------------------- |
| Governance        |             |                        |
| Design            |             |                        |
| Implementation    |             |                        |
| Verification      |             |                        |
| Operations        |             |                        |

### Step 2: SAMM Maturity Levels

| Level | Description | Characteristics |
| ----- | ----------- | --------------- |
| 0     |             |                 |
| 1     |             |                 |
| 2     |             |                 |
| 3     |             |                 |

### Step 3: SAMM Use Case Scenario

**Scenario:** A medium-sized software company with 100 developers currently has no formal software security program. Security is only considered when a problem is found in production. The company wants to mature its security practices over the next 2 years.

**Your Task:** Create a SAMM-based roadmap for Year 1:

| Quarter | Business Function Focus | Specific Activities | Target Maturity Level |
| ------- | ----------------------- | ------------------- | --------------------- |
| Q1      |                         |                     |                       |
| Q2      |                         |                     |                       |
| Q3      |                         |                     |                       |
| Q4      |                         |                     |                       |

---

## Exercise 5: OWASP Testing Guide

### Overview

The OWASP Testing Guide is a comprehensive manual that provides a framework for the security testing of web applications and services. It is designed to help organizations understand and implement a robust testing program.

### Step 1: Testing Phases

List the main phases of the OWASP Testing Framework:

| Phase | Description |
| ----- | ----------- |
| 1     |             |
| 2     |             |
| 3     |             |
| 4     |             |
| 5     |             |

### Step 2: Testing Guide Use Case Scenario

**Scenario:** A SaaS company is about to release a new version of their web application. They want to conduct a comprehensive security test before release but have never done formal security testing before.

**Your Task:** Create a test plan using the OWASP Testing Guide:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    SECURITY TEST PLAN (Based on OWASP Testing Guide)        │
└─────────────────────────────────────────────────────────────────────────────┘

PHASE 1: INFORMATION GATHERING
─────────────────────────────────────────────────────────────────────────────
Tests to perform:
• 
• 
• 

PHASE 2: CONFIGURATION AND DEPLOYMENT MANAGEMENT TESTING
─────────────────────────────────────────────────────────────────────────────
Tests to perform:
• 
• 
• 

PHASE 3: IDENTITY MANAGEMENT TESTING
─────────────────────────────────────────────────────────────────────────────
Tests to perform:
• 
• 
• 

PHASE 4: AUTHENTICATION TESTING
─────────────────────────────────────────────────────────────────────────────
Tests to perform:
• 
• 
• 

PHASE 5: AUTHORIZATION TESTING
─────────────────────────────────────────────────────────────────────────────
Tests to perform:
• 
• 
• 

PHASE 6: SESSION MANAGEMENT TESTING
─────────────────────────────────────────────────────────────────────────────
Tests to perform:
• 
• 
• 

PHASE 7: INPUT VALIDATION TESTING
─────────────────────────────────────────────────────────────────────────────
Tests to perform:
• 
• 
• 

PHASE 8: ERROR HANDLING TESTING
─────────────────────────────────────────────────────────────────────────────
Tests to perform:
• 
• 
• 

PHASE 9: BUSINESS LOGIC TESTING
─────────────────────────────────────────────────────────────────────────────
Tests to perform:
• 
• 
• 

PHASE 10: CLIENT-SIDE TESTING
─────────────────────────────────────────────────────────────────────────────
Tests to perform:
• 
• 
•
```

### Step 3: Testing Methodology Comparison

Compare manual vs automated testing approaches:

| Aspect          | Manual Testing | Automated Testing |
| --------------- | -------------- | ----------------- |
| Best for        |                |                   |
| Limitations     |                |                   |
| Tools           |                |                   |
| Time investment |                |                   |
| False positives |                |                   |

---

## Exercise 6: OWASP Cheat Sheet Series

### Overview

The OWASP Cheat Sheet Series is a collection of concise, high-value documents on various application security topics created by seasoned security professionals. These cheat sheets provide quick, practical security guidance in an easily digestible format.

### Step 1: Explore OWASP Cheat Sheets

Visit the OWASP Cheat Sheet Series: <https://cheatsheetseries.owasp.org/>

**Find cheat sheets for the following topics:**

| Topic                                 | Cheat Sheet Name | Key Recommendations (3) |
| ------------------------------------- | ---------------- | ----------------------- |
| SQL Injection Prevention              |                  |                         |
| Cross-Site Scripting (XSS) Prevention |                  |                         |
| Authentication                        |                  |                         |
| Session Management                    |                  |                         |
| Cryptographic Storage                 |                  |                         |
| Input Validation                      |                  |                         |
| Error Handling                        |                  |                         |
| Logging                               |                  |                         |

### Step 2: Cheat Sheet Use Case Scenario

**Scenario:** A developer on your team is implementing a login feature and asks for quick guidance on secure authentication practices.

**Your Task:** Create a quick reference card (cheat sheet) for the developer:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│              SECURE AUTHENTICATION QUICK REFERENCE CARD                     │
│                         For Developers                                       │
└─────────────────────────────────────────────────────────────────────────────┘

PASSWORD REQUIREMENTS:
─────────────────────────────────────────────────────────────────────────────
• Minimum length: _________ characters
• Complexity requirements: __________________________________________________
• Password storage: ________________________________________________________
• Password recovery: _______________________________________________________

SESSION MANAGEMENT:
─────────────────────────────────────────────────────────────────────────────
• Session ID generation: ___________________________________________________
• Session timeout: _________ minutes
• Logout implementation: ___________________________________________________
• Concurrent sessions: ☐ Allow ☐ Block

MULTI-FACTOR AUTHENTICATION (MFA):
─────────────────────────────────────────────────────────────────────────────
• When to require MFA: _____________________________________________________
• MFA methods to support: __________________________________________________
• Backup codes: ☐ Yes ☐ No

FAILED ATTEMPTS:
─────────────────────────────────────────────────────────────────────────────
• Maximum failed attempts: _________
• Account lockout duration: _________ minutes
• Notification on lockout: ☐ Yes ☐ No

API AUTHENTICATION:
─────────────────────────────────────────────────────────────────────────────
• Method: ☐ API Keys ☐ OAuth 2.0 ☐ JWT ☐ Other: _______
• Token expiration: _________ minutes
• Token storage: ___________________________________________________________
```

### Step 3: Create Your Own Cheat Sheet

Select a security topic of your choice (e.g., "Secure File Uploads," "API Security," "JWT Best Practices") and create a one-page cheat sheet:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    OWASP CHEAT SHEET (Custom)                                │
│                    Topic: ________________________________                   │
└─────────────────────────────────────────────────────────────────────────────┘

TOPIC OVERVIEW:
─────────────────────────────────────────────────────────────────────────────
Purpose: ____________________________________________________________________
Key risks: __________________________________________________________________

BEST PRACTICES:
─────────────────────────────────────────────────────────────────────────────
1. __________________________________________________________________________
   Implementation details: ___________________________________________________

2. __________________________________________________________________________
   Implementation details: ___________________________________________________

3. __________________________________________________________________________
   Implementation details: ___________________________________________________

4. __________________________________________________________________________
   Implementation details: ___________________________________________________

5. __________________________________________________________________________
   Implementation details: ___________________________________________________

CODE EXAMPLE (if applicable):
─────────────────────────────────────────────────────────────────────────────

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________


COMMON PITFALLS TO AVOID:
─────────────────────────────────────────────────────────────────────────────
• __________________________________________________________________________
• __________________________________________________________________________
• __________________________________________________________________________

ADDITIONAL RESOURCES:
─────────────────────────────────────────────────────────────────────────────
• __________________________________________________________________________
• __________________________________________________________________________

```


---

## Exercise 7: OWASP Standards Selection Exercise

### Scenario Matrix

For each scenario below, identify which OWASP resource would be MOST appropriate and explain why.

| Scenario | Appropriate OWASP Resource | Why? |
|----------|---------------------------|------|
| A developer needs quick guidance on preventing XSS attacks | | |
| An organization wants to assess their mobile banking app's security | | |
| A CISO wants to create a 3-year software security improvement plan | | |
| A security tester needs a methodology for testing a web app | | |
| A development team wants to prioritize fixing the most critical web risks | | |
| An organization needs a comprehensive framework to verify application security controls | | |
| A new developer wants to learn about secure coding practices | | |

---

## Exercise 8: Knowledge Check Questions

### Question 1
**When was OWASP founded?**

A. December 1, 2000  
B. December 1, 2001  
C. April 21, 2004  
D. January 1, 2005  

**Answer:** _______

---

### Question 2
**Which OWASP standard provides a framework for assessing web application security through different levels of assurance?**

A. OWASP Top 10  
B. OWASP ASVS  
C. OWASP MASVS  
D. OWASP SAMM  

**Answer:** _______

---

### Question 3
**What does MASVS stand for?**

A. Mobile Application Security Verification Standard  
B. Modern Application Security Verification System  
C. Mobile Authentication Security Verification Standard  
D. Main Application Security Verification Standard  

**Answer:** _______

---

### Question 4
**Which OWASP resource is designed to help organizations integrate security into their existing Software Development Lifecycle (SDLC)?**

A. OWASP Top 10  
B. OWASP Testing Guide  
C. OWASP SAMM  
D. OWASP Cheat Sheet Series  

**Answer:** _______

---

### Question 5
**True or False: The OWASP Cheat Sheet Series provides lengthy, comprehensive textbooks on each security topic.**

A. True  
B. False  

**Answer:** _______

---

### Question 6
**How often is the OWASP Top 10 updated?**

A. Every year  
B. Every 2-3 years (periodically)  
C. Every 5 years  
D. Never (one-time document)  

**Answer:** _______

---

### Question 7
**Match the OWASP resource with its primary purpose:**

| Resource | Purpose |
|----------|---------|
| 1. OWASP Top 10 | A. Framework for mobile app security verification |
| 2. OWASP Testing Guide | B. Critical web application security risks |
| 3. OWASP MASVS | C. Methodology for security testing |
| 4. OWASP Cheat Sheets | D. Quick practical security guidance |

**Answers:** 1-_____, 2-_____, 3-_____, 4-_____

---

### Question 8
**According to the reading, what are the different levels of assurance in ASVS tailored to?**

A. The developer's experience level  
B. The application's risk profile  
C. The programming language used  
D. The size of the organization  

**Answer:** _______

---

### Question 9
**Which OWASP resource would be most useful for a penetration tester conducting a security assessment?**

A. OWASP Top 10 only  
B. OWASP Testing Guide  
C. OWASP SAMM  
D. OWASP MASVS only  

**Answer:** _______

---

### Question 10
**True or False: OWASP resources are only available for paying members.**

A. True  
B. False  

**Answer:** _______

---

### Question 11
**What is the primary focus of OWASP SAMM?**

A. Testing mobile applications  
B. Improving software security practices over time (maturity)  
C. Listing top web vulnerabilities  
D. Providing quick reference guides  

**Answer:** _______

---

### Question 12
**Which OWASP standard is specifically designed for mobile applications?**

A. ASVS  
B. MASVS  
C. SAMM  
D. Testing Guide  

**Answer:** _______

---

### Question 13
**What types of resources does OWASP provide? (Select all that apply)**

☐ Code  
☐ Guides  
☐ Standards  
☐ Paid software licenses  
☐ Forums  

---

### Question 14
**What is the purpose of the OWASP Testing Guide?**

A. To provide a list of vulnerabilities  
B. To provide a framework and methodology for security testing  
C. To certify security testers  
D. To sell testing tools  

**Answer:** _______

---

### Question 15
**True or False: OWASP has over 250 local groups worldwide.**

A. True  
B. False  

**Answer:** _______

---

## Answer Key

| Q# | Answer |
|----|--------|
| 1 | B |
| 2 | B |
| 3 | A |
| 4 | C |
| 5 | B (False - they are concise, high-value documents) |
| 6 | B |
| 7 | 1-B, 2-C, 3-A, 4-D |
| 8 | B |
| 9 | B |
| 10 | B (False - they are free) |
| 11 | B |
| 12 | B |
| 13 | ☐ Code, ☐ Guides, ☐ Standards, ☐ Forums |
| 14 | B |
| 15 | A (True) |

---

## OWASP Standards Quick Reference Card

| Standard | Purpose | Best For | Key Deliverable |
|----------|---------|----------|-----------------|
| **OWASP Top 10** | Critical web risks awareness | All web stakeholders | Risk list with mitigations |
| **ASVS** | Comprehensive verification framework | Security architects, testers | Verification requirements by level |
| **MASVS** | Mobile app security baseline | Mobile developers, testers | Mobile security requirements |
| **SAMM** | Software security maturity | Security programs, CISOs | Maturity model + roadmap |
| **Testing Guide** | Testing methodology | Penetration testers | Testing framework |
| **Cheat Sheets** | Quick practical guidance | Developers | Concise best practices |

---

## Completion Checklist

| Task | Completed |
|------|-----------|
| **Exercise 1: OWASP Top 10** | ☐ |
| Researched and listed Top 10 risks | ☐ |
| Prioritized risks for e-commerce scenario | ☐ |
| Mapped mitigations | ☐ |
| **Exercise 2: OWASP ASVS** | ☐ |
| Completed ASVS levels | ☐ |
| Applied ASVS to healthcare scenario | ☐ |
| Completed verification mapping | ☐ |
| **Exercise 3: OWASP MASVS** | ☐ |
| Completed MASVS levels | ☐ |
| Applied MASVS to banking scenario | ☐ |
| Identified mobile requirements | ☐ |
| **Exercise 4: OWASP SAMM** | ☐ |
| Completed business functions | ☐ |
| Completed maturity levels | ☐ |
| Created SAMM roadmap | ☐ |
| **Exercise 5: OWASP Testing Guide** | ☐ |
| Completed testing phases | ☐ |
| Created test plan | ☐ |
| Compared testing methodologies | ☐ |
| **Exercise 6: OWASP Cheat Sheets** | ☐ |
| Completed cheat sheet research | ☐ |
| Created authentication quick reference | ☐ |
| Created custom cheat sheet | ☐ |
| **Exercise 7: Standards Selection** | ☐ |
| Completed scenario matrix | ☐ |
| **Exercise 8: Knowledge Check** | ☐ |
| Answered all questions | ☐ |

---

## Summary

In this lab, you have:

| Activity | Completed |
|----------|-----------|
| Learned about OWASP and its mission | ☐ |
| Explored the OWASP Top 10 and its critical risks | ☐ |
| Understood ASVS and its verification levels | ☐ |
| Applied MASVS to mobile applications | ☐ |
| Used SAMM for maturity planning | ☐ |
| Created a test plan using the Testing Guide | ☐ |
| Developed quick reference cheat sheets | ☐ |
| Practiced selecting appropriate OWASP resources | ☐ |

---

## Key Takeaways

| Concept | Description |
|---------|-------------|
| **OWASP** | Nonprofit focused on making software more secure |
| **OWASP Top 10** | 10 most critical web application security risks |
| **ASVS** | Application Security Verification Standard (web) |
| **MASVS** | Mobile Application Security Verification Standard |
| **SAMM** | Software Assurance Maturity Model |
| **Testing Guide** | Framework for security testing |
| **Cheat Sheets** | Quick, practical security guidance |
| **Free Resources** | All OWASP resources are free and open source |

---

## Additional Resources

| Resource | URL |
|----------|-----|
| **OWASP Official Website** | https://owasp.org |
| **OWASP Top 10** | https://owasp.org/Top10/ |
| **OWASP ASVS** | https://owasp.org/ASVS/ |
| **OWASP MASVS** | https://owasp.org/MASVS/ |
| **OWASP SAMM** | https://owaspsamm.org/ |
| **OWASP Testing Guide** | https://owasp.org/www-project-web-security-testing-guide/ |
| **OWASP Cheat Sheet Series** | https://cheatsheetseries.owasp.org/ |

---

## Congratulations!

You have successfully completed the **Hands-on Lab: OWASP Use Cases and Standards**. You now understand how to:

- List and describe the major OWASP standards
- Apply the OWASP Top 10 to identify critical web risks
- Use ASVS for application security verification
- Apply MASVS for mobile application security
- Use SAMM for software security maturity planning
- Create test plans using the Testing Guide
- Develop and use cheat sheets for quick guidance
- Select appropriate OWASP resources for specific scenarios

These skills are essential for:
- Web application developers
- Application security professionals
- Penetration testers
- Security architects
- DevOps engineers
- Compliance officers
- Anyone involved in secure software development
```

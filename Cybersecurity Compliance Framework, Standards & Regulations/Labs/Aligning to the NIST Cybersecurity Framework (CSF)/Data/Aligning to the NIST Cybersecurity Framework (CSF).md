![alt text](<../Screenshots/NIST_CSF.png>)

# Hands-on Lab: Aligning to the NIST Cybersecurity Framework (CSF)

**Estimated time needed:** 45 minutes

---

## Overview

An organization must adopt a systematic and comprehensive approach to align itself with the NIST CSF. This hands-on lab will guide you through the process of assessing an organization's current cybersecurity posture and developing an alignment plan using the NIST Cybersecurity Framework (CSF) 2.0.

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective                                                                                        |
| - | ------------------------------------------------------------------------------------------------ |
| 1 | Understand the NIST CSF 2.0 core functions (GOVERN, IDENTIFY, PROTECT, DETECT, RESPOND, RECOVER) |
| 2 | Conduct a gap analysis against the framework                                                     |
| 3 | Develop a prioritized action plan                                                                |
| 4 | Customize framework implementation for an organization                                           |
| 5 | Create a continuous improvement process                                                          |

---

## Prerequisites

| Requirement                   | Description                                   |
| ----------------------------- | --------------------------------------------- |
| NIST CSF familiarity          | Basic understanding of cybersecurity concepts |
| Computer with internet access | For research and template access              |
| Word processor or spreadsheet | For documentation                             |

---

## Background: NIST CSF 2.0 Core Functions

NIST CSF 2.0 consists of **six core functions** with **GOVERN** at the center:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      NIST CYBERSECURITY FRAMEWORK 2.0                        │
│                                                                              │
│                              ┌─────────────┐                                │
│                              │   GOVERN    │                                │
│                              │  (Center)   │                                │
│                              └──────┬──────┘                                │
│                                     │                                        │
│         ┌────────────────────────────┼────────────────────────────┐         │
│         │                            │                            │         │
│         ▼                            ▼                            ▼         │
│   ┌───────────┐                ┌───────────┐                ┌───────────┐   │
│   │ IDENTIFY  │                │  PROTECT  │                │  DETECT   │   │
│   └───────────┘                └───────────┘                └───────────┘   │
│         │                            │                            │         │
│         │                            │                            │         │
│         └────────────────────────────┼────────────────────────────┘         │
│                                      │                                       │
│                                      ▼                                       │
│                              ┌───────────────┐                              │
│                              │  RESPOND      │                              │
│                              ├───────────────┤                              │
│                              │  RECOVER      │                              │
│                              └───────────────┘                              │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Core Functions Overview

| Function           | Purpose                                             | Key Activities                                                           |
| ------------------ | --------------------------------------------------- | ------------------------------------------------------------------------ |
| **GOVERN**   | Establish cybersecurity strategy and oversight      | Risk management strategy, roles & responsibilities, policy development   |
| **IDENTIFY** | Understand assets, risks, and vulnerabilities       | Asset inventory, risk assessment, vulnerability identification           |
| **PROTECT**  | Implement safeguards to ensure delivery of services | Access control, awareness training, data security, protective technology |
| **DETECT**   | Identify cybersecurity events                       | Continuous monitoring, anomaly detection, alerting                       |
| **RESPOND**  | Take action against detected incidents              | Incident response planning, analysis, mitigation                         |
| **RECOVER**  | Restore capabilities after an incident              | Recovery planning, improvements, communication                           |

---

## Exercise 1: Assessment and Gap Analysis

### Scenario

You are the new Cybersecurity Manager for **Community Bank**, a regional bank with 500 employees, 15 branch locations, and approximately 50,000 customers. The bank has decided to implement the NIST Cybersecurity Framework 2.0 to bolster its cybersecurity posture.

### Step 1: Current State Assessment

The following table shows Community Bank's **current cybersecurity capabilities**:

| Function           | Current Capabilities                                                                      | Issues/Gaps |
| ------------------ | ----------------------------------------------------------------------------------------- | ----------- |
| **GOVERN**   | Informal security policies; no dedicated CISO; cybersecurity not discussed at board level |             |
| **IDENTIFY** | Basic asset inventory (spreadsheet); no formal risk assessment in 2 years                 |             |
| **PROTECT**  | Basic firewall; antivirus on endpoints; no MFA; no encryption for sensitive data          |             |
| **DETECT**   | No SIEM; basic logging only; no real-time alerting                                        |             |
| **RESPOND**  | No formal incident response plan; no defined roles                                        |             |
| **RECOVER**  | No disaster recovery plan; backups run weekly but not tested                              |             |

**Your Task:** Complete the Issues/Gaps column by identifying specific problems with each current capability.

```
GOVERN Issues/Gaps:
_________________________________________________________________________
_________________________________________________________________________

IDENTIFY Issues/Gaps:
_________________________________________________________________________
_________________________________________________________________________

PROTECT Issues/Gaps:
_________________________________________________________________________
_________________________________________________________________________

DETECT Issues/Gaps:
_________________________________________________________________________
_________________________________________________________________________

RESPOND Issues/Gaps:
_________________________________________________________________________
_________________________________________________________________________

RECOVER Issues/Gaps:
_________________________________________________________________________
_________________________________________________________________________
```

### Step 2: Conduct a Gap Analysis

A **gap analysis** compares where you are (current state) to where you need to be (target state).

**Target State Definition:** Community Bank wants to achieve "Tier 3: Repeatable" maturity on the NIST CSF maturity scale.

| Maturity Tier                   | Description                                         |
| ------------------------------- | --------------------------------------------------- |
| **Tier 1: Partial**       | Ad hoc, reactive approach; no formal processes      |
| **Tier 2: Risk Informed** | Risk-aware but inconsistent implementation          |
| **Tier 3: Repeatable**    | Formal policies and processes; consistently applied |
| **Tier 4: Adaptive**      | Continuously improving; learns from past incidents  |

**Complete the gap analysis table:**

| Function | Current Tier | Target Tier | Gap (Actions Needed) |
| -------- | ------------ | ----------- | -------------------- |
| GOVERN   | Tier 1       | Tier 3      |                      |
| IDENTIFY | Tier 1       | Tier 3      |                      |
| PROTECT  | Tier 2       | Tier 3      |                      |
| DETECT   | Tier 1       | Tier 3      |                      |
| RESPOND  | Tier 1       | Tier 3      |                      |
| RECOVER  | Tier 1       | Tier 3      |                      |

### Step 3: Prioritized Action Plan

Based on the gaps identified, create a **prioritized action plan** with specific initiatives:

| Priority | Initiative | Function | Timeline | Resources Needed | Success Metric |
| -------- | ---------- | -------- | -------- | ---------------- | -------------- |
| 1        |            |          |          |                  |                |
| 2        |            |          |          |                  |                |
| 3        |            |          |          |                  |                |
| 4        |            |          |          |                  |                |
| 5        |            |          |          |                  |                |

---

## Exercise 2: Senior Management Support

### Step 1: Create a Business Case

Senior management must actively support and engage in successful alignment. Create a business case to present to the board.

```
─────────────────────────────────────────────────────────────────────────────
                    BUSINESS CASE FOR NIST CSF ALIGNMENT
                          Community Bank
─────────────────────────────────────────────────────────────────────────────

Date: _________________
Prepared By: _________________

1. EXECUTIVE SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
(2-3 sentences explaining why NIST CSF alignment is needed)

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

2. CURRENT STATE ASSESSMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Key findings from gap analysis:

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

3. BUSINESS RISKS OF INACTION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• Financial risk: 
_________________________________________________________________________
• Regulatory risk: 
_________________________________________________________________________
• Reputational risk: 
_________________________________________________________________________
• Operational risk: 
_________________________________________________________________________

4. RECOMMENDED ACTION PLAN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Key initiatives and timeline:

_________________________________________________________________________
_________________________________________________________________________

5. RESOURCE REQUIREMENTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• Budget: $_________
• Personnel: 
_________________________________________________________________________
• Technology: 
_________________________________________________________________________

6. EXPECTED BENEFITS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• Reduced risk of breach: 
_________________________________________________________________________
• Regulatory compliance: 
_________________________________________________________________________
• Customer trust: 
_________________________________________________________________________
• Insurance premiums: 
_________________________________________________________________________

─────────────────────────────────────────────────────────────────────────────
```

### Step 2: Define Roles and Responsibilities

To ensure executive support translates into action, define key cybersecurity roles:

| Role               | Responsibility | Reporting Line |
| ------------------ | -------------- | -------------- |
| Board of Directors |                |                |
| CEO                |                |                |
| CISO (to be hired) |                |                |
| IT Manager         |                |                |
| Compliance Officer |                |                |
| All Employees      |                |                |

**Your Task:** Complete the Responsibility column for each role.

---

## Exercise 3: Customization and Collaboration

### Step 1: Tailor the Framework

The organization should customize implementation to fit its size, complexity, and specific risk landscape.

**Community Bank's Specific Context:**

| Factor           | Detail                                          |
| ---------------- | ----------------------------------------------- |
| Industry         | Banking/Financial Services                      |
| Size             | 500 employees, 15 branches                      |
| Key Assets       | Customer PII, account data, transaction systems |
| Regulations      | FFIEC, GLBA, state banking laws                 |
| Threat Landscape | Ransomware, phishing, insider threats           |

**Your Task:** Identify which CSF subcategories are **MOST critical** for Community Bank:

| Function | Priority Subcategory                                         | Why Important for Bank |
| -------- | ------------------------------------------------------------ | ---------------------- |
| GOVERN   | GV.OC-01: Organizational cybersecurity policy is established |                        |
| IDENTIFY | ID.AM-01: Hardware assets inventoried                        |                        |
| PROTECT  | PR.AC-01: Identities and credentials managed                 |                        |
| DETECT   | DE.AE-01: Network operations monitored                       |                        |
| RESPOND  | RS.MI-01: Incidents contained                                |                        |
| RECOVER  | RC.RP-01: Recovery plan executed                             |                        |

### Step 2: Stakeholder Collaboration

Collaborating with stakeholders reinforces the cybersecurity chain.

**Identify key stakeholders:**

| Stakeholder Group | Role in Cybersecurity | How to Engage |
| ----------------- | --------------------- | ------------- |
| Employees         |                       |               |
| IT Department     |                       |               |
| Branch Managers   |                       |               |
| Customers         |                       |               |
| Vendors/Suppliers |                       |               |
| Regulators        |                       |               |
| Law Enforcement   |                       |               |

**Your Task:** Complete the "How to Engage" column for each stakeholder group.

---

## Exercise 4: Continuous Improvement Process

### Step 1: Establish a Review Cycle

The organization should establish a continuous improvement process that regularly reviews cybersecurity practices against the NIST CSF.

**Create a review schedule:**

| Review Type              | Frequency | Responsible Party | Output |
| ------------------------ | --------- | ----------------- | ------ |
| Internal self-assessment |           |                   |        |
| Gap analysis             |           |                   |        |
| External audit           |           |                   |        |
| Board update             |           |                   |        |
| Policy review            |           |                   |        |
| Incident post-mortem     |           |                   |        |

**Your Task:** Complete the table with recommended frequencies (e.g., quarterly, annually, bi-annually).

### Step 2: Create a Maturity Improvement Plan

Track progress toward higher maturity tiers:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    MATURITY IMPROVEMENT ROADMAP                              │
│                           Community Bank                                     │
└─────────────────────────────────────────────────────────────────────────────┘

    TIER 1              TIER 2              TIER 3              TIER 4
    (Partial)       (Risk Informed)       (Repeatable)        (Adaptive)
        │                  │                   │                   │
        ▼                  ▼                   ▼                   ▼
    ┌───────┐          ┌───────┐           ┌───────┐           ┌───────┐
    │Current│─────────►│ Q2    │──────────►│ Q4    │──────────►│ Year 2│
    │ State │          │ 2024  │           │ 2024  │           │       │
    └───────┘          └───────┘           └───────┘           └───────┘

    GOVERN:    [▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰]  Tier 1 → Target: Tier 3
    IDENTIFY:  [▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰]  Tier 1 → Target: Tier 3
    PROTECT:   [▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰]  Tier 2 → Target: Tier 3
    DETECT:    [▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰]  Tier 1 → Target: Tier 3
    RESPOND:   [▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰]  Tier 1 → Target: Tier 3
    RECOVER:   [▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰]  Tier 1 → Target: Tier 3

    LEGEND:  ▰ = Current Progress    ▯ = Remaining to Target
```

**Your Task:** Fill in the progress bars based on where you think Community Bank would be after implementing the action plan.

---

## Exercise 5: CSF in Action - Scenario Application

### Scenario: Community Bank Incident

Using the NIST CSF framework, walk through how Community Bank would handle a **ransomware attack** that has encrypted customer data files on a file server.

**Step through each CSF function:**

### GOVERN

| Question                        | Your Answer |
| ------------------------------- | ----------- |
| Who needs to be notified?       |             |
| What policies apply?            |             |
| How is this incident escalated? |             |

### IDENTIFY

| Question                           | Your Answer |
| ---------------------------------- | ----------- |
| What assets are affected?          |             |
| What is the scope of the incident? |             |
| What is the risk level?            |             |

### PROTECT

| Question                                | Your Answer |
| --------------------------------------- | ----------- |
| What protections failed?                |             |
| What protections worked?                |             |
| What additional protections are needed? |             |

### DETECT

| Question                                | Your Answer |
| --------------------------------------- | ----------- |
| How was the incident detected?          |             |
| Was detection timely?                   |             |
| What detection improvements are needed? |             |

### RESPOND

| Question                          | Your Answer |
| --------------------------------- | ----------- |
| What immediate actions are taken? |             |
| Who is on the response team?      |             |
| How is the threat contained?      |             |

### RECOVER

| Question                    | Your Answer |
| --------------------------- | ----------- |
| How are systems restored?   |             |
| How is data recovered?      |             |
| How are customers notified? |             |

---

## Exercise 6: Knowledge Check Questions

### Question 1

**What are the six core functions of NIST CSF 2.0?**

A. Plan, Do, Check, Act, Review, Improve
B. GOVERN, IDENTIFY, PROTECT, DETECT, RESPOND, RECOVER
C. Assess, Design, Build, Test, Deploy, Monitor
D. Prevent, Detect, Contain, Eradicate, Recover, Learn

**Answer:** _______

---

### Question 2

**Which function is at the center of NIST CSF 2.0?**

A. IDENTIFY
B. PROTECT
C. GOVERN
D. RECOVER

**Answer:** _______

---

### Question 3

**What is the first step in aligning with NIST CSF?**

A. Purchasing security software
B. Hiring a CISO
C. Conducting a gap analysis
D. Writing an incident response plan

**Answer:** _______

---

### Question 4

**True or False: Senior management support is optional for successful NIST CSF alignment.**

A. True
B. False

**Answer:** _______

---

### Question 5

**Match the CSF Tier with its description:**

| Tier                  | Description                                      |
| --------------------- | ------------------------------------------------ |
| Tier 1: Partial       | A. Formal policies, consistently applied         |
| Tier 2: Risk Informed | B. Continuously improving, learns from incidents |
| Tier 3: Repeatable    | C. Ad hoc, reactive, no formal processes         |
| Tier 4: Adaptive      | D. Risk-aware but inconsistent implementation    |

**Answers:** Tier 1-_____, Tier 2-_____, Tier 3-_____, Tier 4-_____

---

### Question 6

**According to the reading, what should organizations do to customize framework implementation?**

A. Use the same approach regardless of size
B. Tailor to fit size, complexity, and specific risk landscape
C. Only implement the PROTECT function
D. Skip customization to save time

**Answer:** _______

---

### Question 7

**Which NIST CSF function involves implementing safeguards like multi-factor authentication and encryption?**

A. IDENTIFY
B. PROTECT
C. DETECT
D. GOVERN

**Answer:** _______

---

### Question 8

**What should an organization establish to ensure alignment stays dynamic and responsive to new threats?**

A. A one-time assessment
B. A continuous improvement process
C. A fixed budget
D. A single annual meeting

**Answer:** _______

---

### Question 9

**In the Community Bank example, what was implemented during the PROTECT phase?**

A. Security software for network monitoring
B. MFA, encryption, and employee training
C. An incident response plan
D. A disaster recovery plan

**Answer:** _______

---

### Question 10

**Which stakeholders should be included in cybersecurity collaboration? (Select all that apply)**

☐ Suppliers and vendors
☐ Employees
☐ Customers
☐ Competitors
☐ Regulators

---

### Question 11

**What is the purpose of the RESPOND function?**

A. Identify vulnerabilities
B. Implement security controls
C. Take action against detected incidents
D. Restore capabilities after an incident

**Answer:** _______

---

### Question 12

**True or False: The RECOVER function includes communicating transparently with stakeholders about incidents.**

A. True
B. False

**Answer:** _______

---

### Question 13

**What maturity tier is characterized by "formal policies and processes that are consistently applied"?**

A. Tier 1: Partial
B. Tier 2: Risk Informed
C. Tier 3: Repeatable
D. Tier 4: Adaptive

**Answer:** _______

---

### Question 14

**Why is collaboration with suppliers and partners important for cybersecurity?**

A. It increases costs
B. It reinforces the cybersecurity chain and helps manage risks comprehensively
C. It reduces regulatory requirements
D. It eliminates the need for internal security

**Answer:** _______

---

### Question 15

**What is the first thing senior management should do according to the Community Bank example?**

A. Purchase security software
B. Develop an understanding of the cybersecurity landscape
C. Hire external consultants
D. Write a disaster recovery plan

**Answer:** _______

---

## Answer Key

| Q# | Answer                                                          |
| -- | --------------------------------------------------------------- |
| 1  | B                                                               |
| 2  | C                                                               |
| 3  | C                                                               |
| 4  | B (False - it is essential)                                     |
| 5  | Tier 1-C, Tier 2-D, Tier 3-A, Tier 4-B                          |
| 6  | B                                                               |
| 7  | B                                                               |
| 8  | B                                                               |
| 9  | B                                                               |
| 10 | ☐ Suppliers/vendors, ☐ Employees, ☐ Customers, ☐ Regulators |
| 11 | C                                                               |
| 12 | A (True)                                                        |
| 13 | C                                                               |
| 14 | B                                                               |
| 15 | B                                                               |

---

## NIST CSF 2.0 Quick Reference

### GOVERN (GV)

| Category | Description                |
| -------- | -------------------------- |
| GV.OC    | Organizational Context     |
| GV.RM    | Risk Management Strategy   |
| GV.RR    | Roles and Responsibilities |
| GV.PO    | Policies and Procedures    |
| GV.OV    | Oversight                  |

### IDENTIFY (ID)

| Category | Description      |
| -------- | ---------------- |
| ID.AM    | Asset Management |
| ID.RM    | Risk Assessment  |
| ID.IM    | Improvement      |

### PROTECT (PR)

| Category | Description            |
| -------- | ---------------------- |
| PR.AC    | Access Control         |
| PR.AW    | Awareness and Training |
| PR.DS    | Data Security          |
| PR.PS    | Platform Security      |
| PR.MA    | Maintenance            |

### DETECT (DE)

| Category | Description           |
| -------- | --------------------- |
| DE.AE    | Anomalies and Events  |
| DE.CM    | Continuous Monitoring |

### RESPOND (RS)

| Category | Description                 |
| -------- | --------------------------- |
| RS.MA    | Incident Management         |
| RS.AN    | Incident Analysis           |
| RS.CO    | Incident Response Reporting |

### RECOVER (RC)

| Category | Description                      |
| -------- | -------------------------------- |
| RC.RP    | Incident Recovery Plan Execution |
| RC.IM    | Incident Recovery Improvement    |

---

## Implementation Templates

### Gap Analysis Template

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         NIST CSF GAP ANALYSIS                                │
│                           Community Bank                                     │
│                         Date: ______________                                 │
└─────────────────────────────────────────────────────────────────────────────┘

FUNCTION: GOVERN
─────────────────────────────────────────────────────────────────────────────
Current State: _______________________________________________________________
Target State:  _______________________________________________________________
Gap: ________________________________________________________________________
Action Plan: ________________________________________________________________

FUNCTION: IDENTIFY
─────────────────────────────────────────────────────────────────────────────
Current State: _______________________________________________________________
Target State:  _______________________________________________________________
Gap: ________________________________________________________________________
Action Plan: ________________________________________________________________

FUNCTION: PROTECT
─────────────────────────────────────────────────────────────────────────────
Current State: _______________________________________________________________
Target State:  _______________________________________________________________
Gap: ________________________________________________________________________
Action Plan: ________________________________________________________________

FUNCTION: DETECT
─────────────────────────────────────────────────────────────────────────────
Current State: _______________________________________________________________
Target State:  _______________________________________________________________
Gap: ________________________________________________________________________
Action Plan: ________________________________________________________________

FUNCTION: RESPOND
─────────────────────────────────────────────────────────────────────────────
Current State: _______________________________________________________________
Target State:  _______________________________________________________________
Gap: ________________________________________________________________________
Action Plan: ________________________________________________________________

FUNCTION: RECOVER
─────────────────────────────────────────────────────────────────────────────
Current State: _______________________________________________________________
Target State:  _______________________________________________________________
Gap: ________________________________________________________________________
Action Plan: ________________________________________________________________
```

### Action Plan Tracking Sheet

| Initiative | Function | Owner | Start Date | Target Date | Status | Completion % |
| ---------- | -------- | ----- | ---------- | ----------- | ------ | ------------ |
|            |          |       |            |             |        |              |
|            |          |       |            |             |        |              |
|            |          |       |            |             |        |              |
|            |          |       |            |             |        |              |
|            |          |       |            |             |        |              |

---

## Completion Checklist

| Task                                                | Completed |
| --------------------------------------------------- | --------- |
| **Exercise 1: Assessment & Gap Analysis**     | ☐        |
| Completed current state assessment                  | ☐        |
| Identified gaps for each function                   | ☐        |
| Completed gap analysis with maturity tiers          | ☐        |
| Created prioritized action plan                     | ☐        |
| **Exercise 2: Senior Management Support**     | ☐        |
| Created business case                               | ☐        |
| Defined roles and responsibilities                  | ☐        |
| **Exercise 3: Customization & Collaboration** | ☐        |
| Identified priority subcategories                   | ☐        |
| Identified stakeholders and engagement strategies   | ☐        |
| **Exercise 4: Continuous Improvement**        | ☐        |
| Created review schedule                             | ☐        |
| Developed maturity improvement roadmap              | ☐        |
| **Exercise 5: Scenario Application**          | ☐        |
| Applied CSF to ransomware scenario                  | ☐        |
| **Exercise 6: Knowledge Check**               | ☐        |
| Completed all quiz questions                        | ☐        |

---

## Summary

In this lab, you have:

| Activity                                           | Completed |
| -------------------------------------------------- | --------- |
| Learned the six NIST CSF 2.0 core functions        | ☐        |
| Conducted a gap analysis for a sample organization | ☐        |
| Created a prioritized action plan                  | ☐        |
| Developed a business case for management support   | ☐        |
| Tailored the framework to organizational needs     | ☐        |
| Identified stakeholders for collaboration          | ☐        |
| Established a continuous improvement process       | ☐        |
| Applied the framework to a real incident scenario  | ☐        |

---

## Key Takeaways

| Concept                             | Description                                                                        |
| ----------------------------------- | ---------------------------------------------------------------------------------- |
| **NIST CSF 2.0**              | Framework of 6 core functions: GOVERN, IDENTIFY, PROTECT, DETECT, RESPOND, RECOVER |
| **Gap Analysis**              | Process of comparing current state to target state                                 |
| **Maturity Tiers**            | Four levels: Partial, Risk Informed, Repeatable, Adaptive                          |
| **Continuous Improvement**    | Regular reviews keep alignment dynamic and responsive                              |
| **Stakeholder Collaboration** | Includes suppliers, partners, and all internal roles                               |
| **GOVERN at Center**          | Leadership and strategy underpin all other functions                               |

---

## Additional Resources

| Resource                                           | URL                                                       |
| -------------------------------------------------- | --------------------------------------------------------- |
| **NIST CSF 2.0 Official Website**            | https://www.nist.gov/cyberframework                       |
| **CSF 2.0 Reference Tool**                   | https://csrc.nist.gov/Projects/cybersecurity-framework    |
| **CSF 2.0 Quick Start Guides**               | https://www.nist.gov/cyberframework/quick-start-guides    |
| **NIST Cybersecurity Framework Spreadsheet** | https://www.nist.gov/cyberframework/csf-20-reference-data |

---

## Congratulations!

You have successfully completed the **Hands-on Lab: Aligning to the NIST Cybersecurity Framework (CSF)** . You now understand how to:

- Assess an organization's cybersecurity posture against NIST CSF
- Conduct gap analyses and create action plans
- Build business cases for management support
- Tailor framework implementation to organizational needs
- Establish continuous improvement processes
- Apply the framework to real-world incidents

These skills are essential for:

- Cybersecurity managers and leaders
- Compliance and risk management professionals
- IT security architects
- Anyone preparing for security framework certifications

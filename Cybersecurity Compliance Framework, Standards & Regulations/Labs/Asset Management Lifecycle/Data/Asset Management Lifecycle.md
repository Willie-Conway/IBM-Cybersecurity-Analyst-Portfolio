
![alt text](<../Screenshots/TechLearn_Solutions.png>)

# Hands-on Lab: Asset Management Lifecycle

**Estimated time needed:** 30 minutes

---

## Overview

Asset management is a way for an organization to add new assets like computers and mobile devices to its inventory. It includes keeping track of these assets from start to finish and ensuring proper disposal when no longer usable.

In this hands-on lab, you will create an asset management plan for a mock company, track assets through their lifecycle, and practice secure disposal procedures.

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective                                                            |
| - | -------------------------------------------------------------------- |
| 1 | Define asset management and its three core processes                 |
| 2 | Explain the acquisition and procurement process                      |
| 3 | Describe the importance and process of monitoring and asset tracking |
| 4 | Explain the importance of the disposal and decommissioning process   |
| 5 | Create and manage an asset inventory spreadsheet                     |
| 6 | Apply secure data destruction methods                                |

---

## Prerequisites

| Required                      | Description                                         |
| ----------------------------- | --------------------------------------------------- |
| Computer with internet access | For accessing templates and research                |
| Spreadsheet software          | Microsoft Excel, Google Sheets, or LibreOffice Calc |
| PDF reader                    | For reading asset management templates              |

---

## Background: Asset Management Processes

Asset management involves **three core processes**:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         ASSET MANAGEMENT LIFECYCLE                          │
│                                                                              │
│   ┌──────────────┐    ┌──────────────┐    ┌──────────────┐                 │
│   │  ACQUISITION │───►│   MONITORING │───►│  DISPOSAL    │                 │
│   │      &       │    │      &       │    │      &       │                 │
│   │ PROCUREMENT  │    │   TRACKING   │    │DECOMMISSIONING│                 │
│   └──────────────┘    └──────────────┘    └──────────────┘                 │
│         │                    │                    │                         │
│         ▼                    ▼                    ▼                         │
│   • Identify need      • Asset tagging      • Data sanitization             │
│   • Evaluate options   • Inventory SW       • Environmental protection      │
│   • Verify compat.     • Reconciliation     • Legal compliance              │
│   • Budget alignment   • Lifecycle tracking • Secure destruction            │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Exercise 1: Acquisition and Procurement Process

### Scenario

You are the IT Asset Manager for **TechLearn Solutions**, a small education technology company with 50 employees. The company needs to purchase **25 new laptops** for a new cohort of customer support representatives starting next month.

### Step 1: Identify Requirements

Before purchasing, you need to document the requirements.

**Complete the following table:**

| Requirement Category            | Questions to Answer                 | Your Answer |
| ------------------------------- | ----------------------------------- | ----------- |
| **Business Need**         | Why do we need these assets?        |             |
| **Number of Assets**      | How many are needed?                |             |
| **Technical Specs**       | What CPU, RAM, storage?             |             |
| **Software Requirements** | What OS and applications?           |             |
| **Compatibility**         | Will it work with existing systems? |             |
| **Budget**                | How much can we spend per unit?     |             |
| **Timeline**              | When do we need them?               |             |

### Step 2: Research Options

Research laptop options that meet the following criteria:

| Criteria     | Minimum Requirement                 |
| ------------ | ----------------------------------- |
| Processor    | Intel i5 or AMD Ryzen 5 (or better) |
| RAM          | 16 GB minimum                       |
| Storage      | 256 GB SSD minimum                  |
| Battery Life | 8+ hours                            |
| Warranty     | 3 years minimum                     |
| Price Range  | $800 - $1,200 per unit              |

**Complete the comparison table:**

| Feature  | Option 1 (Dell) | Option 2 (Lenovo) | Option 3 (HP) |
| -------- | --------------- | ----------------- | ------------- |
| Model    |                 |                   |               |
| CPU      |                 |                   |               |
| RAM      |                 |                   |               |
| Storage  |                 |                   |               |
| Price    |                 |                   |               |
| Warranty |                 |                   |               |
| Pros     |                 |                   |               |
| Cons     |                 |                   |               |

**Your Recommendation:** Which laptop would you choose and why?

```
Your answer:
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
```

### Step 3: Create a Procurement Request

Draft a procurement request to management using the template below:

```
─────────────────────────────────────────────────────────────────────────────
                    PROCUREMENT REQUEST FORM
─────────────────────────────────────────────────────────────────────────────

Request Date: _________________

Requested By: _________________
Department: IT Asset Management

ASSET DETAILS:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Asset Type: Laptop Computers
Quantity: 25
Preferred Model: _________________
Vendor: _________________

JUSTIFICATION:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Business Need:
_________________________________________________________________________
_________________________________________________________________________

Expected Lifespan: 4 years

TOTAL COST:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Unit Cost: $_________
Total Hardware Cost: $_________
Software Licenses: $_________
Shipping/Handling: $_________
Total Request Amount: $_________

APPROVALS:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Manager Approval: _____________ Date: _______
Finance Approval: _____________ Date: _______
IT Approval: _____________ Date: _______

─────────────────────────────────────────────────────────────────────────────
```

---

## Exercise 2: Monitoring and Asset Tracking

### Step 1: Create an Asset Inventory Spreadsheet

Open your spreadsheet software and create a new file. Set up columns as follows:

| Column | Heading         | Description                      |
| ------ | --------------- | -------------------------------- |
| A      | Asset ID        | Unique identifier for each asset |
| B      | Asset Type      | Laptop, Desktop, Monitor, etc.   |
| C      | Brand/Model     | Manufacturer and model number    |
| D      | Serial Number   | Manufacturer serial number       |
| E      | Assigned To     | Employee name or department      |
| F      | Location        | Office, cubicle, remote          |
| G      | Purchase Date   | Date acquired                    |
| H      | Cost            | Purchase price                   |
| I      | Warranty Expiry | Date warranty ends               |
| J      | Status          | Active, Maintenance, Retired     |
| K      | Last Audit Date | Date last physically verified    |

### Step 2: Populate Sample Asset Data

Add the following sample assets to your spreadsheet:

**Sample Assets:**

| Asset ID | Asset Type | Brand/Model         | Serial #  | Assigned To  | Location    | Purchase Date | Cost   | Warranty Expiry | Status | Last Audit |
| -------- | ---------- | ------------------- | --------- | ------------ | ----------- | ------------- | ------ | --------------- | ------ | ---------- |
| TLC-001  | Laptop     | Dell Latitude 5540  | DEL123ABC | Sarah Chen   | Bldg A-201  | 1/15/2024     | $1,250 | 1/15/2027       | Active | 4/1/2026   |
| TLC-002  | Laptop     | Lenovo ThinkPad E16 | LEN456DEF | Mike Ross    | Bldg A-203  | 1/15/2024     | $1,100 | 1/15/2027       | Active | 4/1/2026   |
| TLC-003  | Desktop    | HP EliteDesk        | HP789GHI  | Finance Dept | Bldg B-101  | 6/10/2023     | $950   | 6/10/2026       | Active | 3/15/2026  |
| TLC-004  | Monitor    | Dell 27"            | DEL321JKL | Sarah Chen   | Bldg A-201  | 1/15/2024     | $250   | 1/15/2027       | Active | 4/1/2026   |
| TLC-005  | Server     | Dell PowerEdge      | DEL654MNO | IT Dept      | Server Rm A | 3/20/2022     | $5,500 | 3/20/2025       | Active | 4/10/2026  |
| TLC-006  | Laptop     | MacBook Pro         | APL789PQR | Remote Pool  | Remote      | 9/5/2023      | $2,000 | 9/5/2026        | Active | 3/30/2026  |
| TLC-007  | Printer    | HP LaserJet         | HP321STU  | Admin Dept   | Bldg A-100  | 11/1/2022     | $450   | 11/1/2025       | Active | 4/5/2026   |
| TLC-008  | iPad       | iPad Air 5          | APL654VWX | Sales Team   | Remote      | 7/20/2024     | $600   | 7/20/2027       | Active | N/A        |

### Step 3: Add Asset Tagging Information

For each asset, create a unique asset ID using a consistent naming convention:

**Naming Convention Example:**

```
[COMPANY CODE]-[ASSET TYPE]-[SEQUENTIAL NUMBER]

Example: TLC-LPT-001
- TLC = TechLearn Solutions
- LPT = Laptop
- 001 = First laptop
```

**Create asset tags for all assets in your inventory:**

| Asset Type    | Code |
| ------------- | ---- |
| Laptop        | LPT  |
| Desktop       | DTP  |
| Monitor       | MNT  |
| Server        | SRV  |
| Printer       | PRN  |
| Mobile Device | MOB  |

**Your Task:** Rename the Asset IDs in your spreadsheet using this naming convention.

### Step 4: Perform a Reconciliation Process

**Scenario:** Your physical audit has discovered the following discrepancies:

| Discrepancy        | Details                                                                 |
| ------------------ | ----------------------------------------------------------------------- |
| Missing asset      | TLC-006 (MacBook Pro) - assigned to Remote Pool, not returned           |
| Undocumented asset | Dell monitor found in Bldg A-205, no asset tag                          |
| Wrong location     | TLC-002 (Lenovo laptop) found in Bldg A-205, but records say Bldg A-203 |

**Your Task:** Update your spreadsheet to reflect these findings:

1. Change TLC-002 location to Bldg A-205
2. Mark TLC-006 status as "Missing - Investigation Required"
3. Add the undocumented monitor as TLC-MNT-009 with location Bldg A-205

### Step 5: Calculate Asset Statistics

Use spreadsheet formulas to calculate:

| Statistic                       | Formula                                    | Your Result |
| ------------------------------- | ------------------------------------------ | ----------- |
| Total number of assets          | `=COUNTA(AssetID_column)`                |             |
| Total asset value               | `=SUM(Cost_column)`                      |             |
| Average asset cost              | `=AVERAGE(Cost_column)`                  |             |
| Number of active assets         | `=COUNTIF(Status_column,"Active")`       |             |
| Number of assets under warranty | `=COUNTIF(Warranty_column,">="&TODAY())` |             |
| Number of assets by type        | `=COUNTIF(AssetType_column,"Laptop")`    |             |

---

## Exercise 3: Disposal and Decommissioning

### Step 1: Identify Assets for Disposal

**Scenario:** The following assets have reached end-of-life:

| Asset ID | Asset Type            | Reason for Disposal                            | Sensitive Data?      |
| -------- | --------------------- | ---------------------------------------------- | -------------------- |
| TLC-005  | Dell PowerEdge Server | Warranty expired 3/20/2025, performance issues | YES (customer data)  |
| TLC-007  | HP LaserJet Printer   | Beyond economical repair                       | YES (network config) |
| TLC-003  | HP EliteDesk Desktop  | 4 years old, slow performance                  | YES (user files)     |

### Step 2: Select Secure Data Destruction Methods

For each asset above, select the appropriate data destruction method:

| Method                                | Description                                   | Best For                                     |
| ------------------------------------- | --------------------------------------------- | -------------------------------------------- |
| **Physical destruction**        | Crushing, shredding, or drilling hard drives  | Highly sensitive data, non-reusable devices  |
| **Degaussing**                  | Powerful magnetic field erases magnetic media | Hard drives, tapes (device becomes unusable) |
| **Incineration**                | High-temperature melting                      | Complete destruction required                |
| **Chemical destruction**        | Dissolving memory chips                       | Specialized high-security needs              |
| **Electromagnetic destruction** | EMP erases electronic data                    | Solid-state drives                           |
| **Secure wipe (software)**      | Overwrite data multiple times                 | Reusable devices, less sensitive data        |

**Complete the table:**

| Asset ID          | Destruction Method Selected | Justification |
| ----------------- | --------------------------- | ------------- |
| TLC-005 (Server)  |                             |               |
| TLC-007 (Printer) |                             |               |
| TLC-003 (Desktop) |                             |               |

### Step 3: Create Disposal Documentation

Complete the Disposal Request Form for one of the assets:

```
─────────────────────────────────────────────────────────────────────────────
                      ASSET DISPOSAL REQUEST FORM
─────────────────────────────────────────────────────────────────────────────

Request Date: _________________

Asset ID: _________________
Asset Type: _________________
Serial Number: _________________

DISPOSAL REASON:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
☐ End of Life (EOL)        ☐ Damaged/Repair not feasible
☐ Lost/Stolen              ☐ Upgrade/Replacement
☐ Performance issues       ☐ Other: _______________

DATA DESTRUCTION METHOD:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
☐ Physical destruction (shredding/crushing)
☐ Degaussing
☐ Secure wipe (software)
☐ Incineration
☐ Chemical destruction
☐ Electromagnetic destruction

Date of Data Destruction: _________________
Destroyed By: _________________
Witnessed By: _________________

ENVIRONMENTAL DISPOSAL:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
☐ Recycled through certified e-waste vendor
☐ Donated (data sanitized)
☐ Sent to landfill (if no other option)
☐ Returned to manufacturer

Certification of Destruction:
I certify that the asset above has been properly decommissioned, all data has
been securely destroyed, and disposal followed environmental regulations.

Signature: _________________ Date: _______

Final Approval: _________________ Date: _______

─────────────────────────────────────────────────────────────────────────────
```

### Step 4: Update Asset Inventory

After disposal, update your asset spreadsheet:

| Action                   | How to Record                                |
| ------------------------ | -------------------------------------------- |
| Mark asset as retired    | Change Status to "Retired - [disposal date]" |
| Record disposal method   | Add column "Disposal Method"                 |
| Record destruction date  | Add column "Data Destruction Date"           |
| Remove from active count | Ensure retired assets not counted as active  |

---

## Exercise 4: Asset Management Policy Creation

### Step 1: Draft an Asset Management Policy

Create a simple asset management policy for TechLearn Solutions using the template below:

```
─────────────────────────────────────────────────────────────────────────────
                  TECHLEARN SOLUTIONS - ASSET MANAGEMENT POLICY
─────────────────────────────────────────────────────────────────────────────

Policy Number: IT-ASSET-001
Effective Date: _________________
Version: 1.0

1. PURPOSE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
The purpose of this policy is to establish guidelines for the acquisition,
tracking, and disposal of all company assets.

2. SCOPE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
This policy applies to all employees, contractors, and temporary workers who
use company assets including:
• Laptops and desktop computers
• Mobile devices and tablets
• Servers and networking equipment
• Peripherals (monitors, printers, keyboards)

3. ACQUISITION AND PROCUREMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
All asset acquisitions must:
• Be approved by IT Asset Management
• Meet minimum technical specifications
• Be sourced from approved vendors
• Have a valid business justification

4. ASSET TRACKING
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• All assets will be assigned a unique asset ID upon receipt
• Asset inventory will be updated within 24 hours of assignment
• Physical audits will be conducted quarterly
• Employees are responsible for assigned assets

5. DATA SECURITY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• All company assets must use full-disk encryption
• Assets containing sensitive data must be tracked with higher scrutiny
• Lost or stolen assets must be reported within 2 hours

6. DISPOSAL AND DECOMMISSIONING
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
All data must be securely destroyed before disposal using:
• For HDD: Degaussing or physical destruction
• For SSD: Secure wipe or physical destruction
• Disposal must use certified e-waste vendors
• Disposal documentation must be retained for 3 years

7. COMPLIANCE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Violations of this policy may result in disciplinary action.

8. REVIEW
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
This policy will be reviewed annually by IT Asset Management.

Approved By: _________________ Date: _______

─────────────────────────────────────────────────────────────────────────────
```

---

## Exercise 5: Knowledge Check Questions

Answer the following questions based on the reading and lab activities.

### Question 1

**What are the three core processes of asset management?**

A. Planning, implementing, reviewing
B. Acquisition/procurement, monitoring/tracking, disposal/decommissioning
C. Buying, using, selling
D. Identification, authentication, authorization

**Answer:** _______

---

### Question 2

**Why is asset tagging important for monitoring and tracking?**

A. It makes assets look professional
B. It assigns a unique identifier for easy monitoring and tracking
C. It increases the asset's resale value
D. It prevents the asset from being stolen

**Answer:** _______

---

### Question 3

**Which method uses a powerful magnetic field to erase data from hard drives?**

A. Physical destruction
B. Incineration
C. Degaussing
D. Chemical destruction

**Answer:** _______

---

### Question 4

**True or False: Proper disposal of electronic assets is only important for data security, not environmental protection.**

A. True
B. False

**Answer:** _______

---

### Question 5

**Which of the following is a valid reason to dispose of an asset? (Select all that apply)**

☐ End of life/warranty expired
☐ Performance issues
☐ Employee wants a newer model without justification
☐ Beyond economical repair

---

### Question 6

**What type of software helps record, update, and maintain asset information on a centralized platform?**

A. Word processor
B. Inventory management software
C. Email client
D. Web browser

**Answer:** _______

---

### Question 7

**Which destruction method renders a hard drive completely unusable by crushing, shredding, or drilling?**

A. Degaussing
B. Physical destruction
C. Electromagnetic destruction
D. Secure wipe

**Answer:** _______

---

### Question 8

**How often should physical asset audits be conducted according to best practices?**

A. Never
B. Only when an asset is lost
C. Quarterly or annually
D. Every 5 years

**Answer:** _______

---

### Question 9

**Match the asset management process with its description:**

| Process                       | Description                                                  |
| ----------------------------- | ------------------------------------------------------------ |
| 1. Acquisition & Procurement  | A. Securely erasing data and responsibly disposing of assets |
| 2. Monitoring & Tracking      | B. Selecting, evaluating, and purchasing new assets          |
| 3. Disposal & Decommissioning | C. Recording, updating, and maintaining asset information    |

**Answers:** 1-_____, 2-_____, 3-_____

---

### Question 10

**Why is reconciliation between recorded asset data and physical inventory important?**

A. It increases the company's budget
B. It identifies discrepancies and ensures accurate records
C. It automatically disposes of old assets
D. It prevents employees from using company assets

**Answer:** _______

---

## Answer Key

| Q# | Answer                                                                         |
| -- | ------------------------------------------------------------------------------ |
| 1  | B                                                                              |
| 2  | B                                                                              |
| 3  | C                                                                              |
| 4  | B (False - it's important for BOTH data security AND environmental protection) |
| 5  | ☐ End of life, ☐ Performance issues, ☐ Beyond economical repair             |
| 6  | B                                                                              |
| 7  | B                                                                              |
| 8  | C                                                                              |
| 9  | 1-B, 2-C, 3-A                                                                  |
| 10 | B                                                                              |

---

## Asset Management Checklist for Organizations

Use this checklist to evaluate your organization's asset management practices:

| Practice                                      | Status (Yes/No/Partial) | Notes |
| --------------------------------------------- | ----------------------- | ----- |
| **Acquisition**                         |                         |       |
| Clear procurement process documented          |                         |       |
| Asset requirements defined before purchase    |                         |       |
| Budget approval required                      |                         |       |
| Vendor evaluation process in place            |                         |       |
| **Monitoring & Tracking**               |                         |       |
| Unique asset IDs assigned to all assets       |                         |       |
| Inventory management software used            |                         |       |
| Regular physical audits conducted             |                         |       |
| Asset assignment records maintained           |                         |       |
| **Disposal & Decommissioning**          |                         |       |
| Data destruction policy exists                |                         |       |
| Secure destruction methods used               |                         |       |
| E-waste disposed of through certified vendors |                         |       |
| Disposal documentation maintained             |                         |       |
| **Compliance**                          |                         |       |
| Regulatory requirements understood            |                         |       |
| Audit trail maintained                        |                         |       |
| Policy reviewed annually                      |                         |       |

---

## Completed Lab Deliverables

| Deliverable                 | Format           | Completed |
| --------------------------- | ---------------- | --------- |
| Procurement Request Form    | Completed form   | ☐        |
| Asset Inventory Spreadsheet | Spreadsheet file | ☐        |
| Disposal Request Form       | Completed form   | ☐        |
| Asset Management Policy     | Draft document   | ☐        |
| Knowledge Check Answers     | Answer sheet     | ☐        |

---

## Summary

In this lab, you have:

| Activity                                              | Completed |
| ----------------------------------------------------- | --------- |
| Defined asset management and its three core processes | ☐        |
| Completed acquisition and procurement activities      | ☐        |
| Created an asset inventory spreadsheet with tracking  | ☐        |
| Performed asset reconciliation                        | ☐        |
| Selected appropriate data destruction methods         | ☐        |
| Created asset disposal documentation                  | ☐        |
| Drafted an asset management policy                    | ☐        |
| Answered knowledge check questions                    | ☐        |

---

## Key Takeaways

| Concept                                 | Description                                                        |
| --------------------------------------- | ------------------------------------------------------------------ |
| **Asset Management**              | Systematic process of tracking assets from acquisition to disposal |
| **Acquisition & Procurement**     | Selecting and purchasing assets that meet business needs           |
| **Asset Tagging**                 | Assigning unique identifiers for easy tracking                     |
| **Inventory Management Software** | Centralized platform for asset data                                |
| **Reconciliation**                | Comparing records against physical inventory                       |
| **Secure Data Destruction**       | Ensuring data cannot be recovered from disposed assets             |
| **Degaussing**                    | Magnetic field erasure for hard drives                             |
| **Physical Destruction**          | Crushing, shredding, or drilling storage media                     |
| **E-waste Compliance**            | Following regulations for electronic waste disposal                |

---

## Additional Resources

| Resource                                            | URL                                                            |
| --------------------------------------------------- | -------------------------------------------------------------- |
| **NIST Asset Management Guidelines**          | https://csrc.nist.gov                                          |
| **EPA Electronics Recycling**                 | https://www.epa.gov/recycle/electronics-donation-and-recycling |
| **ISO 55000 Asset Management**                | https://www.iso.org/standard/55000                             |
| **IT Asset Management (ITAM) Best Practices** | https://www.iaitam.org                                         |

---

## Congratulations!

You have successfully completed the **Hands-on Lab: Asset Management Lifecycle**. You now understand how to:

- Manage assets from acquisition through disposal
- Create and maintain an asset inventory
- Track assets using unique identifiers
- Securely destroy data during decommissioning
- Create asset management policies and documentation

These skills are essential for:

- IT asset managers
- Security professionals
- Compliance officers
- System administrators

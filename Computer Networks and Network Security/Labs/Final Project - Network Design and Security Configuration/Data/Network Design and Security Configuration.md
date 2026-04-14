
![alt text](<../Screenshots/Windows Defender.png>)

# Final Project: Network Design and Security Configuration

**Estimated time needed:** 60 minutes

---

## Final Project Requirements

You will use an online Windows environment for this project.

### Required Tools and Resources:

- A screenshot or screen-capturing application, with the ability to crop images
- A location to store your screenshots

### Optional: Using Your Own Machine

If you choose to complete this project on your own computer, you will need:

- A workstation running Microsoft Windows 10 or later
- Administrator rights on the workstation

---

## Project Overview

This final project consists of four real-world, network-related tasks. Some tasks may include several subtasks. For each task, you will capture and save screenshots that document your successful completion of the required steps. You will later submit these screenshots for evaluation as part of your course completion.

Let's get started!

---

## Scenario

**TechSafe, Ltd.** has hired you to design and secure its network. The company uses a fixed IP address from its Internet service provider (ISP) and wants a structured network with compatible IP addressing, subnetting, and security configurations.

---

# Task 1: Design a Network with Subnets

## Scenario

Design a network diagram for TechSafe Ltd. that includes three departments: **Administration**, **Sales**, and **IT**. Each department requires its own subnet.

### Deliverable

A screenshot of the network diagram. The submitted network screenshot must include the following devices and labels:

- One router connected to one switch (connect the router to the switch with a line)
- Label the router as **Router** and label the switch as **Switch**
- Three subnets that connect to the switch using solid lines
- The three subnets are labeled as **Administration**, **Sales**, and **IT**
- The diagram includes no additional elements beyond the router, switch, and subnets

---

## Step 1: Access a Diagram Tool

You can use any diagram tool for this task. Options include:

| Tool                      | Access Method                                     |
| :------------------------ | :------------------------------------------------ |
| **Draw.io**         | https://app.diagrams.net/ (free, web-based)       |
| **Microsoft Visio** | If installed on your system                       |
| **Lucidchart**      | https://www.lucidchart.com/ (free tier available) |
| **PowerPoint**      | Insert → Shapes                                  |

For this lab, we'll use **Draw.io**.

### Step 2: Open Draw.io

1. Open your web browser
2. Navigate to: **https://app.diagrams.net/**
3. Select where to save your diagram (choose **Device** to save locally)

![Draw.io storage selection]

4. Click **Create New Diagram**
5. Name the file: **TechSafe_Network_Design**
6. Select **Blank Diagram**
7. Click **Create**

### Step 3: Add Router and Switch

1. In the shape library, search for **router** or browse **Network** category
2. Drag a **Router** shape to the canvas
3. Search for **switch** and drag a **Switch** shape below the router

![Router and switch placed on canvas]

![alt text](<../Screenshots/Router and switch placed on canvas.jpg>)

### Step 4: Connect Router to Switch

1. Select the **Connector** tool from the toolbar (or use the line shape)
2. Click on the router, then drag to the switch to create a connection line

### Step 5: Add Subnets

1. Search for **cloud** or use a **rounded rectangle** to represent each subnet
2. Add three subnet shapes below the switch

**Option A: Using cloud shapes**

- Add three cloud shapes labeled Administration, Sales, and IT

**Option B: Using rectangles**

- Add three rectangles labeled with each department name

![Three subnets placed below switch]

![alt text](<../Screenshots/TechSafe_ Ltd_network_diagram.drawio (2).png>)

### Step 6: Connect Subnets to Switch

1. Use the connector tool to draw solid lines from the switch to each subnet
2. Ensure all three subnets are connected to the switch

### Step 7: Label All Components

Add text labels to each component:

| Component     | Label          |
| :------------ | :------------- |
| Router        | Router         |
| Switch        | Switch         |
| First subnet  | Administration |
| Second subnet | Sales          |
| Third subnet  | IT             |

![Complete network diagram with labels]

### Step 8: Format the Diagram (Optional)

- Adjust colors for better visibility
- Ensure lines are solid (not dashed)
- Remove any extra elements not required

### Step 9: Take Screenshot

1. Ensure the diagram shows only:

   - Router (labeled)
   - Switch (labeled)
   - Connection line between router and switch
   - Three subnets (labeled Administration, Sales, IT)
   - Solid lines from switch to each subnet
2. No additional elements beyond these
3. Take a screenshot:

   - **Windows:** Use Snipping Tool (Start → Snipping Tool) → New → drag over diagram
   - **macOS:** Press Shift + Command + 4, drag over diagram
4. Save the screenshot as **`Task1_NetworkDiagram.png`**

---

## Sample Network Diagram

```
                          ┌─────────────┐
                          │   Router    │
                          │   (Router)  │
                          └──────┬──────┘
                                 │
                                 │
                          ┌──────▼──────┐
                          │   Switch    │
                          │   (Switch)  │
                          └──────┬──────┘
                                 │
        ┌────────────────────────┼────────────────────────┐
        │                        │                        │
        ▼                        ▼                        ▼
┌───────────────┐      ┌───────────────┐      ┌───────────────┐
│ Administration │      │     Sales     │      │      IT       │
│   Subnet      │      │   Subnet      │      │   Subnet      │
└───────────────┘      └───────────────┘      └───────────────┘
```

---

# Task 2: Calculate Subnet Addresses and Subnet Masks

## Scenario

You are working with a fixed IP address of **198.51.100.0/24**. The network is divided into three subnets with the following IP address ranges for each department:

| Department               | IP Address Range                 |
| :----------------------- | :------------------------------- |
| **Administration** | 198.51.100.1 – 198.51.100.62    |
| **Sales**          | 198.51.100.65 – 198.51.100.126  |
| **IT**             | 198.51.100.129 – 198.51.100.190 |

Your task is to calculate each department's subnet addresses and subnet masks based on their specified IP address ranges and save that information into a text-based table for later use.

![alt text](<../Screenshots/Calculate Subnet Address for Each Department.png>)


---

## Understanding Subnet Calculation

### Step 1: Calculate Subnet Address for Each Department

The **subnet address** is the first address in the range (network address).

| Department     | IP Address Range                 | Subnet Address |
| :------------- | :------------------------------- | :------------- |
| Administration | 198.51.100.1 – 198.51.100.62    | 198.51.100.0   |
| Sales          | 198.51.100.65 – 198.51.100.126  | 198.51.100.64  |
| IT             | 198.51.100.129 – 198.51.100.190 | 198.51.100.128 |


### Step 2: Calculate Subnet Mask for Each Department

The subnet mask determines the network size. To find the mask, calculate how many addresses are in each range.

Visit: https://www.vultr.com/resources/subnet-calculator/

![alt text](<../Screenshots/IPv4 Subnet Calculator - Vultr.png>)

**Administration:**

- Addresses: 198.51.100.1 to 198.51.100.62
- Total usable addresses: 62
- Network size: 64 addresses (including network and broadcast)
- CIDR: /26
- Subnet Mask: 255.255.255.192

**Sales:**

- Addresses: 198.51.100.65 to 198.51.100.126
- Total usable addresses: 62
- Network size: 64 addresses
- CIDR: /26
- Subnet Mask: 255.255.255.192

**IT:**

- Addresses: 198.51.100.129 to 198.51.100.190
- Total usable addresses: 62
- Network size: 64 addresses
- CIDR: /26
- Subnet Mask: 255.255.255.192

### Step 3: Create the Subnet Table

Create a table with the following information:

| Subnet Name    | Subnet Address | Subnet Mask     | IP Address Range                 |
| :------------- | :------------- | :-------------- | :------------------------------- |
| Administration | 198.51.100.0   | 255.255.255.192 | 198.51.100.1 – 198.51.100.62    |
| Sales          | 198.51.100.64  | 255.255.255.192 | 198.51.100.65 – 198.51.100.126  |
| IT             | 198.51.100.128 | 255.255.255.192 | 198.51.100.129 – 198.51.100.190 |

### Step 4: Create the Table in a Text Editor

1. Open Notepad (or any text editor)
2. Create the table using a formatted layout:

```
+----------------+----------------+-------------------+-------------------------------------+
|  Subnet Name   |  Subnet Address |    Subnet Mask    |         IP Address Range            |
+----------------+----------------+-------------------+-------------------------------------+
| Administration | 198.51.100.0    | 255.255.255.192   | 198.51.100.1 – 198.51.100.62        |
| Sales          | 198.51.100.64   | 255.255.255.192   | 198.51.100.65 – 198.51.100.126      |
| IT             | 198.51.100.128  | 255.255.255.192   | 198.51.100.129 – 198.51.100.190     |
+----------------+----------------+-------------------+-------------------------------------+
```

### Step 5: Take Screenshot

1. Ensure the screenshot shows:

   - Four columns: Subnet Name, Subnet Address, Subnet Mask, IP Address Range
   - Labels at the top of each column
   - One row for each subnet (Administration, Sales, IT)
   - No additional text beyond the table
2. Take a screenshot of the table
3. Save the screenshot as **`Task2_Screenshot1.png`**

![alt text](<../Screenshots/Subnet Table.png>)

---

# Task 3: Configure Windows Firewall Rules

## Scenario

As part of securing the network, you need to configure Windows Firewall on the IT department's server. You will create an inbound rule to block Remote Desktop Protocol (RDP) traffic on the Public network profile.

### Deliverable

A screenshot showing the newly created inbound rule in Windows Defender Firewall with Advanced Security.

---

## Step 1: Open Windows Defender Firewall with Advanced Security

1. Click the **Start** button
2. Type **Windows Defender Firewall** in the search bar
3. Select **Windows Defender Firewall with Advanced Security**

![Windows Defender Firewall with Advanced Security in search]

![alt text](<../Screenshots/Windows Defender Firewall with Advanced Security in search.png>)

![alt text](<../Screenshots/Advanced Settings .png>)

### Step 2: Select Inbound Rules

1. In the left navigation pane, click **Inbound Rules**

![Inbound Rules selected]

![alt text](<../Screenshots/Inbound Rules selected.png>)

### Step 3: Create New Rule

1. In the right Actions pane, click **New Rule...**

![New Rule option]

![alt text](<../Screenshots/New Rule option.png>)

### Step 4: Select Rule Type

1. Select **Port**
2. Click **Next**

### Step 5: Configure Protocol and Port

1. Select **TCP**
2. Select **Specific local ports**
3. Enter **3389** (default RDP port)
4. Click **Next**

![Port configuration with TCP port 3389]

![alt text](<../Screenshots/Port configuration with TCP port 3389.png>)

### Step 6: Specify Action

1. Select **Block the connection**
2. Click **Next**

![Block the connection selected]

![alt text](<../Screenshots/Block the connection selected.png>)

### Step 7: Select Profile

1. Check only **Public** (uncheck Domain and Private)
2. Click **Next**

![Profile selection with only Public checked]

![alt text](<../Screenshots/Profile selection with only Public checked.png>)

### Step 8: Name the Rule

1. Enter a name: **Block RDP on Public Network**
2. Click **Finish**

![Rule naming]

![alt text](<../Screenshots/Rule naming.png>)

### Step 9: Verify the Rule

1. In the Inbound Rules list, locate **Block RDP on Public Network**
2. Verify the rule shows:
   - **Enabled:** Yes (green checkmark)
   - **Action:** Block
   - **Profile:** Public

![Inbound Rules list showing new rule]

![alt text](<../Screenshots/Inbound Rules list showing new rule.png>)

### Step 10: Take Screenshot

1. Take a screenshot showing the new inbound rule in the list
2. Save the screenshot as **`Task3_Firewall_Rule.png`**

---

# Task 4: Configure DNS Filtering

## Scenario

TechSafe Ltd. wants to restrict access to social media websites during business hours. You need to create an outbound firewall rule to block DNS queries to the domain `www.socialmedia.com` (use `www.example.com` for testing purposes).

### Deliverable

A screenshot showing the newly created outbound rule with custom scope configured to block the specific IP address of the website.

---

## Step 1: Find the IP Address to Block

1. Open Command Prompt
2. Use nslookup to find the IP address of the website:

```cmd
nslookup www.example.com
```

**Example output:**

```
Non-authoritative answer:
Name:    www.example.com
Address:  93.184.216.34
```

Note the IP address (for this example, we'll use `93.184.216.34`).

![nslookup command output]

![alt text](<../Screenshots/nslookup command output.png>)

### Step 2: Open Windows Defender Firewall with Advanced Security

1. Open **Windows Defender Firewall with Advanced Security**
2. In the left pane, click **Outbound Rules**

### Step 3: Create New Rule

1. In the right Actions pane, click **New Rule...**

### Step 4: Select Custom Rule Type

1. Select **Custom**
2. Click **Next**

![Custom rule type selected]

### Step 5: Configure Program

1. Select **All programs**
2. Click **Next**

### Step 6: Configure Protocol and Ports

1. Keep default settings (Protocol type: Any)
2. Click **Next**

### Step 7: Configure Scope

1. In **Which remote IP addresses does this rule apply to?**
2. Select **These IP addresses**
3. Click **Add**

![Scope configuration with These IP addresses selected]

4. In the Add IP Address dialog:
   - Select **This IP address or subnet**
   - Enter the IP address: `93.184.216.34`
   - Click **OK**

![Add IP address dialog]

5. Click **Next**

### Step 8: Specify Action

1. Select **Block the connection**
2. Click **Next**

### Step 9: Specify Profile

1. Select all three profiles:
   - ☑ Domain
   - ☑ Private
   - ☑ Public
2. Click **Next**

![Profile selection with all three checked]

### Step 10: Name the Rule

1. Enter a name: **Block Social Media DNS**
2. Click **Finish**

![Rule naming]

### Step 11: Verify the Rule

1. In the Outbound Rules list, locate **Block Social Media DNS**
2. Verify the rule shows:
   - **Enabled:** Yes (green checkmark)
   - **Action:** Block
   - **Profile:** Domain, Private, Public

![Outbound Rules list showing new rule]

### Step 12: Take Screenshot

1. Take a screenshot showing the new outbound rule in the list
2. Save the screenshot as **`Task4_DNS_Filtering.png`**

---

## Cleanup (Optional)

After completing the project, you may want to disable or delete the firewall rules you created:

1. In Windows Defender Firewall with Advanced Security
2. Right-click each rule and select **Disable Rule** or **Delete**

---

## Submission Checklist

Before submitting, ensure you have the following screenshots:

| Task             | Screenshot File              | Description                                                                           |
| :--------------- | :--------------------------- | :------------------------------------------------------------------------------------ |
| **Task 1** | `Task1_NetworkDiagram.png` | Network diagram with router, switch, and three subnets (Administration, Sales, IT)    |
| **Task 2** | `Task2_Screenshot1.png`    | Subnet table with columns: Subnet Name, Subnet Address, Subnet Mask, IP Address Range |
| **Task 3** | `Task3_Firewall_Rule.png`  | Inbound rule "Block RDP on Public Network" in Windows Firewall                        |
| **Task 4** | `Task4_DNS_Filtering.png`  | Outbound rule blocking specific IP address for DNS filtering                          |

---

## Summary

In this final project, you have:

| Task             | Activity                                                                | Completed |
| :--------------- | :---------------------------------------------------------------------- | :-------- |
| **Task 1** | Designed network diagram with router, switch, and three subnets         | ☐        |
| **Task 2** | Calculated subnet addresses and masks for Administration, Sales, and IT | ☐        |
| **Task 3** | Created inbound firewall rule to block RDP on Public network            | ☐        |
| **Task 4** | Created outbound firewall rule to block specific IP address             | ☐        |

---

## Congratulations!

You have successfully completed the **Network Design and Security Configuration** final project. You have demonstrated your ability to:

- Design a structured network with subnets
- Calculate subnet addresses and subnet masks
- Configure Windows Firewall rules for network security
- Implement DNS filtering using outbound firewall rules

Submit your four screenshots as directed by your instructor to complete this project.

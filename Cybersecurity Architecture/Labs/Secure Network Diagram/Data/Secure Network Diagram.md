
![alt text](../Screenshots/vplogo_300.png)


# Hands-on Lab: Secure Network Diagram


**Estimated time needed: 15 minutes**

---

## Scenario

Consider this scenario. You are a newly appointed IT security professional for **Llobex Corporation**, an EdTech startup. While the organization has grown in terms of revenue and customers, Llobex's network infrastructure has not been updated in over three years.

As a result, Llobex recently experienced a **significant data breach** resulting in the loss of sensitive customer information. As an aftermath of the data breach, the organization has seen a drop in customers.

The Board of Directors has tasked you with **overhauling and enhancing the security** of Llobex's network infrastructure to prevent future incidents.

The next steps will guide you through the process of determining a secure network infrastructure.

---

## Objectives

After completing this lab, you will be able to **create a secure network infrastructure diagram**.

---

## Prerequisites

Before you begin, make sure to complete the *Securing Network Infrastructure* reading.

---

## Exercise 1: Setting up the diagramming tool

For the purposes of this exercise, you will use a web-based online diagramming tool named **Visual Paradigm** (https://online.visual-paradigm.com/). In this exercise, you will sign up for a free version of the tool.

### Steps:

1. Navigate to **https://online.visual-paradigm.com/**
2. Click **Sign up**
3. On the Sign-up page, accept the default selection, **Use the Free Edition**
4. Next, enter a valid email address and click **Sign Up**
5. On the Welcome to Visual Paradigm! page, click the **Visit your Visual Paradigm workspace** link
6. The Visual Paradigm Online page will be displayed

---

## Exercise 2: Review the existing network architecture

The IT team has shared the diagram of the existing network setup. You need to **analyze the diagram** and make changes to ensure a secure network.

### Step 1: Download the existing network diagram

Right-click here and then click **Save link as…** to download the file containing the existing network diagram. Save the file in the relevant folder.

### Step 2: Import the downloaded file in Visual Paradigm Online

1. In the Visual Paradigm Online page, click the **Create New** drop-down button
2. Then, select **Import/Open**
3. Next, select **Device**
4. When prompted, click **Choose File**
5. Navigate to the device or folder where you downloaded the file
6. Select the file and click **Open**

The network diagram with all the components in the current layout will be displayed. The network diagram consists of components, such as:

- Internet Service Provider (ISP)
- Modem
- External router
- Internal switch
- Wireless router
- Local Area Network (LAN)

### Explore the Visual Paradigm Online tool

- Notice the network icons available, such as **firewall** and **cloud**, and tools such as **Text**, **Image**, and **Diagram Shapes**
- You can click a shape and drag them to the required location in the diagram
- Right-click the shape → click **Order** → click **Send to Back** to move a layer backward

---

## Exercise 3: Update the diagram to build a secure network

In this exercise, you will update the diagram to add components that will help build a secure network.

### Step 1: Add a Demilitarized Zone (DMZ) to the network

Add a **DMZ** to the network, which is a separate network that should include:

- A **web server**
- A **DNS server**

The DMZ should be **separated from the internal LAN**.

> **Tip:** In the Visual Paradigm Online tool, use the toolbar on the left of the diagram to add shapes and text. Right-click the shape → click **Order** → click **Send to Back** to make the web server and DNS server visible.

### Step 2: Add two firewalls to the network

Add **two firewalls** to the network:

- One to **filter external traffic**
- Another to **filter internal traffic**

> **Tip:** In the Visual Paradigm Online tool, you can use the search bar to find a network component.

### Step 3: Add an Intrusion Detection System (IDS)

Add an **IDS** to the network, which will:

- Monitor internal network traffic
- Provide alerts for any malicious activities detected

> **Tip:** In the Visual Paradigm Online tool, you can use the search bar to lookup a server component.

---

## Summary of Security Enhancements

| Component                   | Purpose                                                                    |
| --------------------------- | -------------------------------------------------------------------------- |
| **DMZ**               | Isolates public-facing servers (web, DNS) from the internal network        |
| **External Firewall** | Filters traffic between the internet and the network perimeter             |
| **Internal Firewall** | Filters traffic between the DMZ and the internal LAN                       |
| **IDS**               | Monitors internal traffic for malicious activity and alerts administrators |

---

## Next Steps

After completing your secure network diagram, review it against the **Five Principles of Cybersecurity** and the **CIA Triad** to ensure all security bases are covered.

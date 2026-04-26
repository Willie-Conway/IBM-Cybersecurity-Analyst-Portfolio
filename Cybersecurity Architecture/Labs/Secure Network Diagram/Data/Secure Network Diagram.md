
![alt text](../Screenshots/vplogo_300.png)


# Hands-on Lab: Secure Network Diagram

**Estimated time needed:** 15 minutes

---

## Scenario

You are a newly appointed IT security professional for **Llobex Corporation**, an EdTech startup. While the organization has grown in terms of revenue and customers, Llobex's network infrastructure has not been updated in over three years.

As a result, Llobex recently experienced a **significant data breach** resulting in the loss of sensitive customer information. Following the breach, the organization has seen a drop in customers.

The Board of Directors has tasked you with overhauling and enhancing the security of Llobex's network infrastructure to prevent future incidents.

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective |
|---|-----------|
| 1 | Create a secure network infrastructure diagram |
| 2 | Identify and add critical security components to an existing network |
| 3 | Design a DMZ with proper segmentation |
| 4 | Place firewalls at appropriate boundaries |
| 5 | Add intrusion detection capabilities |

---

## Prerequisites

Before you begin, make sure to complete the **Securing Network Infrastructure** reading.

---

## Exercise 1: Setting Up the Diagramming Tool

For the purposes of this exercise, you will use a web-based online diagramming tool named **Visual Paradigm** (https://online.visual-paradigm.com/). In this exercise, you will sign up for a free version of the tool.

### Step-by-Step Sign-Up Process

#### Step 1: Navigate to Visual Paradigm

Open your web browser and go to:
```
https://online.visual-paradigm.com/
```

#### Step 2: Click Sign Up

Locate and click the **Sign up** button on the homepage.

```
┌─────────────────────────────────────────────────────────────────┐
│                    VISUAL PARADIGM ONLINE                        │
│                                                                  │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │                    [Sign up for Free]                    │   │
│   └─────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

#### Step 3: Select Free Edition

On the Sign-up page:
- Accept the default selection: **Use the Free Edition**
- Enter a valid email address
- Click **Sign Up**

```
┌─────────────────────────────────────────────────────────────────┐
│                      SIGN UP FOR FREE                            │
│                                                                  │
│   ○ Use the Free Edition (Recommended)                          │
│   ○ Use the Trial Edition (14 days)                             │
│                                                                  │
│   Email Address: [________________________]                     │
│                                                                  │
│                        [Sign Up]                                 │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

#### Step 4: Access Your Workspace

On the **Welcome to Visual Paradigm!** page:
- Click the **Visit your Visual Paradigm workspace** link

#### Step 5: Home Page Display

The **Visual Paradigm Online** page will be displayed, showing the main dashboard with diagramming options.

```
┌─────────────────────────────────────────────────────────────────┐
│                   VISUAL PARADIGM WORKSPACE                      │
│                                                                  │
│   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐            │
│   │ Create New  │  │  Import     │  │   Templates │            │
│   │   Diagram   │  │             │  │             │            │
│   └─────────────┘  └─────────────┘  └─────────────┘            │
│                                                                  │
│   Recent Diagrams:                                               │
│   • (Empty)                                                      │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Exercise 2: Review the Existing Network Architecture

The IT team has shared the diagram of the existing network setup. You need to analyze the diagram and make changes to ensure a secure network.

### Step 1: Download the Existing Network Diagram

Right-click the link provided in your course materials and select **Save link as…** to download the file containing the existing network diagram. Save the file in a relevant folder on your computer.

### Step 2: Import the Downloaded File in Visual Paradigm Online

#### Import Process:

```
┌─────────────────────────────────────────────────────────────────┐
│                    IMPORTING THE DIAGRAM                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   Step 2.1: Click "Create New" Drop-down                        │
│              │                                                   │
│              ▼                                                   │
│   Step 2.2: Select "Import/Open"                                │
│              │                                                   │
│              ▼                                                   │
│   Step 2.3: Select "Device"                                     │
│              │                                                   │
│              ▼                                                   │
│   Step 2.4: Click "Choose File"                                 │
│              │                                                   │
│              ▼                                                   │
│   Step 2.5: Navigate to downloaded file                         │
│              │                                                   │
│              ▼                                                   │
│   Step 2.6: Select file and click "Open"                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Existing Network Components

After importing, the network diagram will display the following components in the current (insecure) layout:

| Component | Symbol | Current Location |
|-----------|--------|-------------------|
| **ISP (Internet Service Provider)** | ☁️ Cloud | Internet connection point |
| **Modem** | 📟 Device | Between ISP and router |
| **External Router** | 📡 Router | Between modem and switch |
| **Internal Switch** | 🔌 Switch | Connecting all internal devices |
| **Wireless Router** | 📶 Wi-Fi | Connected to switch |
| **LAN (Local Area Network)** | 💻 Computers | Connected to switch |

### Current Insecure Diagram (Conceptual)

```
┌─────────────────────────────────────────────────────────────────┐
│              EXISTING (INSECURE) NETWORK DIAGRAM                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   INTERNET                                                       │
│      │                                                           │
│      ▼                                                           │
│    [ISP]                                                         │
│      │                                                           │
│      ▼                                                           │
│   [MODEM]                                                        │
│      │                                                           │
│      ▼                                                           │
│   [ROUTER] ─────────────────────────────────────────┐           │
│      │                                               │           │
│      ▼                                               │           │
│   [SWITCH] ◄───────────────────────────────────────┘           │
│      │                                               │           │
│      ├──────────┬──────────┬──────────┬────────────┘           │
│      │          │          │          │                          │
│      ▼          ▼          ▼          ▼                          │
│   [LAN]      [LAN]     [WIRELESS]   [SERVER]                     │
│   (PC)       (PC)      [ROUTER]     (Internal)                   │
│                           │                                      │
│                           ▼                                      │
│                      [Wi-Fi DEVICES]                             │
│                                                                  │
│   PROBLEMS:                                                      │
│   ✗ No firewall(s)                                              │
│   ✗ Web server直接在内部网络中 (in internal network)              │
│   ✗ No DMZ                                                       │
│   ✗ No IDS/IPS                                                  │
│   ✗ Single router handles all traffic                           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Explore Visual Paradigm Online

Take a moment to familiarize yourself with the tool:

| Feature | Location | Function |
|---------|----------|----------|
| **Network Icons** | Left toolbar (search bar) | Find firewall, cloud, server shapes |
| **Text Tool** | Left toolbar | Add labels and annotations |
| **Image Tool** | Left toolbar | Add custom images |
| **Diagram Shapes** | Left toolbar | Basic shapes (rectangles, circles, arrows) |
| **Layer Management** | Right-click shape → Order → Send to Back | Control shape visibility |

---

## Exercise 3: Update the Diagram to Build a Secure Network

In this exercise, you will update the diagram to add components that will help build a secure network.

### Step 1: Add a Demilitarized Zone (DMZ) to the Network

#### What is a DMZ?

A **DMZ (Demilitarized Zone)** is a separate network segment that sits between the internet and the internal network. It hosts public-facing services while keeping the internal network isolated.

#### Task: Add DMZ to the Diagram

Add a DMZ to the network that should include:
- **Web Server** (for public website)
- **DNS Server** (for domain name resolution)

The DMZ should be **separated from the internal LAN** by firewalls.

#### How to Add DMZ in Visual Paradigm:

```
┌─────────────────────────────────────────────────────────────────┐
│                    ADDING A DMZ - STEPS                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   1. Use the shape tool to draw a large dashed rectangle         │
│      or use a cloud/segment shape                                │
│                                                                  │
│   2. Label it: "DMZ (Demilitarized Zone) - Semi-Trusted"        │
│                                                                  │
│   3. Inside the DMZ, add:                                        │
│      • Web Server icon (search: "server")                        │
│      • DNS Server icon (search: "dns")                           │
│                                                                  │
│   4. Right-click the DMZ and DNS/Web shapes → Order →            │
│      Send to Back to ensure proper layering                      │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

#### DMZ Placement in Diagram:

```
┌─────────────────────────────────────────────────────────────────┐
│                    NETWORK WITH DMZ                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   INTERNET                                                       │
│      │                                                           │
│      ▼                                                           │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │                     DMZ ZONE                             │   │
│   │   ┌─────────────┐      ┌─────────────┐                  │   │
│   │   │ Web Server  │      │  DNS Server │                  │   │
│   │   └─────────────┘      └─────────────┘                  │   │
│   └─────────────────────────────────────────────────────────┘   │
│      │                                                           │
│      ▼                                                           │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │                  INTERNAL ZONE (Trusted)                 │   │
│   │   ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐   │   │
│   │   │   PC    │  │   PC    │  │ Server  │  │  Wi-Fi  │   │   │
│   │   └─────────┘  └─────────┘  └─────────┘  └─────────┘   │   │
│   └─────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

> **Note:** In Visual Paradigm, right-click the shape → click **Order** → click **Send to Back** to make the Web server and DNS server visible inside the DMZ.

---

### Step 2: Add Two Firewalls to the Network

#### Why Two Firewalls?

| Firewall | Location | Purpose |
|----------|----------|---------|
| **External Firewall** | Between Internet and DMZ | Filters all incoming traffic from the internet |
| **Internal Firewall** | Between DMZ and Internal LAN | Controls traffic entering the internal network |

#### Task: Add Firewalls

Add two firewalls to the network:
1. One to filter **external traffic** (between Internet and DMZ)
2. One to filter **internal traffic** (between DMZ and Internal LAN)

#### How to Add Firewalls in Visual Paradigm:

```
┌─────────────────────────────────────────────────────────────────┐
│                   ADDING FIREWALLS - STEPS                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   1. Use the search bar in the left toolbar                     │
│   2. Type: "firewall"                                           │
│   3. Drag the firewall shape to the diagram                     │
│   4. Position:                                                   │
│      • External Firewall: Between ISP/Modem and DMZ             │
│      • Internal Firewall: Between DMZ and Internal switch       │
│   5. Label each firewall appropriately                          │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

#### Complete Firewall Placement:

```
┌─────────────────────────────────────────────────────────────────┐
│                 NETWORK WITH DUAL FIREWALLS                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   INTERNET                                                       │
│      │                                                           │
│      ▼                                                           │
│   ┌─────────────────┐                                           │
│   │  ISP / Modem    │                                           │
│   └────────┬────────┘                                           │
│            │                                                     │
│            ▼                                                     │
│   ┌─────────────────────────────────────────┐                   │
│   │      EXTERNAL FIREWALL                   │                   │
│   │  "Filters all incoming internet traffic" │                   │
│   └────────────────────┬────────────────────┘                   │
│                        │                                         │
│                        ▼                                         │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │                     DMZ ZONE                             │   │
│   │   ┌─────────────┐      ┌─────────────┐                  │   │
│   │   │ Web Server  │      │  DNS Server │                  │   │
│   │   └─────────────┘      └─────────────┘                  │   │
│   └─────────────────────────────────────────────────────────┘   │
│                        │                                         │
│                        ▼                                         │
│   ┌─────────────────────────────────────────┐                   │
│   │      INTERNAL FIREWALL                   │                   │
│   │  "Controls traffic to internal network"  │                   │
│   └────────────────────┬────────────────────┘                   │
│                        │                                         │
│                        ▼                                         │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │                  INTERNAL ZONE (Trusted)                 │   │
│   │                                                          │   │
│   │   ┌─────────┐     ┌─────────┐     ┌─────────┐           │   │
│   │   │ Switch  │────►│   PC    │     │   PC    │           │   │
│   │   └────┬────┘     └─────────┘     └─────────┘           │   │
│   │        │                                                │   │
│   │        ├───────┐                                        │   │
│   │        │       │                                        │   │
│   │        ▼       ▼                                        │   │
│   │   ┌───────┐ ┌─────────┐                                │   │
│   │   │Server │ │Wireless │──► Wi-Fi Devices               │   │
│   │   └───────┘ │ Router  │                                │   │
│   │            └─────────┘                                │   │
│   └─────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

### Step 3: Add an Intrusion Detection System (IDS)

#### What is an IDS?

An **Intrusion Detection System (IDS)** monitors network traffic for suspicious activity and alerts administrators when potential threats are detected.

#### Task: Add IDS

Add an IDS to the network that will:
- Monitor internal network traffic
- Provide alerts for any malicious activities detected

#### How to Add IDS in Visual Paradigm:

```
┌─────────────────────────────────────────────────────────────────┐
│                     ADDING IDS - STEPS                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   1. Use the search bar in the left toolbar                     │
│   2. Type: "ids" or "intrusion" or "server"                     │
│   3. Drag the IDS/server shape to the diagram                   │
│   4. Position it to monitor internal traffic                    │
│      (Typically connected to the internal switch)               │
│   5. Label it: "Intrusion Detection System (IDS)"               │
│   6. Add annotation: "Monitors network traffic & alerts"        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

#### IDS Placement in Diagram:

```
┌─────────────────────────────────────────────────────────────────┐
│                  FINAL SECURE NETWORK DIAGRAM                    │
│                      (With IDS Added)                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   INTERNET                                                       │
│      │                                                           │
│      ▼                                                           │
│   ┌─────────────────┐                                           │
│   │  ISP / Modem    │                                           │
│   └────────┬────────┘                                           │
│            │                                                     │
│            ▼                                                     │
│   ┌─────────────────────────────────────────┐                   │
│   │      EXTERNAL FIREWALL                   │                   │
│   │  "Allows only HTTPS (443), DNS (53)"     │                   │
│   └────────────────────┬────────────────────┘                   │
│                        │                                         │
│                        ▼                                         │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │                     DMZ ZONE (Semi-Trusted)              │   │
│   │                                                          │   │
│   │   ┌─────────────┐      ┌─────────────┐                  │   │
│   │   │ Web Server  │      │  DNS Server │                  │   │
│   │   │  (Public)   │      │  (Public)   │                  │   │
│   │   └─────────────┘      └─────────────┘                  │   │
│   │                                                          │   │
│   └─────────────────────────────────────────────────────────┘   │
│                        │                                         │
│                        ▼                                         │
│   ┌─────────────────────────────────────────┐                   │
│   │      INTERNAL FIREWALL                   │                   │
│   │  "Restricts access to authorized only"   │                   │
│   └────────────────────┬────────────────────┘                   │
│                        │                                         │
│                        ▼                                         │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │               INTERNAL ZONE (Trusted)                    │   │
│   │                                                          │   │
│   │   ┌─────────────────────────────────────────────┐       │   │
│   │   │                 SWITCH                       │       │   │
│   │   └──────┬──────────┬──────────┬────────┬───────┘       │   │
│   │          │          │          │        │                │   │
│   │          ▼          ▼          ▼        ▼                │   │
│   │   ┌─────────┐ ┌─────────┐ ┌──────────────┐ ┌─────────┐   │   │
│   │   │   PC    │ │   PC    │ │   Server     │ │ Wireless│   │   │
│   │   │(Employee│ │(Employee│ │  (Internal)  │ │ Router  │   │   │
│   │   │   1)    │ │   2)    │ │              │ │         │   │   │
│   │   └─────────┘ └─────────┘ └──────┬───────┘ └────┬────┘   │   │
│   │                                  │              │         │   │
│   │                                  │              ▼         │   │
│   │                                  │       ┌──────────┐     │   │
│   │                                  │       │ Wi-Fi    │     │   │
│   │                                  │       │ Devices  │     │   │
│   │                                  │       └──────────┘     │   │
│   │                                  │                         │   │
│   │                    ┌─────────────┴─────────────┐           │   │
│   │                    │           IDS             │           │   │
│   │                    │  "Monitors internal       │           │   │
│   │                    │   traffic & alerts"       │           │   │
│   │                    └───────────────────────────┘           │   │
│   │                                                          │   │
│   └─────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Final Secure Network Diagram Components Summary

| Component | Symbol | Location | Purpose |
|-----------|--------|----------|---------|
| **External Firewall** | ▭ Firewall | Internet ↔ DMZ | Filters incoming internet traffic |
| **DMZ** | ┌─ dashed ─┐ | Between firewalls | Hosts public-facing services |
| **Web Server** | 🖥️ Server | Inside DMZ | Hosts public website |
| **DNS Server** | 🖥️ Server | Inside DMZ | Resolves domain names |
| **Internal Firewall** | ▭ Firewall | DMZ ↔ Internal | Controls internal access |
| **Switch** | 🔌 Switch | Internal zone | Connects internal devices |
| **IDS** | 📊 IDS | Internal zone (monitoring) | Detects and alerts on threats |
| **Internal Servers** | 🖥️ Server | Internal zone | Internal applications/data |
| **Workstations** | 💻 PC | Internal zone | Employee computers |
| **Wireless Router** | 📶 Wi-Fi | Internal zone | Wi-Fi access |
| **Wi-Fi Devices** | 📱 Devices | Wireless network | Mobile devices |

---

## Before vs. After: Security Comparison

| Security Aspect | BEFORE (Insecure) | AFTER (Secure) |
|-----------------|-------------------|----------------|
| **Firewalls** | None | Dual firewalls (External + Internal) |
| **Web Server Location** | Internal network | DMZ |
| **DNS Server** | Not present | DMZ |
| **DMZ** | Not present | Added between firewalls |
| **IDS/IPS** | None | IDS monitoring internal traffic |
| **Network Segmentation** | Flat network | Segmented (Internet, DMZ, Internal) |
| **Internal Traffic Filtering** | None | Internal firewall controls |
| **Threat Detection** | None | IDS with alerts |

---

## Security Annotations to Add

Add these text annotations to your diagram:

| Annotation | Location | Text |
|------------|----------|------|
| **External Firewall Rule** | Near External Firewall | "Rule: Allow HTTPS (443) and DNS (53) only. Block all other inbound traffic." |
| **Internal Firewall Rule** | Near Internal Firewall | "Rule: Allow only DMZ → Internal responses. Block direct DMZ → Internal initiation." |
| **DMZ Purpose** | Inside DMZ box | "Public-facing services isolated from internal network" |
| **IDS Function** | Near IDS | "Monitors all internal traffic. Alerts security team of suspicious patterns." |
| **Encryption Note** | Near Web Server | "All web traffic encrypted with TLS 1.3" |

---

## Diagram Legend

Add a legend to your completed diagram:

```
┌─────────────────────────────────────────────────────────────────┐
│                         LEGEND                                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   ▭▭▭▭▭▭  Firewall           ┌─────┐  Server                     │
│   ┌─ ──┐   DMZ Boundary       💻      Workstation                │
│   ───►    Data Flow           📶      Wireless Router            │
│   🔒      Encryption Point    📊      IDS/Security                │
│                                                                  │
│   Colors:                                                        │
│   🔴 Red Zone = Internet (Untrusted)                             │
│   🟡 Yellow Zone = DMZ (Semi-Trusted)                            │
│   🟢 Green Zone = Internal (Trusted)                             │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Completion Checklist

| Task | Completed |
|------|-----------|
| **Exercise 1: Setup** | ☐ |
| Signed up for Visual Paradigm Free Edition | ☐ |
| Accessed Visual Paradigm workspace | ☐ |
| **Exercise 2: Review Existing Diagram** | ☐ |
| Downloaded existing network diagram | ☐ |
| Imported diagram into Visual Paradigm | ☐ |
| Explored tool features (icons, shapes, layering) | ☐ |
| **Exercise 3: Build Secure Network** | ☐ |
| Added DMZ zone to diagram | ☐ |
| Added Web Server inside DMZ | ☐ |
| Added DNS Server inside DMZ | ☐ |
| Added External Firewall (Internet ↔ DMZ) | ☐ |
| Added Internal Firewall (DMZ ↔ Internal) | ☐ |
| Added IDS monitoring internal traffic | ☐ |
| Added security annotations | ☐ |
| Added legend | ☐ |
| **Final Review** | ☐ |
| Saved the completed diagram | ☐ |
| Exported diagram as PNG/PDF | ☐ |

---

## Troubleshooting Tips

| Issue | Solution |
|-------|----------|
| **Can't find firewall icon** | Use search bar in left toolbar and type "firewall" |
| **Web server hidden behind DMZ box** | Right-click web server → Order → Send to Back |
| **Can't move shapes** | Click and drag; ensure shape is selected first |
| **Lost diagram changes** | Visual Paradigm auto-saves; check version history |
| **Can't add IDS** | Search for "server" and label it as IDS, or search "intrusion" |

---

## Key Takeaways

| Concept | Description |
|---------|-------------|
| **DMZ** | A separate network segment for public-facing services |
| **Dual Firewalls** | External + Internal firewalls create defense-in-depth |
| **Network Segmentation** | Separating networks by trust level (Internet, DMZ, Internal) |
| **IDS** | Monitors traffic and alerts on suspicious activity |
| **Web Server Placement** | Always in DMZ, never in internal network |
| **DNS Server Placement** | Public DNS in DMZ for external resolution |

---

## Summary

In this hands-on lab, you have:

| Activity | Completed |
|----------|-----------|
| Set up a free Visual Paradigm account | ☐ |
| Imported an existing insecure network diagram | ☐ |
| Analyzed the security flaws in the current setup | ☐ |
| Added a DMZ with Web Server and DNS Server | ☐ |
| Added an External Firewall between Internet and DMZ | ☐ |
| Added an Internal Firewall between DMZ and Internal network | ☐ |
| Added an IDS for internal threat detection | ☐ |
| Created a complete secure network architecture diagram | ☐ |

---

## Congratulations!

You have successfully completed the **Hands-on Lab: Secure Network Diagram**. You now know how to:

- Use Visual Paradigm Online for network diagramming
- Identify security flaws in an existing network
- Design a secure network with proper segmentation
- Place firewalls at appropriate trust boundaries
- Add a DMZ for public-facing services
- Incorporate IDS for threat detection
- Create professional security architecture diagrams

These skills are essential for:
- Security professionals designing secure networks
- IT administrators implementing defense-in-depth
- Network architects planning infrastructure upgrades
- Anyone preparing for security certification exams

---

## Additional Resources

| Resource | URL |
|----------|-----|
| **Visual Paradigm Online** | https://online.visual-paradigm.com/ |
| **Visual Paradigm Tutorials** | https://online.visual-paradigm.com/tutorials/ |
| **Network Diagram Templates** | https://online.visual-paradigm.com/diagrams/templates/ |
| **NIST Network Security Guidelines** | https://csrc.nist.gov |
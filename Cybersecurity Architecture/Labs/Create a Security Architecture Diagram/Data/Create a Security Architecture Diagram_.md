![alt text](../Screenshots/DrawIO.png)

# Hands-on Lab: Create a Security Architecture Diagram

**Estimated time needed:** 30 minutes

---

## Overview

Security architecture diagrams are visual representations that show how security controls, components, and data flows are organized to protect an organization's systems and information. As an architect stepping into cybersecurity, learning to create these diagrams is essential for communicating security designs to stakeholders, identifying vulnerabilities, and planning security implementations.

In this lab, you'll learn the fundamental elements of a security architecture diagram and create a simple diagram for a web application scenario.

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective                                                          |
| - | ------------------------------------------------------------------ |
| 1 | Identify the core components of a security architecture diagram    |
| 2 | Understand security zones and network segmentation concepts        |
| 3 | Place security controls appropriately in an architecture           |
| 4 | Create a basic security architecture diagram for a web application |

---

## Tools Needed

| Tool                             | Purpose                  | Availability                        |
| -------------------------------- | ------------------------ | ----------------------------------- |
| **draw.io (diagrams.net)** | Free diagramming tool    | Web-based, no installation required |
| **Microsoft Visio**        | Professional diagramming | Paid, Windows only                  |
| **Lucidchart**             | Cloud-based diagramming  | Free tier available                 |
| **PowerPoint**             | Presentation diagramming | Microsoft Office                    |
| **Pen and paper**          | Quick sketching          | Available to everyone               |

For this lab, **draw.io** is recommended as it's free and web-based.

---

## The Scenario

You're designing security for a simple **e-commerce web application**. The application has:

| Component                       | Description                                 |
| ------------------------------- | ------------------------------------------- |
| **Public-facing website** | Where customers browse and shop             |
| **Database**              | Stores customer information and orders      |
| **Administrative portal** | For employees to manage products and orders |

---

## Exercise 1: Understanding Security Architecture Components

In this exercise, you will learn about the essential building blocks that make up a security architecture diagram.

### Step 1: Identify the Security Zones

Before drawing anything, you need to understand **security zones**. These are logical groupings of systems based on their security requirements and trust levels.

For our scenario, identify these three zones:

| Zone                    | Trust Level  | Description                                        | Color Code |
| ----------------------- | ------------ | -------------------------------------------------- | ---------- |
| **Internet Zone** | Untrusted    | Where external users and potential threats exist   | 🔴 Red     |
| **DMZ Zone**      | Semi-Trusted | Public-facing services, exposed but protected      | 🟡 Yellow  |
| **Internal Zone** | Trusted      | Sensitive systems like databases and internal apps | 🟢 Green   |

#### The House Analogy

Think of zones like rooms in a house with different security levels:

| Analogy           | Security Zone             |
| ----------------- | ------------------------- |
| Front Porch       | Internet Zone (Untrusted) |
| Living Room       | DMZ (Semi-Trusted)        |
| Bedroom with Safe | Internal Zone (Trusted)   |

### Step 2: List the Core Components

Write down or mentally note these essential components you'll need in your diagram:

| Component                    | Role                                             | Placement         |
| ---------------------------- | ------------------------------------------------ | ----------------- |
| **Firewall**           | Security guard controlling traffic between zones | Between each zone |
| **Web Server**         | Hosts public website                             | DMZ               |
| **Application Server** | Runs business logic                              | Internal Zone     |
| **Database Server**    | Stores sensitive data                            | Internal Zone     |
| **External Users**     | Customers browsing the site                      | Internet Zone     |
| **Admin Users**        | Employees managing the system                    | Internal Zone     |

> **Key Principle:** The web server needs to be accessible from the internet, but we want to keep the database as far from direct internet access as possible.

### Step 3: Understand the Traffic Flow

Security architecture isn't just about placing components. It is about understanding **how data moves securely**:

```
Traffic Flow Paths:

1. Customers: Internet → Firewall → Web Server (DMZ)

2. Web to App: Web Server → Internal Firewall → Application Server (Internal)

3. App to DB: Application Server → Database Server (Internal)

4. Admin Access: Admin Users → Internal Firewall → Application Server
```

> **Critical Concept:** Notice how every connection crosses a security control? That's intentional. We never allow direct access across zones without security validation.

---

## Exercise 2: Creating Your Security Architecture Diagram

In this exercise, you will create your first security architecture diagram using the components and concepts from Exercise 1.

### Task A: Set Up Your Diagram Canvas

#### Step 1: Create Three Horizontal Zones

Open your diagramming tool and create three distinct horizontal sections:

```
┌─────────────────────────────────────────────────────────────┐
│                    INTERNET ZONE (Untrusted)                 │
├─────────────────────────────────────────────────────────────┤
│                       DMZ (Demilitarized Zone)               │
├─────────────────────────────────────────────────────────────┤
│                   INTERNAL ZONE (Trusted)                    │
└─────────────────────────────────────────────────────────────┘
```

> **Design Note:** Using horizontal zones is a common convention—the most trusted areas are typically shown at the bottom or center, with less trusted areas above or to the sides.

#### Step 2: Add Visual Distinction

Make each zone visually distinct by using:

| Method              | Internet Zone       | DMZ                    | Internal Zone         |
| ------------------- | ------------------- | ---------------------- | --------------------- |
| **Colors**    | Light Red (#FFCDD2) | Light Yellow (#FFF9C4) | Light Green (#C8E6C9) |
| **Grayscale** | Dark Gray border    | Medium Gray border     | Light Gray border     |
| **Patterns**  | Crosshatch          | Dots                   | Solid                 |

> **Why this matters:** Visual separation helps viewers quickly understand trust boundaries, even if they're not security experts.

---

### Task B: Place Security Components

#### Step 1: Position the Firewalls (Security Boundaries)

Place firewall icons or rectangles at the boundaries between zones:

```
Internet Zone                    DMZ                      Internal Zone
     │                            │                            │
     ▼                            ▼                            ▼
┌─────────┐                  ┌─────────┐                  ┌─────────┐
│ External│                  │ Internal│                  │         │
│ Firewall│ ◄──────────────► │ Firewall│ ◄──────────────► │         │
└─────────┘                  └─────────┘                  └─────────┘
   (Border)                    (Between                    (Edge of
                              DMZ & Internal)              Internal)
```

**Label them clearly:**

- **External Firewall** - Between Internet and DMZ
- **Internal Firewall** - Between DMZ and Internal Zone

> **Analogy:** Think of firewalls as checkpoints. Just like airport security checks passengers before they enter secure areas, firewalls inspect network traffic before allowing it through.

#### Step 2: Add the Servers and Components

Place these components in their appropriate zones:

| Zone                    | Component                  | Icon Suggestion                  |
| ----------------------- | -------------------------- | -------------------------------- |
| **Internet Zone** | External Users / Customers | 👤 User icon or multiple figures |
| **DMZ**           | Web Server                 | 🖥️ Server icon or rectangle    |
| **Internal Zone** | Application Server         | 🖥️ Server icon                 |
| **Internal Zone** | Database Server            | 🗄️ Database cylinder icon      |
| **Internal Zone** | Admin Users / IT Staff     | 👤 Shield icon or figure         |

**Complete Layout:**

```
┌─────────────────────────────────────────────────────────────┐
│                    INTERNET ZONE (Untrusted)                 │
│                                                              │
│                    [👤 External Users]                       │
│                                                              │
└────────────┬────────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────────┐
│                 EXTERNAL FIREWALL                            │
└────────────┬────────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────────┐
│                       DMZ (Semi-Trusted)                     │
│                                                              │
│                    [🖥️ Web Server]                           │
│                                                              │
└────────────┬────────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────────┐
│                 INTERNAL FIREWALL                            │
└────────────┬────────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────────┐
│                   INTERNAL ZONE (Trusted)                    │
│                                                              │
│   [🖥️ Application Server]    [🗄️ Database Server]           │
│                                                              │
│                    [👤 Admin Users]                          │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

#### Step 3: Draw the Connection Lines (Traffic Flows)

Connect your components with arrows to show how traffic flows:

| Path        | From               | To                 | Via | Purpose              |
| ----------- | ------------------ | ------------------ | --- | -------------------- |
| **A** | External Users     | External Firewall  | →  | User requests        |
| **B** | External Firewall  | Web Server         | →  | Filtered traffic     |
| **C** | Web Server         | Internal Firewall  | →  | App requests         |
| **D** | Internal Firewall  | Application Server | →  | Filtered app traffic |
| **E** | Application Server | Database Server    | →  | Data queries         |
| **F** | Admin Users        | Internal Firewall  | →  | Admin access         |
| **G** | Internal Firewall  | Application Server | →  | Admin functions      |

**Complete Flow Diagram:**

```
Internet Zone          DMZ              Internal Zone
     │                  │                     │
[Users] ──┐             │                     │
     │    │             │                     │
     ▼    ▼             │                     │
[Ext FW] ──► [Web Server] ──┐                │
                           │ │                │
                           ▼ ▼                │
                        [Int FW] ◄────────────┘
                           │ │                │
                           ▼ ▼                ▼
                    [App Server] ──► [DB Server]
                           ▲
                           │
                      [Admin Users]
```

#### Step 4: Add Protocol Labels

Add labels to the arrows indicating the protocol or purpose:

| Connection               | Protocol     | Port      | Label Text                   |
| ------------------------ | ------------ | --------- | ---------------------------- |
| Users → Web Server      | HTTPS        | 443       | `HTTPS (Port 443)`         |
| Web Server → App Server | Internal API | -         | `Internal API Calls`       |
| App Server → Database   | SQL          | 1433/3306 | `Database Queries (SQL)`   |
| Admin → App Server      | HTTPS / SSH  | 443/22    | `Admin Access (HTTPS/SSH)` |

---

### Task C: Add Security Controls and Annotations

#### Step 1: Document Key Security Controls

Add text boxes or notes to highlight important security measures:

| Location                     | Annotation Text                                            |
| ---------------------------- | ---------------------------------------------------------- |
| **External Firewall**  | "Allows only HTTPS (443) inbound, blocks all other ports"  |
| **Web Server**         | "SSL/TLS encryption for all customer data"                 |
| **Internal Firewall**  | "Restricts access to authorized internal traffic only"     |
| **Application Server** | "Input validation, authentication, and session management" |
| **Database Server**    | "Encrypted at rest, access logged, least privilege access" |

> **Why annotations matter:** These annotations transform your diagram from a simple network map into a security architecture diagram. They show *how* security is implemented, not just *where* components exist.

#### Step 2: Add a Legend (Optional but Recommended)

Create a small legend box explaining your symbols:

```
┌─────────────────────────────────────────────┐
│                    LEGEND                    │
├─────────────────────────────────────────────┤
│  ┌────┐  Server/Component                   │
│  └────┘                                      │
│  ▭▭▭▭   Firewall                             │
│  ──►    Data Flow / Connection               │
│  🔴     Internet Zone (Untrusted)            │
│  🟡     DMZ (Semi-Trusted)                   │
│  🟢     Internal Zone (Trusted)              │
│  ===    Encrypted Traffic                    │
│  - - -  Optional/Management Traffic          │
└─────────────────────────────────────────────┘
```

#### Step 3: Review Your Diagram

Ask yourself these questions to verify your diagram is complete:

| Question                                               | Check |
| ------------------------------------------------------ | ----- |
| Are all three security zones clearly labeled?          | ☐    |
| Are firewalls placed at every zone boundary?           | ☐    |
| Is every component in the correct zone?                | ☐    |
| Are traffic flows shown with arrows?                   | ☐    |
| Are protocols/ports documented?                        | ☐    |
| Are security controls annotated?                       | ☐    |
| Is there a legend for symbols and colors?              | ☐    |
| Is the diagram readable by non-technical stakeholders? | ☐    |

---

## Exercise 3: Final Diagram Example

Below is a complete text-based representation of what your final diagram should look like:

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│                           SECURITY ARCHITECTURE DIAGRAM                             │
│                              E-Commerce Web Application                             │
└────────────────────────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────────────────────────┐
│                           INTERNET ZONE (Untrusted) 🔴                              │
│                                                                                     │
│                              ┌─────────────────┐                                   │
│                              │   👤 Customers   │                                   │
│                              │  (External Users) │                                  │
│                              └────────┬────────┘                                   │
│                                       │                                             │
│                                       │ HTTPS (Port 443)                            │
│                                       ▼                                             │
└───────────────────────────────────────┬────────────────────────────────────────────┘
                                        │
                                        ▼
┌────────────────────────────────────────────────────────────────────────────────────┐
│                           EXTERNAL FIREWALL                                         │
│                    "Allows only HTTPS (443) inbound"                                │
│                    "Blocks all other ports"                                         │
└───────────────────────────────────────┬────────────────────────────────────────────┘
                                        │
                                        │ Filtered HTTPS
                                        ▼
┌────────────────────────────────────────────────────────────────────────────────────┐
│                              DMZ (Semi-Trusted) 🟡                                  │
│                                                                                     │
│                          ┌─────────────────────┐                                   │
│                          │     🖥️ Web Server    │                                   │
│                          │                     │                                   │
│                          │ "SSL/TLS encryption │                                   │
│                          │  for all customer   │                                   │
│                          │      data"          │                                   │
│                          └──────────┬──────────┘                                   │
│                                     │                                               │
│                                     │ Internal API Calls                            │
│                                     ▼                                               │
└─────────────────────────────────────┬──────────────────────────────────────────────┘
                                      │
                                      ▼
┌────────────────────────────────────────────────────────────────────────────────────┐
│                           INTERNAL FIREWALL                                         │
│                    "Restricts access to authorized"                                 │
│                    "internal traffic only"                                          │
└─────────────────────────────────────┬──────────────────────────────────────────────┘
                                      │
                                      │ Filtered API Traffic
                                      ▼
┌────────────────────────────────────────────────────────────────────────────────────┐
│                           INTERNAL ZONE (Trusted) 🟢                                │
│                                                                                     │
│            ┌─────────────────────┐         ┌─────────────────────┐                │
│            │  🖥️ Application      │         │    🗄️ Database       │                │
│            │      Server         │────────►│       Server         │                │
│            │                     │  SQL    │                     │                │
│            │ "Input validation,  │ Queries │ "Encrypted at rest,  │                │
│            │  authentication,    │         │  access logged,      │                │
│            │  session mgmt"      │         │  least privilege"    │                │
│            └──────────▲──────────┘         └─────────────────────┘                │
│                       │                                                             │
│                       │ Admin Access (HTTPS/SSH)                                    │
│                       │                                                             │
│            ┌──────────┴──────────┐                                                 │
│            │   👤 Admin Users     │                                                 │
│            │   (IT Staff)        │                                                 │
│            └─────────────────────┘                                                 │
│                                                                                     │
└────────────────────────────────────────────────────────────────────────────────────┘

                                        LEGEND
                        ┌─────────────────────────────────────────┐
                        │  ┌────┐  Server/Component              │
                        │  └────┘                                 │
                        │  ▭▭▭▭   Firewall                        │
                        │  ──►    Data Flow                       │
                        │  🔴     Internet (Untrusted)            │
                        │  🟡     DMZ (Semi-Trusted)              │
                        │  🟢     Internal (Trusted)               │
                        └─────────────────────────────────────────┘
```

---

## Exercise 4: Common Security Architecture Patterns

### Pattern 1: Three-Tier Architecture with DMZ

```
Internet ──► Firewall ──► Web Tier (DMZ) ──► Firewall ──► App Tier ──► DB Tier
                                    (Internal)
```

**Best for:** Public-facing web applications, e-commerce sites

### Pattern 2: Microservices Architecture

```
API Gateway ──► Service Mesh ──► Microservices ──► Databases
     ▲              │                  │
     │              ▼                  ▼
Auth Service   Monitoring        Message Queue
```

**Best for:** Cloud-native applications, distributed systems

### Pattern 3: Zero Trust Architecture

```
User ──► Identity Provider ──► Trust Broker ──► Resource
         (Authentication)      (Policy Decision)
```

**Best for:** Remote work, cloud environments, high-security requirements

---

## Security Controls Reference Table

| Control Type           | Examples                                  | Placement                                   |
| ---------------------- | ----------------------------------------- | ------------------------------------------- |
| **Preventive**   | Firewalls, Encryption, Authentication     | Zone boundaries, Data at rest/transit       |
| **Detective**    | IDS/IPS, Logging, Monitoring              | Internal zone, between tiers                |
| **Corrective**   | Patching, Backup, Failover                | Internal zone, management network           |
| **Deterrent**    | Warning banners, Audits                   | User access points                          |
| **Compensating** | Additional authentication, Manual reviews | Where primary controls can't be implemented |

---

## Common Mistakes to Avoid

| Mistake                                        | Why It's Wrong                                   | Correction                              |
| ---------------------------------------------- | ------------------------------------------------ | --------------------------------------- |
| **Direct database access from DMZ**      | Database is exposed to potential web compromises | Always route through application server |
| **Missing firewalls between zones**      | No boundary enforcement                          | Place firewall at every trust boundary  |
| **No encryption labels**                 | Unclear where sensitive data is protected        | Annotate encryption points              |
| **Same color for all zones**             | Trust boundaries are invisible                   | Use distinct colors for each zone       |
| **Missing admin access paths**           | Internal access is overlooked                    | Show all access paths                   |
| **Bidirectional arrows without control** | Implies symmetric access rules                   | Use directional arrows, specify rules   |

---

## Lab Completion Checklist

| Task                                           | Completed | Notes                     |
| ---------------------------------------------- | --------- | ------------------------- |
| **Exercise 1: Understanding Components** | ☐        |                           |
| Identify three security zones                  | ☐        | Internet, DMZ, Internal   |
| List core components                           | ☐        | Firewalls, servers, users |
| Understand traffic flow paths                  | ☐        |                           |
| **Exercise 2: Creating Diagram**         | ☐        |                           |
| Set up three horizontal zones                  | ☐        |                           |
| Add visual distinction (colors/patterns)       | ☐        |                           |
| Place external firewall                        | ☐        |                           |
| Place internal firewall                        | ☐        |                           |
| Add web server in DMZ                          | ☐        |                           |
| Add application server in Internal             | ☐        |                           |
| Add database server in Internal                | ☐        |                           |
| Add external users (Internet)                  | ☐        |                           |
| Add admin users (Internal)                     | ☐        |                           |
| Draw connection arrows                         | ☐        |                           |
| Add protocol labels                            | ☐        |                           |
| **Exercise 3: Security Annotations**     | ☐        |                           |
| Add security control notes                     | ☐        |                           |
| Create legend                                  | ☐        |                           |
| Review diagram against checklist               | ☐        |                           |
| Save/export final diagram                      | ☐        |                           |

---

## Diagram Export Options

| Tool                 | Export Formats           |
| -------------------- | ------------------------ |
| **draw.io**    | PNG, JPG, SVG, PDF, XML  |
| **Visio**      | VSDX, PDF, PNG, SVG      |
| **Lucidchart** | PNG, JPG, PDF, SVG, VSDX |
| **PowerPoint** | PPTX, PDF, PNG           |

**Recommended:** Export as **PNG** for sharing and **PDF** for printing/documentation.

---

## Key Takeaways

| Concept                      | Description                                  |
| ---------------------------- | -------------------------------------------- |
| **Security Zones**     | Logical groupings based on trust levels      |
| **DMZ**                | Semi-trusted zone for public-facing services |
| **Firewall Placement** | At every trust boundary between zones        |
| **Traffic Flow**       | All traffic crosses security controls        |
| **Least Privilege**    | Only necessary access should be allowed      |
| **Defense in Depth**   | Multiple layers of security controls         |
| **Annotations**        | Explain*how* security is implemented       |

---

## Summary

In this hands-on lab, you have:

| Activity                                                        | Completed |
| --------------------------------------------------------------- | --------- |
| Learned the three core security zones (Internet, DMZ, Internal) | ☐        |
| Identified essential security architecture components           | ☐        |
| Understood traffic flow principles across trust boundaries      | ☐        |
| Created a three-zone security architecture diagram              | ☐        |
| Placed firewalls, servers, and users in correct zones           | ☐        |
| Added traffic arrows with protocol labels                       | ☐        |
| Documented security controls with annotations                   | ☐        |
| Created a legend for diagram readability                        | ☐        |
| Reviewed diagram against quality checklist                      | ☐        |

---

## Congratulations!

You have successfully completed the **Create a Security Architecture Diagram** lab. You now know how to:

- Identify security zones and their trust levels
- Place security controls appropriately in an architecture
- Create security architecture diagrams using a standard three-zone model
- Document security controls with annotations
- Design secure traffic flows across trust boundaries
- Apply defense-in-depth principles to architecture

These skills are essential for:

- Security architects designing secure systems
- Technical leads communicating security designs
- Security analysts identifying architectural vulnerabilities
- IT professionals planning security implementations

---

## Additional Resources

| Resource                              | URL                             |
| ------------------------------------- | ------------------------------- |
| **draw.io (diagrams.net)**      | https://www.draw.io             |
| **Lucidchart**                  | https://www.lucidchart.com      |
| **SABSA Framework**             | https://sabsa.org               |
| **TOGAF Security Architecture** | https://www.opengroup.org/togaf |
| **NIST Security Architecture**  | https://csrc.nist.gov           |

---

## Bonus: Advanced Diagram Elements

As you progress, consider adding these advanced elements to your security diagrams:

| Element                                  | Purpose                                   |
| ---------------------------------------- | ----------------------------------------- |
| **IDS/IPS Sensors**                | Intrusion detection/prevention            |
| **WAF (Web Application Firewall)** | Application-layer protection              |
| **SIEM**                           | Security monitoring and logging           |
| **HSM (Hardware Security Module)** | Key management and encryption             |
| **Load Balancers**                 | Traffic distribution with SSL termination |
| **VPN Gateway**                    | Remote access secure connectivity         |
| **Proxy Servers**                  | Content filtering and anonymization       |
| **Data Loss Prevention (DLP)**     | Data exfiltration prevention              |

# [Optional] Lab: Create a Security Architecture Diagram for Jackson Corporation

**Estimated time needed:** 30 minutes

---

## Overview

In this optional lab, you'll create a comprehensive security architecture diagram that visualizes your recommended solutions for Jackson Corporation.

---

## Prerequisites

Before starting this lab, ensure you have completed:

| Prerequisite | Lab                                                                                   |
| ------------ | ------------------------------------------------------------------------------------- |
| ☐           | **"Create Your First Security Architecture Diagram"** lab earlier in the course |
| ☐           | **"Final Project: Recommendations to Improve Network Security"**                |

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective                                                                          |
| - | ---------------------------------------------------------------------------------- |
| 1 | Apply security architecture principles to a real-world scenario                    |
| 2 | Translate security recommendations into a visual architecture diagram              |
| 3 | Design a multi-layered security infrastructure with appropriate zones and controls |
| 4 | Document security improvements in a clear, professional format                     |

---

## The Challenge

Jackson Corporation has accepted your security recommendations from the previous assignment. Now they need to see how these improvements will fit together in an actual architecture.

**Your task** is to create a security architecture diagram that shows:

| Requirement                            | Description                                           |
| -------------------------------------- | ----------------------------------------------------- |
| **Infrastructure Restructuring** | How the infrastructure will be restructured           |
| **Security Control Placement**   | Where new security controls will be placed            |
| **Traffic Flow**                 | How traffic will flow through the secured environment |
| **Asset Protection**             | Where critical assets will be protected               |

---

## Exercise 1: Plan Your Architecture

Before you start drawing, spend **10 minutes** planning your diagram on paper or in notes.

### Task A: Identify Your Security Zones

Based on the Jackson Corporation scenario, you'll need at least these zones:

**Hint:** What zones should Jackson Corporation have?

#### Recommended Security Zones

| Zone                               | Trust Level    | Description                                      | Color     |
| ---------------------------------- | -------------- | ------------------------------------------------ | --------- |
| **Internet Zone**            | Untrusted      | External users, customers, attackers             | 🔴 Red    |
| **DMZ (Demilitarized Zone)** | Semi-Trusted   | Public-facing services (Web Server)              | 🟡 Yellow |
| **Internal Zone**            | Trusted        | Application servers, databases, internal systems | 🟢 Green  |
| **Management Zone**          | Highly Trusted | SIEM, monitoring, admin workstations             | 🔵 Blue   |
| **Remote Access Zone**       | Conditional    | VPN users, remote employees                      | 🟣 Purple |

**Your task:** List out the security zones you'll include in your diagram.

```
Write your zones here:
1. _______________________________
2. _______________________________
3. _______________________________
4. _______________________________
5. _______________________________
```

---

### Task B: Map Components to Zones

For each of the **seven areas** from your recommendations, identify:

| Question                                                   | Action      |
| ---------------------------------------------------------- | ----------- |
| What new components or security controls need to be added? | List them   |
| Which security zone should each component be placed in?    | Assign zone |
| Why does that placement make sense?                        | Justify     |

**Hint:** Common components to include

#### Component-to-Zone Mapping Table

| Component                                | Zone                            | Justification                                  |
| ---------------------------------------- | ------------------------------- | ---------------------------------------------- |
| **External Firewall**              | Internet-DMZ Boundary           | First line of defense from internet threats    |
| **WAF (Web Application Firewall)** | DMZ (in front of Web Server)    | Protects web applications from OWASP Top 10    |
| **Web Server**                     | DMZ                             | Public-facing, accessible from internet        |
| **Internal Firewall**              | DMZ-Internal Boundary           | Controls traffic between DMZ and Internal      |
| **Application Server**             | Internal Zone                   | Business logic, not directly internet-facing   |
| **Database Server**                | Internal Zone (secure subnet)   | Sensitive data, maximum protection             |
| **IDS/IPS**                        | Spanning all zones              | Detects and prevents intrusions across network |
| **SIEM System**                    | Management Zone                 | Collects and analyzes logs from all zones      |
| **VPN Gateway**                    | DMZ or Internet Boundary        | Secure remote access for employees             |
| **Employee Workstations**          | Internal Zone                   | Day-to-day operations                          |
| **Backup Server**                  | Internal Zone (separate subnet) | Data recovery and business continuity          |
| **Monitoring Console**             | Management Zone                 | Centralized security monitoring                |

**Your task:** Create a simple table mapping each component to its appropriate zone.

```
Fill in your table:

| Component | Zone | Justification |
|-----------|------|---------------|
| 1. ________ | _______ | _________________ |
| 2. ________ | _______ | _________________ |
| 3. ________ | _______ | _________________ |
| 4. ________ | _______ | _________________ |
| 5. ________ | _______ | _________________ |
| 6. ________ | _______ | _________________ |
| 7. ________ | _______ | _________________ |
```

---

### Task C: Define Traffic Flows

Think about how different users and systems will communicate.

**Hint:** Key traffic flows to consider

| Flow # | Source              | Destination          | Protocol           | Path                                    |
| ------ | ------------------- | -------------------- | ------------------ | --------------------------------------- |
| 1      | Customer (Internet) | Web Server           | HTTPS              | Internet → Ext FW → WAF → Web Server |
| 2      | Web Server          | Application Server   | Internal API       | DMZ → Int FW → App Server             |
| 3      | Application Server  | Database Server      | SQL (encrypted)    | App Server → DB Server (Internal)      |
| 4      | Remote Employee     | VPN Gateway          | IPSec/SSL          | Internet → VPN Gateway                 |
| 5      | VPN Gateway         | Internal Resources   | Internal protocols | VPN → Int FW → Internal               |
| 6      | Internal Employee   | Application Server   | HTTPS/SSH          | Workstation → App Server               |
| 7      | All Systems         | SIEM                 | Syslog             | All components → SIEM                  |
| 8      | SIEM                | Monitoring Console   | Management         | SIEM → Admin Console                   |
| 9      | IDS/IPS             | Firewalls            | Alert/Block        | IDS/IPS → Firewall (automated)         |
| 10     | Backup Server       | Database/App Servers | Backup protocol    | Backup → Backup targets                |

**Your task:** List the major traffic flows you need to show in your diagram.

```
List your key traffic flows:
1. _________________________________
2. _________________________________
3. _________________________________
4. _________________________________
5. _________________________________
```

---

## Exercise 2: Create Your Security Architecture Diagram

Now it's time to create your diagram. Use any tool you're comfortable with:

| Tool                             | Type                | Access                     |
| -------------------------------- | ------------------- | -------------------------- |
| **draw.io (diagrams.net)** | Free, web-based     | https://www.draw.io        |
| **Lucidchart**             | Free tier available | https://www.lucidchart.com |
| **Microsoft Visio**        | Professional        | Paid license               |
| **PowerPoint**             | Basic shapes        | Microsoft Office           |
| **PlantUML**               | Code-based          | Free, open-source          |
| **Pen and paper**          | Hand-drawn          | Scan or photograph         |

---

### What to Include

Your diagram **MUST** include the following 6 elements:

#### 1. Security Zones (Clearly Labeled)

```
┌─────────────────────────────────────────────────────────────┐
│                    INTERNET ZONE (Untrusted)                 │
│                        🟡 YELLOW (if colored)                │
├─────────────────────────────────────────────────────────────┤
│                    DMZ (Semi-Trusted)                        │
│                        🟡 YELLOW (if colored)                │
├─────────────────────────────────────────────────────────────┤
│                    INTERNAL ZONE (Trusted)                   │
│                        🟢 GREEN (if colored)                 │
├─────────────────────────────────────────────────────────────┤
│                    MANAGEMENT ZONE (Secure)                  │
│                        🔵 BLUE (if colored)                  │
└─────────────────────────────────────────────────────────────┘
```

#### 2. Security Controls at Boundaries

| Control                     | Placement                     | Purpose                         |
| --------------------------- | ----------------------------- | ------------------------------- |
| **External Firewall** | Between Internet and DMZ      | Filter inbound/outbound traffic |
| **Internal Firewall** | Between DMZ and Internal Zone | Restrict internal access        |
| **VPN Gateway**       | Internet boundary             | Secure remote access            |
| **IDS/IPS**           | Spanning zones (inline/tap)   | Threat detection and prevention |
| **WAF**               | In front of Web Server (DMZ)  | OWASP protection                |

#### 3. Core Infrastructure Components

| Component              | Zone                             | Notes                           |
| ---------------------- | -------------------------------- | ------------------------------- |
| Web Server             | DMZ                              | Relocated from internal network |
| Application Servers    | Internal Zone                    | Business logic tier             |
| Database Servers       | Internal Zone (protected subnet) | Sensitive data                  |
| Monitoring/SIEM System | Management Zone                  | Log collection from all zones   |
| Employee Workstations  | Internal Zone                    | Day-to-day operations           |
| Backup Server          | Internal Zone (separate subnet)  | Disaster recovery               |

#### 4. Traffic Flows

| Element                         | Requirement                                           |
| ------------------------------- | ----------------------------------------------------- |
| **Arrows**                | Show how data moves between components                |
| **Protocol Labels**       | Indicate HTTPS, VPN, internal APIs, SQL, etc.         |
| **Encryption Indication** | Show where encryption is applied (lock icon or label) |

#### 5. Security Annotations

| Annotation Type                    | Example                                                    |
| ---------------------------------- | ---------------------------------------------------------- |
| **Control descriptions**     | "WAF blocks SQL injection and XSS attacks"                 |
| **OWASP protections**        | "Input validation, parameterized queries, output encoding" |
| **Data protection measures** | "Encryption at rest (AES-256)"                             |
| **Access control rules**     | "Least privilege access to database"                       |

#### 6. Legend

```
┌─────────────────────────────────────────────────────────────┐
│                         LEGEND                               │
├─────────────────────────────────────────────────────────────┤
│  Symbol        Meaning                                       │
│  ┌────┐        Server / Component                            │
│  └────┘                                                      │
│  ▭▭▭▭▭▭        Firewall                                     │
│  ══════        Encrypted Traffic                             │
│  ────►         Data Flow Direction                           │
│  🔒             Encryption Point                              │
│  🟢             Green = Internal Zone (Trusted)               │
│  🟡             Yellow = DMZ (Semi-Trusted)                   │
│  🔴             Red = Internet Zone (Untrusted)               │
│  🔵             Blue = Management Zone                        │
└─────────────────────────────────────────────────────────────┘
```

---

## Complete Diagram Example

Below is a comprehensive text-based security architecture diagram for Jackson Corporation:

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                         JACKSON CORPORATION - SECURITY ARCHITECTURE DIAGRAM                          │
│                                   Recommended Security Improvements                                   │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                   INTERNET ZONE (Untrusted) 🔴                                       │
│                                                                                                       │
│     ┌─────────────┐                    ┌─────────────┐                    ┌─────────────┐           │
│     │  👤 Public   │                    │  👤 Remote   │                    │  💀 Threat   │           │
│     │  Customers  │                    │  Employees   │                    │  Actors     │           │
│     └──────┬──────┘                    └──────┬──────┘                    └──────┬──────┘           │
│            │ HTTPS (443)                       │ VPN/IPSec                         │ Malicious        │
│            ▼                                   ▼                                   ▼                  │
└────────────┼───────────────────────────────────┼───────────────────────────────────┼──────────────────┘
             │                                   │                                   │
             ▼                                   │                                   │
┌────────────────────────────────────────────────┼───────────────────────────────────┼──────────────────┐
│                           EXTERNAL FIREWALL (Border Gateway)                        │                  │
│                    "Allow only HTTPS (443) and VPN (500/4500)"                      │                  │
│                    "Block all other inbound traffic"                                │                  │
└────────────────────────────────────────────────┼───────────────────────────────────┴──────────────────┘
             │                                   │
             │ HTTPS                             │ VPN
             ▼                                   ▼
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                       DMZ (Semi-Trusted) 🟡                                          │
│                                                                                                       │
│    ┌─────────────────────┐              ┌─────────────────────┐                                    │
│    │       🛡️ WAF         │              │    🔐 VPN Gateway    │                                    │
│    │  (Web Application    │              │  (SSL/IPSec Tunnel)  │                                    │
│    │     Firewall)        │              │                     │                                    │
│    │                     │              │ "Secure remote      │                                    │
│    │ "Blocks:            │              │  access for         │                                    │
│    │  - SQL Injection    │              │  employees"         │                                    │
│    │  - XSS              │              └──────────┬──────────┘                                    │
│    │  - CSRF             │                         │                                               │
│    │  - Path Traversal"  │                         │                                               │
│    └──────────┬──────────┘                         │                                               │
│               │                                     │                                               │
│               │ Filtered HTTPS                      │ Decrypted Tunnel                              │
│               ▼                                     ▼                                               │
│    ┌─────────────────────┐                         │                                               │
│    │     🖥️ Web Server    │                         │                                               │
│    │   (Public Website)   │                         │                                               │
│    │                     │                         │                                               │
│    │ "Relocated from     │                         │                                               │
│    │  Internal zone"     │                         │                                               │
│    │ "SSL/TLS certs"     │                         │                                               │
│    └──────────┬──────────┘                         │                                               │
│               │                                     │                                               │
│               │ Internal API Calls                  │                                               │
│               │ (JSON/REST)                         │                                               │
└───────────────┼─────────────────────────────────────┼───────────────────────────────────────────────┘
                │                                     │
                ▼                                     ▼
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                    INTERNAL FIREWALL                                                  │
│                    "Restrict access to authorized internal traffic only"                             │
│                    "Allow only from Web Server to App Server on specific ports"                      │
│                    "Allow VPN users to specific internal resources"                                  │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘
                │                                     │
                │                                     │
                ▼                                     ▼
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                              INTERNAL ZONE (Trusted) 🟢                                               │
│                                                                                                       │
│  ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│  │                           APPLICATION & DATA TIER                                            │   │
│  │                                                                                               │   │
│  │  ┌─────────────────────┐         ┌─────────────────────┐         ┌─────────────────────┐    │   │
│  │  │  🖥️ Application      │────────►│    🗄️ Database       │◄────────│  💾 Backup Server    │    │   │
│  │  │     Server           │  SQL     │      Server         │ Backup  │                     │    │   │
│  │  │                     │(Encrypted)│                     │         │  "Daily backups,    │    │   │
│  │  │ "Business logic,    │         │ "Customer data,     │         │   encrypted storage,│    │   │
│  │  │  input validation,  │         │  orders, PII,       │         │   offsite copy"     │    │   │
│  │  │  session mgmt"      │         │  encrypted at rest" │         └─────────────────────┘    │   │
│  │  └──────────┬──────────┘         └─────────────────────┘                                      │   │
│  │             │                                                                                  │   │
│  └─────────────┼─────────────────────────────────────────────────────────────────────────────────┘   │
│                │                                                                                       │
│  ┌─────────────┼─────────────────────────────────────────────────────────────────────────────────┐   │
│  │             │                    EMPLOYEE ZONE                                                 │   │
│  │             │                                                                                   │   │
│  │  ┌──────────┴──────────┐         ┌─────────────────────┐                                      │   │
│  │  │  👤 Internal         │         │  🖥️ Admin            │                                      │   │
│  │  │  Employees          │────────►│  Workstations       │                                      │   │
│  │  │                     │ Internal│                     │                                      │   │
│  │  │ "On-site staff"     │ Network │ "Endpoint security, │                                      │   │
│  │  └─────────────────────┘         │  EDR, patching"     │                                      │   │
│  │                                   └─────────────────────┘                                      │   │
│  └─────────────────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                                       │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘
                │
                │ All logs (Syslog, SNMP, API)
                ▼
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                              MANAGEMENT ZONE 🔵                                                       │
│                                                                                                       │
│  ┌─────────────────────┐         ┌─────────────────────┐         ┌─────────────────────┐           │
│  │     📊 SIEM System   │         │    🖥️ Monitoring     │         │    📈 IDS/IPS        │           │
│  │                     │         │      Console         │         │   Management        │           │
│  │ "Centralized log    │         │                     │         │                     │           │
│  │  collection,        │         │ "Security team      │         │ "Alert & policy     │           │
│  │  correlation,       │         │  dashboard,         │         │  management,        │           │
│  │  alerting"          │         │  incident response" │         │  signature updates" │           │
│  └─────────────────────┘         └─────────────────────┘         └─────────────────────┘           │
│                                                                                                       │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘

                                        ════════════════════════════
                                         SECURITY CONTROLS LEGEND
                                        ════════════════════════════

    SYMBOLS:                               ZONES (COLOR):
    ┌────┐  Server/Component               🔴  RED      = Internet Zone (Untrusted)
    └────┘                                  🟡  YELLOW   = DMZ (Semi-Trusted)
    ▭▭▭▭   Firewall                         🟢  GREEN    = Internal Zone (Trusted)
    🛡️     Security Control                 🔵  BLUE     = Management Zone
    🔐     Encryption/VPN
    📊     Monitoring/SIEM                  TRAFFIC:
                                             ──►  Standard Traffic
    PROTOCOLS:                               ═══►  Encrypted Traffic
    HTTPS (443)  = Web Traffic              - -►  Management Traffic
    SQL (1433/3306) = Database Queries
    Syslog (514) = Log Collection
```


![alt text](<../Screenshots/JACKSON CORPORATION - SECURITY ARCHITECTURE DIAGRAM.png>)

---


## Guiding Questions as You Draw

Ask yourself these questions to ensure your diagram is complete:

### About Zone Separation

| Question                                                          | Check | Correct Answer            |
| ----------------------------------------------------------------- | ----- | ------------------------- |
| Is the web server now in the DMZ instead of the internal network? | ☐    | YES                       |
| Is the database protected by at least two layers of firewalls?    | ☐    | YES (External + Internal) |
| Can external users reach the internal network directly?           | ☐    | NO (They shouldn't!)      |

### About Security Controls

| Question                                                             | Check | Correct Answer |
| -------------------------------------------------------------------- | ----- | -------------- |
| Does every zone boundary have a firewall or security control?        | ☐    | YES            |
| Is there a WAF protecting the web server from OWASP vulnerabilities? | ☐    | YES            |
| Is there an IDS/IPS monitoring for breaches?                         | ☐    | YES            |
| Is there a SIEM collecting logs from all systems?                    | ☐    | YES            |

### About Traffic Flow

| Question                                                                | Check | Correct Answer |
| ----------------------------------------------------------------------- | ----- | -------------- |
| Can you trace the path of a customer request from internet to database? | ☐    | YES            |
| Does traffic pass through security controls at each step?               | ☐    | YES            |
| Are all connections labeled with protocols and encryption status?       | ☐    | YES            |

---

## Exercise 3: Reflection Questions

After completing your diagram, answer these questions:

### Question 1

**How did visualizing the architecture help you understand the security improvements better than just writing recommendations?**

```
Your answer:
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
```

### Question 2

**Which security control do you think will have the biggest impact on Jackson Corporation's security posture, and why is it visible in your diagram?**

```
Your answer:
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
```

### Question 3

**If you were presenting this diagram to Jackson Corporation's executives (non-technical), what would you emphasize?**

```
Your answer:
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
```

### Question 4

**What trade-offs or challenges might Jackson Corporation face when implementing this architecture?**

```
Your answer:
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
```

---

## Diagram Submission Checklist

Before submitting your diagram, verify all items are complete:

| Requirement                         | Included | Notes                             |
| ----------------------------------- | -------- | --------------------------------- |
| **Security Zones**            | ☐       | Internet, DMZ, Internal (minimum) |
| Zones clearly labeled               | ☐       |                                   |
| Visual distinction between zones    | ☐       | Colors or patterns                |
| **Security Controls**         | ☐       |                                   |
| External Firewall                   | ☐       |                                   |
| Internal Firewall                   | ☐       |                                   |
| VPN Gateway                         | ☐       |                                   |
| IDS/IPS                             | ☐       |                                   |
| WAF                                 | ☐       |                                   |
| **Infrastructure Components** | ☐       |                                   |
| Web Server (in DMZ)                 | ☐       |                                   |
| Application Servers (Internal)      | ☐       |                                   |
| Database Servers (Internal)         | ☐       |                                   |
| SIEM/Monitoring                     | ☐       |                                   |
| Employee Workstations               | ☐       |                                   |
| Backup Server                       | ☐       |                                   |
| **Traffic Flows**             | ☐       |                                   |
| Arrows showing direction            | ☐       |                                   |
| Protocol labels (HTTPS, SQL, etc.)  | ☐       |                                   |
| Encryption indicators               | ☐       |                                   |
| **Annotations**               | ☐       |                                   |
| Control descriptions                | ☐       |                                   |
| OWASP/security notes                | ☐       |                                   |
| **Legend**                    | ☐       |                                   |
| Symbol explanations                 | ☐       |                                   |
| Color/zone meanings                 | ☐       |                                   |
| **Professional Quality**      | ☐       |                                   |
| Readable fonts                      | ☐       |                                   |
| Clean layout                        | ☐       |                                   |
| No spelling errors                  | ☐       |                                   |

---

## Common Mistakes to Avoid

| Mistake                           | Why It's Wrong                      | Correction                              |
| --------------------------------- | ----------------------------------- | --------------------------------------- |
| Web server still in Internal zone | Direct exposure of internal network | Move web server to DMZ                  |
| Missing WAF                       | No application-layer protection     | Add WAF between firewall and web server |
| Direct database access from DMZ   | Database exposed to web tier        | Route through application server        |
| No VPN for remote access          | Insecure remote connections         | Add VPN gateway                         |
| Missing SIEM                      | No centralized logging              | Add SIEM in management zone             |
| No encryption labels              | Unclear data protection             | Add 🔒 or "encrypted" labels            |
| No IDS/IPS                        | No threat detection                 | Add IDS/IPS spanning zones              |
| Missing backup server             | No disaster recovery                | Add backup server in Internal zone      |

---

## Grading Criteria (If Applicable)

| Criteria                       | Weight | Excellent (100%)                                                | Good (80%)                                 | Needs Work (60%)                     |
| ------------------------------ | ------ | --------------------------------------------------------------- | ------------------------------------------ | ------------------------------------ |
| **Zone Architecture**    | 25%    | All zones clearly defined, proper placement, visual distinction | Most zones defined, minor placement issues | Missing zones or incorrect placement |
| **Security Controls**    | 25%    | All required controls present, properly placed, well annotated  | Most controls present                      | Missing key controls                 |
| **Traffic Flows**        | 20%    | All flows shown, labeled, encrypted vs unencrypted clear        | Most flows shown                           | Missing critical flows               |
| **Documentation**        | 15%    | Comprehensive legend, clear annotations                         | Basic legend and notes                     | Missing legend or annotations        |
| **Professional Quality** | 15%    | Clean, readable, organized, no errors                           | Mostly clean                               | Hard to read or disorganized         |

---

## Summary

Congratulations! You've now applied your security architecture skills to a real-world scenario. You have:

| Achievement                                                            | Completed |
| ---------------------------------------------------------------------- | --------- |
| Translated written security recommendations into a visual architecture | ☐        |
| Documented how security controls work together                         | ☐        |
| Created a professional diagram for stakeholder communication           | ☐        |
| Applied defense-in-depth principles                                    | ☐        |
| Designed proper zone separation                                        | ☐        |
| Included all required security controls                                | ☐        |

---

## Additional Resources

| Resource                              | URL                                                           |
| ------------------------------------- | ------------------------------------------------------------- |
| **draw.io (diagrams.net)**      | https://www.draw.io                                           |
| **Lucidchart Templates**        | https://www.lucidchart.com/pages/templates                    |
| **AWS Security Architecture**   | https://aws.amazon.com/architecture/security/                 |
| **Azure Security Architecture** | https://docs.microsoft.com/en-us/azure/architecture/security/ |
| **NIST Security Architecture**  | https://csrc.nist.gov                                         |

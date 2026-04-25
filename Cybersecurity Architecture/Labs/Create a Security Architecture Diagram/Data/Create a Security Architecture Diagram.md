
# Create a Security Architecture Diagram

**Estimated time needed: 30 minutes**

---

## Introduction

Security architecture diagrams are visual representations that show how security controls, components, and data flows are organized to protect an organization's systems and information. As an architect stepping into cybersecurity, learning to create these diagrams is essential for communicating security designs to stakeholders, identifying vulnerabilities, and planning security implementations.

In this lab, you'll learn the fundamental elements of a security architecture diagram and create a simple diagram for a web application scenario.

---

## Objectives

After completing this lab, you will be able to:

- Identify the core components of a security architecture diagram
- Understand security zones and network segmentation concepts
- Place security controls appropriately in an architecture
- Create a basic security architecture diagram for a web application

---

## Exercise 1: Understanding security architecture components

In this exercise, you will learn about the essential building blocks that make up a security architecture diagram.

### What you'll need

- Any diagramming tool you're comfortable with (draw.io, Visio, Lucidchart, PowerPoint, or even pen and paper)
- The scenario described below

### The scenario

You're designing security for a simple e-commerce web application. The application has:

- A **public-facing website** where customers browse and shop
- A **database** that stores customer information and orders
- An **administrative portal** for employees to manage products and orders

### Identify the security zones

Before drawing anything, you need to understand **security zones**. These are logical groupings of systems based on their security requirements and trust levels.

For our scenario, identify these three zones:

| Zone | Trust Level | Description |
|------|-------------|-------------|
| **Internet Zone** | Untrusted | Where external users and potential threats exist |
| **DMZ Zone** | Semi-Trusted | Where public-facing services live, exposed to the internet but with some protection |
| **Internal Zone** | Trusted | Where sensitive systems like databases and internal applications reside |

> **Analogy:** Think of zones like rooms in a house with different security levels: your front porch (Internet), your living room (DMZ), and your bedroom with the safe (Internal).

### List the core components

Write down or mentally note these essential components you'll need in your diagram:

| Component | Purpose | Location |
|-----------|---------|----------|
| **Firewall** | Acts as a security guard, controlling what traffic can pass between zones | Zone boundaries |
| **Web Server** | Hosts the public website | DMZ |
| **Application Server** | Runs the business logic | Internal zone |
| **Database Server** | Stores sensitive data | Internal zone |
| **Users/Actors** | Customers (from Internet) and Administrators (from Internal network) | Respective zones |

> The web server needs to be accessible from the internet, but we want to keep the database as far from direct internet access as possible.

### Understand the traffic flow

Security architecture isn't just about placing components. It is about understanding **how data moves securely**:

1. Customers connect from the **Internet** → through **Firewall** → to **Web Server**
2. Web Server communicates → through **internal Firewall** → to **Application Server**
3. Application Server queries → through **internal controls** → to **Database Server**
4. Administrators connect from **Internal network** → through **Firewall** → to **Admin Portal**

> **Key Principle:** Notice how every connection crosses a security control. That's intentional. We never allow direct access across zones without security validation.

---

## Exercise 2: Creating your security architecture diagram

In this exercise, you will create your first security architecture diagram using the components and concepts from Exercise 1.

### Task A: Set up your diagram canvas

#### Create three horizontal zones

Open your diagramming tool and create **three distinct horizontal sections** (you can use rectangles or just horizontal lines to separate them):

- **Top section:** Label it "Internet Zone (Untrusted)"
- **Middle section:** Label it "DMZ (Demilitarized Zone)"
- **Bottom section:** Label it "Internal Zone (Trusted)"

> **Convention:** Using horizontal zones is common practice—the most trusted areas are typically shown at the bottom or center, with less trusted areas above or to the sides.

#### Add visual distinction

Make each zone visually distinct by using:

- Different background colors (light red for Internet, yellow for DMZ, green for Internal), or
- Different border styles if you prefer grayscale, or
- Simple shading/patterns

> This visual separation helps viewers quickly understand trust boundaries, even if they're not security experts.

### Task B: Place security components

#### Position the Firewalls (security boundaries)

Place firewall icons or rectangles at the boundaries between zones:

- **One between Internet Zone and DMZ** (label it "External Firewall")
- **One between DMZ and Internal Zone** (label it "Internal Firewall")

> **Analogy:** Think of firewalls as checkpoints. Just like airport security checks passengers before they enter secure areas, firewalls inspect network traffic before allowing it through.

#### Add the servers and components

Place these components in their appropriate zones:

| Zone | Component |
|------|-----------|
| **Internet Zone** | External Users/Customers |
| **DMZ** | Web Server (handles customer requests) |
| **Internal Zone** | Application Server (processes business logic), Database Server (stores customer data), Admin Users/IT Staff |

> **Goal:** Label each component clearly. The goal is to have clarity.

#### Draw the connection lines (traffic flows)

Connect your components with **arrows** to show how traffic flows:

| Connection | Path |
|------------|------|
| Customer traffic | External Users → External Firewall → Web Server |
| Web to App | Web Server → Internal Firewall → Application Server |
| App to DB | Application Server → Database Server |
| Admin access | Admin Users → Internal Firewall → Application Server |

#### Add protocol labels

Add labels to the arrows indicating the protocol or purpose:

- **"HTTPS (Port 443)"** for web traffic
- **"Internal API"** for application communication
- **"Database Queries"** for database access

### Task C: Add security controls and annotations

#### Document key security controls

Add text boxes or notes to highlight important security measures:

| Component | Annotation |
|-----------|------------|
| **External Firewall** | "Allows only HTTPS (443) inbound, blocks all other ports" |
| **Web Server** | "SSL/TLS encryption for all customer data" |
| **Internal Firewall** | "Restricts access to authorized internal traffic only" |
| **Database** | "Encrypted at rest, access logged" |

> These annotations transform your diagram from a simple network map into a **security architecture diagram**. They show *how* security is implemented, not just where components exist.

#### Add a legend (optional but recommended)

Create a small legend box explaining your symbols:

- What shape represents servers
- What shape represents firewalls
- What arrow styles represent (solid = encrypted, dashed = internal, etc.)
- What colors represent (if using colors)

### Review your diagram

Ask yourself these questions to verify your diagram is complete:

| Question | Check |
|----------|-------|
| Can I trace how a customer request flows from the internet to the database? | ☐ |
| Are there security controls (firewalls) at every zone boundary? | ☐ |
| Is sensitive data (database) furthest from untrusted zones? | ☐ |
| Would a non-security person understand the basic flow? | ☐ |
| Are all components labeled clearly? | ☐ |

> If you answered **"yes"** to these questions, congratulations! You've created a functional security architecture diagram.

### Sample architecture diagram

Here is a sample architecture diagram for your reference. Your architecture may contain more or less details based on your requirements. Use this sample architecture for reference and validate your work.

```

[Internet Zone (Untrusted)]
    External Users (Customers)
           │
           │ HTTPS (443)
           ▼
    ┌─────────────┐
    │   External  │
    │   Firewall  │
    └─────────────┘
           │
           │ HTTPS (443)
           ▼
[DMZ (Demilitarized Zone)]
    ┌─────────────┐
    │  Web Server │
    └─────────────┘
           │
           │ Internal API
           ▼
    ┌─────────────┐
    │   Internal  │
    │   Firewall  │
    └─────────────┘
           │
           │ Internal API
           ▼
[Internal Zone (Trusted)]
    ┌─────────────┐    ┌─────────────┐
    │ Application │───▶│  Database   │
    │   Server    │    │   Server    │
    └─────────────┘    └─────────────┘
           ▲
           │ Admin Access
           │
    ┌─────────────┐
    │  Admin Users│
    │ (IT Staff)  │
    └─────────────┘

```

![alt text](<../Screenshots/Sample Security architecture diagram.png>)

---

## Summary and next steps

You've now created a security architecture diagram! You learned about security zones, understood the principle of **defense in depth** (multiple layers of security), and documented how components interact across security boundaries.

### Key takeaways

| Concept | Description |
|---------|-------------|
| **Security architecture diagrams** | Communicate how security is designed into systems |
| **Security zones** | Separate systems by trust level (Internet, DMZ, Internal) |
| **Firewalls** | Act as gatekeepers between zones |
| **Traffic flow arrows** | Show how data moves through security controls |
| **Annotations** | Explain what security measures are in place |


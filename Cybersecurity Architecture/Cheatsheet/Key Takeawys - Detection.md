
# Key Takeaways: Detection

**Estimated time needed: 10 minutes**

Here are some key takeaways from the Detection video.

---

## The Big Picture

The **CIA Triad** represents the **What** of cybersecurity and shows what we are trying to do with cybersecurity.

**Security is about Prevention, Detection, and Response (S = P + D + R).** This represents the **How** of security.

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/pdr.png>)

---

## Prevention Domains

The different domains, including:
- Identity and Access Management (IAM)
- Endpoint security
- Application security
- Data security

...can be considered to be **prevention**, especially with the controls added.

---

## Detection

**Detection** is about:
- Receiving information from **all the domains**
- Feeding them into a **monitoring engine**
- Followed by **analyzing**, **reporting**, and **threat hunting**

> Detection and Response activities are performed by the **Security Operations Center (SOC)** team within an organization.

---

## Types of Detection Technologies

Technologies used to do this kind of work include:

| Technology | Description |
|------------|-------------|
| **SIEM** | Security Information and Event Management |
| **XDR** | Extended Detection and Response |

---

## Security Information and Event Management (SIEM)

### Need for SIEM

Having individual security consoles for each domain with specialized cybersecurity analysts for each domain can be:
- **Expensive**
- No way to get a single consistent view of all domains
- If an attacker breaks one system, there may be alarms on different domain consoles, resulting in several people trying to solve the same problem (inefficient)

> This is why the SIEM system came into existence.

### Functioning of SIEM Systems

It is necessary to **reduce the footprint** and provide a **single point** that gives you visibility of all the systems, gather all the information, and bring it up through analysis.

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/siem1.png>)

With SIEM, a new layer is added at the **top of all system consoles**.

### Steps in SIEM Processing

| Step | Description |
|------|-------------|
| **1. Collect** | Collect information (logs, alarms, events, flow data) from each domain's security consoles. Store in a database |
| **2. Apply Analytics** | Correlate the information and reduce it to a manageable subset |
| **3. Analyze** | Leverage rules (pre-set or customized) to set priorities (High, Medium, Low). Look for anomalies using AI/ML |
| **4. Review Reports** | Understand trends and answer questions about performance |

### User Behavior Analytics (UBA)

> The technology used to find and analyze anomalies is referred to as **User Behavior Analytics (UBA)** . Using Artificial Intelligence (AI), specifically Machine Learning (ML), to determine patterns is very useful.

### Key Questions Reports Help Answer

- Are we doing better now than earlier?
- Are we resolving faster?

---

## Extended Detection and Response (XDR)

### Evolution

| Technology | Description |
|------------|-------------|
| **EDR** (Endpoint Detection and Response) | Agent installed on each system for detection along with a certain level of response |
| **XDR** | Developed to read and hold all information from EDR or SIEM. Added federated search capability to look for specific indicators of compromise across all systems |

### Advantage of XDR

- No need for prefetched data in a database
- Get information **just in time**
- Federated search tells systems to fetch data on demand

---

## SIEM vs. XDR

| Aspect | SIEM | XDR |
|--------|------|-----|
| **Approach** | Bottom-up | Top-down |
| **Strength** | Good at triggering alarms | Good at investigation |

> **Important:** XDR plus SIEM can **complement each other** and make a stronger security response. They help monitor, analyze, and report on all activities happening in the environment.

---

## Threat Hunting

### Threat Hunting Timeline

```

Reconnaissance → Attack → MTTI → MTTC → Recovery

```

| Term | Description | Typical Duration |
|------|-------------|------------------|
| **Reconnaissance** | Attacker figures out weak points or vulnerabilities | Varies |
| **Mean Time to Identify (MTTI)** | Time for organization to identify that an attack has occurred | ~200 days |
| **Mean Time to Contain (MTTC)** | Time taken to fix and recover after attack is identified | Varies |

> It is important to **detect an attack as soon as possible**. This is done with **threat hunting**.

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/threathunt.png>)

### What is Threat Hunting?

Threat hunting is a **proactive initiative** for an organization. A cybersecurity analyst with experience and good instinct can help with a **hypothesis**, based on which we can determine the tools to detect threats or possible attacks, resulting in **early detection**.

---

## Summary

| Concept | Key Point |
|---------|-----------|
| **S = P + D + R** | Security = Prevention + Detection + Response |
| **SIEM** | Bottom-up, good at triggering alarms, uses collected data |
| **XDR** | Top-down, good at investigation, uses federated search |
| **SIEM + XDR** | Complementary, stronger security response |
| **Threat Hunting** | Proactive detection to reduce MTTI |


# Key Takeaways: Response

**Estimated time needed: 5 minutes**

Here are some key takeaways from the Response video.

---

## Attack to Recovery Timeline

### Threat Hunting Timeline

| Phase | Description | Typical Duration |
|-------|-------------|------------------|
| **Reconnaissance** | The attacker spends time figuring out your weak points or vulnerabilities | Varies |
| **Mean Time to Identify (MTTI)** | Time for the organization to identify that an attack has occurred | ~200 days |
| **Mean Time to Contain (MTTC)** | Time taken to fix and recover after the attack is identified | Varies |

> It is important to **move the awareness of an attack sooner**. This is done with **threat hunting**.

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/threathunt (1).png>)

---

## Responding to an Attack

> A good incident response can **cut the cost of a data breach**.

### Traditional Approach

- An attack is referred to as an **incident**
- The response is **Incident Response (IR)**
- An IR is typically resolved by an **expert manually**
- The expert will **triage** and **remediate** the incident

### Modern Approach

With a focus on shortening the **MTTC**, you can use **Security Orchestration, Automation, and Response (SOAR)** technology.

> The focus of SOAR is on **automating as much of the IR process as possible**.

---

## Cases

When an attack generates an alarm, the following process occurs:

| Step | Action |
|------|--------|
| 1 | SIEM or XDR system initiates a **case** in the case management component of the SOAR system |
| 2 | **Assign** the case to the appropriate cybersecurity analyst |
| 3 | The analyst **investigates** the incident |
| 4 | To ensure consistency and repeatability, the analyst uses the **dynamic playbook** |
| 5 | The dynamic playbook provides a set of steps based on an **algorithm** to enable investigation activities |
| 6 | Once the analyst determines the cause and remediation steps, **action** is applied to remediate the system |

---

## Automation and Orchestration

> While automation is a great practice, **not everything can be automated** because there are several **first-of-a-kind (FOAK)** events.

| Approach | Application |
|----------|-------------|
| **Automate** | Automate what you can |
| **Orchestrate** | Orchestrate wherever automation is not possible |

---

## Breach Notification

In case of a breach, you will need to:

1. **Determine** the data sets that are impacted
2. **Determine** the geographic location where the data was breached
3. **Inform** the regulatory body in that location

> **IMPORTANT:** You will pay a **penalty** if you do not notify the regulatory body in the location.

---

## Summary

| Concept | Key Point |
|---------|-----------|
| **MTTI** | Time to identify an attack (target for improvement via threat hunting) |
| **MTTC** | Time to contain and recover (target for improvement via SOAR) |
| **SOAR** | Security Orchestration, Automation, and Response – automates IR processes |
| **Dynamic Playbook** | Algorithm-based steps for consistent, repeatable investigations |
| **Breach Notification** | Must notify regulatory body based on data set and geography; penalties apply for non-compliance |
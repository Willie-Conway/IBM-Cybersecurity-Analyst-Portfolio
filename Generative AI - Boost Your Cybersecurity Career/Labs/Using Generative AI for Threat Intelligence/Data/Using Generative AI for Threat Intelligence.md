
![alt text](<../Screenshots/Claude_AI_logo.png>)

# Hands-on Lab: Using Generative AI for Threat Intelligence

**Estimated time:** 20 minutes

---

## Project Scenario

You are a **threat intelligence analyst** at a regional bank. Overnight, your SIEM generated multiple alerts involving the same external IP address: `203.0.113.42`.

- One alert shows brute-force login attempts against your public web server
- Ten separate alerts show unusual outbound traffic from internal user workstations to the same IP

Your SOC manager wants answers in 30 minutes: **Is this a coordinated attack? Are we breached? What is 203.0.113.42?**

Manual analysis of 11 log entries would take an hour. You'll use **Generative AI** to rapidly correlate events, identify patterns, and produce threat intelligence — cutting analysis time to under 10 minutes.

> *"Threat intelligence is about connecting dots. Generative AI helps you see the connections faster."*

---

## Introduction

In this lab, you will use a generative AI model (ChatGPT, Claude, IBM watsonx, etc.) to:

| Activity                     | Outcome                            |
| ---------------------------- | ---------------------------------- |
| Analyze network logs         | Identify patterns and correlations |
| Detect potential threats     | Recognize attack signatures        |
| Generate threat intelligence | Produce actionable insights        |

> *"Generative AI doesn't replace threat intelligence analysts. It makes them faster, allowing focus on strategic analysis instead of data sorting."*

---

## Learning Objectives

After completing this lab, you will be able to:

**Leverage generative AI to process threat intelligence data and identify potential threats.**

---

## The Scenario: Suspicious Activity at a Financial Institution

Your organization has observed two concerning patterns:

### Pattern A: Web Server Attack

| Field                 | Value                                                                            |
| --------------------- | -------------------------------------------------------------------------------- |
| **Date/Time**   | 2023-12-20 18:45:22                                                              |
| **Web Server**  | 192.168.1.102                                                                    |
| **Source IP**   | 203.0.113.42                                                                     |
| **Protocol**    | HTTP                                                                             |
| **Event Type**  | Suspicious Login Attempt                                                         |
| **Username**    | admin                                                                            |
| **Status**      | Failed                                                                           |
| **Description** | Multiple failed login attempts targeting 'admin' account — possible brute force |

### Pattern B: Unusual Outbound User Traffic (10 Users)

All traffic is going to the **same external IP: 203.0.113.42**

| #  | User           | Time     | Source IP     | Protocol | Port | Volume | Description             |
| -- | -------------- | -------- | ------------- | -------- | ---- | ------ | ----------------------- |
| 1  | john_doe       | 09:15:30 | 192.168.1.101 | TCP      | 443  | 500 MB | High outbound traffic   |
| 2  | alice_smith    | 09:20:45 | 192.168.1.102 | UDP      | 8080 | 700 MB | Unusually high UDP      |
| 3  | robert_jones   | 09:25:10 | 192.168.1.103 | TCP      | 22   | 1.2 GB | Elevated SSH traffic    |
| 4  | emily_wang     | 09:30:22 | 192.168.1.104 | ICMP     | N/A  | 800 MB | Unusual ICMP traffic    |
| 5  | michael_davis  | 09:35:40 | 192.168.1.105 | UDP      | 53   | 600 MB | High DNS traffic        |
| 6  | sarah_miller   | 09:40:55 | 192.168.1.106 | TCP      | 80   | 900 MB | Elevated web traffic    |
| 7  | kevin_wilson   | 09:45:12 | 192.168.1.107 | UDP      | 123  | 1.5 GB | High NTP traffic        |
| 8  | lisa_jackson   | 09:50:30 | 192.168.1.108 | TCP      | 8080 | 1.8 GB | Significant web traffic |
| 9  | mark_taylor    | 09:55:45 | 192.168.1.109 | UDP      | 514  | 1.2 GB | High syslog traffic     |
| 10 | jessica_martin | 10:00:00 | 192.168.1.110 | TCP      | 443  | 2.5 GB | Extremely high HTTPS    |

> **Note:** These examples are generic. Real investigations require correlation with additional logs and context.

---

## Exercise: Threat Intelligence and Potential Threat Identification

### Step 1: Prepare Your Prompt

Copy and paste this prompt into ChatGPT (or your chosen AI platform):

```
You are a senior threat intelligence analyst. Analyze the following network logs and identify potential threats, patterns, and correlations.

Specifically:
1. Correlate the web server attack with the user traffic
2. Identify the external IP address involved
3. Determine the likely attack type or campaign
4. Assess the severity (Critical/High/Medium/Low)
5. Provide recommended immediate actions

Here are the logs:
```

### Step 2: Add the Log Data

Copy and paste all 11 log entries after your prompt:

```
--- WEB SERVER LOG ---
Date/Time: 2023-12-20 18:45:22
Web Server: 192.168.1.102
Source IP: 203.0.113.42
Protocol: HTTP
Event Type: Suspicious Login Attempt
Username: admin
Status: Failed
Description: Multiple failed login attempts from external IP 203.0.113.42 to web server 192.168.1.102. The username 'admin' was targeted — possible brute force.

--- USER TRAFFIC LOGS (10 entries) ---
1. Date/Time: 2023-12-20 09:15:30 | User: john_doe | Source IP: 192.168.1.101 | Destination IP: 203.0.113.42 | Protocol: TCP | Port: 443 | Traffic Volume: 500 MB | Description: High outbound traffic observed from user john_doe's system to IP 203.0.113.42 on port 443.

2. Date/Time: 2023-12-20 09:20:45 | User: alice_smith | Source IP: 192.168.1.102 | Destination IP: 203.0.113.42 | Protocol: UDP | Port: 8080 | Traffic Volume: 700 MB | Description: Unusually high UDP traffic from user alice_smith's system to IP 203.0.113.42 on port 8080.

3. Date/Time: 2023-12-20 09:25:10 | User: robert_jones | Source IP: 192.168.1.103 | Destination IP: 203.0.113.42 | Protocol: TCP | Port: 22 | Traffic Volume: 1.2 GB | Description: Elevated outbound TCP traffic from user robert_jones's system to IP 203.0.113.42 on port 22.

4. Date/Time: 2023-12-20 09:30:22 | User: emily_wang | Source IP: 192.168.1.104 | Destination IP: 203.0.113.42 | Protocol: ICMP | Traffic Volume: 800 MB | Description: Unusual ICMP traffic observed from user emily_wang's system to IP 203.0.113.42.

5. Date/Time: 2023-12-20 09:35:40 | User: michael_davis | Source IP: 192.168.1.105 | Destination IP: 203.0.113.42 | Protocol: UDP | Port: 53 | Traffic Volume: 600 MB | Description: High outbound UDP traffic from user michael_davis's system to IP 203.0.113.42 on port 53.

6. Date/Time: 2023-12-20 09:40:55 | User: sarah_miller | Source IP: 192.168.1.106 | Destination IP: 203.0.113.42 | Protocol: TCP | Port: 80 | Traffic Volume: 900 MB | Description: Elevated outbound TCP traffic from user sarah_miller's system to IP 203.0.113.42 on port 80.

7. Date/Time: 2023-12-20 09:45:12 | User: kevin_wilson | Source IP: 192.168.1.107 | Destination IP: 203.0.113.42 | Protocol: UDP | Port: 123 | Traffic Volume: 1.5 GB | Description: Abnormally high UDP traffic from user kevin_wilson's system to IP 203.0.113.42 on port 123.

8. Date/Time: 2023-12-20 09:50:30 | User: lisa_jackson | Source IP: 192.168.1.108 | Destination IP: 203.0.113.42 | Protocol: TCP | Port: 8080 | Traffic Volume: 1.8 GB | Description: Significantly elevated outbound TCP traffic from user lisa_jackson's system to IP 203.0.113.42 on port 8080.

9. Date/Time: 2023-12-20 09:55:45 | User: mark_taylor | Source IP: 192.168.1.109 | Destination IP: 203.0.113.42 | Protocol: UDP | Port: 514 | Traffic Volume: 1.2 GB | Description: Unusually high UDP traffic from user mark_taylor's system to IP 203.0.113.42 on port 514.

10. Date/Time: 2023-12-20 10:00:00 | User: jessica_martin | Source IP: 192.168.1.110 | Destination IP: 203.0.113.42 | Protocol: TCP | Port: 443 | Traffic Volume: 2.5 GB | Description: Extremely high outbound TCP traffic from user jessica_martin's system to IP 203.0.113.42 on port 443.
```

### Step 3: Review the AI's Threat Analysis

The AI should produce an analysis similar to:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    AI THREAT INTELLIGENCE ANALYSIS                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   SEVERITY: CRITICAL                                                         │
│                                                                              │
│   KEY FINDINGS:                                                              │
│                                                                              │
│   1. EXTERNAL IP: 203.0.113.42 is the common threat actor C2 server         │
│      • Targeted web server brute force at 18:45:22                          │
│      • Received outbound data from 10 internal users (09:15-10:00)          │
│      • Multiple protocols (TCP, UDP, ICMP) suggests data exfiltration       │
│                                                                              │
│   2. ATTACK PATTERN: Likely Data Exfiltration Campaign                       │
│      • Initial access: Brute force on 'admin' account (web server)          │
│      • Lateral movement: Attacker pivoted to internal network               │
│      • Data staging: 10 workstations sending data to external IP            │
│      • Exfiltration: 10+ GB total data transferred                          │
│                                                                              │
│   3. TIMELINE ANOMALY                                                        │
│      • User traffic occurred in the MORNING (09:15-10:00)                   │
│      • Web attack occurred in the EVENING (18:45)                           │
│      • Possible explanation: Attacker breached web server, installed        │
│        malware, malware activated on workstations next morning              │
│                                                                              │
│   4. SUSPICIOUS TRAFFIC PATTERNS                                             │
│      • Port 22 (SSH): 1.2 GB - unusual for standard users                   │
│      • Port 53 (DNS): 600 MB - potential DNS tunneling                      │
│      • ICMP: 800 MB - data exfiltration via ping packets                    │
│      • Port 123 (NTP): 1.5 GB - timing channel or covert channel           │
│                                                                              │
│   5. RECOMMENDATIONS                                                         │
│      IMMEDIATE:                                                              │
│      • Block 203.0.113.42 at firewall                                       │
│      • Isolate affected workstations (10 users)                             │
│      • Force password reset for all affected accounts                       │
│      • Initiate IR plan                                                     │
│                                                                              │
│      INVESTIGATION:                                                          │
│      • Pull full PCAP for 203.0.113.42 traffic                              │
│      • Analyze web server logs for compromise timeframe                     │
│      • Run memory forensics on affected workstations                        │
│      • Check for persistence mechanisms                                     │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Step 4: Refine the Analysis (Optional)

Ask the AI follow-up questions to dig deeper:

```
What MITRE ATT&CK techniques are likely being used here?

What additional data would help confirm this is data exfiltration vs. something else?

Write a one-paragraph executive summary for my CISO.
```

---

## Investigation Questions

Answer these based on your AI-generated analysis:

| # | Question                                                                    | Your Answer |
| - | --------------------------------------------------------------------------- | ----------- |
| 1 | What external IP address appears in ALL the suspicious logs?                |             |
| 2 | What username was targeted in the web server brute force attempt?           |             |
| 3 | How many internal users showed unusual outbound traffic to the external IP? |             |
| 4 | Which user had the highest traffic volume (2.5 GB)?                         |             |
| 5 | What protocol was used for the suspicious traffic on port 53?               |             |
| 6 | Why is ICMP traffic (800 MB) considered suspicious?                         |             |
| 7 | What is the likely overall attack pattern based on the AI's analysis?       |             |

---

## Threat Intelligence Workflow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    AI-ASSISTED THREAT INTELLIGENCE                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   STEP 1: DATA COLLECTION                                                    │
│   └── SIEM logs, firewall logs, endpoint logs, threat feeds                 │
│                    │                                                         │
│                    ▼                                                         │
│   STEP 2: AI PATTERN RECOGNITION                                             │
│   └── Identify correlations across disparate data sources                   │
│                    │                                                         │
│                    ▼                                                         │
│   STEP 3: CONTEXT ENRICHMENT                                                 │
│   └── AI checks external threat intel, known bad IPs, malware signatures    │
│                    │                                                         │
│                    ▼                                                         │
│   STEP 4: PRIORITIZATION                                                     │
│   └── Assign severity, recommend response actions                           │
│                    │                                                         │
│                    ▼                                                         │
│   STEP 5: HUMAN ANALYSIS & DECISION                                          │
│   └── Analyst validates, refines, and actions                               │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Key Takeaways

| Concept                       | Description                                                       |
| ----------------------------- | ----------------------------------------------------------------- |
| **Pattern Recognition** | AI identifies correlations humans might miss (common external IP) |
| **Contextual Analysis** | AI connects web server attack to internal user traffic            |
| **Threat Intelligence** | AI provides actionable insights, not just raw data                |
| **Speed**               | Minutes vs. hours for manual correlation                          |
| **Force Multiplier**    | One analyst + AI = team of analysts                               |

---

## Test Your Knowledge

**Q1:** What made the traffic to port 53 (DNS) suspicious?

```
Your answer:
_________________________________________________________________
```

**Q2:** Why is the timing discrepancy between the web attack (6:45 PM) and user traffic (9:15 AM - 10:00 AM) significant?

```
Your answer:
_________________________________________________________________
```

**Q3:** What additional data would you request to confirm this is data exfiltration?

```
Your answer:
_________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                                                                                                |
| -- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1  | DNS traffic normally uses very little bandwidth (KB range); 600 MB is massive and indicates DNS tunneling for data exfiltration                       |
| 2  | Suggests the web server compromise happened first (evening), then malware activated on workstations the next morning — typical staged attack pattern |
| 3  | Full packet captures (PCAPs) to see WHAT data was sent, EDR logs to see process lineage, memory forensics to find malware                             |

---

## Lab Completion Checklist

| Task                                    | Completed |
| --------------------------------------- | --------- |
| **Step 1-2: Setup**               | ☐        |
| Prepared prompt for AI                  | ☐        |
| Copied all 11 log entries               | ☐        |
| **Step 3: Analysis**              | ☐        |
| AI generated threat analysis            | ☐        |
| Reviewed correlations and severity      | ☐        |
| **Step 4: Refinement (Optional)** | ☐        |
| Asked follow-up questions               | ☐        |
| Generated executive summary             | ☐        |
| **Questions**                     | ☐        |
| Answered all 7 investigation questions  | ☐        |

---

## Screenshot Checklist

| Screenshot                  | Description                              |
| --------------------------- | ---------------------------------------- |
| `ai_threat_analysis.png`  | AI's full threat intelligence response   |
| `correlation_finding.png` | AI identifying 203.0.113.42 as common IP |
| `executive_summary.png`   | AI-generated summary for CISO (optional) |
| `answers.png`             | Your completed answers                   |

---

## Summary

In this lab, you have:

| Activity                                                 | Completed |
| -------------------------------------------------------- | --------- |
| Used generative AI to analyze network and security logs  | ☐        |
| Correlated web server attacks with internal user traffic | ☐        |
| Identified a common external threat IP address           | ☐        |
| Generated actionable threat intelligence                 | ☐        |
| Learned how AI accelerates threat analysis               | ☐        |

These skills are essential for:

- Threat intelligence analysts processing large data volumes
- SOC teams triaging complex multi-source alerts
- Incident responders identifying attack patterns
- Organizations scaling limited analyst resources

---

## Additional Resources

| Resource                   | URL                                            |
| -------------------------- | ---------------------------------------------- |
| MITRE ATT&CK Framework     | https://attack.mitre.org                       |
| CISA Threat Intelligence   | https://www.cisa.gov/cyber-threat-intelligence |
| VirusTotal (IP reputation) | https://www.virustotal.com                     |

---

## Congratulations!

You have successfully completed the **Using Generative AI for Threat Intelligence** lab.

> *"Threat intelligence is about connecting dots across time, systems, and data sources. Generative AI helps you see the connections before the attacker achieves their objective."*

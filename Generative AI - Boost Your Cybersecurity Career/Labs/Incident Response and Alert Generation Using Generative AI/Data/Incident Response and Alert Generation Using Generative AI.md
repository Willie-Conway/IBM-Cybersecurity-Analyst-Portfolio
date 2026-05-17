![alt text](<../Screenshots/Claude_AI_logo.png>)


# Hands-on Lab: Incident Response and Alert Generation Using Generative AI

**Estimated time:** 25 minutes

---

## Project Scenario

You are a **security analyst** at a regional bank. Your SIEM just generated 5 alerts in the last 10 minutes. Your SOC team is small — only 3 analysts covering 24/7 operations. You need to quickly determine which alerts are critical and which can wait.

Traditional triage would take 30-45 minutes of manual analysis. You'll use **Generative AI** to prioritize alerts and draft communication to system administrators — reducing triage time to under 5 minutes.

> *"In incident response, minutes matter. Generative AI helps you focus on the real threats, not the noise."*

---

## Introduction

In this lab, you will use a generative AI model (IBM watsonx, ChatGPT, Claude, etc.) to:

| Task                        | Outcome                                                       |
| --------------------------- | ------------------------------------------------------------- |
| **Prioritize alerts** | Assign High/Medium/Low severity to 5 different attack alerts  |
| **Generate email**    | Create professional communication for high-priority incidents |

> *"Automated triage doesn't replace analyst judgment — it augments it. AI sorts; you decide."*

---

## Learning Objective

After completing this lab, you will be able to:

**Leverage generative AI to aid in automated triage of security incidents**

---

## The Alerts You Received

You are a security analyst at a bank. Your SIEM just generated these 5 alerts:

| # | Alert Type                                 | Message                                                                                                                                                                    |
| - | ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 | **SQL Injection**                    | SQL injection attempt detected in web server logs. Suspicious input:`'; DROP TABLE Users--`                                                                              |
| 2 | **Zero-Day Exploit**                 | Unusual system behavior detected on Server X. Possible zero-day exploit. Investigate abnormal code execution patterns.                                                     |
| 3 | **Man-in-the-Middle (MitM)**         | Anomalous SSL/TLS certificate changes during secure communication. Potential Man-in-the-Middle attack detected. Investigate immediately.                                   |
| 4 | **Advanced Persistent Threat (APT)** | Persistent unauthorized access attempts across multiple systems. Possible APT campaign detected. Implement enhanced monitoring and investigate further.                    |
| 5 | **Cross-Site Scripting (XSS)**       | Client-side script injection detected in web application logs. Malicious script found in user input. Possible Cross-Site Scripting (XSS) attack. Investigate and mitigate. |

> **Note:** These examples are generic. Real investigations require correlation with other logs and additional context.

---

## Exercise 1: Log Alert Prioritization

### Step 1: Prepare Your Prompt

Copy and paste this prompt into your generative AI tool:

```
You are a senior security analyst. Assign priority levels (High, Medium, or Low) to the following security alerts based on:
- Potential business impact
- Data sensitivity (customer financial data at a bank)
- Likelihood of active compromise
- Urgency of response required

For each alert, provide:
1. Priority (High/Medium/Low)
2. Brief justification (1 sentence)
3. Recommended initial response action
```

### Step 2: Add the Alerts

Copy and paste the 5 alerts after your prompt (or take a screenshot and upload it if your AI supports images).

### Step 3: Review the AI's Prioritization

Your AI should produce output similar to:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    ALERT PRIORITIZATION RESULTS                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   HIGH PRIORITY (Immediate action required)                                 │
│   ──────────────────────────────────────────────────────────────────────── │
│                                                                              │
│   1. Zero-Day Exploit (Alert #2)                                            │
│      Justification: Unknown vulnerability with active exploitation          │
│      Response: Isolate Server X immediately, capture memory, begin analysis │
│                                                                              │
│   2. APT Campaign (Alert #4)                                                │
│      Justification: Persistent access across multiple systems indicates     │
│      sophisticated, targeted attack potentially seeking customer data       │
│      Response: Initiate incident response plan, contain affected systems,   │
│      notify IR team lead                                                    │
│                                                                              │
│   ──────────────────────────────────────────────────────────────────────── │
│                                                                              │
│   MEDIUM PRIORITY (Address within 1-2 hours)                                │
│   ──────────────────────────────────────────────────────────────────────── │
│                                                                              │
│   3. MitM Attack (Alert #3)                                                 │
│      Justification: Certificate anomalies could indicate interception of    │
│      customer banking sessions                                              │
│      Response: Revoke suspicious certificates, review encrypted traffic     │
│                                                                              │
│   4. SQL Injection (Alert #1)                                               │
│      Justification: Attempt to drop tables indicates active testing         │
│      Response: Review WAF logs, patch application, implement input         │
│      validation                                                             │
│                                                                              │
│   ──────────────────────────────────────────────────────────────────────── │
│                                                                              │
│   LOW PRIORITY (Address within 24 hours)                                    │
│   ──────────────────────────────────────────────────────────────────────── │
│                                                                              │
│   5. XSS Attack (Alert #5)                                                  │
│      Justification: Client-side injection less likely to directly expose    │
│      backend customer data                                                  │
│      Response: Implement output encoding, review web application firewall   │
│      rules                                                                  │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Step 4: Challenge the AI (Optional)

Try refining the prioritization with this follow-up prompt:

```
The bank processes credit card applications through the web server with SQL injection alert (#1). Does this change the priority? Re-evaluate.
```

---

## Exercise 2: Automatic Email Communication for High-Priority Alerts

After prioritization, you need to notify the system administrator about high-priority alerts.

### Step 1: Prepare the Email Generation Prompt

Copy and paste this prompt:

```
Generate a professional email to the System Administrator about the HIGH priority alerts identified in the previous analysis.

The email must include:
- Clear subject line indicating urgency
- List of high-priority alerts with brief descriptions
- Recommended immediate actions for each
- Escalation path if not resolved within 1 hour
- Request for confirmation of receipt
```

### Step 2: Review the AI-Generated Email

Your AI should produce an email similar to:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    EMAIL TO SYSTEM ADMINISTRATOR                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   To: system-admin@bank.com                                                 │
│   From: security-soc@bank.com                                               │
│   Subject: URGENT: High Priority Security Alerts - Action Required          │
│   Priority: High                                                            │
│                                                                              │
│   ---                                                                        │
│                                                                              │
│   System Administrator,                                                     │
│                                                                              │
│   The SOC has identified TWO high-priority security alerts requiring your   │
│   immediate attention:                                                      │
│                                                                              │
│   **HIGH PRIORITY ALERTS**                                                  │
│                                                                              │
│   1. ZERO-DAY EXPLOIT - Server X                                            │
│      • Unusual system behavior detected                                      │
│      • Possible unknown vulnerability being exploited                        │
│      • ACTION: Isolate Server X from network IMMEDIATELY                     │
│                                                                              │
│   2. APT CAMPAIGN - Multiple Systems                                         │
│      • Persistent unauthorized access attempts across network                │
│      • Indicators suggest targeted campaign                                  │
│      • ACTION: Begin enhanced monitoring, preserve logs                      │
│                                                                              │
│   **IMMEDIATE ACTIONS REQUIRED (Next 30 minutes)**                          │
│   ☐ Isolate Server X from production network                                │
│   ☐ Capture memory and network logs from affected systems                   │
│   ☐ Block suspicious outbound connections at firewall                       │
│   ☐ Notify Incident Response Team Lead                                       │
│                                                                              │
│   **ESCALATION**                                                             │
│   If these actions are not completed within 1 hour, this alert will be      │
│   escalated to the CISO and IT Director.                                    │
│                                                                              │
│   Please reply to this email confirming receipt and when isolation is       │
│   complete.                                                                 │
│                                                                              │
│   ---                                                                        │
│   Security Operations Center                                                 │
│   [Bank Name]                                                               │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Step 3: Customize the Email (Optional)

Ask the AI to adjust the email for different scenarios:

```
Rewrite the email for:
- A small bank with no 24/7 admin (on-call only)
- Add specific commands to isolate Server X
- Include regulatory reporting requirement (30 days for data breach notification)
```

---

## Investigation Questions

Answer these using your AI-generated outputs:

| # | Question                                                                 | Your Answer |
| - | ------------------------------------------------------------------------ | ----------- |
| 1 | Which alert did the AI classify as highest priority and why?             |             |
| 2 | What justification did the AI give for classifying APT as high priority? |             |
| 3 | What was the lowest priority alert and why?                              |             |
| 4 | What immediate action did the AI recommend for the zero-day alert?       |             |
| 5 | What information did the AI include in the email subject line?           |             |
| 6 | Why might SQL injection be lower priority than APT in this scenario?     |             |
| 7 | What escalation path did the AI's email include?                         |             |

---

## Advanced Challenge (Optional)

### Step 5: Create a Triage Dashboard Summary

Ask the AI:

```
Create a one-paragraph summary of all 5 alerts for the SOC shift lead, including:
- Number of alerts by priority (High/Medium/Low)
- Top 2 threats to focus on
- Estimated time to resolve each
- Any alerts that can be ignored/deferred
```

### Step 6: Generate Playbook Steps for Top Alert

Ask the AI:

```
For the highest priority alert (zero-day), write a 5-step immediate response procedure that a junior analyst could follow.
```

---

## Lab Completion Checklist

| Task                                        | Completed |
| ------------------------------------------- | --------- |
| **Exercise 1: Prioritization**        | ☐        |
| Generated priority assignments for 5 alerts | ☐        |
| Reviewed justifications and recommendations | ☐        |
| **Exercise 2: Email Generation**      | ☐        |
| Generated professional alert email          | ☐        |
| Reviewed email for clarity and action items | ☐        |
| **Questions**                         | ☐        |
| Answered all 7 investigation questions      | ☐        |
| **Advanced (Optional)**               | ☐        |
| Created triage summary                      | ☐        |
| Generated playbook steps                    | ☐        |

---

## Screenshot Checklist

| Screenshot               | Description                                  |
| ------------------------ | -------------------------------------------- |
| `alert_priorities.png` | AI output showing High/Medium/Low priorities |
| `email_generated.png`  | AI-generated email to system administrator   |
| `customized_email.png` | Your customized email (optional)             |
| `answers.png`          | Your completed answers                       |

---

## Key Takeaways

| Concept                           | Description                                                                        |
| --------------------------------- | ---------------------------------------------------------------------------------- |
| **Automated Triage**        | AI can quickly sort alerts by severity, saving analyst time                        |
| **Context Matters**         | Same alert type may have different priority based on environment (bank vs. retail) |
| **AI + Human Judgment**     | AI suggests; analyst decides based on organizational context                       |
| **Communication Templates** | AI generates professional emails, ensuring consistency                             |
| **Continuous Improvement**  | Refine prompts to get better prioritization                                        |

---

## Test Your Knowledge

**Q1:** Why is automated triage critical for a small SOC team?

```
Your answer:
_________________________________________________________________
```

**Q2:** What factor might change a SQL injection alert from Medium to High priority?

```
Your answer:
_________________________________________________________________
```

**Q3:** Why should AI-generated emails be reviewed before sending?

```
Your answer:
_________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                                                                 |
| -- | ---------------------------------------------------------------------------------------------------------------------- |
| 1  | Small teams lack bandwidth to manually triage every alert; automation helps them focus on critical threats first       |
| 2  | If the vulnerable web application processes sensitive data (e.g., credit card applications, PII) or is publicly facing |
| 3  | AI may include incorrect details, wrong urgency level, or inappropriate language for the organizational culture        |

---

## Summary

In this lab, you have:

| Activity                                                | Completed |
| ------------------------------------------------------- | --------- |
| Used generative AI to prioritize 5 security alerts      | ☐        |
| Assigned High/Medium/Low priorities with justifications | ☐        |
| Generated a professional email for high-priority alerts | ☐        |
| Learned how AI accelerates incident triage workflows    | ☐        |

These skills are essential for:

- SOC analysts managing high-volume alert queues
- Small security teams needing force multiplication
- Organizations adopting AI-assisted security operations
- Incident responders who need to communicate clearly under pressure

---

## Additional Resources

| Resource                                       | URL                                             |
| ---------------------------------------------- | ----------------------------------------------- |
| NIST Guide to Cyber Threat Information Sharing | https://www.nist.gov/cyberframework             |
| SANS Alert Triage Guide                        | https://www.sans.org/white-papers/415/          |
| CISA Incident Response Training                | https://www.cisa.gov/incident-response-training |

---

## Congratulations!

You have successfully completed the **Incident Response and Alert Generation Using Generative AI** lab.

> *"AI won't replace the SOC analyst. But analysts who use AI for triage will outperform those who don't. You just learned how to work smarter, not harder."*

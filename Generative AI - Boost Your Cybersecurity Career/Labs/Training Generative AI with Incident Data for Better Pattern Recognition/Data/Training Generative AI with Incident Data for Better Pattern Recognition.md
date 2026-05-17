![alt text](<../Screenshots/Claude_AI_logo.png>)

# Hands-on Lab: Training Generative AI with Incident Data for Better Pattern Recognition

**Estimated time:** 30 minutes

---

## Project Scenario

You are a **security analytics engineer** at a university that recently deployed a generative AI assistant to help your small SOC team triage network alerts.

During a pilot test, the AI incorrectly flagged legitimate online exam traffic as a DDoS attack. This created unnecessary panic, wasted 4 analyst-hours of investigation, and nearly caused the university to block access to a critical exam server during final exams.

Your task: **Train the AI to understand your organization's specific context** so it stops flagging normal behavior as malicious.

> *"Generative AI is powerful out of the box — but it doesn't know YOUR network. Training it on your context is the difference between noise and insight."*

---

## Introduction

In this lab, you will:

| Activity                                | Outcome                                        |
| --------------------------------------- | ---------------------------------------------- |
| Analyze a network log with untrained AI | See how AI misinterprets normal traffic        |
| Train the AI with specific context      | Correct the AI's misunderstanding              |
| Observe improved pattern recognition    | Learn how to customize AI for your environment |

> *"Out-of-the-box AI sees patterns. Trained AI sees YOUR patterns."*

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective                                                  |
| - | ---------------------------------------------------------- |
| 1 | Leverage generative AI models for specific requirements    |
| 2 | Enhance pattern recognition through targeted training      |
| 3 | Reduce false positives by providing organizational context |

---

## The Problem: AI Doesn't Know Your Network

| What AI Thinks                | Reality            |
| ----------------------------- | ------------------ |
| Many requests to one IP       | DDoS attack        |
| Traffic from multiple sources | Botnet activity    |
| Unusual traffic patterns      | Malicious behavior |

| What's Actually Happening | The Context AI Misses                  |
| ------------------------- | -------------------------------------- |
| Online exam server        | 500 students connecting simultaneously |
| API gateway               | Normal aggregated traffic              |
| Backup server             | Scheduled high-bandwidth transfers     |

> *"AI sees the 'what' but not the 'why.' You have to teach it the 'why.'"*

---

## Exercise: Train a Generative AI Model for Specific Pattern Analysis

### The Scenario

You receive a network activity log. After analyzing it with a generative AI platform (ChatGPT, Claude, etc.), it incorrectly flags IP address `186.20.20.27` as a victim of a DDoS attack.

**The reality:** This IP is hosting an online exam. Multiple requests from various IP addresses are standard and expected — NOT a DDoS attack.

Your mission: **Train the AI to understand this context.**

> **Note:** You will need a ChatGPT account (free tier works) or access to another generative AI platform for this exercise.

---

### Step 1: Review the Network Log

Here is the sample network log (also downloadable from your lab materials):

```
Timestamp: 2024-01-16 01:00:00
Source IP: 192.168.45.10
Destination IP: 186.20.20.27
Protocol: TCP
Port: 80
Description: Normal inbound web traffic from a local network source to the server. No signs of unusual activity.

Timestamp: 2024-01-16 02:15:20
Source IP: 10.0.0.5
Destination IP: 186.20.20.27
Protocol: UDP
Port: 53
Description: Routine DNS request from an internal source to the server. Expected behavior with no signs of malicious intent.

Timestamp: 2024-01-16 03:30:45
Source IP: 172.16.8.12
Destination IP: 186.20.20.27
Protocol: TCP
Port: 443
Description: Encrypted web traffic from internal workstation to server. Normal business operations.

Timestamp: 2024-01-16 08:00:00
Source IP: 10.10.50.25
Destination IP: 186.20.20.27
Protocol: TCP
Port: 80
Description: Morning login surge - 45 simultaneous connections from student subnet. Standard daily pattern.

Timestamp: 2024-01-16 10:15:30
Source IP: 10.10.50.28
Destination IP: 186.20.20.27
Protocol: TCP
Port: 443
Description: Mid-morning exam traffic - 120 connections from various student IPs. Elevated but expected during exam windows.

Timestamp: 2024-01-16 13:00:00
Source IP: 10.10.50.32
Destination IP: 186.20.20.27
Protocol: TCP
Port: 80
Description: Post-lunch exam session - 200+ connections from diverse source IPs. Peak usage period.

Timestamp: 2024-01-16 15:45:10
Source IP: 10.10.50.15
Destination IP: 186.20.20.27
Protocol: TCP
Port: 443
Description: Afternoon exam traffic - 180 connections. Sustained high volume.

Timestamp: 2024-01-16 18:30:00
Source IP: 10.10.50.40
Destination IP: 186.20.20.27
Protocol: TCP
Port: 80
Description: Evening exam traffic - Decreasing to 60 connections. End of exam window.

Timestamp: 2024-01-16 22:00:00
Source IP: 10.0.0.5
Destination IP: 186.20.20.27
Protocol: UDP
Port: 53
Description: Routine DNS. Normal volume.
```

---

### Step 2: Open ChatGPT

Navigate to chat.openai.com and log in (free account works).

---

### Step 3: Analyze the Log with Untrained AI

Copy and paste this prompt:

```
Examine the given log entries and provide insights regarding potential security threats or indications of malicious activity.

[PASTE THE NETWORK LOG FROM STEP 1 HERE]
```

### Step 4: Observe ChatGPT's Response

The untrained AI will likely respond with something like:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    UNTRAINED AI RESPONSE                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   POTENTIAL SECURITY THREATS IDENTIFIED:                                     │
│                                                                              │
│   1. Possible DDoS Attack on 186.20.20.27                                   │
│      • Multiple connections from diverse source IPs (10.10.50.x subnet)     │
│      • Traffic spikes: 45 → 120 → 200+ simultaneous connections            │
│      • Sustained high volume over several hours                             │
│      • RECOMMENDATION: Investigate 186.20.20.27 for potential DDoS         │
│                                                                              │
│   2. Unusual Traffic Pattern                                                 │
│      • Rapid increase in connections during specific time windows           │
│      • Multiple student subnet IPs connecting simultaneously                │
│      • RECOMMENDATION: Correlate with threat intelligence feeds             │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

> **Note:** AI responses vary. You may need to tweak your prompt to get a clear misinterpretation.

**The problem:** The AI sees a pattern (many connections to one IP) and incorrectly labels it a DDoS attack. It doesn't know this is an **exam server** with legitimate traffic spikes.

---

### Step 5: Train the AI with Specific Context

Now, teach the AI about your environment.

Copy and paste this prompt **in the same conversation** (so the AI has memory/context):

```
I need to correct your analysis. IP Address 186.20.20.27 is hosting an online exam platform. Here's what you need to know:

1. This server runs scheduled online exams for 500+ students
2. Multiple requests from various IP addresses during exam windows (8am-6pm) are NORMAL
3. Traffic spikes of 200+ simultaneous connections are EXPECTED during peak exam times
4. The source IPs (10.10.50.x) are legitimate student subnets

Do not consider multiple requests to this IP as DDoS attacks. Update your analysis of the log with this context.
```

---

### Step 6: Observe the Trained AI Response

After training, the AI should respond with something like:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    TRAINED AI RESPONSE                                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   REVISED ANALYSIS WITH CONTEXT:                                             │
│                                                                              │
│   Thank you for the correction. With the context that 186.20.20.27 is an    │
│   online exam server:                                                        │
│                                                                              │
│   1. Traffic to 186.20.20.27 is LEGITIMATE                                  │
│      • Connection spikes align with exam windows (8am-6pm)                  │
│      • 200+ simultaneous connections is normal for 500+ students           │
│      • Student subnet (10.10.50.x) is expected source                       │
│      • VERDICT: No DDoS attack detected                                     │
│                                                                              │
│   2. What to Actually Monitor                                                │
│      • Connections outside exam windows (before 8am, after 6pm)             │
│      • Traffic from unexpected subnets (not 10.10.50.x)                     │
│      • Protocol anomalies (e.g., SSH on port 80)                            │
│                                                                              │
│   3. Recommendation                                                          │
│      • Whitelist 186.20.20.27 for DDoS detection during exam hours         │
│      • Create baseline of normal exam traffic for future reference          │
│      • No action needed on this log                                         │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

> **Note:** The AI now correctly identifies the traffic as legitimate because you provided context.

---

## The Training Effect: Before vs. After

| Analysis Factor                           | Untrained AI             | Trained AI                |
| ----------------------------------------- | ------------------------ | ------------------------- |
| **DDoS detection**                  | False positive           | Correctly ignored         |
| **Understanding of traffic spikes** | Suspicious               | Expected (exam pattern)   |
| **Source IP analysis**              | Potentially malicious    | Recognized student subnet |
| **Recommendation**                  | Investigate DDoS         | No action needed          |
| **Analyst hours saved**             | 0 (wasted investigation) | 4+                        |

> *"Training took 30 seconds. It saved 4 hours of investigation. That's ROI."*

---

## How This Works: AI Training Methods

| Method                                         | What It Does                             | Best For                             |
| ---------------------------------------------- | ---------------------------------------- | ------------------------------------ |
| **In-context learning** (what you did)   | Provide context in the same conversation | Quick corrections, temporary context |
| **Fine-tuning**                          | Train model on custom dataset            | Permanent organizational knowledge   |
| **RAG (Retrieval Augmented Generation)** | AI queries your knowledge base           | Dynamic, updatable context           |
| **System prompts**                       | Pre-set instructions for all responses   | Consistent rules and constraints     |

> *"For most SOCs, in-context learning + RAG is the sweet spot."*

---

## Investigation Questions

Answer these based on your AI training experiment:

| # | Question                                                                | Your Answer |
| - | ----------------------------------------------------------------------- | ----------- |
| 1 | What IP address did the untrained AI incorrectly flag as a DDoS victim? |             |
| 2 | What is the actual purpose of the server at 186.20.20.27?               |             |
| 3 | What time periods show the highest connection spikes in the log?        |             |
| 4 | What subnet do legitimate student connections come from?                |             |
| 5 | How did the AI's recommendation change after training?                  |             |
| 6 | What is one thing the trained AI suggested monitoring instead of DDoS?  |             |
| 7 | Why is in-context learning useful for SOC analysts?                     |             |

---

## Real-World Application: Enterprise AI Training

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    ENTERPRISE AI TRAINING WORKFLOW                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   STEP 1: Identify False Positives                                          │
│   └── AI flags alert → Analyst investigates → Finds false positive         │
│                                                                              │
│   STEP 2: Document Context                                                   │
│   └── Create training entry: "Server X is backup server. High traffic at    │
│       2am is normal."                                                        │
│                                                                              │
│   STEP 3: Update Knowledge Base                                              │
│   └── Add to RAG database or fine-tuning dataset                            │
│                                                                              │
│   STEP 4: AI Learns                                                          │
│   └── Future similar traffic is correctly categorized                       │
│                                                                              │
│   STEP 5: Measure Improvement                                                │
│   └── False positive rate decreases over time                               │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Advanced Challenge (Optional)

### Step 7: Train on Multiple Scenarios

Ask the AI to remember multiple context rules:

```
Remember these additional facts about our network:

1. 10.0.0.0/16 is our internal corporate network
2. Backup server (10.0.0.50) does full backups every Sunday at 2am (high traffic)
3. Our CI/CD pipeline deploys to production every Tuesday at 10am (connection spike)
4. The HR system (10.0.0.100) has low traffic except during payroll runs (1st and 15th)

When I give you future logs, apply this context automatically.
```

### Step 8: Create a Training Document

Ask the AI:

```
Based on this exercise, create a one-page template for documenting "normal" network behavior that we can use to train AI models. Include sections for:
- Servers and their normal traffic patterns
- Scheduled events (backups, exams, payroll)
- Expected traffic spikes
- Subnets and their purposes
```

---

## Key Takeaways

| Concept                                 | Description                                       |
| --------------------------------------- | ------------------------------------------------- |
| **Out-of-the-box AI limitations** | AI doesn't know your specific network context     |
| **In-context learning**           | Provide context in the conversation to correct AI |
| **False positive reduction**      | Training AI reduces wasted analyst hours          |
| **Organizational knowledge**      | Document normal behavior to train AI repeatedly   |
| **Continuous improvement**        | Each false positive is a training opportunity     |

---

## Test Your Knowledge

**Q1:** Why would an untrained AI flag online exam traffic as a DDoS attack?

```
Your answer:
_________________________________________________________________
```

**Q2:** What is the difference between in-context learning and fine-tuning?

```
Your answer:
_________________________________________________________________
```

**Q3:** Besides DDoS detection, what other security alerts might benefit from organizational training?

```
Your answer:
_________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                                                                                                                                         |
| -- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1  | AI sees a pattern (many connections to one IP) without understanding the business context (exam server, scheduled testing)                                                                     |
| 2  | In-context learning provides temporary context in the conversation; fine-tuning permanently updates the model's knowledge with training data                                                   |
| 3  | False positives for: vulnerability scans (legitimate vs. malicious), backup traffic (normal high volume), API traffic (normal patterns), admin logins (scheduled maintenance vs. unauthorized) |

---

## Lab Completion Checklist

| Task                                   | Completed |
| -------------------------------------- | --------- |
| **Step 1-2: Setup**              | ☐        |
| Downloaded/accessed sample network log | ☐        |
| Opened ChatGPT or AI platform          | ☐        |
| **Step 3-4: Untrained Analysis** | ☐        |
| Log analyzed by untrained AI           | ☐        |
| Observed false positive DDoS flag      | ☐        |
| **Step 5-6: Training**           | ☐        |
| Provided training context to AI        | ☐        |
| Observed corrected analysis            | ☐        |
| **Questions**                    | ☐        |
| Answered all 7 investigation questions | ☐        |
| **Advanced (Optional)**          | ☐        |
| Trained on multiple scenarios          | ☐        |
| Created training template              | ☐        |

---

## Screenshot Checklist

| Screenshot                    | Description                            |
| ----------------------------- | -------------------------------------- |
| `untrained_ai_response.png` | AI's initial (incorrect) DDoS flag     |
| `training_prompt.png`       | Your training prompt with context      |
| `trained_ai_response.png`   | AI's corrected analysis after training |
| `answers.png`               | Your completed answers                 |

---

## Summary

In this lab, you have:

| Activity                                                            | Completed |
| ------------------------------------------------------------------- | --------- |
| Observed how untrained AI misinterprets normal traffic as malicious | ☐        |
| Trained an AI model with specific organizational context            | ☐        |
| Saw how training reduces false positives                            | ☐        |
| Learned a workflow for continuous AI improvement                    | ☐        |

These skills are essential for:

- SOC teams deploying AI assistants
- Security engineers customizing detection rules
- Organizations reducing alert fatigue
- Analysts who want AI to work WITH them, not against them

---

## Additional Resources

| Resource                          | URL                                                   |
| --------------------------------- | ----------------------------------------------------- |
| OpenAI Fine-tuning Guide          | https://platform.openai.com/docs/guides/fine-tuning   |
| RAG for Cybersecurity             | https://www.pinecone.io/learn/rag-cybersecurity/      |
| NIST AI Risk Management Framework | https://www.nist.gov/itl/ai-risk-management-framework |

---

## Congratulations!

You have successfully completed the **Training Generative AI with Incident Data for Better Pattern Recognition** lab.

> *"The AI doesn't know your network. You do. Your job is to bridge that gap. Now you know how."*

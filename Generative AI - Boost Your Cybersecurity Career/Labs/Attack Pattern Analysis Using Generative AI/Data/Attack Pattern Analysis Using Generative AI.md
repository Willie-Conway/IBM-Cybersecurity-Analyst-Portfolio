![alt text](<../Screenshots/IBM_watsonx_logo.png>)

# Hands-on Lab: Attack Pattern Analysis Using Generative AI

**Estimated time:** 30 minutes

---

## Project Scenario

You are a **cybersecurity analyst** at a mid-sized financial firm. Your SIEM alerted on an unknown process running on a senior accountant's workstation. After isolating the system and performing initial triage, your reverse engineering team extracted the following Python code from memory.

Management wants a rapid assessment: **What does this code do? What assets are at risk? How do we confirm if we've been compromised?**

Traditional static analysis would take hours. You'll use **Generative AI** to accelerate attack pattern analysis — a critical skill in modern Security Operations Centers (SOCs).

---

## Introduction

In this lab, you will use a generative AI model (like IBM watsonx, ChatGPT, or any LLM) to analyze malicious code and identify attack patterns.

**Why Generative AI for Attack Analysis?**

| Traditional Code Analysis      | AI-Powered Analysis         |
| ------------------------------ | --------------------------- |
| Hours of manual review         | Minutes of guided analysis  |
| Requires deep coding expertise | Accessible to SOC analysts  |
| Misses obfuscated patterns     | Identifies hidden behaviors |
| Documentation is separate      | Explains as it analyzes     |

> *"Generative AI doesn't replace the analyst — it amplifies them. You still make the final call, but AI helps you get there faster."*

---

## Learning Objectives

After completing this exercise, you will be able to:

| # | Objective                                                                 |
| - | ------------------------------------------------------------------------- |
| 1 | Analyze code to detect and understand malicious behavior using AI         |
| 2 | Identify vulnerable assets at risk of infection                           |
| 3 | Describe effective methods to assess attack success and system compromise |

---

## The Malicious Code

You've retrieved this Python program from a suspicious process on an infected workstation:

```python
import time
import daemonize
import pygetwindow as gw
import keyboard

# Function to record URL to the 'history' file
def record_url(url):
    with open('history.txt', 'a') as history_file:
        history_file.write(f"{url}\n")

# Main function to monitor browser activity and record URLs
def main():
    while True:
        try:
            # Check if the browser window is active
            active_window = gw.getActiveWindow()
            if active_window and "browser" in active_window.title.lower():
                # Assuming 'Ctrl + L' is used to focus on the browser address bar
                keyboard.press_and_release('ctrl + l')
                time.sleep(0.5)
                # Allow time for the address bar to be in focus
                keyboard.press_and_release('ctrl + c')
                # Copy the URL from the address bar
                url_to_record = keyboard.read_event().name
                # Record the URL
                record_url(url_to_record)
        except Exception as e:
            # Handle exceptions
            print(f"Error: {e}")
        # Sleep before checking again
        time.sleep(2)

if __name__ == "__main__":
    # Define the paths for the daemon process
    pid = "url_recorder.pid"
    stdout = "url_recorder.log"
    stderr = "url_recorder_error.log"
  
    # Create the daemon context
    daemon = daemonize.Daemonize(app="url_recorder", pid=pid, action=main, keep_fds=[1, 2])
  
    # Start the daemon
    daemon.start()
```

> **Note:** This code is for educational purposes. Real-world malware would include obfuscation, anti-debugging, and more sophisticated techniques.

---

## Part 1: Attack Pattern Analysis

### Step 1: Prepare Your Prompt

Copy and paste the following prompt into your generative AI tool (ChatGPT, IBM watsonx, Claude, etc.):

```
You are a cybersecurity analyst specializing in malware analysis. Analyze the following Python code and answer:

1. What is the malicious behavior of this code?
2. What attack pattern or MITRE ATT&CK techniques does this represent?
3. What is the attacker's objective?

Code:
[PASTE THE CODE HERE]
```

### Step 2: Analyze the AI Response

Review the AI's analysis. It should identify:

| Behavior                              | MITRE Technique                                  |
| ------------------------------------- | ------------------------------------------------ |
| Runs as a daemon (background process) | T1543 - Create or Modify System Process          |
| Monitors active browser windows       | T1057 - Process Discovery                        |
| Captures URLs from address bar        | T1005 - Data from Local System                   |
| Writes URLs to `history.txt`        | T1074 - Data Staged                              |
| Runs continuously in background       | T1497 - Virtualization/Sandbox Evasion (partial) |

---

## Part 2: Identify Vulnerable Assets

### Step 3: Prompt for Asset Identification

Copy and paste this prompt:

```
Based on the malicious code analysis, answer:
1. What specific assets on the infected system are at risk?
2. What type of data is the attacker trying to collect?
3. What makes this attack particularly dangerous for a financial services company?
```

### Expected AI Response Highlights

| Asset at Risk                           | Why                                                     |
| --------------------------------------- | ------------------------------------------------------- |
| Browser history                         | Reveals internal systems, cloud apps, financial portals |
| User credentials (via URL parameters)   | Some apps pass tokens in URLs                           |
| Internal server addresses               | Reveals network layout                                  |
| Personal identifiable information (PII) | Accessible via HR/payroll portals                       |

> *"The attacker is mapping the victim's digital life — which banking sites, internal tools, and cloud apps they use."*

---

## Part 3: Determine Attack Success Verification

### Step 4: Prompt for Detection & Verification

Copy and paste this prompt:

```
As an incident responder, answer:
1. How can I verify if this attack has succeeded on a system?
2. What forensic artifacts should I look for?
3. What commands would you run on a可疑 Windows endpoint to confirm infection?
```

### Expected AI Response Highlights

| Verification Method            | Artifact to Check                  |
| ------------------------------ | ---------------------------------- |
| Check for `history.txt` file | Contains captured URLs             |
| Look for `url_recorder.pid`  | Indicates daemon ran               |
| Check running processes        | `python.exe` running headless    |
| Review Windows Event Logs      | Process creation events            |
| Check startup persistence      | Scheduled tasks, registry run keys |

**Example hunting commands:**

```bash
# Find the history file
dir C:\*history.txt /s

# Check for the PID file
dir C:\*url_recorder.pid /s

# Look for Python processes
tasklist | findstr python

# Check recent file modifications
Get-ChildItem -Recurse -Filter "*.txt" | Where-Object {$_.LastWriteTime -gt (Get-Date).AddHours(-24)}
```

---

## Part 4: Complete Investigation Questions

Answer these using your generative AI analysis:

| # | Question                                                                   | Your Answer |
| - | -------------------------------------------------------------------------- | ----------- |
| 1 | What library does the malware use to detect active browser windows?        |             |
| 2 | What keyboard shortcut simulation does the malware use to copy URLs?       |             |
| 3 | What is the name of the output file where captured URLs are stored?        |             |
| 4 | What technique does the malware use to run continuously in the background? |             |
| 5 | What MITRE ATT&CK tactic does URL capture fall under?                      |             |
| 6 | Why does the malware sleep for 2 seconds between checks?                   |             |
| 7 | What is one detection method a SOC analyst could use to find this malware? |             |

---

## Part 5: Extend the Analysis (Optional)

### Step 5: Ask AI for Remediation

Copy and paste:

```
Based on this malware analysis, provide:
1. A one-paragraph executive summary for management
2. Three immediate containment steps
3. How to prevent similar attacks in the future
```

### Step 6: Ask AI to Improve the Code (Blue Team)

Copy and paste:

```
As a defensive programmer, rewrite this code as a legitimate security monitoring tool that could help incident responders detect this type of malware.
```

---

## Lab Completion Checklist

| Task                                   | Completed |
| -------------------------------------- | --------- |
| **Part 1: Attack Analysis**      | ☐        |
| Analyzed code for malicious behavior   | ☐        |
| Identified MITRE ATT&CK techniques     | ☐        |
| **Part 2: Asset Identification** | ☐        |
| Listed vulnerable assets               | ☐        |
| Identified targeted data types         | ☐        |
| **Part 3: Verification**         | ☐        |
| Determined success indicators          | ☐        |
| Listed forensic artifacts              | ☐        |
| **Part 4: Questions**            | ☐        |
| Answered all 7 investigation questions | ☐        |

---

## Screenshot Checklist

| Screenshot            | Description                               |
| --------------------- | ----------------------------------------- |
| `ai_analysis_1.png` | First AI response analyzing the code      |
| `ai_analysis_2.png` | AI response for asset identification      |
| `ai_analysis_3.png` | AI response for verification methods      |
| `your_answers.png`  | Your completed answers to the 7 questions |

---

## Key Takeaways

| Concept                                      | Description                                                              |
| -------------------------------------------- | ------------------------------------------------------------------------ |
| **Generative AI for Malware Analysis** | Accelerates understanding of malicious code                              |
| **Attack Pattern Recognition**         | Identifying common techniques like keylogging, data staging, persistence |
| **MITRE ATT&CK Mapping**               | Translating code behavior into standardized TTPs                         |
| **Asset Impact Assessment**            | Determining what data/business functions are at risk                     |
| **Verification Methodology**           | Proving compromise through forensic artifacts                            |

---

## Test Your Knowledge

**Q1:** What is the primary malicious function of the code?

```
Your answer:
_________________________________________________________________
```

**Q2:** How does the code maintain persistence on the infected system?

```
Your answer:
_________________________________________________________________
```

**Q3:** Why would an attacker want browser history instead of direct keystrokes?

```
Your answer:
_________________________________________________________________
```

---

### Answer Key

| Q# | Answer                                                                                                                                                                         |
| -- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1  | The code continuously monitors browser activity and copies URLs from the address bar, saving them to a history file                                                            |
| 2  | It uses the `daemonize` library to run as a background daemon process                                                                                                        |
| 3  | Browser history reveals sensitive internal systems, cloud applications, and potential credential exposure via URL parameters; it's lower risk for the attacker than keylogging |

---

## Summary

In this lab, you have:

| Activity                                            | Completed |
| --------------------------------------------------- | --------- |
| Used generative AI to analyze malicious Python code | ☐        |
| Identified attack patterns and MITRE techniques     | ☐        |
| Listed vulnerable assets and data at risk           | ☐        |
| Determined verification methods for compromise      | ☐        |
| Practiced AI-assisted incident response             | ☐        |

These skills are essential for:

- SOC analysts triaging potential threats
- Incident responders conducting rapid assessments
- Threat hunters looking for IOCs at scale
- Security teams leveraging AI for efficiency

---

## Additional Resources

| Resource                        | URL                                       |
| ------------------------------- | ----------------------------------------- |
| MITRE ATT&CK Framework          | https://attack.mitre.org                  |
| OWASP AI Security               | https://owasp.org/www-project-ai-security |
| National Vulnerability Database | https://nvd.nist.gov                      |

---

## Congratulations!

You have successfully completed the **Attack Pattern Analysis Using Generative AI** lab. You now know how to:

- Use generative AI to accelerate malware analysis
- Identify attack patterns and map to MITRE ATT&CK
- Assess asset risk and data exposure
- Verify system compromise through forensic artifacts

> *"Generative AI won't replace cybersecurity analysts. But analysts who use AI will replace those who don't."*

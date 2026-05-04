![alt text](<../Screenshots/TheHive_Logo.png>)

# Hands-on Lab: Using TheHive for Security Incident Response

**Estimated time:** 90-120 minutes

---

## Introduction

In this lab, you will become familiar with **TheHive**, an open-source Security Incident Response Platform (SIRP) designed to help SOCs, CSIRTs, and CERTs manage security incidents efficiently . TheHive provides a centralized platform for case management, alert ingestion, task tracking, and collaboration among security analysts.

Unlike Snyk (code scanning) and Nessus (vulnerability scanning), TheHive focuses on **incident response**—organizing security alerts into structured cases that analysts can investigate and resolve .

---

## Learning Objectives

After completing this exercise, you will be able to:

| # | Objective                                                |
| - | -------------------------------------------------------- |
| 1 | Install and configure TheHive using Docker Compose       |
| 2 | Understand TheHive's core features for incident response |
| 3 | Create and manage security cases                         |
| 4 | Add observables and tasks to cases                       |
| 5 | Integrate TheHive with Cortex for observable analysis    |
| 6 | Simulate an incident response workflow                   |

---

## Prerequisites

You must have:

| Requirement                                   | Status                |
| :-------------------------------------------- | :-------------------- |
| **Computer with 8GB+ RAM**              | ☐ (16GB recommended) |
| **50GB free disk space**                | ☐                    |
| **Docker and Docker Compose installed** | ☐                    |
| **Basic Linux command line knowledge**  | ☐                    |
| **Virtualization enabled in BIOS**      | ☐ (for Docker)       |

If Docker is not installed, follow the official installation guide for your operating system.

---

## What is TheHive?

TheHive is a scalable incident response platform that helps security teams manage investigations . It works alongside Cortex (an analysis engine) and MISP (threat intelligence platform) to provide a complete SOC workflow .

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         THEHIVE CAPABILITIES                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                         THEHIVE PLATFORM                             │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                    │                                        │
│           ┌────────────────────────┼────────────────────────┐               │
│           │                        │                        │               │
│           ▼                        ▼                        ▼               │
│   ┌───────────────┐        ┌───────────────┐        ┌───────────────┐       │
│   │  Case         │        │  Alert        │        │  Observable   │       │
│   │  Management   │        │  Ingestion    │        │  Analysis     │       │
│   │               │        │               │        │               │       │
│   │ • Create cases│        │ • SIEM alerts │        │ • IP addresses│       │
│   │ • Assign tasks│        │ • Email alerts│        │ • Domains     │       │
│   │ • Track status│        │ • Custom webhooks│     │ • File hashes │       │
│   │ • Collaborate │        │ • MISP events │        │ • URLs        │       │
│   └───────────────┘        └───────────────┘        └───────────────┘       │
│                                                                              │
│   External Integrations:                                                     │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │  Cortex (Analysis)  │  MISP (Threat Intel)  │  Webhooks (Custom)   │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Key Features

| Feature                      | Description                                                       |
| :--------------------------- | :---------------------------------------------------------------- |
| **Case Management**    | Organize incidents into structured cases with tasks and assignees |
| **Alert Ingestion**    | Receive alerts from SIEMs, email, or webhooks                     |
| **Observables**        | Track IOCs like IPs, domains, and file hashes                     |
| **Cortex Integration** | Analyze observables using 100+ analyzers                          |
| **MISP Integration**   | Import/export threat intelligence                                 |
| **Collaboration**      | Real-time comments and task assignment                            |

---

## Architecture Overview

This lab sets up a complete SOC analysis environment:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         LAB ARCHITECTURE                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                        DOCKER COMPOSE                                │   │
│   │                                                                       │   │
│   │   ┌─────────────┐    ┌─────────────┐    ┌─────────────────────────┐ │   │
│   │   │  TheHive    │    │   Cortex    │    │      Elasticsearch      │ │   │
│   │   │   :9000     │◄──►│   :9001     │    │         :9200           │ │   │
│   │   └─────────────┘    └─────────────┘    └─────────────────────────┘ │   │
│   │         │                  │                         │               │   │
│   │         └──────────────────┼─────────────────────────┘               │   │
│   │                            │                                          │   │
│   │                     ┌──────┴──────┐                                  │   │
│   │                     │  PostgreSQL │                                  │   │
│   │                     │   :5432     │                                  │   │
│   │                     └─────────────┘                                  │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
│   External Access:                                                           │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │   Browser → http://localhost:9000 (TheHive)                         │   │
│   │   Browser → http://localhost:9001 (Cortex)                          │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Part 1: Installing TheHive with Docker Compose

Docker Compose is the recommended method for deploying TheHive as it handles all dependencies automatically .

### Step 1: Verify Docker Installation

Open a terminal and verify Docker is installed:

```bash
docker --version
docker-compose --version
```

Expected output (versions may vary):

```
Docker version 24.0.7, build afdd53b
Docker Compose version v2.20.2
```

### Step 2: Create Project Directory

```bash
mkdir thehive-lab
cd thehive-lab
```

### Step 3: Create Docker Compose File

Create `docker-compose.yml` with the following content :

```yaml
version: "3.8"

services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.17.9
    environment:
      - discovery.type=single-node
      - xpack.security.enabled=false
      - cluster.name=thehive
      - http.host=0.0.0.0
      - transport.host=0.0.0.0
    ulimits:
      memlock:
        soft: -1
        hard: -1
    mem_limit: 2g
    ports:
      - "9200:9200"
    volumes:
      - elasticsearch_data:/usr/share/elasticsearch/data

  cortex:
    image: thehiveproject/cortex:latest
    depends_on:
      - elasticsearch
    ports:
      - "9001:9001"
    volumes:
      - cortex_data:/opt/cortex/data
    environment:
      - JWT_SECRET=$(openssl rand -hex 32)
    mem_limit: 2g

  thehive:
    image: strangebee/thehive:5.2.0  # Use latest stable version 
    depends_on:
      - elasticsearch
      - cortex
    ports:
      - "9000:9000"
    volumes:
      - thehive_data:/opt/thehive/data
    environment:
      - JAVA_OPTS=-Xms2g -Xmx2g
    mem_limit: 4g

volumes:
  elasticsearch_data:
  cortex_data:
  thehive_data:
```

### Step 4: Start the Services

```bash
docker-compose up -d
```

Expected output:

```
[+] Running 4/4
 ✔ Network thehive-lab_default            Created
 ✔ Container thehive-lab-elasticsearch-1  Started
 ✔ Container thehive-lab-cortex-1         Started
 ✔ Container thehive-lab-thehive-1        Started
```

Verify containers are running:

```bash
docker-compose ps
```

Expected output:

```
NAME                          IMAGE                                   STATUS         PORTS
thehive-lab-cortex-1         thehiveproject/cortex:latest             Up            0.0.0.0:9001->9001/tcp
thehive-lab-elasticsearch-1  docker.elastic.co/elasticsearch/elasticsearch:7.17.9  Up   0.0.0.0:9200->9200/tcp
thehive-lab-thehive-1        strangebee/thehive:5.2.0                 Up            0.0.0.0:9000->9000/tcp
```

![Docker containers running]

*[Screenshot: `docker-compose ps` output showing all three containers running]*

### Step 5: Verify Services are Healthy

Wait 1-2 minutes for services to initialize, then check Elasticsearch:

```bash
curl -X GET "localhost:9200/"
```

Expected output:

```json
{
  "name" : "your-hostname",
  "cluster_name" : "thehive",
  "cluster_uuid" : "abc123...",
  "version" : {
    "number" : "7.17.9"
  }
}
```

---

## Part 2: Initial Configuration and Login

### Step 1: Access TheHive Web Interface

Open your browser and navigate to:

```
http://localhost:9000
```

### Step 2: Log in with Default Credentials

| Field              | Value                   |
| :----------------- | :---------------------- |
| **Login**    | `admin@thehive.local` |
| **Password** | `secret`              |

![TheHive login page]

*[Screenshot: TheHive login screen at http://localhost:9000]*

### Step 3: Change Default Password

1. After first login, you'll be prompted to change the admin password
2. Enter a strong password and confirm
3. Click **Update Password**

> **Important:** In a production environment, always change default credentials immediately.

### Step 4: Explore the Dashboard

The main dashboard shows:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         THEHIVE DASHBOARD                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │  Cases        │  Alerts        │  Tasks        │  Observables      │   │
│   │    0          │    0           │    0          │    0              │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │  Recent Activity                                                     │   │
│   │  • No recent activity                                                │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │  My Open Cases                                                       │   │
│   │  • No open cases                                                     │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

![TheHive Dashboard]

*[Screenshot: TheHive main dashboard after login]*

---

## Part 3: Creating and Managing Cases

Cases are the core of TheHive—each investigation becomes a case with tasks, observables, and a timeline .

### Step 1: Create a New Case

1. Click the **New Case** button (top right)
2. Fill in the case details:

| Field                 | Value                                                                                                                                      | Description                             |
| :-------------------- | :----------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------- |
| **Title**       | `Suspicious Phishing Email Investigation`                                                                                                | Brief case description                  |
| **Severity**    | `Medium`                                                                                                                                 | Impact level (Low/Medium/High/Critical) |
| **TLP**         | `Amber`                                                                                                                                  | Traffic Light Protocol for sharing      |
| **PAP**         | `Amber`                                                                                                                                  | Permissible Actions Protocol            |
| **Description** | `User reported suspicious email claiming to be from IT support requesting password verification. Email originated from external domain.` | Detailed case description               |

![Create New Case]

*[Screenshot: New Case creation form with fields filled]*

3. Click **Create Case**

### Step 2: Add Tasks to the Case

Tasks help track investigation steps :

1. In the case view, click **Add Task**
2. Add tasks one by one:

| Task Title           | Description                                          | Assignee |
| :------------------- | :--------------------------------------------------- | :------- |
| `Initial Triage`   | Verify email headers and determine if malicious      | Yourself |
| `Extract IOCs`     | Extract indicators (sender IP, domains, attachments) | Yourself |
| `Sandbox Analysis` | Submit attachments to sandbox for analysis           | Yourself |
| `Block Indicators` | Block malicious IPs/domains on firewall              | Yourself |
| `User Remediation` | Reset user password and verify no compromise         | Yourself |

3. Click **Create** after each task

### Step 3: View the Case Timeline

The case timeline shows all activity:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         CASE TIMELINE                                        │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   [10:30:00]  Case created by admin                                         │
│   [10:32:15]  Task "Initial Triage" assigned to admin                       │
│   [10:32:15]  Task "Extract IOCs" assigned to admin                         │
│   [10:32:15]  Task "Sandbox Analysis" assigned to admin                     │
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │  Add comment...                                               [Send] │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Step 4: Update Task Status

1. Click on a task to expand it
2. Mark tasks as complete as you progress:

```
Task: Initial Triage
Status: [x] Complete  [ ] In Progress  [ ] Waiting  [ ] Cancel

Notes: Analyzed email headers. Sender IP 185.130.5.253 identified as malicious.
```

---

## Part 4: Working with Observables

Observables are Indicators of Compromise (IOCs) associated with a case .

### Step 1: Add Observables to the Case

1. In the case view, scroll to **Observables** section
2. Click **Add observable**
3. Add the following IOCs:

| Observable Type | Value                              | Description                |
| :-------------- | :--------------------------------- | :------------------------- |
| `ip`          | `185.130.5.253`                  | Sender IP address          |
| `domain`      | `secure-login-help.com`          | Malicious link domain      |
| `email`       | `security@secure-login-help.com` | Sender email address       |
| `filename`    | `invoice_923845.pdf`             | Suspicious attachment name |

![Add observable]

*[Screenshot: Add observable dialog with ip type and value entered]*

### Step 2: Set Observable Status

For each observable, set the status:

| Status               | Meaning        | When to Use          |
| :------------------- | :------------- | :------------------- |
| **Suspicious** | Potential IOC  | Initial triage phase |
| **Malicious**  | Confirmed IOC  | After analysis       |
| **Safe**       | False positive | After investigation  |
| **Unknown**    | Needs analysis | Default state        |

For this lab, mark all as **Suspicious** initially.

### Step 3: View All Observables

The observables list displays all IOCs with their status:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         OBSERVABLES LIST                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Type     Value                         Status       Created              │
│   ───────────────────────────────────────────────────────────────────────── │
│   ip       185.130.5.253                Suspicious   2024-01-15 10:35      │
│   domain   secure-login-help.com        Suspicious   2024-01-15 10:35      │
│   email    security@secure-login-...    Suspicious   2024-01-15 10:36      │
│   filename invoice_923845.pdf           Suspicious   2024-01-15 10:36      │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Part 5: Integrating Cortex for Observable Analysis

Cortex provides automated analysis of observables using over 100 analyzers .

### Step 1: Access Cortex Web Interface

Open your browser and navigate to:

```
http://localhost:9001
```

### Step 2: Configure First-Time Setup

1. Click **Update Database**
2. Create an admin user:

| Field                  | Value                    |
| :--------------------- | :----------------------- |
| **Login**        | `admin`                |
| **Password**     | Choose a strong password |
| **Organization** | `admin`                |

3. Click **Create**

![Cortex setup]

*[Screenshot: Cortex first-time setup screen with user creation form]*

### Step 3: Create an API Key for TheHive Integration

1. Log into Cortex as `admin`
2. Navigate to **Organization** → **Users**
3. Click on your user (`admin`)
4. Click **Create API Key**
5. Name it `thehive-integration`
6. Copy the generated API key (starts with `api-key-...`)

### Step 4: Configure TheHive to Use Cortex

1. Return to TheHive (`http://localhost:9000`)
2. Click your user avatar → **Organization settings**
3. Select **Cortex** from the left menu
4. Click **Add Cortex Instance**
5. Fill in:

| Field          | Value                           |
| :------------- | :------------------------------ |
| **Name** | `Local Cortex`                |
| **URL**  | `http://cortex:9001`          |
| **Key**  | (Paste the API key from Cortex) |

6. Click **Test Connection** (should show "Connected")
7. Click **Save**

### Step 5: Analyze an Observable with Cortex

1. In TheHive, open your phishing case
2. In the observables list, find the IP address `185.130.5.253`
3. Click the **...** (more options) menu → **Analyze with Cortex**
4. Select an analyzer (e.g., `VirusTotal_IP_1_0`)
5. Click **Run**

Wait a few seconds for analysis results:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    CORTEX ANALYSIS RESULTS                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Observable: 185.130.5.253                                                 │
│   Analyzer: VirusTotal_IP_1_0                                               │
│                                                                              │
│   Results:                                                                   │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │ • Detected by 12/85 antivirus engines                               │   │
│   │ • Associated domains: malware-distribution[.]com                    │   │
│   │ • Country: RU (Russia)                                              │   │
│   │ • ASN: 12389 - Malware Hosting                                      │   │
│   │ • First seen: 2024-01-10                                            │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
│   Recommendation: Mark as Malicious                                         │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

Based on positive results, update the observable status to **Malicious**.

---

## Part 6: Complete Incident Response Simulation

Now, walk through a complete incident response workflow.

### Scenario

A user reports receiving a suspicious email. The security team needs to investigate, contain, and remediate the incident.

### Phase 1: Initial Triage (5 minutes)

1. **Create the case** (you already did this)
2. **Task 1: Initial Triage**
   - Open the email in a sandbox
   - Review email headers
   - Determine if malicious

Add this comment to the task:

```
Email headers show spoofed display name. Sender IP resolves to known malicious domain. Attachment
appears to be phishing attempt for credentials. Marking as HIGH severity.
```

3. Update case severity to **High**

### Phase 2: IOC Extraction (10 minutes)

1. **Task 2: Extract IOCs** - Complete
2. Add observables (already added)
3. Analyze each with Cortex

### Phase 3: Containment (5 minutes)

1. **Task 4: Block Indicators**
2. Add a comment:
   ```
   Submitted blocking request to network team. Provided IPs and domains for firewall block.
   ```

### Phase 4: User Remediation (5 minutes)

1. **Task 5: User Remediation**
2. Add steps taken:
   ```
   - User password reset performed
   - No unusual login activity detected
   - MFA enabled on user account
   - User notified and educated on phishing awareness
   ```

### Phase 5: Case Closure

1. Mark all tasks as **Complete**
2. Add final case summary:
   ```
   Phishing campaign targeting user accounts. IOCs blocked. User remediated. No data loss confirmed.
   ```
3. Close case with status **Resolved**

---

## Part 7: Advanced Features

### Creating Custom Alert Webhooks

TheHive can receive alerts from any system via webhooks:

1. Go to **Settings** → **Alert Webhooks**
2. Click **Create Webhook**
3. Configure:

| Field                 | Value           |
| :-------------------- | :-------------- |
| **Name**        | `SIEM Alerts` |
| **Type**        | `Custom`      |
| **URL Pattern** | `/api/alert`  |

### Exporting Cases to MISP

TheHive can push case data to MISP for threat intelligence sharing:

1. In a case, click **Export** → **MISP Event**
2. Select observables to include
3. Name the event
4. Click **Export**

### Custom Dashboards

Create dashboards to visualize case metrics:

1. Click **Dashboards** → **New Dashboard**
2. Add widgets for:
   - Open cases by severity
   - Tasks by status
   - Observables by type

---

## Part 8: Troubleshooting

| Issue                                          | Solution                                                                                               |
| :--------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| **TheHive won't start**                  | Run `docker-compose logs thehive` to see errors                                                      |
| **Elasticsearch out of memory**          | Increase memory limit in docker-compose.yml or reduce Java heap size                                   |
| **Login fails with default credentials** | Check if Elasticsearch is healthy; may need to reset database                                          |
| **Cortex connection fails**              | Verify API key and URL; Cortex must be accessible at `http://cortex:9001` from within Docker network |
| **Port conflicts**                       | Change host ports in docker-compose.yml (e.g.,`"9005:9000"`)                                         |
| **Slow performance**                     | Allocate more RAM; close unused applications                                                           |

### Database Reset (if needed)

To completely reset TheHive:

```bash
docker-compose down -v
docker-compose up -d
```

This removes all volumes and starts fresh.

---

## Lab Completion Checklist

| Task                                            | Completed |
| :---------------------------------------------- | :-------- |
| **Part 1: Installation**                  | ☐        |
| Docker and Docker Compose verified              | ☐        |
| docker-compose.yml created                      | ☐        |
| All containers running (docker-compose ps)      | ☐        |
| Elasticsearch responding on port 9200           | ☐        |
| **Part 2: Initial Configuration**         | ☐        |
| Accessed TheHive at http://localhost:9000       | ☐        |
| Logged in with admin@thehive.local / secret     | ☐        |
| Changed default admin password                  | ☐        |
| **Part 3: Case Management**               | ☐        |
| Created a case with title and description       | ☐        |
| Added at least 3 tasks to the case              | ☐        |
| Updated task status (Complete/In Progress)      | ☐        |
| **Part 4: Observables**                   | ☐        |
| Added observables (IP, domain, email, filename) | ☐        |
| Set observable status (Suspicious/Malicious)    | ☐        |
| **Part 5: Cortex Integration**            | ☐        |
| Accessed Cortex at http://localhost:9001        | ☐        |
| Created Cortex admin user                       | ☐        |
| Generated Cortex API key                        | ☐        |
| Configured TheHive to use Cortex                | ☐        |
| Analyzed an observable with Cortex              | ☐        |
| **Part 6: Incident Simulation**           | ☐        |
| Completed all 5 phases of investigation         | ☐        |
| Added comments to tasks                         | ☐        |
| Resolved and closed the case                    | ☐        |
| **Part 7: Troubleshooting**               | ☐        |
| Verified container logs work                    | ☐        |
| Tested database reset command                   | ☐        |

---

## Screenshot Checklist

| Screenshot                | Description                                          |
| :------------------------ | :--------------------------------------------------- |
| `docker_ps.png`         | `docker-compose ps` showing all containers running |
| `thehive_login.png`     | TheHive login page                                   |
| `thehive_dashboard.png` | Main dashboard after login                           |
| `new_case.png`          | New case creation form                               |
| `case_view.png`         | Case detail view with tasks and observables          |
| `observables.png`       | Observables list                                     |
| `cortex_setup.png`      | Cortex first-time setup                              |
| `cortex_api_key.png`    | Creating API key in Cortex                           |
| `cortex_analysis.png`   | Cortex analysis results for IP                       |
| `resolved_case.png`     | Resolved case with closure notes                     |

---

## Key Takeaways

| Concept              | Description                                               |
| :------------------- | :-------------------------------------------------------- |
| **TheHive**    | Open-source Security Incident Response Platform           |
| **Case**       | Container for an investigation with tasks and observables |
| **Observable** | Indicator of Compromise (IP, domain, hash, email)         |
| **Task**       | Action item assigned to an analyst                        |
| **Cortex**     | Analysis engine that scans observables                    |
| **TLP**        | Traffic Light Protocol (sharing restrictions)             |
| **PAP**        | Permissible Actions Protocol (handling instructions)      |

---

## Test Your Knowledge

**Q1:** What external tool does TheHive use for analyzing observables?

```
Your answer:
_________________________________________________________________________
```

**Q2:** What are the four severity levels in TheHive?

```
Your answer:
_________________________________________________________________________
```

**Q3:** What does TLP stand for and what does it indicate?

```
Your answer:
_________________________________________________________________________
```

**Q4:** How can TheHive receive alerts from external systems?

```
Your answer:
_________________________________________________________________________
```

**Q5:** What command completely resets TheHive and removes all data?

```
Your answer:
_________________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                          |
| -- | ------------------------------------------------------------------------------- |
| 1  | Cortex                                                                          |
| 2  | Low, Medium, High, Critical                                                     |
| 3  | Traffic Light Protocol - indicates sharing restrictions for threat intelligence |
| 4  | Alert webhooks (plus SIEM, email, MISP)                                         |
| 5  | `docker-compose down -v`                                                      |

---

## Summary

In this lab, you have:

| Activity                                      | Completed |
| :-------------------------------------------- | :-------- |
| Deployed TheHive with Docker Compose          | ☐        |
| Configured initial settings and login         | ☐        |
| Created and managed security cases            | ☐        |
| Added tasks and observables to cases          | ☐        |
| Integrated Cortex for observable analysis     | ☐        |
| Completed a full incident response simulation | ☐        |

These skills are essential for:

- SOC analysts conducting investigations
- Incident response team members
- Security automation engineers
- Anyone responsible for managing security incidents

---

## Additional Resources

| Resource                        | URL                                                 |
| :------------------------------ | :-------------------------------------------------- |
| **TheHive Official**      | https://strangebee.com/thehive/                     |
| **TheHive Documentation** | https://docs.strangebee.com/thehive/                |
| **Cortex Project**        | https://github.com/TheHive-Project/Cortex           |
| **Cortex Analyzers**      | https://github.com/TheHive-Project/Cortex-Analyzers |
| **StrangeBee Community**  | https://community.strangebee.com/                   |

---

## Congratulations!

You have successfully completed the **Using TheHive for Security Incident Response** lab. You now know how to:

- Deploy TheHive using Docker Compose
- Create and manage security cases
- Track investigation tasks and observables
- Integrate with Cortex for automated analysis
- Complete a full incident response lifecycle

These skills form the foundation of modern SOC operations, enabling you to efficiently manage and respond to security incidents.

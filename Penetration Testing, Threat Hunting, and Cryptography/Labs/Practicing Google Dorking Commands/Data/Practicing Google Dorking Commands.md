![alt text](<../Screenshots/Google_Dork.png>)

# Lab: Practicing Google Dorking Commands

**Estimated time needed:** 20 minutes

---

## Introduction

After you complete this hands-on lab, you will be able to use advanced Google search operators (Google Dorking) to discover information that is not easily accessible through standard searches. You will learn how to find specific file types, locate historical content, search within page text and URLs, and combine operators for powerful reconnaissance. Google Dorking is an essential skill for penetration testers, security researchers, and OSINT analysts to identify exposed sensitive information and potential vulnerabilities.

**Note:** These techniques should only be used on systems you have explicit permission to test. Unauthorized access to information may violate laws and regulations. Always practice ethical hacking principles.

---

## Learning Objectives

By the end of this session, you will be able to:

- Use the `before:` operator to find historical content
- Use the `filetype:` operator to locate specific file types
- Use the `intext:` operator to search within page body text
- Use the `link:` operator to find pages linking to a target
- Use the `inanchor:` operator to search link anchor text
- Use the `*` wildcard operator for variable matching
- Use the `-` operator to exclude terms from search results
- Combine multiple operators for advanced Google Dorking

---

## Important Notices About This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About Search Results

Google search results can vary based on location, search history, and algorithm changes. Your results may look slightly different than what you see in the screenshots. Focus on understanding the operators rather than matching exact results.

### Ethical Use Warning

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           IMPORTANT DISCLAIMER                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Google Dorking commands should ONLY be used for:                           │
│  • Ethical hacking with proper authorization                                 │
│  • Security research on your own systems                                     │
│  • Bug bounty programs with permission                                       │
│  • Educational purposes in controlled environments                          │
│                                                                              │
│  DO NOT use these techniques to access unauthorized information or          │
│  attempt to exploit vulnerabilities without explicit permission.            │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Understanding Google Dorking Operators

| Operator      | Syntax                 | Purpose                                       |
| :------------ | :--------------------- | :-------------------------------------------- |
| `before:`   | `before:YYYY-MM-DD`  | Find content published before a specific date |
| `after:`    | `after:YYYY-MM-DD`   | Find content published after a specific date  |
| `filetype:` | `filetype:pdf`       | Search for specific file types                |
| `intitle:`  | `intitle:"index of"` | Search within page titles                     |
| `inurl:`    | `inurl:admin`        | Search within URLs                            |
| `intext:`   | `intext:password`    | Search within page body text                  |
| `link:`     | `link:example.com`   | Find pages linking to a URL                   |
| `inanchor:` | `inanchor:download`  | Search link anchor text                       |
| `*`         | `"password * .txt"`  | Match any word (wildcard)                     |
| `-`         | `-site:example.com`  | Exclude terms from results                    |
| `site:`     | `site:example.com`   | Limit search to specific domain               |
| `""`        | `"exact phrase"`     | Search for exact phrase                       |

---

## Task 1: Finding Historical Content

### Objective

To identify outdated technologies or practices that may present vulnerabilities by finding content published before a specific date.

### Step 1: Open Google Chrome

1. Launch **Google Chrome** (recommended for this lab)
2. Navigate to **https://www.google.com**

![Google Chrome homepage]

![alt text](<../Screenshots/Google Chrome homepage.png>)

### Step 2: Ensure Search Bar is Empty

1. Click on the search bar
2. Clear any existing text

### Step 3: Enter the Before Operator Command

Type the following command in the search bar:

```
artificial intelligence before:2015-01-01
```

![Before operator search]

![alt text](<../Screenshots/Before operator search.png>)

### Step 4: Press Enter and Examine Results

1. Press **Enter**
2. Examine the articles about artificial intelligence published prior to January 1, 2015

**What to look for:**

- Older articles referencing outdated AI libraries or technologies
- Deprecated frameworks or software versions
- Historical security vulnerabilities in older systems

![After operator results]

![alt text](<../Screenshots/After operator results.gif>)

### Step 5: Practice with Different Queries

Try these variations:

```
security vulnerability before:2010-01-01
outdated software before:2015-06-01
flash player vulnerabilities before:2017-01-01
```

![alt text](<../Screenshots/Practice with Different Queries.gif>)

---

## Task 2: Locating File Types

### Objective

To find specific file types that might contain sensitive information such as confidential reports, configuration files, or passwords.

### Step 1: Ensure Search Bar is Empty

1. Click on the Google search bar
2. Clear any existing text

### Step 2: Enter the Filetype Operator Command

Type the following command:

```
filetype:pdf climate change
```

![Filetype operator search]

![alt text](<../Screenshots/Filetype operator search.png>)

### Step 3: Press Enter and Examine Results

1. Press **Enter**
2. Review the list of PDF documents related to climate change

**What to look for:**

- PDF documents that might include confidential reports
- Internal data relevant to the target
- Documents with sensitive metadata

![Filetype operator results]

![alt text](<../Screenshots/Filetype operator results.gif>)

### Step 4: Practice with Sensitive File Types

Try these commands to find potentially sensitive files:

| Command                           | File Type           | Why Valuable         |
| :-------------------------------- | :------------------ | :------------------- |
| `filetype:xlsx "salary"`        | Excel spreadsheets  | Financial data       |
| `filetype:sql "INSERT INTO"`    | SQL database dumps  | Database credentials |
| `filetype:env "DB_PASSWORD"`    | Environment configs | API keys, passwords  |
| `filetype:log "error"`          | Log files           | System errors, paths |
| `filetype:conf "configuration"` | Config files        | System settings      |

![Sensitive filetype searches]

![alt text](<../Screenshots/Sensitive filetype searches.gif>)

---

## Task 3: Searching Within Text

### Objective

To identify web pages that discuss certain technologies or topics that could indicate potential weaknesses.

### Step 1: Ensure Search Bar is Empty

1. Click on the Google search bar
2. Clear any existing text

### Step 2: Enter the Intext Operator Command

Type the following command:

```
intext:benefits meditation
```

![Intext operator search]

![alt text](<../Screenshots/Intext operator search.png>)

### Step 3: Press Enter and Examine Results

1. Press **Enter**
2. Review the web pages that mention these terms in the body text

**What to look for:**

- Web pages discussing specific technologies
- Internal documentation or references
- Potential weaknesses disclosed in forums or blogs

![Intext operator results]

![alt text](<../Screenshots/Intext operator results.gif>)

* Step 4: Practice with Security-Focused Queries

Try these commands:

```
intext:confidential "internal use only"
intext:"API key" filetype:java
intext:"username" filetype:txt
```

**Why these matter:** Attackers search for exposed credentials, internal documents, and configuration details accidentally indexed by search engines.

![alt text](<../Screenshots/Practice with Security-Focused Queries.gif>)

---

## Task 4: Identifying Linked Pages

### Objective

To find other sites that link to the target and could offer additional insights or entry points.

### Step 1: Ensure Search Bar is Empty

1. Click on the Google search bar
2. Clear any existing text

### Step 2: Enter the Link Operator Command

Type the following command:

```
link:https://www.wikipedia.org
```

![Link operator search]

![alt text](<../Screenshots/Link operator search.png>)

### Step 3: Press Enter and Examine Results

1. Press **Enter**
2. Review the list of web pages that contain links to Wikipedia

**What to look for:**

- External sites linking to the target
- Forums, blogs, or news sites discussing the target
- Potential points of compromise through linked resources

![Link operator results]

![alt text](<../Screenshots/Link operator results.gif>)

> **Note:** The `link:` operator has limited functionality in modern Google search. It may return fewer results than expected.

### Step 4: Understanding Link Analysis

In a real penetration test, you would use this to:

- Find other sites associated with the target organization
- Discover employee blogs or personal sites
- Identify third-party vendors or partners

---

## Task 5: Exploring Anchor Text

### Objective

To find pages that use specific anchor texts, which might lead to downloadable content or sensitive resources.

### Step 1: Ensure Search Bar is Empty

1. Click on the Google search bar
2. Clear any existing text

### Step 2: Enter the Inanchor Operator Command

Type the following command:

```
inanchor:download now
```

![Inanchor operator search]

![alt text](<../Screenshots/Inanchor operator search.png>)

### Step 3: Press Enter and Examine Results

1. Press **Enter**
2. Review the web pages with links containing **Download now** as the anchor text

**What to look for:**

- Links that lead to downloadable content
- Files, software, or resources that could be analyzed
- Login pages linked with "sign in" or "admin portal"

![Inanchor operator results]

![alt text](<../Screenshots/Inanchor operator results.gif>)

### Step 4: Practice with Login Anchor Texts

Try these anchor text searches:

```
inanchor:"sign in"
inanchor:"admin login"
inanchor:"click here"
```

## Task 6: Using Wildcards

### Objective

To capture pages with various terms that might reveal varied information between two search terms.

### Step 1: Ensure Search Bar is Empty

1. Click on the Google search bar
2. Clear any existing text

### Step 2: Enter the Wildcard Operator Command

Type the following command:

```
data * analysis
```

![Wildcard operator search]

![alt text](<../Screenshots/Wildcard operator search.png>)

### Step 3: Press Enter and Examine Results

1. Press **Enter**
2. Review the searches that capture different terms between "data" and "analysis"

**What to look for:**

- Analyze the various terms and contexts between "data" and "analysis"
- Patterns or common phrases that reveal information
- Variations in terminology used across different sites

![Wildcard operator results]

![alt text](<../Screenshots/Wildcard operator results.gif>)

### Step 4: Practice with Security Wildcards

Try these commands:

```
"password * .txt"
"username * password"
"SELECT * FROM * WHERE"
```

---

## Task 7: Excluding Terms

### Objective

To find relevant information while excluding typical, irrelevant results, enabling more precise targeting.

### Step 1: Ensure Search Bar is Empty

1. Click on the Google search bar
2. Clear any existing text

### Step 2: Enter the Exclusion Operator Command

Type the following command:

```
apple -fruit -pie -recipe
```

![Exclusion operator search]

![alt text](<../Screenshots/Exclusion operator search.png>)

### Step 3: Press Enter and Examine Results

1. Press **Enter**
2. Review the search results that exclude pages about fruit, pie, and recipes

**What to look for:**

- Results focused on Apple Inc. (technology) rather than apple the fruit
- Ability to filter out noise and focus on relevant content
- More precise targeting of search results

1. ![Exclusion operator results]

![alt text](<../Screenshots/Exclusion operator results.gif>)

### Step 4: Practice with Security Exclusions

Try these commands:

```
java -coffee -island -script
security -guard -camera -blanket
```

![alt text](<../Screenshots/Exclusion operator results security.gif>)

---

## Task 8: Combining Operators (Advanced)

### Objective

To combine multiple search operators for more precise and powerful Google Dorking reconnaissance.

### Step 1: Try Combined Search - Sensitive Files on a Specific Site

Type the following command:

```
site:example.com filetype:xlsx "confidential"
```

![Combined operators - site and filetype]

![alt text](<../Screenshots/Combined operators - site and filetype.png>)

![alt text](<../Screenshots/Combined operators - site and filetype.gif>)

### Step 2: Try Combined Search - Directory Listings

Type the following command:

```
intitle:"index of" "parent directory" -inurl:apache -inurl:nginx
```

1. ![Combined operators - directory listings]

![alt text](<../Screenshots/Combined operators - directory listings_.gif>)

### Step 3: Try Combined Search - Admin Panels

Type the following command:

```
inurl:admin intext:username filetype:php
```

![Combined operators - admin panels]

![alt text](<../Screenshots/Combined operators - admin panels.gif>)

### Step 4: Try Combined Search - Exposed API Keys

Type the following command:

```
filetype:env "DB_PASSWORD" -git -github
```

![Combined operators - API keys]

![alt text](<../Screenshots/Combined operators - API keys.gif>)

---

## Task 9: Create Your Own Powerful Dorks

### Step 1: Build a Custom Dork

Combine at least three operators to create a powerful search:

```
Your custom dork: _____________________________________________________________
```

### Step 2: Document Your Findings

| Search Term | Operators Used | Number of Results | Interesting Findings |
| :---------- | :------------- | :---------------- | :------------------- |
|             |                |                   |                      |
|             |                |                   |                      |
|             |                |                   |                      |

### Step 3: Test Results

1. Enter your custom dork into Google
2. Record the number of results
3. Note any interesting findings

![Custom dork results]

![alt text](<../Screenshots/Custom dork results.gif>)

---

## Common Google Dorks for Penetration Testing

| Purpose                            | Dork Command                   |
| :--------------------------------- | :----------------------------- |
| **Find login pages**         | `intitle:login inurl:admin`  |
| **Find exposed directories** | `intitle:"index of"`         |
| **Find SQL dumps**           | `filetype:sql "INSERT INTO"` |
| **Find password files**      | `filetype:txt "password"`    |
| **Find configuration files** | `filetype:conf "server"`     |
| **Find backup files**        | `filetype:bak "backup"`      |
| **Find WordPress admin**     | `inurl:wp-admin`             |
| **Find phpMyAdmin**          | `inurl:phpmyadmin`           |
| **Find AWS keys**            | `"AKIA" filetype:txt`        |
| **Find exposed env files**   | `filetype:env DB_PASSWORD`   |

---

## Lab Completion Checklist

| Task                                                | Completed |
| :-------------------------------------------------- | :-------- |
| **Task 1: Finding Historical Content**        | ☐        |
| `before:` operator with "artificial intelligence" | ☐        |
| Practiced with different date queries               | ☐        |
| **Task 2: Locating File Types**               | ☐        |
| `filetype:pdf climate change`                     | ☐        |
| `filetype:xlsx "salary"`                          | ☐        |
| `filetype:sql "INSERT INTO"`                      | ☐        |
| **Task 3: Searching Within Text**             | ☐        |
| `intext:benefits meditation`                      | ☐        |
| `intext:confidential "internal use only"`         | ☐        |
| **Task 4: Identifying Linked Pages**          | ☐        |
| `link:https://www.wikipedia.org`                  | ☐        |
| **Task 5: Exploring Anchor Text**             | ☐        |
| `inanchor:download now`                           | ☐        |
| **Task 6: Using Wildcards**                   | ☐        |
| `data * analysis`                                 | ☐        |
| `"password * .txt"`                               | ☐        |
| **Task 7: Excluding Terms**                   | ☐        |
| `apple -fruit -pie -recipe`                       | ☐        |
| `java -coffee -island`                            | ☐        |
| **Task 8: Combining Operators**               | ☐        |
| `site:example.com filetype:xlsx "confidential"`   | ☐        |
| `intitle:"index of" "parent directory"`           | ☐        |
| `inurl:admin intext:username filetype:php`        | ☐        |
| **Task 9: Create Custom Dorks**               | ☐        |
| Built and tested custom dork                        | ☐        |
| Documented findings                                 | ☐        |

---

## Screenshot Checklist

| Screenshot         | File Name                     | Description                                 |
| :----------------- | :---------------------------- | :------------------------------------------ |
| Before Operator    | `GD_Before_Operator.png`    | Search showing `before:` operator results |
| Filetype Operator  | `GD_Filetype_Operator.png`  | PDF filetype search results                 |
| Intext Operator    | `GD_Intext_Operator.png`    | Intext search showing body text matches     |
| Link Operator      | `GD_Link_Operator.png`      | Link operator results (if available)        |
| Inanchor Operator  | `GD_Inanchor_Operator.png`  | Anchor text search results                  |
| Wildcard Operator  | `GD_Wildcard_Operator.png`  | Wildcard showing variable terms             |
| Exclusion Operator | `GD_Exclusion_Operator.png` | Excluding terms from results                |
| Combined Operators | `GD_Combined_Operators.png` | Multi-operator advanced search              |
| Custom Dork        | `GD_Custom_Dork.png`        | Custom dork with findings                   |

---

## Google Dorking Cheat Sheet

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    GOOGLE DORKING QUICK REFERENCE CARD                      │
└─────────────────────────────────────────────────────────────────────────────┘

DATE-BASED SEARCHES
─────────────────────────────────────────────────────────────────────────────
before:2020-01-01        Find content before date
after:2020-01-01         Find content after date
2020...2022              Find within date range

FILE TYPE SEARCHES
─────────────────────────────────────────────────────────────────────────────
filetype:pdf             Portable Document Format
filetype:xlsx            Excel spreadsheets
filetype:sql             Database dumps
filetype:log             Log files
filetype:env             Environment configuration
filetype:conf            Configuration files
filetype:docx            Word documents
filetype:csv             Comma-separated values

TITLE SEARCHES
─────────────────────────────────────────────────────────────────────────────
intitle:"index of"       Directory listings
intitle:"log in"         Login pages
intitle:"admin"          Admin panels
intitle:dashboard        Dashboard pages

URL SEARCHES
─────────────────────────────────────────────────────────────────────────────
inurl:admin              Admin pages in URL
inurl:login              Login pages in URL
inurl:config             Configuration pages
inurl:.env               Environment file exposure

TEXT SEARCHES
─────────────────────────────────────────────────────────────────────────────
intext:"password"        Pages containing "password"
intext:"confidential"    Confidential documents
intext:"API key"         API key disclosures

LINK & ANCHOR SEARCHES
─────────────────────────────────────────────────────────────────────────────
link:example.com         Pages linking to example.com
inanchor:"click here"    Links with specific anchor text

SITE RESTRICTIONS
─────────────────────────────────────────────────────────────────────────────
site:example.com         Search only within domain
-site:example.com        Exclude domain from results

POWERFUL DORKING COMBINATIONS
─────────────────────────────────────────────────────────────────────────────
intitle:"index of" "parent directory" -inurl:apache -inurl:nginx
filetype:env "DB_PASSWORD" -git -github
inurl:admin intext:username filetype:php
site:target.com filetype:xlsx "confidential"
"-----BEGIN RSA PRIVATE KEY-----" filetype:txt
```

---

## Troubleshooting Tips

| Issue                                         | Solution                                                                |
| :-------------------------------------------- | :---------------------------------------------------------------------- |
| **No results for `link:` operator**   | Link operator has limited functionality; try using `related:` instead |
| **Too many irrelevant results**         | Use `-` operator to exclude common terms; add more specific keywords  |
| **Results vary from screenshots**       | Google personalizes results; focus on learning the operators            |
| **Filetype search returns few results** | Try different file extensions (`.xls` vs `.xlsx`)                   |
| **Date operators not working**          | Use format `YYYY-MM-DD` exactly (e.g., `before:2020-01-01`)         |
| **Wildcard not matching**               | Put phrase in quotes:`"data * analysis"`                              |

---

## Key Takeaways

| Concept                       | Description                                                             |
| :---------------------------- | :---------------------------------------------------------------------- |
| **Google Dorking**      | Using advanced search operators to find hidden/discoverable information |
| **OSINT**               | Open Source Intelligence gathered from publicly available sources       |
| **Reconnaissance**      | Information gathering phase of penetration testing                      |
| **Operator Chaining**   | Combining multiple operators for precise searches                       |
| **Ethical Use**         | Only use with permission on authorized targets                          |
| **Filetype Discovery**  | Identify exposed sensitive documents and config files                   |
| **Historical Analysis** | Find outdated technologies with known vulnerabilities                   |

---

## Summary

In this hands-on lab, you have:

| Activity                                                  | Completed |
| :-------------------------------------------------------- | :-------- |
| Used `before:` operator to find historical content      | ✓        |
| Used `filetype:` operator to locate specific file types | ✓        |
| Used `intext:` operator to search within page body      | ✓        |
| Used `link:` operator to find linking pages             | ✓        |
| Used `inanchor:` operator to search anchor text         | ✓        |
| Used `*` wildcard for variable matching                 | ✓        |
| Used `-` operator to exclude terms                      | ✓        |
| Combined multiple operators for advanced dorking          | ✓        |
| Created and tested custom Google Dorks                    | ✓        |
| Documented findings from searches                         | ✓        |

---

## Congratulations!

You have successfully completed the **Practicing Google Dorking Commands** lab. You now know how to:

- Use advanced Google search operators for reconnaissance
- Find historical content and outdated technologies
- Locate specific file types containing sensitive information
- Search within page text, titles, and URLs
- Identify linked pages and anchor text
- Use wildcards and exclusions for precise searching
- Combine operators for advanced dorking techniques
- Apply Google Dorking in authorized penetration testing scenarios

These skills are essential for:

- Penetration testers and ethical hackers
- Security researchers
- OSINT analysts
- Bug bounty hunters
- Security auditors
- Anyone responsible for finding exposed sensitive information

---

## Additional Resources

| Resource                                 | URL                                                 |
| :--------------------------------------- | :-------------------------------------------------- |
| **Google Hacking Database (GHDB)** | https://www.exploit-db.com/google-hacking-database  |
| **Google Search Operators**        | https://support.google.com/websearch/answer/2466433 |
| **OWASP Google Dorking**           | https://owasp.org/www-project-google-hacking        |
| **Google Dorking Cheat Sheet**     | https://www.stationx.net/google-dorking-cheat-sheet |

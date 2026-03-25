![alt text](../Screenshots/Linux.jpg)

# Hands-on Lab: Common Linux/Unix Commands

**Estimated time needed:** 40 minutes

---

## Learning Objectives

In this lab, you will be introduced to basic Unix commands related to the following categories:

- General purpose commands
- Directory management commands
- File management commands
- Access control commands
- Text processing commands
- Networking commands

---

## About Skills Network Cloud IDE

Skills Network Cloud IDE (based on Theia and Docker) provides an environment for hands-on labs for course and project related labs. Theia is an open-source IDE (Integrated Development Environment) that can be run on desktop or on the cloud. To complete this lab, we will be using the Cloud IDE based on Theia.

---

## Important Notice about this Lab Environment

Please be aware that sessions for this lab environment are **not persisted**. Every time you connect to this lab, a new environment is created for you. Any data or files you may have saved in an earlier session would get lost. Plan to complete these labs in a single session to avoid losing your data.

---

## Getting Started: Open a Terminal

1. In the Cloud IDE, click on the menu bar at the top of the screen
2. Select **Terminal → New Terminal**

![Terminal menu with New Terminal option highlighted]


![alt text](<../Screenshots/Terminal menu with New Terminal option highlighted.png>)

1. A new terminal window will open at the bottom of the screen

![New terminal opened at bottom of screen]

![alt text](<../Screenshots/New terminal opened at bottom of screen.png>)

1. All commands in this lab will be run in this terminal

---

## Exercise 1: General Purpose Commands

In this exercise, you will learn basic commands for user information, date/time, and listing files.

### Step 1.1: Display the Current User

Run the following command to see who you are logged in as:

```bash
whoami
```

**Expected output:**

```
theia
```

**Explanation:** You are logged into this lab environment as the user `theia`.

![whoami command output showing "theia"]

![alt text](<../Screenshots/whoami command output showing - theia.png>)

### Alternative: List Logged-in Users

To see a list of currently logged-in users, you would normally use:

```bash
who
```

**Note:** This command may not work in the Theia environment, but it's good to know for standard Linux systems.

### Step 1.2: Display User and Group Identity Information

Run the following command to see detailed user and group information:

```bash
id
```

**Expected output (similar to):**

```
uid=1000(theia) gid=1000(theia) groups=1000(theia),4(adm),27(sudo),44(video),50(staff)
```

**Explanation:** This displays:

- **uid** - User ID number (1000 for the first regular user)
- **gid** - Primary group ID number
- **groups** - All groups the user belongs to

![id command output showing uid and gid information]

![alt text](<../Screenshots/id command output showing uid and gid information.png>)

### Step 1.3: Display Date and Time

Run the following command to see the current date and time:

```bash
date
```

**Expected output (similar to):**

```
Thu Feb 28 01:02:03 UTC 2026
```

### Format the Date in Different Ways

The `date` command has several options to format output:

| Command              | Purpose               | Example Output |
| -------------------- | --------------------- | -------------- |
| `date "+%D"`       | MM/DD/YY format       | 02/28/26       |
| `date "+%m-%d-%Y"` | MM-DD-YYYY format     | 02-28-2026     |
| `date "+%Y-%m-%d"` | YYYY-MM-DD format     | 2026-02-28     |
| `date "+%T"`       | 24-hour time HH:MM:SS | 01:02:03       |
| `date "+%H:%M:%S"` | Custom time format    | 01:02:03       |

Try each of these commands:

```bash
date "+%D"
date "+%Y-%m-%d"
date "+%T"
```

**Date Format Specifiers:**

| Specifier        | Explanation                         |
| :--------------- | :---------------------------------- |
| `%d`           | Day of the month (01 to 31)         |
| `%h` or `%b` | Abbreviated month name (Jan to Dec) |
| `%m`           | Month of year (01 to 12)            |
| `%Y`           | Four-digit year                     |
| `%y`           | Two-digit year                      |
| `%T`           | Time in 24-hour format HH:MM:SS     |
| `%H`           | Hour (00 to 23)                     |
| `%M`           | Minute (00 to 59)                   |
| `%S`           | Second (00 to 59)                   |

![Various date command formats showing different outputs]

![alt text](<../Screenshots/Various date command formats showing different outputs.png>)

### Step 1.4: List Files and Directories

The `ls` command lists files and directories in the current location.

Run the basic `ls` command:

```bash
ls
```

**Expected output:** If your directory is empty, you may see no output at all.

List files in the `/bin` directory:

```bash
ls /bin
```

This will show all executable files in the system's binary directory.

![ls /bin showing many files]

![alt text](<../Screenshots/ls  - bin showing many files.png>)

List files starting with 'b' in the `/bin` directory:

```bash
ls /bin/b*
```

This uses a wildcard (`*`) to match any file starting with 'b'.

**Useful `ls` options:**

| Command     | Purpose                                                |
| :---------- | :----------------------------------------------------- |
| `ls -l`   | Long format (permissions, size, date)                  |
| `ls -a`   | Show all files (including hidden ones starting with .) |
| `ls -la`  | Long format including hidden files                     |
| `ls -lh`  | Human-readable file sizes (KB, MB, GB)                 |
| `ls -lt`  | Sort by time (newest first)                            |
| `ls -ltr` | Sort by time (oldest first, reverse)                   |

Try these options:

```bash
ls -l /bin
ls -la
```

![ls -l output showing detailed file information]

![alt text](<../Screenshots/ls -l output showing detailed file information.png>)

## Exercise 2: Directory Management Commands

In this exercise, you will learn commands to create, navigate, and remove directories.

### Step 2.1: Print Working Directory

The `pwd` command shows your current location in the filesystem:

```bash
pwd
```

**Expected output:**

```
/home/theia
```

This is your home directory.

![pwd command showing /home/theia]

![alt text](<../Screenshots/pwd command showing  - home - theia.png>)

### Step 2.2: Create a Directory

The `mkdir` command creates new directories:

```bash
mkdir lab-directory
```

Verify it was created:

```bash
ls
```

You should see `lab-directory` in the output.

### Create Multiple Directories

Create several directories at once:

```bash
mkdir dir1 dir2 dir3
ls
```

### Create Nested Directories

Use the `-p` option to create parent directories if they don't exist:

```bash
mkdir -p projects/linux/labs
ls -R projects
```

The `-R` option shows directories recursively.

![mkdir -p creating nested directories]

![alt text](<../Screenshots/mkdir -p creating nested directories.png>)

### Step 2.3: Change Directory

The `cd` command changes your current directory:

```bash
cd lab-directory
pwd
```

**Expected output:**

```
/home/theia/lab-directory
```

### Navigate Back

Go back to the previous directory:

```bash
cd ..
pwd
```

The `..` represents the parent directory.

### Go to Home Directory

There are several ways to return to your home directory:

```bash
cd ~
# or
cd
# or
cd /home/theia
```

All of these take you to `/home/theia`.

### Step 2.4: Remove a Directory

The `rmdir` command removes **empty** directories only:

```bash
cd ~
rmdir dir1
ls
```

`dir1` should no longer appear.

To remove a directory with contents, you'll need `rm -r` (covered later).

### Step 2.5: Create a Directory Structure

Create a structure for practice:

```bash
cd ~
mkdir -p projects/linux/labs/day1
mkdir -p projects/linux/labs/day2
mkdir -p projects/linux/scripts
mkdir documents downloads
```

### Step 2.6: View Directory Tree

Install and use the `tree` command (if available):

```bash
tree projects
```

If `tree` is not installed, you can use:

```bash
ls -R projects
```

This shows all files and directories recursively.

![tree or ls -R showing directory structure]

![alt text](<../Screenshots/tree or ls -R showing directory structure.png>)

### Directory Commands Summary

| Command      | Purpose                   | Example            |
| :----------- | :------------------------ | :----------------- |
| `pwd`      | Print working directory   | `pwd`            |
| `mkdir`    | Create directory          | `mkdir newdir`   |
| `mkdir -p` | Create parent directories | `mkdir -p a/b/c` |
| `cd`       | Change directory          | `cd /home`       |
| `cd ..`    | Go to parent directory    | `cd ..`          |
| `cd ~`     | Go to home directory      | `cd ~`           |
| `rmdir`    | Remove empty directory    | `rmdir emptydir` |

---

## Exercise 3: File Management Commands

In this exercise, you will learn to create, view, copy, move, and delete files.

### Step 3.1: Create Empty Files

The `touch` command creates empty files or updates timestamps:

```bash
cd ~/lab-directory
touch file1.txt file2.txt file3.txt
ls
```

### Step 3.2: Create Files with Content

Use `echo` with redirection to create files with content:

```bash
echo "Hello, World!" > hello.txt
echo "This is a test file." > test.txt
echo "Linux commands are powerful." >> test.txt
```

The `>` operator creates/overwrites a file. The `>>` operator appends to a file.

### Step 3.3: View File Contents

Several commands can display file contents:

**`cat` - Display entire file:**

```bash
cat hello.txt
cat test.txt
```

**`less` - View page by page (use Space to scroll, q to quit):**

```bash
less test.txt
```

**`head` - View first few lines (default 10):**

```bash
head /etc/passwd
head -n 5 /etc/passwd  # First 5 lines
```

**`tail` - View last few lines:**

```bash
tail /etc/passwd
tail -n 20 /etc/passwd  # Last 20 lines
tail -f /var/log/syslog  # Follow file as it grows (Ctrl+C to stop)
```

![cat, head, tail commands showing output]

![alt text](<../Screenshots/cat show output.png>)

![alt text](<../Screenshots/head show output.png>)

![alt text](<../Screenshots/tail show output.png>)

### Step 3.4: Copy Files

The `cp` command copies files:

```bash
cp hello.txt hello_copy.txt
ls
```

Copy multiple files to a directory:

```bash
cp file1.txt file2.txt ~/documents/
ls ~/documents
```

Copy entire directories recursively:

```bash
cp -r ~/projects ~/projects_backup
```

### Step 3.5: Move and Rename Files

The `mv` command moves or renames files:

```bash
mv hello_copy.txt renamed.txt
ls
```

Move a file to another directory:

```bash
mv renamed.txt ~/documents/
ls ~/documents
```

### Step 3.6: Delete Files

The `rm` command removes files:

```bash
rm file3.txt
ls
```

Delete multiple files:

```bash
rm file1.txt file2.txt
```

Delete directories recursively:

```bash
rm -r ~/projects_backup
```

**⚠️ Warning:** `rm -rf` is powerful and dangerous. It forces recursive deletion without confirmation.

### Step 3.7: Count Words, Lines, Characters

The `wc` command counts words, lines, and characters:

```bash
wc test.txt
wc -l test.txt  # Only line count
wc -w test.txt  # Only word count
wc -c test.txt  # Only character count
```

### Step 3.8: Compare Files

Create two similar files and compare them:

```bash
echo "apple" > fruit1.txt
echo "apple" > fruit2.txt
echo "orange" > fruit3.txt
```

Compare identical files:

```bash
diff fruit1.txt fruit2.txt
```

Compare different files:

```bash
diff fruit1.txt fruit3.txt
```

### File Management Commands Summary

| Command   | Purpose               | Example                 |
| :-------- | :-------------------- | :---------------------- |
| `touch` | Create empty file     | `touch file.txt`      |
| `cat`   | Display file contents | `cat file.txt`        |
| `less`  | Page through file     | `less largefile`      |
| `head`  | Show first lines      | `head -n 20 file.txt` |
| `tail`  | Show last lines       | `tail -f logfile`     |
| `cp`    | Copy file/directory   | `cp file1 file2`      |
| `cp -r` | Copy recursively      | `cp -r dir1 dir2`     |
| `mv`    | Move/rename file      | `mv old new`          |
| `rm`    | Remove file           | `rm file.txt`         |
| `rm -r` | Remove recursively    | `rm -r directory`     |
| `wc`    | Word count            | `wc -l file.txt`      |
| `diff`  | Compare files         | `diff file1 file2`    |

---

## Exercise 4: Access Control Commands

In this exercise, you will learn about file permissions and how to change them.

### Step 4.1: View File Permissions

Use `ls -l` to see detailed file information including permissions:

```bash
cd ~/lab-directory
touch permissions.txt
echo "Test file for permissions" > permissions.txt
ls -l permissions.txt
```

**Expected output (similar to):**

```
-rw-r--r-- 1 theia theia 28 Feb 28 01:23 permissions.txt
```

**Permission String Breakdown:**

| Part    | Meaning                                         |
| :------ | :---------------------------------------------- |
| `-`   | File type (`-` for file, `d` for directory) |
| `rw-` | Owner permissions (read, write, no execute)     |
| `r--` | Group permissions (read only)                   |
| `r--` | Others permissions (read only)                  |

### Step 4.2: Understanding Permission Codes

Each permission set has numeric values:

| Permission | Symbol | Numeric Value |
| :--------- | :----- | :------------ |
| Read       | r      | 4             |
| Write      | w      | 2             |
| Execute    | x      | 1             |

**Common Permission Combinations:**

| Numeric | Symbolic | Meaning              |
| :------ | :------- | :------------------- |
| 7       | rwx      | Read, write, execute |
| 6       | rw-      | Read, write          |
| 5       | r-x      | Read, execute        |
| 4       | r--      | Read only            |
| 0       | ---      | No permissions       |

### Step 4.3: Change File Permissions with `chmod`

**Symbolic Method:**

```bash
chmod u+x permissions.txt  # Add execute for user (owner)
ls -l permissions.txt

chmod g-w permissions.txt  # Remove write for group
ls -l permissions.txt

chmod o=r permissions.txt  # Set others to read only
ls -l permissions.txt

chmod u=rwx,g=rx,o=r permissions.txt  # Set specific permissions
ls -l permissions.txt
```

**Numeric Method:**

```bash
chmod 755 permissions.txt  # rwxr-xr-x
ls -l permissions.txt

chmod 644 permissions.txt  # rw-r--r--
ls -l permissions.txt

chmod 700 permissions.txt  # rwx------
ls -l permissions.txt
```

### Step 4.4: Change File Ownership

The `chown` command changes file owner and group (may require sudo):

```bash
sudo chown root permissions.txt  # Change owner to root
ls -l permissions.txt
```

Change both owner and group:

```bash
sudo chown theia:theia permissions.txt  # Change back
ls -l permissions.txt
```

### Step 4.5: Change Group Ownership

The `chgrp` command changes only the group:

```bash
sudo chgrp staff permissions.txt
ls -l permissions.txt
```

### Access Control Commands Summary

| Command              | Purpose                | Example                   |
| :------------------- | :--------------------- | :------------------------ |
| `chmod`            | Change permissions     | `chmod 755 file`        |
| `chmod` (symbolic) | Change permissions     | `chmod u+x file`        |
| `chown`            | Change owner           | `chown user file`       |
| `chown` (both)     | Change owner and group | `chown user:group file` |
| `chgrp`            | Change group           | `chgrp group file`      |

---

## Exercise 5: Text Processing Commands

In this exercise, you will learn commands to search and process text.

### Step 5.1: Create a Sample File

Create a file with sample data for processing:

```bash
cd ~/lab-directory
cat > employees.txt << EOF
John Smith,Developer,55000
Jane Doe,Manager,75000
Bob Johnson,Developer,52000
Alice Brown,Director,95000
Charlie Wilson,Developer,58000
Diana Prince,Manager,72000
EOF
```

### Step 5.2: Search with `grep`

The `grep` command searches for patterns in files:

```bash
grep "Developer" employees.txt
```

Case-insensitive search:

```bash
grep -i "developer" employees.txt
```

Count matches:

```bash
grep -c "Manager" employees.txt
```

Show line numbers:

```bash
grep -n "Director" employees.txt
```

Search for lines NOT matching:

```bash
grep -v "Developer" employees.txt
```

Search multiple files:

```bash
grep "50000" *.txt
```

![grep command examples showing search results]

![alt text](<../Screenshots/grep command examples showing search results.png>)

### Step 5.3: Sort Data

The `sort` command arranges lines alphabetically or numerically:

```bash
sort employees.txt
```

Sort in reverse order:

```bash
sort -r employees.txt
```

Sort by specific field (using comma as delimiter):

```bash
sort -t',' -k2 employees.txt  # Sort by department
sort -t',' -k3 -n employees.txt  # Sort numerically by salary
```

### Step 5.4: Unique Values

The `uniq` command finds unique lines (requires sorted input):

```bash
cut -d',' -f2 employees.txt | sort | uniq
```

Count occurrences:

```bash
cut -d',' -f2 employees.txt | sort | uniq -c
```

### Step 5.5: Cut Fields

The `cut` command extracts specific columns:

```bash
cut -d',' -f1 employees.txt  # Names only
cut -d',' -f2 employees.txt  # Departments only
cut -d',' -f1,3 employees.txt  # Names and salaries
```

### Step 5.6: Word Count

Count lines, words, and characters:

```bash
wc employees.txt
wc -l employees.txt  # Lines only
```

### Step 5.7: Stream Editor with `sed`

The `sed` command performs text transformations:

Replace text:

```bash
sed 's/Developer/Engineer/' employees.txt
```

Replace globally (all occurrences per line):

```bash
sed 's/Developer/Engineer/g' employees.txt
```

Save changes to file:

```bash
sed -i 's/Manager/Lead/g' employees.txt
cat employees.txt
```

### Step 5.8: Awk for Advanced Processing

`awk` is powerful for text processing:

Print specific fields:

```bash
awk -F',' '{print $1}' employees.txt  # Names
```

Print formatted output:

```bash
awk -F',' '{print $1 " earns " $3}' employees.txt
```

Calculate average salary:

```bash
awk -F',' '{sum+=$3; count++} END {print "Average: " sum/count}' employees.txt
```

### Text Processing Commands Summary

| Command  | Purpose         | Example                |
| :------- | :-------------- | :--------------------- |
| `grep` | Search text     | `grep pattern file`  |
| `sort` | Sort lines      | `sort file`          |
| `uniq` | Unique lines    | `uniq file`          |
| `cut`  | Extract columns | `cut -d',' -f1 file` |
| `sed`  | Stream editor   | `sed 's/old/new/g'`  |
| `awk`  | Text processing | `awk '{print $1}'`   |

---

## Exercise 6: Networking Commands

In this exercise, you will learn basic networking commands.

### Step 6.1: Check Network Configuration with `ifconfig`

```bash
ifconfig
```

Or use the newer `ip` command:

```bash
ip addr show
```

These commands display network interfaces, IP addresses, and MAC addresses.

![ifconfig or ip addr show output]

![alt text](<../Screenshots/ifconfig or ip addr show output.png>)

### Step 6.2: Test Connectivity with `ping`

```bash
ping -c 4 google.com
```

![alt text](<../Screenshots/ping -c 4 google.com.png>)

The `-c 4` option sends only 4 packets. Without this, ping continues until stopped with Ctrl+C.

**Understanding ping output:**

| Metric      | Meaning                         |
| :---------- | :------------------------------ |
| time=XXms   | Round-trip time in milliseconds |
| packet loss | Percentage of lost packets      |
| ttl         | Time to live (packet lifetime)  |

### Step 6.3: Trace Network Route with `traceroute`

```bash
traceroute google.com
```

![alt text](<../Screenshots/traceroute google.com.png>)

This shows each hop (router) between your computer and the destination.

**Note:** `traceroute` may not be installed in all environments.

### Step 6.4: DNS Lookup with `nslookup` or `dig`

```bash
nslookup google.com
```

![alt text](<../Screenshots/nslookup google.com.png>)

Or use `dig`:

```bash
dig google.com
```

![alt text](<../Screenshots/dig google.com.png>)

### Step 6.5: Download Files with `wget`

```bash
wget https://www.example.com/index.html
ls
```

### Step 6.6: Transfer Files with `curl`

```bash
curl -O https://www.example.com/index.html
```

### Step 6.7: Check Network Connections with `netstat`

```bash
netstat -tulpn
```


![alt text](<../Screenshots/Check Network Connections with `netstat`.png>)


Or use the newer `ss` command:

```bash
ss -tulpn
```

This shows listening ports and active connections.

### Networking Commands Summary

| Command              | Purpose           | Example             |
| :------------------- | :---------------- | :------------------ |
| `ifconfig`/`ip`  | Network config    | `ip addr show`    |
| `ping`             | Test connectivity | `ping -c 4 host`  |
| `traceroute`       | Trace route       | `traceroute host` |
| `nslookup`/`dig` | DNS lookup        | `nslookup domain` |
| `wget`             | Download files    | `wget URL`        |
| `curl`             | Transfer data     | `curl URL`        |
| `netstat`/`ss`   | Network stats     | `ss -tulpn`       |

---

## Exercise 7: Command Combination and Pipes

In this exercise, you will learn to combine commands using pipes (`|`).

### Step 7.1: Understanding Pipes

The pipe (`|`) takes the output of one command and sends it as input to another.

### Step 7.2: Examples of Command Pipes

**Find all Developer entries and sort them:**

```bash
grep "Developer" employees.txt | sort
```

**Count how many entries contain "Developer":**

```bash
grep "Developer" employees.txt | wc -l
```

**List unique departments:**

```bash
cut -d',' -f2 employees.txt | sort | uniq
```

**Find largest files in /bin:**

```bash
ls -l /bin | sort -k5 -n -r | head -10
```

**Find processes for a specific user:**

```bash
ps aux | grep theia
```

### Step 7.3: Redirecting Output

Save command output to a file:

```bash
grep "Developer" employees.txt > developers.txt
cat developers.txt
```

Append to a file:

```bash
grep "Manager" employees.txt >> managers.txt
cat managers.txt
```

### Step 7.4: Count Files in a Directory

```bash
ls -l /bin | wc -l
```

### Step 7.5: Find Files Modified in Last 24 Hours

```bash
find ~ -type f -mtime -1
```

![alt text](<../Screenshots/Examples of Command Pipes.png>)

---

## Exercise 8: Create a Practice Script

In this exercise, you will create a simple shell script combining multiple commands.

### Step 8.1: Create a Script File

```bash
cd ~
cat > system_info.sh << 'EOF'
#!/bin/bash
# System Information Script

echo "======================================"
echo "     SYSTEM INFORMATION REPORT"
echo "======================================"
echo ""

echo "Current User: $(whoami)"
echo "Current Date: $(date "+%Y-%m-%d %H:%M:%S")"
echo "Current Directory: $(pwd)"
echo ""

echo "======================================"
echo "     DIRECTORY CONTENTS"
echo "======================================"
ls -la | head -20

echo ""
echo "======================================"
echo "     DISK USAGE"
echo "======================================"
df -h | head -10

echo ""
echo "======================================"
echo "     REPORT COMPLETE"
echo "======================================"
EOF
```

### Step 8.2: Make Script Executable

```bash
chmod +x system_info.sh
```

### Step 8.3: Run the Script

```bash
./system_info.sh
```

![System info script output]

![alt text](<../Screenshots/System info script output.png>)

---

## Exercise 9: Command Reference Card

Create your own quick reference card:

```bash
cat > linux_command_reference.txt << 'EOF'
LINUX/UNIX COMMAND REFERENCE
=============================

GENERAL COMMANDS
----------------
whoami          - Display current user
id              - Show user/group IDs
date            - Display date/time
cal             - Show calendar
uptime          - Show system uptime

DIRECTORY COMMANDS
------------------
pwd             - Print working directory
ls              - List directory contents
ls -la          - List all files (including hidden) with details
cd [dir]        - Change directory
cd ~            - Go to home directory
cd ..           - Go to parent directory
mkdir [name]    - Create directory
mkdir -p a/b/c  - Create nested directories
rmdir [dir]     - Remove empty directory

FILE COMMANDS
-------------
touch [file]    - Create empty file or update timestamp
cp [src] [dst]  - Copy file
cp -r [src] [dst] - Copy directory
mv [src] [dst]  - Move or rename file
rm [file]       - Remove file
rm -r [dir]     - Remove directory
cat [file]      - Display file contents
less [file]     - Page through file
head [file]     - Show first lines
tail [file]     - Show last lines
wc [file]       - Word count
diff [f1] [f2]  - Compare files

PERMISSION COMMANDS
-------------------
chmod 755 [file] - Set permissions (rwxr-xr-x)
chmod u+x [file] - Add execute for user
chown user [file] - Change owner
chgrp group [file] - Change group

TEXT PROCESSING
---------------
grep pattern [file] - Search for pattern
grep -i pattern [file] - Case-insensitive search
grep -c pattern [file] - Count matches
sort [file]     - Sort lines
sort -n [file]  - Numeric sort
cut -d',' -f1 [file] - Cut first field
sed 's/old/new/g' [file] - Replace text
awk '{print $1}' [file] - Print first column

NETWORK COMMANDS
----------------
ping -c 4 host  - Test connectivity
ifconfig        - Network configuration
ip addr show    - Network configuration (new)
wget URL        - Download file
curl URL        - Transfer data
nslookup domain - DNS lookup

PIPES AND REDIRECTION
---------------------
cmd1 | cmd2     - Pipe output to another command
cmd > file      - Redirect output (overwrite)
cmd >> file     - Redirect output (append)
cmd 2> file     - Redirect errors
cmd &> file     - Redirect all output

SYSTEM INFORMATION
------------------
df -h           - Disk space usage
du -sh [dir]    - Directory size
free -h         - Memory usage
ps aux          - Process list
top             - System monitor
uname -a        - System information

Created by: [Your Name]
Date: [Current Date]
EOF

cat linux_command_reference.txt
```

---

## Summary

In this hands-on lab, you have:

| Category                       | Commands Practiced                                                               | Completed |
| :----------------------------- | :------------------------------------------------------------------------------- | :-------- |
| **General Purpose**      | `whoami`, `id`, `date`, `ls`                                             | ✓        |
| **Directory Management** | `pwd`, `mkdir`, `cd`, `rmdir`, `tree`                                  | ✓        |
| **File Management**      | `touch`, `cat`, `cp`, `mv`, `rm`, `head`, `tail`, `wc`, `diff` | ✓        |
| **Access Control**       | `chmod`, `chown`, `chgrp`                                                  | ✓        |
| **Text Processing**      | `grep`, `sort`, `uniq`, `cut`, `sed`, `awk`                          | ✓        |
| **Networking**           | `ping`, `ifconfig`, `wget`, `curl`, `nslookup`                         | ✓        |
| **Command Combination**  | Pipes (`\|`), redirection (`>`, `>>`)                                       | ✓        |
| **Scripting**            | Created and ran a shell script                                                   | ✓        |
| **Reference Creation**   | Built personal command reference                                                 | ✓        |

---

<video controls src="Common Linux - Unix commands.mp4" title="Common Linux - Unix commands"></video>

## Key Takeaways

1. **Linux commands follow a pattern:** `command [options] [arguments]`
2. **Manual pages** (`man command`) provide detailed help
3. **Pipes and redirection** allow powerful command combinations
4. **File permissions** are essential for security
5. **Practice regularly** to build muscle memory for common commands

### Essential Commands to Remember

| Purpose          | Command                           |
| :--------------- | :-------------------------------- |
| Where am I?      | `pwd`                           |
| What's here?     | `ls -la`                        |
| Go somewhere     | `cd directory`                  |
| Create directory | `mkdir name`                    |
| Create file      | `touch file` or `echo > file` |
| View file        | `cat file` or `less file`     |
| Copy             | `cp source destination`         |
| Move/Rename      | `mv old new`                    |
| Delete           | `rm file` (careful!)            |
| Search           | `grep pattern file`             |
| Find help        | `man command`                   |

---

## Additional Practice Ideas

1. Create a directory structure for a project and populate it with files
2. Write a script that backs up important files to a backup directory
3. Use `grep` to search through system logs
4. Practice permission changes by creating files for different users
5. Combine `find`, `grep`, and `wc` to count specific file types

---

## Troubleshooting Tips

| Issue                               | Solution                                              |
| :---------------------------------- | :---------------------------------------------------- |
| **Command not found**         | Check spelling; command may need installation         |
| **Permission denied**         | Use `sudo` or check file permissions with `ls -l` |
| **No such file or directory** | Verify path with `pwd` and `ls`                   |
| **Can't delete directory**    | Use `rm -r` for directories with contents           |
| **Pipes not working**         | Check syntax; ensure first command produces output    |

---

## Congratulations!

You have successfully completed the **Common Linux/Unix Commands** lab. You now have hands-on experience with essential Linux commands across multiple categories. These fundamental skills are the building blocks for system administration, development, and cybersecurity tasks in Linux environments.

Remember: The best way to learn Linux commands is through regular practice. Use your command reference card and continue exploring new commands and combinations.

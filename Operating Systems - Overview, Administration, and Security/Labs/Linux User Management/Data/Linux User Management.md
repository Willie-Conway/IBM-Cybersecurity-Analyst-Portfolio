![alt text](../Screenshots/Linux.jpg)

# Hands-on Lab: Linux User Management

**Estimated time needed:** 15 minutes

---

## About This Lab

In this lab you will learn how to create users, create groups, and add users to groups within Kali Linux. Kali Linux is a well-known, open-source Linux operating system built on the Debian platform. It's tailored for professionals and learners in the field of cybersecurity and is purposefully crafted for tasks like penetration testing and ethical hacking.

---

## Learning Objectives

After completing this lab:

- You will be able to run a dockerized version of Kali Linux
- Create a user
- Create a group
- Modify the name of a group
- Add a user to a group
- Delete a user from a group
- Delete a group

---

## Prerequisites

This lab requires Docker, which is preinstalled in the Skills Network lab environment.

---

## Important Notice about this Lab Environment

Please be aware that sessions for this lab environment are **not persisted**. Every time you connect to this lab, a new environment is created for you. Any data or files you may have saved in an earlier session would get lost. Plan to complete these labs in a single session to avoid losing your data.

---

## Getting Started: Open a Terminal

1. In the Cloud IDE, click on the menu bar at the top of the screen
2. Select **Terminal → New Terminal**

![Terminal menu with New Terminal option highlighted]

![alt text](<../Screenshots/Terminal menu with New Terminal option highlighted.jpg>)

1. A new terminal window will open at the bottom of the screen

![New terminal opened at bottom of screen]

![alt text](<../Screenshots/New terminal opened at bottom of screen.png>)

1. All commands in this lab will be run in this terminal

---

## Exercise 1: Start a Kali Linux Container

Since this lab focuses on Kali Linux, we'll start by running a Kali Linux container using Docker.

### Step 1.1: Pull the Kali Linux Docker Image

```bash
docker pull kalilinux/kali-rolling
```

This command downloads the latest Kali Linux image from Docker Hub.

![Docker pull command downloading Kali Linux]

![alt text](<../Screenshots/Docker pull command downloading Kali Linux.png>)

### Step 1.2: Run the Kali Linux Container

```bash
docker run -it --name kali-lab kalilinux/kali-rolling bash
```

This command:

- `docker run` - Creates and starts a new container
- `-it` - Interactive mode with terminal
- `--name kali-lab` - Names the container "kali-lab" for easy reference
- `kalilinux/kali-rolling` - The image to use
- `bash` - Starts a bash shell inside the container

You should now see a prompt similar to:

```
root@abc123def456:/#
```

![Kali Linux container bash prompt]

![alt text](<../Screenshots/Kali Linux container bash prompt.png>)

### Step 1.3: Update Package Lists (Optional)

Inside the Kali container, update the package lists:

```bash
apt update
```

This ensures you have the latest package information, though it's not required for user management commands.

---

## Exercise 2: User and Group Management

In this exercise, you will learn the fundamental commands for managing users and groups in Linux.

### Step 2.1: Create a New User

Create a user named `guest`:

```bash
useradd guest
```

**Note:** You're already root inside the container, so `sudo` is not needed. In a regular Linux system, you would use `sudo useradd guest`.

**What this command does:** Creates a new user account with default settings. The user is created but doesn't have a password or home directory yet.

### Step 2.2: Verify User Creation

Check if the user was created:

```bash
cat /etc/passwd | grep guest
```

This should show a line like:

```
guest:x:1000:1000::/home/guest:/bin/sh
```

![Verifying user creation with cat /etc/passwd]

![alt text](<../Screenshots/Verifying user creation with cat_etc_passwd.png>)

**Understanding /etc/passwd fields (colon-separated):**

| Field    | Example     | Meaning                             |
| :------- | :---------- | :---------------------------------- |
| Username | guest       | Login name                          |
| Password | x           | Password hash stored in /etc/shadow |
| UID      | 1000        | User ID number                      |
| GID      | 1000        | Primary group ID                    |
| GECOS    | (empty)     | User info (full name, etc.)         |
| Home     | /home/guest | Home directory                      |
| Shell    | /bin/sh     | Login shell                         |

### Step 2.3: Create a New Group

Create a group named `analysts`:

```bash
groupadd analysts
```

**What this command does:** Creates a new group that can be used to manage permissions for multiple users.

### Step 2.4: Verify Group Creation

View all groups to confirm creation:

```bash
cat /etc/group | grep analysts
```

This should show:

```
analysts:x:1001:
```

Alternatively, view the entire group file:

```bash
cat /etc/group
```

![cat /etc/group showing all groups]


![alt text](<../Screenshots/cat_etc_group showing all groups.png>)

**Understanding /etc/group fields:**

| Field      | Example  | Meaning                      |
| :--------- | :------- | :--------------------------- |
| Group name | analysts | Name of the group            |
| Password   | x        | Group password (rarely used) |
| GID        | 1001     | Group ID number              |
| Members    | (empty)  | Users in the group           |

### Step 2.5: Modify the Group Name

Change the group name from `analysts` to `developers`:

```bash
groupmod -n developers analysts
```

**Command breakdown:**

- `groupmod` - Modify group
- `-n developers` - New name
- `analysts` - Current name

### Step 2.6: Verify Group Name Change

Check that the group was renamed:

```bash
cat /etc/group | grep developers
```

You should see:

```
developers:x:1001:
```

Note that the GID (1001) remains the same; only the name changed.

![Verifying group name change]

![alt text](<../Screenshots/Verifying group name change.png>)

### Step 2.7: Add User to Group

Add the user `guest` to the `developers` group:

```bash
usermod -a -G developers guest
```

**Command breakdown:**

- `usermod` - Modify user account
- `-a` - Append (add to group without removing from others)
- `-G developers` - Supplementary group to add user to
- `guest` - Username

### Step 2.8: Verify User Added to Group

Check that the user was added to the group:

```bash
groups guest
```

This should show:

```
guest : guest developers
```

Or check the group file directly:

```bash
cat /etc/group | grep developers
```

Now you should see the user listed:

```
developers:x:1001:guest
```

![Verifying user added to group]

![alt text](<../Screenshots/Verifying user added to group.png>)


### Step 2.9: Remove User from Group

Remove the user `guest` from the `developers` group:

```bash
gpasswd --delete guest developers
```

**Command breakdown:**

- `gpasswd` - Administer /etc/group and /etc/gshadow
- `--delete guest developers` - Remove user from group

### Step 2.10: Verify User Removal

Check that the user was removed:

```bash
groups guest
```

This should show only:

```
guest : guest
```

The user is no longer a member of the `developers` group.

![Verifying user removed from group]

![alt text](<../Screenshots/Verifying user removed from group.png>)

### Step 2.11: Delete the Group

Delete the `developers` group:

```bash
groupdel developers
```

**What this command does:** Permanently removes the group from the system.

### Step 2.12: Verify Group Deletion

Confirm the group no longer exists:

```bash
cat /etc/group | grep developers
```

This should return no output, confirming the group was deleted.

![Verifying group deletion - no output]

![alt text](<../Screenshots/Verifying group deletion - no output.png>)

### Step 2.13: Delete the User (Optional)

If you want to clean up completely:

```bash
userdel guest
```

To also remove the user's home directory and mail spool:

```bash
userdel -r guest
```

---

## Exercise 3: Additional User Management Commands

In this exercise, you'll explore more user management commands for practice.

### Step 3.1: Create a User with Home Directory

The `useradd` command can create a home directory automatically:

```bash
useradd -m -s /bin/bash john
```

**Command breakdown:**

- `-m` - Create home directory (/home/john)
- `-s /bin/bash` - Set login shell to bash

### Step 3.2: Set a Password

Set a password for the user:

```bash
passwd john
```

You'll be prompted to enter and confirm the password:

```
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
```

![Setting password with passwd command]

![alt text](<../Screenshots/Setting password with passwd command.png>)

### Step 3.3: Create Multiple Groups

Create several groups for different purposes:

```bash
groupadd sales
groupadd engineering
groupadd support
```

### Step 3.4: Add User to Multiple Groups

Add john to multiple groups at once:

```bash
usermod -a -G sales,engineering,support john
```

### Step 3.5: View Detailed User Information

View detailed information about a user:

```bash
id john
```

Output example:

```
uid=1001(john) gid=1002(john) groups=1002(john),1002(sales),1003(engineering),1004(support)
```

![alt text](<../Screenshots/View Detailed User Information.png>)


### Step 3.6: Lock and Unlock User Account

Lock a user account (prevent login):

```bash
passwd -l john
```

Unlock the account:

```bash
passwd -u john
```

### Step 3.7: View Login Information

View last login times:

```bash
lastlog | grep john
```

---

## Exercise 4: Understanding User and Group Files

In this exercise, you'll explore the system files that store user and group information.

### Step 4.1: Examine /etc/passwd

View the structure of the password file:

```bash
head -5 /etc/passwd
```

This shows the first 5 lines of the file.

### Step 4.2: Examine /etc/group

View the structure of the group file:

```bash
head -5 /etc/group
```

### Step 4.3: Examine /etc/shadow

View the shadow file (password hashes) - requires root:

```bash
head -5 /etc/shadow
```

**Note:** The shadow file contains encrypted passwords and is only readable by root.

### Step 4.4: Examine /etc/gshadow

View the shadow group file:

```bash
head -5 /etc/gshadow
```

![alt text](<../Screenshots/Understanding User and Group Files.png>)

---

## Exercise 5: Clean Up

### Step 5.1: Exit the Kali Container

```bash
exit
```

This exits the container and returns to your host terminal.

### Step 5.2: Stop and Remove the Container

```bash
docker stop kali-lab
docker rm kali-lab
```

![alt text](<../Screenshots/Clean Up.png>)

This cleans up the container to free resources.

---

## Command Reference Card

Create your own quick reference for user management commands:

```bash
cat > user_management_reference.txt << 'EOF'
LINUX USER MANAGEMENT COMMAND REFERENCE
=======================================

USER COMMANDS
-------------
useradd username           - Create a new user
useradd -m username       - Create user with home directory
useradd -m -s /bin/bash username - Create with bash shell
passwd username           - Set or change password
userdel username          - Delete user
userdel -r username       - Delete user and home directory
usermod -a -G group user  - Add user to group
usermod -G group1,group2 user - Set supplementary groups
id username               - Show user and group IDs
groups username           - Show groups user belongs to
passwd -l username        - Lock user account
passwd -u username        - Unlock user account
lastlog                   - Show last login times

GROUP COMMANDS
--------------
groupadd groupname        - Create a new group
groupmod -n newname oldname - Rename group
groupdel groupname        - Delete group
gpasswd --delete user group - Remove user from group

IMPORTANT FILES
---------------
/etc/passwd     - User account information
/etc/shadow     - Encrypted passwords (root only)
/etc/group      - Group information
/etc/gshadow    - Group passwords (root only)

COMMAND OPTIONS SUMMARY
-----------------------
useradd:
  -m    Create home directory
  -s    Specify login shell
  -G    Specify supplementary groups

usermod:
  -a    Append (use with -G)
  -G    Set supplementary groups
  -l    Change login name
  -L    Lock account
  -U    Unlock account

groupmod:
  -n    New name
  -g    New GID

Created by: [Your Name]
Date: [Current Date]
EOF

cat user_management_reference.txt
```

---

## Summary

In this hands-on lab, you have:

| Activity                         | Command Used                                     | Completed |
| :------------------------------- | :----------------------------------------------- | :-------- |
| Started a Kali Linux container   | `docker run -it kalilinux/kali-rolling bash`   | ✓        |
| Created a user                   | `useradd guest`                                | ✓        |
| Created a group                  | `groupadd analysts`                            | ✓        |
| Viewed user/group information    | `cat /etc/group`                               | ✓        |
| Modified a group name            | `groupmod -n developers analysts`              | ✓        |
| Added a user to a group          | `usermod -a -G developers guest`               | ✓        |
| Verified user in group           | `groups guest`                                 | ✓        |
| Removed user from group          | `gpasswd --delete guest developers`            | ✓        |
| Deleted a group                  | `groupdel developers`                          | ✓        |
| Created user with home directory | `useradd -m -s /bin/bash john`                 | ✓        |
| Set a user password              | `passwd john`                                  | ✓        |
| Added user to multiple groups    | `usermod -a -G sales,engineering,support john` | ✓        |
| Viewed detailed user info        | `id john`                                      | ✓        |
| Locked and unlocked an account   | `passwd -l / -u`                               | ✓        |
| Cleaned up the container         | `docker stop/rm`                               | ✓        |

---


<video controls src="Linux User Management.mp4" title="Linux User Management"></video>


## Key Takeaways

### Essential User Management Commands

| Task                   | Command                                 |
| :--------------------- | :-------------------------------------- |
| Create user            | `useradd username`                    |
| Create user with home  | `useradd -m username`                 |
| Set password           | `passwd username`                     |
| Delete user            | `userdel username`                    |
| Create group           | `groupadd groupname`                  |
| Rename group           | `groupmod -n newname oldname`         |
| Delete group           | `groupdel groupname`                  |
| Add user to group      | `usermod -a -G groupname username`    |
| Remove user from group | `gpasswd --delete username groupname` |
| View user groups       | `groups username`                     |
| View user details      | `id username`                         |

### Important System Files

| File             | Purpose                         |
| :--------------- | :------------------------------ |
| `/etc/passwd`  | User account information        |
| `/etc/shadow`  | Encrypted passwords (root only) |
| `/etc/group`   | Group information               |
| `/etc/gshadow` | Group passwords (root only)     |

### Best Practices

1. **Use strong passwords** - Enforce password complexity
2. **Principle of least privilege** - Give users only necessary permissions
3. **Regular audits** - Review user accounts and group memberships
4. **Remove inactive accounts** - Delete unused accounts promptly
5. **Use groups for permissions** - Manage permissions through groups, not individual users
6. **Document changes** - Keep records of user/group modifications

---

## Troubleshooting Tips

| Issue                                                     | Solution                                     |
| :-------------------------------------------------------- | :------------------------------------------- |
| **useradd: cannot lock /etc/passwd**                | Try again; another process is using the file |
| **Permission denied**                               | Use `sudo` or run as root                  |
| **User already exists**                             | Choose a different username                  |
| **Group already exists**                            | Choose a different group name                |
| **Cannot remove primary group**                     | Change user's primary group first            |
| **User still in group after removal**               | User may need to log out and back in         |
| **passwd: Authentication token manipulation error** | Run as root or with sudo                     |

---

## Additional Practice Ideas

1. Create a script that adds multiple users from a list
2. Set up group-based permissions for shared directories
3. Experiment with different useradd options (`-c` for comment, `-e` for expiry date)
4. Practice using `chown` and `chgrp` to change file ownership
5. Create a user with an expired password that must be changed on first login

---

## Congratulations!

You have successfully completed the **Linux User Management** lab. You now have hands-on experience with:

- Creating and managing user accounts
- Creating and modifying groups
- Adding and removing users from groups
- Understanding the system files that store user and group information
- Using Docker to run a Kali Linux environment

These user management skills are fundamental for Linux system administration and are essential for maintaining secure, well-organized multi-user systems.

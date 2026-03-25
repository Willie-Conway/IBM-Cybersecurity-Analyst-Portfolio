![alt text](../Screenshots/Linux.jpg)

# Hands-on Lab: Updating Linux

**Estimated time needed:** 20 minutes

---

## Learning Objectives

After completing this lab, you will know how to:

- Update package lists
- Perform Linux system upgrade

---

## Prerequisites

This lab requires Docker, which is preinstalled in the Skills Network lab environment.

---

## Important Notice about this Lab Environment

Please be aware that sessions for this lab environment are **not persisted**. Every time you connect to this lab, a new environment is created for you. Any data or files you may have saved in an earlier session would get lost. Plan to complete these labs in a single session to avoid losing your data.

---

## Introduction

Keeping your Linux system updated is one of the most important security practices you can perform. Regular updates provide:

- **Security patches** - Fix vulnerabilities before attackers can exploit them
- **Bug fixes** - Resolve issues that may cause system instability
- **New features** - Access to improved functionality
- **Performance improvements** - Optimized software and drivers

This lab covers the fundamental commands for updating Debian-based Linux distributions (Ubuntu, Debian, Kali Linux, etc.) using `apt` (Advanced Package Tool).

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

## Exercise 1: Start a Linux Container

Since this lab focuses on Linux updates, we'll start by running a Linux container using Docker.

### Step 1.1: Pull a Linux Distribution Image

Choose one of the following Debian-based images:

```bash
# Ubuntu (recommended)
docker pull ubuntu:latest

# Or Kali Linux
docker pull kalilinux/kali-rolling

# Or Debian
docker pull debian:latest
```

![Docker pull command downloading Ubuntu image]

### Step 1.2: Run the Linux Container

For Ubuntu:

```bash
docker run -it --name update-lab ubuntu:latest bash
```

For Kali Linux:

```bash
docker run -it --name update-lab kalilinux/kali-rolling bash
```

You should now see a prompt similar to:

```
root@abc123def456:/#
```

![Linux container bash prompt]

---

## Exercise 2: Understanding APT Package Management

Before updating, it's helpful to understand how APT works.

### What is APT?

**APT (Advanced Package Tool)** is the package management system used by Debian-based Linux distributions. It handles:

- Installing software
- Removing software
- Updating software
- Managing dependencies

### Key APT Commands

| Command                   | Purpose                                |
| :------------------------ | :------------------------------------- |
| `apt update`            | Update package lists from repositories |
| `apt upgrade`           | Upgrade all installed packages         |
| `apt list --upgradable` | Show packages that can be upgraded     |
| `apt install <package>` | Install a specific package             |
| `apt remove <package>`  | Remove a package                       |
| `apt autoremove`        | Remove unnecessary dependencies        |

---

## Exercise 3: Update Package Lists

The `apt update` command retrieves the latest information about available packages from the system's configured repositories.

### Step 3.1: Run Package List Update

```bash
apt update
```

**Note:** You're already root inside the container, so `sudo` is not needed. In a regular Linux system, you would use `sudo apt update`.

![apt update command output]

![alt text](<../Screenshots/apt update command output.png>)

**What this command does:**

- Connects to repositories listed in `/etc/apt/sources.list`
- Downloads information about available packages
- Updates the local package index
- Does NOT install or upgrade any packages

**Understanding the output:**

- `Hit` - Package list is up to date
- `Get` - Downloading new package information
- `Ign` - Ignoring (no changes)
- `Reading package lists... Done` - Process completed successfully

### Step 3.2: Examine Package Sources

View the repositories configured on your system:

```bash
cat /etc/apt/sources.list
```

For Ubuntu, this typically shows:

```
deb http://archive.ubuntu.com/ubuntu focal main universe
deb http://security.ubuntu.com/ubuntu focal-security main universe
```

For Kali Linux:

```
deb http://http.kali.org/kali kali-rolling main non-free contrib
```

![cat /etc/apt/sources.list output]

![alt text](<../Screenshots/cat_etc_apt_sources.list output.png>)

---

## Exercise 4: View Available Updates

After updating package lists, you can see which packages have available updates.

### Step 4.1: List Upgradable Packages

```bash
apt list --upgradable
```

**Output example:**

```
Listing... Done
base-files/focal-updates 11ubuntu5.8 amd64 [upgradable from: 11ubuntu5.7]
openssl/focal-updates 1.1.1f-1ubuntu2.20 amd64 [upgradable from: 1.1.1f-1ubuntu2.19]
python3/focal-updates 3.8.2-0ubuntu2 amd64 [upgradable from: 3.8.2-0ubuntu1]
systemd/focal-updates 245.4-4ubuntu3.22 amd64 [upgradable from: 245.4-4ubuntu3.21]
```

![apt list --upgradable output]

![alt text](<../Screenshots/apt list --upgradable output.png>)

### Step 4.2: Count Available Updates

Count how many packages need updating:

```bash
apt list --upgradable 2>/dev/null | grep -c "upgradable"
```

Or using:

```bash
apt list --upgradable 2>/dev/null | wc -l
```

### Step 4.3: Show Specific Package Information

Check details about a specific package:

```bash
apt show base-files
```

This shows:

- Package description
- Version information
- Dependencies
- Size
- Maintainer

![alt text](<../Screenshots/Count Available Updates.png>)

---

## Exercise 5: Perform System Upgrade

The `apt upgrade` command installs the latest versions of all installed packages.

### Step 5.1: Run System Upgrade

```bash
apt upgrade
```

![apt upgrade command running]

![alt text](<../Screenshots/apt upgrade command running.png>)

![alt text](<../Screenshots/apt upgrade command running_2.png>)

**What this command does:**

- Downloads and installs new versions of packages
- Resolves dependencies automatically
- Upgrades the Linux kernel (if available)
- Preserves existing configuration files

### Step 5.2: Confirm the Upgrade

When prompted:

```
After this operation, XX.X MB of additional disk space will be used.
Do you want to continue? [Y/n]
```

Type **`Y`** and press **Enter** to continue with the upgrade.

![Upgrade confirmation prompt with Y selected]

![alt text](<../Screenshots/Upgrade confirmation prompt with Y selected.png>)

### Step 5.3: Monitor the Upgrade Process

During the upgrade, you'll see:

- Downloading packages (`Get:1 ...`)
- Unpacking packages (`Preparing to unpack ...`)
- Setting up packages (`Setting up ...`)
- Processing triggers (`Processing triggers ...`)

### Step 5.4: Upgrade Completes

When complete, you'll see:

```
Processing triggers for libc-bin (2.31-0ubuntu9.16) ...
```

---

## Exercise 6: Advanced Upgrade Options

### Step 6.1: Perform a Dist-Upgrade (Optional)

`apt dist-upgrade` is more aggressive than `apt upgrade` and can remove packages if necessary:

```bash
apt dist-upgrade
```

**Difference between upgrade and dist-upgrade:**

| Command              | Behavior                                           |
| :------------------- | :------------------------------------------------- |
| `apt upgrade`      | Only upgrades packages; never removes packages     |
| `apt dist-upgrade` | May add or remove packages to resolve dependencies |

### Step 6.2: Upgrade a Specific Package

Upgrade only one package:

```bash
apt install --only-upgrade <package-name>
```

Example:

```bash
apt install --only-upgrade openssl
```

### Step 6.3: Simulate Upgrade (Dry Run)

See what would be upgraded without actually doing it:

```bash
apt upgrade --dry-run
```

Or:

```bash
apt upgrade -s
```

![alt text](<../Screenshots/Advanced Upgrade Options.png>)

---

## Exercise 7: Clean Up After Upgrades

### Step 7.1: Remove Unnecessary Packages

Remove packages that were automatically installed and are no longer needed:

```bash
apt autoremove
```

![apt autoremove output]

![alt text](<../Screenshots/apt autoremove output.png>)

### Step 7.2: Clean Package Cache

Clear downloaded package files to free disk space:

```bash
apt clean
```

Or remove only outdated packages:

```bash
apt autoclean
```

**Disk space saved:**

```bash
du -sh /var/cache/apt/archives/
```

![alt text](<../Screenshots/Clean Package Cache.png>)

---

## Exercise 8: Working with a Container

Since this is a container environment, we can't actually reboot the system, but we can simulate the experience.

### Step 8.1: Check Kernel Version

```bash
uname -a
```

If the kernel was upgraded, the new version would be active after reboot.

### Step 8.2: Check OS Version

```bash
cat /etc/os-release
```

### Step 8.3: Verify Upgrade Success

Check that packages are up to date:

```bash
apt list --upgradable 2>/dev/null
```

If no packages are listed, your system is fully updated.

![alt text](<../Screenshots/Working with a Container.png>)

---

## Exercise 9: Automation with Scripting

### Step 9.1: Create an Update Script

Create a script that performs all update tasks:

```bash
cat > update_system.sh << 'EOF'
#!/bin/bash
# System Update Script
# Created for Linux Update Lab

echo "========================================"
echo "     SYSTEM UPDATE SCRIPT"
echo "========================================"
echo ""

echo "Step 1: Updating package lists..."
apt update

echo ""
echo "Step 2: Checking for available updates..."
UPDATES=$(apt list --upgradable 2>/dev/null | grep -c "upgradable")
echo "Found $UPDATES packages with available updates."

if [ $UPDATES -gt 0 ]; then
    echo ""
    echo "Step 3: Upgrading packages..."
    apt upgrade -y
  
    echo ""
    echo "Step 4: Cleaning up..."
    apt autoremove -y
    apt autoclean
  
    echo ""
    echo "========================================"
    echo "     UPDATE COMPLETE"
    echo "========================================"
    echo "$UPDATES packages were upgraded."
else
    echo ""
    echo "========================================"
    echo "     NO UPDATES AVAILABLE"
    echo "========================================"
    echo "System is already up to date."
fi

echo ""
echo "System information:"
echo "-------------------"
uname -a
echo ""
cat /etc/os-release | grep PRETTY_NAME
EOF
```

### Step 9.2: Make Script Executable

```bash
chmod +x update_system.sh
```

### Step 9.3: Run the Script

```bash
./update_system.sh
```

![Update script running]

![alt text](<../Screenshots/Update script running.png>)

---

## Exercise 10: Command Reference Card

Create your own APT command reference:

```bash
cat > apt_reference.txt << 'EOF'
LINUX APT COMMAND REFERENCE
===========================

PACKAGE LIST MANAGEMENT
----------------------
apt update                    - Update package lists from repositories
apt list                      - List packages based on criteria
apt list --installed          - List all installed packages
apt list --upgradable         - List packages that can be upgraded
apt list --all-versions       - List all available versions

PACKAGE UPGRADE
---------------
apt upgrade                   - Upgrade all installed packages
apt upgrade <package>         - Upgrade a specific package
apt dist-upgrade              - Upgrade with dependency resolution
apt full-upgrade              - Same as dist-upgrade
apt upgrade --dry-run         - Simulate upgrade (no changes)

PACKAGE INSTALLATION
--------------------
apt install <package>         - Install a package
apt install <pkg1> <pkg2>     - Install multiple packages
apt install ./file.deb        - Install a local .deb file
apt install -y <package>      - Install without confirmation

PACKAGE REMOVAL
---------------
apt remove <package>          - Remove a package (keep config files)
apt purge <package>           - Remove package and config files
apt autoremove                - Remove unnecessary packages
apt autoremove <package>      - Remove package and dependencies

CLEANUP
-------
apt clean                     - Clear local repository cache
apt autoclean                 - Clear only outdated cache

INFORMATION
------------
apt show <package>            - Show package details
apt search <keyword>          - Search for packages
apt depends <package>         - Show package dependencies
apt rdepends <package>        - Show reverse dependencies

CONFIGURATION FILES
-------------------
/etc/apt/sources.list         - Repository configuration
/etc/apt/sources.list.d/      - Additional repository files
/var/cache/apt/archives/      - Downloaded package cache
/var/lib/apt/lists/           - Package list cache

SYSTEM INFO
-----------
uname -a                      - Show kernel version
cat /etc/os-release           - Show OS version
lsb_release -a                - Show distribution info (if installed)

Created by: [Your Name]
Date: [Current Date]
EOF

cat apt_reference.txt
```

---

## Exercise 11: Clean Up

### Step 11.1: Exit the Container

```bash
exit
```

### Step 11.2: Stop and Remove the Container

```bash
docker stop update-lab
docker rm update-lab
```

---

## Summary

In this hands-on lab, you have:

| Activity                     | Command Used                          | Completed |
| :--------------------------- | :------------------------------------ | :-------- |
| Started a Linux container    | `docker run -it ubuntu:latest bash` | ✓        |
| Updated package lists        | `apt update`                        | ✓        |
| Listed upgradable packages   | `apt list --upgradable`             | ✓        |
| Counted available updates    | `grep -c` with pipe                 | ✓        |
| Performed system upgrade     | `apt upgrade`                       | ✓        |
| Confirmed upgrade with Y     | `Y` at prompt                       | ✓        |
| Removed unnecessary packages | `apt autoremove`                    | ✓        |
| Cleaned package cache        | `apt clean` / `apt autoclean`     | ✓        |
| Checked kernel version       | `uname -a`                          | ✓        |
| Checked OS version           | `cat /etc/os-release`               | ✓        |
| Created an update script     | Script writing with `cat`           | ✓        |
| Made script executable       | `chmod +x`                          | ✓        |
| Ran the update script        | `./update_system.sh`                | ✓        |
| Created command reference    | `apt_reference.txt`                 | ✓        |
| Cleaned up container         | `docker stop/rm`                    | ✓        |

---

<video controls src="Updating Linux.mp4" title="Updating Linux"></video>

## Key Takeaways

### The Update Process

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   apt update    │────▶│ apt list        │────▶│   apt upgrade   │
│                 │     │ --upgradable    │     │                 │
│ Update package  │     │ Review available│     │ Install         │
│ lists           │     │ updates         │     │ updates         │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

### Essential Commands

| Command                   | Purpose                        |
| :------------------------ | :----------------------------- |
| `apt update`            | Refresh package information    |
| `apt list --upgradable` | See what updates are available |
| `apt upgrade`           | Install all updates            |
| `apt autoremove`        | Clean up unused dependencies   |
| `apt clean`             | Free up disk space             |

### Best Practices

1. **Update regularly** - Set a schedule (weekly at minimum)
2. **Review before upgrading** - Check what will be updated
3. **Test in non-production first** - Verify updates don't break critical applications
4. **Reboot after kernel updates** - New kernels require reboot to take effect
5. **Keep backups** - Have a recovery plan in case updates cause issues
6. **Monitor security advisories** - Prioritize security updates

### Why Updates Matter

| Risk                     | Without Updates        | With Regular Updates |
| :----------------------- | :--------------------- | :------------------- |
| Security vulnerabilities | Unpatched, exploitable | Protected            |
| System stability         | Known bugs persist     | Fixed                |
| Compatibility            | Outdated dependencies  | Modern standards     |
| Performance              | Suboptimal             | Optimized            |

---

## Troubleshooting Tips

| Issue                                                        | Solution                                               |
| :----------------------------------------------------------- | :----------------------------------------------------- |
| **"Unable to lock the administration directory"**      | Another process is using apt; wait or kill the process |
| **"Failed to fetch"**                                  | Check internet connection; verify repository URLs      |
| **"dpkg was interrupted"**                             | Run `dpkg --configure -a` to fix                     |
| **"Package not found"**                                | Run `apt update` first; check package name spelling  |
| **"Permission denied"**                                | Use `sudo` or run as root                            |
| **"You might want to run 'apt --fix-broken install'"** | Run the suggested command to fix dependencies          |

---

## Additional Practice Ideas

1. Add a new repository and install a package from it
2. Create a scheduled update script using `cron`
3. Practice using `apt-get` (the older command) and compare with `apt`
4. Research and implement unattended upgrades for automatic security updates
5. Learn about `snap` and `flatpak` as alternative package managers

---

## Additional Resources

- [APT Manual](https://manpages.debian.org/apt/apt.8)
- [Debian Package Management](https://www.debian.org/doc/manuals/debian-reference/ch02.en.html)
- [Ubuntu Package Management](https://ubuntu.com/server/docs/package-management)
- [CVE Database](https://cve.mitre.org/) - Track security vulnerabilities

---

## Congratulations!

You have successfully completed the **Updating Linux** lab. You now know how to:

- Update package lists with `apt update`
- List available updates with `apt list --upgradable`
- Perform system upgrades with `apt upgrade`
- Clean up after upgrades with `apt autoremove` and `apt clean`
- Create scripts to automate the update process
- Understand why regular updates are critical for system security

Regular system updates are one of the most effective security practices you can implement. By keeping your Linux system current, you protect it from known vulnerabilities and ensure optimal performance.

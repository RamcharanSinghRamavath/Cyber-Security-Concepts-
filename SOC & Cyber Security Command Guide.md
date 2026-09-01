

# 🐧 Kali Linux — Beginner to SOC & Cyber Security Command Guide

> A practical **Kali Linux command reference** for beginners who want to build strong Linux fundamentals and progress toward **SOC Analyst / Cyber Security** roles.

---

## 📚 Table of Contents

* [🎯 What is Kali Linux?](#-what-is-kali-linux)
* [🔄 System Update & Information](#-system-update--information)
* [📍 Navigation Commands](#-navigation-commands)
* [📂 Linux File System](#-linux-file-system)
* [📁 File & Directory Management](#-file--directory-management)
* [📝 Reading & Editing Files](#-reading--editing-files)
* [🔐 File Permissions](#-file-permissions)
* [👤 Users & Authentication](#-users--authentication)
* [⚙️ Processes](#️-processes)
* [🔧 Services](#-services)
* [🌐 Networking](#-networking)
* [🔎 Searching & Filtering](#-searching--filtering)
* [🔗 Pipes & Redirection](#-pipes--redirection)
* [📰 Linux Logs](#-linux-logs)
* [🚨 SOC Investigation](#-soc-investigation)
* [🔒 File Integrity & Hashing](#-file-integrity--hashing)
* [💽 System & Disk Investigation](#-system--disk-investigation)
* [🛡️ Security Checks](#️-security-checks)
* [⭐ SOC Command Cheat Sheet](#-soc-command-cheat-sheet)
* [📅 30-Day Learning Plan](#-30-day-learning-plan)
* [🎓 Final Learning Strategy](#-final-learning-strategy)

---

# 🎯 What is Kali Linux?

**Kali Linux** is a Debian-based Linux distribution designed primarily for:

* 🔐 Cyber Security
* 🕵️ Digital Forensics
* 🛡️ Defensive Security
* 🔎 Security Research
* 🌐 Network Analysis
* 🧪 Penetration Testing

For a SOC Analyst, Linux knowledge is especially important for:

```text
Logs
Processes
Users
Permissions
Network Connections
Services
File Systems
Incident Investigation
```

---

# 🔄 System Update & Information

## Update Package Information

```bash
sudo apt update
```

### Purpose

Updates the local package index with information about available packages.

---

## Upgrade Installed Packages

```bash
sudo apt upgrade -y
```

### Purpose

Upgrades installed packages to newer available versions.

---

## Update + Upgrade

```bash
sudo apt update && sudo apt upgrade -y
```

### Flow

```text
apt update
     ↓
Check available packages
     ↓
apt upgrade
     ↓
Install available updates
```

> **Note:** `apt update` checks for updated package information. `apt upgrade` installs available package upgrades.

---

## Check Kali Linux Version

```bash
cat /etc/os-release
```

---

## Check Kernel Version

```bash
uname -r
```

For complete kernel/system information:

```bash
uname -a
```

---

## Check Hostname

```bash
hostname
```

Detailed information:

```bash
hostnamectl
```

---

# 📍 Navigation Commands

## `pwd` — Print Working Directory

```bash
pwd
```

Shows your current location.

Example:

```text
/home/kali
```

### Remember

```text
pwd → Where am I?
```

---

## `ls` — List Files

```bash
ls
```

Displays files and directories in the current directory.

---

## `ls -l` — Detailed Listing

```bash
ls -l
```

Shows:

* File permissions
* Owner
* Group
* File size
* Modification time
* File name

---

## `ls -a` — Show Hidden Files

```bash
ls -a
```

---

## `ls -la` — Detailed + Hidden Files

```bash
ls -la
```

Example:

```text
drwxr-xr-x
-rw-r--r--
```

These permissions indicate who can:

```text
r → Read
w → Write
x → Execute
```

---

## `cd` — Change Directory

```bash
cd test
```

Moves into the `test` directory.

---

## Go Back One Directory

```bash
cd ..
```

---

## Go to Home Directory

```bash
cd ~
```

or:

```bash
cd
```

---

## Go to Root Directory

```bash
cd /
```

---

## Clear Terminal

```bash
clear
```

> `clear` only clears the visible terminal screen. It does not delete files.

---

# 📂 Linux File System

The Linux file system starts at `/`.

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
├── opt
├── root
├── tmp
├── usr
└── var
```

## Important Directories for Cyber Security

### `/etc`

Contains system configuration files.

Examples:

```text
/etc/passwd
/etc/shadow
/etc/hosts
/etc/ssh/
```

---

### `/var`

Contains frequently changing system data.

Important location:

```text
/var/log/
```

This is one of the most important directories for Linux log analysis.

---

### `/home`

Contains normal users' home directories.

Example:

```text
/home/kali
```

---

### `/tmp`

Contains temporary files.

Suspicious files can sometimes be found here during investigations.

---

### `/root`

Home directory of the root user.

---

# 📁 File & Directory Management

## `mkdir` — Create Directory

```bash
mkdir test
```

Create multiple directories:

```bash
mkdir test1 test2 test3
```

Create nested directories:

```bash
mkdir -p project/logs/security
```

---

## `rmdir` — Remove Empty Directory

```bash
rmdir test
```

---

## `touch` — Create File

```bash
touch file.txt
```

Creates an empty file if it does not exist.

Create multiple files:

```bash
touch file1.txt file2.txt file3.txt
```

### `touch` Functionality

`touch`:

* Creates an empty file if it does not exist.
* Updates access/modification timestamps if the file already exists.
* Does not normally modify the file's existing content.

---

## `rm` — Remove File

```bash
rm file.txt
```

> ⚠️ Be careful when using `rm`. Deleted files do not normally go to a recycle bin.

---

## Remove Directory Recursively

```bash
rm -r test
```

> ⚠️ Use recursive deletion carefully.

---

## `cp` — Copy File

```bash
cp file.txt backup.txt
```

Copy into another directory:

```bash
cp file.txt Documents/
```

Copy a directory:

```bash
cp -r folder1 folder2
```

---

## `mv` — Move or Rename

Rename:

```bash
mv old.txt new.txt
```

Move:

```bash
mv file.txt Documents/
```

---

## `file` — Identify File Type

```bash
file file.txt
```

Useful during security investigations:

```bash
file suspicious_file
```

A file named:

```text
invoice.pdf
```

could potentially be something other than a PDF. The `file` command helps identify the actual file type.

---

# 📝 Reading & Editing Files

## `cat` — Display File Contents

```bash
cat file.txt
```

---

## Display Multiple Files

```bash
cat file1.txt file2.txt
```

---

## `cat >` — Create/Overwrite a File

```bash
cat > file2.txt
```

Type:

```text
This file was created using the cat command.
I am Ramcharan.
I am learning Kali Linux.
```

Press:

```text
Ctrl + D
```

to finish.

### ⚠️ Important

```bash
cat > file2.txt
```

will **overwrite existing content** in the file.

---

## `cat >>` — Append to a File

```bash
cat >> file2.txt
```

Type additional content:

```text
This is Kali Linux.
```

Press:

```text
Ctrl + D
```

The new content is added without deleting the existing content.

### Difference

```text
>   → Overwrite
>>  → Append
```

---

## Combine Files

```bash
cat file.txt file2.txt
```

Displays both files sequentially.

To create a combined file:

```bash
cat file.txt file2.txt > combined.txt
```

---

## `less` — Read Large Files

```bash
less /var/log/auth.log
```

Useful controls:

```text
Space  → Next page
b      → Previous page
/word  → Search
q      → Quit
```

---

## `head` — First Lines

```bash
head file.txt
```

First 20 lines:

```bash
head -n 20 file.txt
```

---

## `tail` — Last Lines

```bash
tail file.txt
```

Last 50 lines:

```bash
tail -n 50 file.txt
```

---

## `tail -f` — Monitor Logs in Real Time

```bash
tail -f /var/log/auth.log
```

This is very useful when monitoring authentication activity.

Stop:

```text
Ctrl + C
```

---

## `nano` — Text Editor

```bash
nano file.txt
```

Important shortcuts:

```text
Ctrl + O → Save
Enter    → Confirm
Ctrl + X → Exit
```

---

# 🔐 File Permissions

Check permissions:

```bash
ls -l
```

Example:

```text
-rwxr-xr--
```

Breakdown:

```text
Owner  → rwx
Group  → r-x
Others → r--
```

Permission values:

```text
r = 4
w = 2
x = 1
```

Therefore:

```text
7 = rwx
6 = rw-
5 = r-x
4 = r--
```

---

## `chmod` — Change Permissions

Make a script executable:

```bash
chmod +x script.sh
```

Numeric permissions:

```bash
chmod 755 script.sh
```

Meaning:

```text
Owner  → rwx → 7
Group  → r-x → 5
Others → r-x → 5
```

---

## `chown` — Change Ownership

```bash
sudo chown user1 file.txt
```

Change owner and group:

```bash
sudo chown user1:group1 file.txt
```

Check ownership:

```bash
ls -l file.txt
```

---

# 👤 Users & Authentication

## `whoami`

```bash
whoami
```

Shows the current user.

---

## `id`

```bash
id
```

Shows:

* UID
* GID
* Group membership

---

## `who`

```bash
who
```

Shows currently logged-in users.

---

## `w`

```bash
w
```

Shows logged-in users and their current activity.

---

## `last`

```bash
last
```

Shows login history.

Useful SOC questions:

```text
Who logged in?
When did they log in?
Was the login expected?
```

---

## `lastb`

```bash
sudo lastb
```

Shows failed login attempts when the relevant database is available.

---

## `/etc/passwd`

```bash
cat /etc/passwd
```

Contains information about local user accounts.

Display usernames:

```bash
cut -d: -f1 /etc/passwd
```

---

## `sudo`

```bash
sudo command
```

Runs a command with elevated privileges if the user is authorized.

Example:

```bash
sudo apt update
```

---

# ⚙️ Processes

A **process** is a running instance of a program.

Examples:

```text
Browser
SSH
Apache
MySQL
Wazuh Agent
```

---

## `ps`

```bash
ps
```

Show detailed processes:

```bash
ps aux
```

Important fields can include:

```text
USER
PID
%CPU
%MEM
COMMAND
```

---

## Search Processes

```bash
ps aux | grep ssh
```

---

## `top`

```bash
top
```

Provides real-time process and resource information.

Exit:

```text
q
```

---

## `htop`

```bash
htop
```

Interactive process viewer.

> It may need to be installed separately.

---

## `kill`

```bash
kill PID
```

Example:

```bash
kill 1234
```

Force termination:

```bash
kill -9 1234
```

> ⚠️ Use `kill -9` carefully. It forcefully terminates a process.

---

# 🔧 Services

Linux services are background programs that provide functionality.

Examples:

```text
SSH
Apache
MySQL
Wazuh Agent
```

---

## Check Service Status

```bash
systemctl status ssh
```

---

## Start Service

```bash
sudo systemctl start ssh
```

---

## Stop Service

```bash
sudo systemctl stop ssh
```

---

## Restart Service

```bash
sudo systemctl restart ssh
```

---

## Enable Service at Boot

```bash
sudo systemctl enable ssh
```

---

## List Running Services

```bash
systemctl list-units --type=service --state=running
```

This can help identify unexpected services during investigation.

---

# 🌐 Networking

Networking knowledge is essential for SOC analysts.

Important concepts:

```text
IP Address
    ↓
Port
    ↓
Protocol
    ↓
Connection
    ↓
Network Log
    ↓
Security Alert
```

---

## `ip addr`

```bash
ip addr
```

or:

```bash
ip a
```

Displays network interfaces and IP addresses.

---

## `ip route`

```bash
ip route
```

Displays the routing table.

---

## `hostname -I`

```bash
hostname -I
```

Displays the system's IP addresses.

---

## `ping`

```bash
ping 8.8.8.8
```

Tests network connectivity.

Stop:

```text
Ctrl + C
```

---

## `ss` — Network Connections

```bash
ss -tulnp
```

Useful for identifying:

* Listening ports
* TCP connections
* UDP sockets
* Associated processes

This is a very useful SOC investigation command.

---

## `netstat`

```bash
netstat -tulnp
```

> `netstat` may require the `net-tools` package on modern Linux systems.

---

## `curl`

```bash
curl https://example.com
```

Display HTTP headers:

```bash
curl -I https://example.com
```

Useful for troubleshooting and understanding HTTP responses.

---

## `wget`

```bash
wget https://example.com/file.txt
```

Downloads a file from a URL.

> Only download files from trusted or authorized sources.

---

# 🔎 Searching & Filtering

## `grep`

Search for text:

```bash
grep "error" file.txt
```

Case-insensitive:

```bash
grep -i "error" file.txt
```

Show line numbers:

```bash
grep -n "error" file.txt
```

Recursive search:

```bash
grep -r "password" /etc/
```

---

## Search Authentication Failures

```bash
sudo grep "Failed password" /var/log/auth.log
```

---

## Search Successful SSH Authentication

```bash
sudo grep "Accepted" /var/log/auth.log
```

---

## Count Matches

```bash
grep -c "Failed password" /var/log/auth.log
```

---

## `find`

Find a file:

```bash
find /home -name "file.txt"
```

Find log files:

```bash
find /var/log -name "*.log"
```

Find recently modified files:

```bash
find /tmp -type f -mtime -1
```

---

## `locate`

```bash
locate file.txt
```

Update database:

```bash
sudo updatedb
```

---

# 🔗 Pipes & Redirection

## Pipe `|`

A pipe sends the output of one command into another command.

Example:

```bash
ps aux | grep ssh
```

Flow:

```text
ps aux
   ↓
Process list
   ↓
grep ssh
   ↓
SSH-related results
```

---

## `>`

Redirect output to a file:

```bash
ls > files.txt
```

⚠️ Overwrites existing content.

---

## `>>`

Append output:

```bash
date >> investigation.txt
```

---

## `2>`

Redirect errors:

```bash
command 2> errors.txt
```

---

## Redirect Output + Errors

```bash
command > output.txt 2>&1
```

---

# 🧮 Text Processing

## `cut`

Extract fields:

```bash
cut -d: -f1 /etc/passwd
```

Here:

```text
-d: → delimiter is :
-f1 → select field 1
```

---

## `sort`

```bash
sort file.txt
```

Reverse order:

```bash
sort -r file.txt
```

---

## `uniq`

```bash
uniq file.txt
```

Count repeated values:

```bash
sort file.txt | uniq -c
```

---

## `awk`

Print the first column:

```bash
awk '{print $1}' file.txt
```

`awk` becomes particularly useful when parsing structured logs.

---

# 📰 Linux Logs

Logs are records of system and application events.

Common sources include:

```text
Operating System
Applications
Servers
Authentication Systems
Firewalls
IDS/IPS
Endpoints
SIEM
```

Important directory:

```text
/var/log/
```

---

## Common Linux Logs

Depending on the distribution and configuration:

```text
/var/log/auth.log
/var/log/syslog
/var/log/messages
/var/log/kern.log
/var/log/dpkg.log
```

> Some modern Linux systems use `systemd-journald` and `journalctl` instead of, or alongside, traditional text log files.

---

## View Authentication Logs

```bash
sudo less /var/log/auth.log
```

---

## Search Failed Logins

```bash
sudo grep "Failed password" /var/log/auth.log
```

---

## Search Successful Logins

```bash
sudo grep "Accepted" /var/log/auth.log
```

---

## Monitor Authentication Logs

```bash
sudo tail -f /var/log/auth.log
```

---

# 📖 `journalctl`

View system journal:

```bash
journalctl
```

---

## Recent Logs

```bash
journalctl -n 50
```

---

## Follow Logs in Real Time

```bash
journalctl -f
```

---

## Service Logs

```bash
journalctl -u ssh
```

---

## Today's Logs

```bash
journalctl --since today
```

---

# 🔒 File Integrity & Hashing

Hashes provide a fixed-length representation of file data.

Common uses:

```text
File Identification
Integrity Verification
Malware Investigation
Evidence Comparison
```

---

## SHA-256

```bash
sha256sum file.exe
```

Example:

```text
HASH_VALUE  file.exe
```

During an investigation:

```text
Suspicious File
      ↓
Calculate SHA-256
      ↓
Record Hash
      ↓
Compare Against Trusted Intelligence
      ↓
Continue Investigation
```

---

## MD5

```bash
md5sum file.txt
```

> MD5 has known collision weaknesses and should not be relied upon as a modern cryptographic integrity mechanism where stronger hashes such as SHA-256 are available.

---

# 💽 System & Disk Investigation

## Disk Usage

```bash
df -h
```

---

## Directory Size

```bash
du -sh foldername
```

---

## Memory Usage

```bash
free -h
```

---

## System Uptime

```bash
uptime
```

---

# 🛡️ Basic Security Checks

## Current User

```bash
whoami
```

---

## User Information

```bash
id
```

---

## Logged-in Users

```bash
who
```

---

## Login History

```bash
last
```

---

## Failed Login History

```bash
sudo lastb
```

---

## Running Processes

```bash
ps aux
```

---

## Listening Ports

```bash
sudo ss -tulnp
```

---

## Running Services

```bash
systemctl list-units --type=service --state=running
```

---

## Recently Modified Files

```bash
find /tmp -type f -mtime -1
```

> A finding is not automatically malicious. Always investigate it in context.

---

# 🚨 SOC Investigation Scenario

## Scenario: Multiple SSH Login Failures

Imagine your monitoring system generates:

```text
🚨 ALERT

Multiple SSH authentication failures detected.

Source IP: 192.168.1.50
Username: admin
Service: SSH
```

Your investigation should follow:

```text
Alert
  ↓
Identify Host
  ↓
Identify Source IP
  ↓
Check Authentication Logs
  ↓
Count Failed Attempts
  ↓
Check Successful Authentication
  ↓
Review Login History
  ↓
Check Processes
  ↓
Check Network Connections
  ↓
Determine Severity
  ↓
Document & Escalate
```

---

## Step 1 — Search the Source IP

```bash
sudo grep "192.168.1.50" /var/log/auth.log
```

---

## Step 2 — Search Failed Passwords

```bash
sudo grep "Failed password" /var/log/auth.log
```

---

## Step 3 — Count Attempts

```bash
sudo grep -c "192.168.1.50" /var/log/auth.log
```

---

## Step 4 — Check Successful Authentication

```bash
sudo grep "Accepted" /var/log/auth.log
```

Ask:

```text
Did the suspicious source eventually authenticate successfully?
```

---

## Step 5 — Check Login History

```bash
last
```

---

## Step 6 — Check Failed Login History

```bash
sudo lastb
```

---

## Step 7 — Check Running Processes

```bash
ps aux
```

Look for:

```text
Unknown processes
Unexpected processes
Unusual execution locations
High CPU usage
High memory usage
```

---

## Step 8 — Check Network Connections

```bash
sudo ss -tulnp
```

Look for:

```text
Unknown listening ports
Unexpected services
Unexpected connections
Unknown processes
```

---

# 🧠 SOC Investigation Questions

When investigating an alert, don't just run commands.

Ask:

### ❓ WHO?

```text
Which user is involved?
Who logged in?
Who started the process?
```

### ❓ WHAT?

```text
What happened?
What process executed?
What file changed?
What connection was created?
```

### ❓ WHEN?

```text
When did the event happen?
Was it during normal working hours?
```

### ❓ WHERE?

```text
Which host?
Which directory?
Which source IP?
Which destination?
```

### ❓ WHY?

```text
Is this expected behavior?
Could it be legitimate administration?
Is there evidence of compromise?
```

### ❓ HOW?

```text
How did the activity occur?
How did the user authenticate?
How was the process launched?
```

---

# 🔥 Useful SOC Command Combinations

## Find SSH Processes

```bash
ps aux | grep ssh
```

---

## Find Failed SSH Logins

```bash
sudo grep "Failed password" /var/log/auth.log
```

---

## Find Successful SSH Logins

```bash
sudo grep "Accepted" /var/log/auth.log
```

---

## Count Failed SSH Attempts

```bash
sudo grep "Failed password" /var/log/auth.log | wc -l
```

---

## Extract Source IPs

Depending on the exact log format:

```bash
sudo grep "Failed password" /var/log/auth.log
```

Then use appropriate parsing tools such as:

```bash
awk
cut
grep
sort
uniq
```

Example pattern for many OpenSSH logs:

```bash
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}'
```

> Always verify the log format before relying on a field position. Log formats can vary.

---

# 🧰 Essential Command Categories

| Category       | Important Commands                 |
| -------------- | ---------------------------------- |
| 📍 Navigation  | `pwd`, `ls`, `cd`                  |
| 📁 Files       | `touch`, `mkdir`, `cp`, `mv`, `rm` |
| 📖 Reading     | `cat`, `less`, `head`, `tail`      |
| 🔎 Search      | `grep`, `find`, `locate`           |
| 🔐 Permissions | `chmod`, `chown`                   |
| 👤 Users       | `whoami`, `id`, `who`, `w`, `last` |
| ⚙️ Processes   | `ps`, `top`, `htop`, `kill`        |
| 🔧 Services    | `systemctl`, `journalctl`          |
| 🌐 Networking  | `ip`, `ping`, `ss`, `curl`, `wget` |
| 📰 Logs        | `grep`, `tail`, `journalctl`       |
| 🧮 Parsing     | `awk`, `cut`, `sort`, `uniq`       |
| 🔒 Integrity   | `sha256sum`, `md5sum`              |
| 💽 System      | `df`, `du`, `free`, `uptime`       |

---

# ⭐ SOC Analyst Command Cheat Sheet

```bash
# ─────────────────────────────
# SYSTEM
# ─────────────────────────────

cat /etc/os-release
uname -a
hostname
hostnamectl
uptime


# ─────────────────────────────
# NAVIGATION
# ─────────────────────────────

pwd
ls
ls -la
cd directory
cd ..
cd ~
cd /


# ─────────────────────────────
# FILES
# ─────────────────────────────

mkdir test
touch file.txt
cp file.txt backup.txt
mv old.txt new.txt
rm file.txt
file suspicious_file


# ─────────────────────────────
# FILE CONTENT
# ─────────────────────────────

cat file.txt
less file.txt
head file.txt
tail file.txt
tail -f file.txt
nano file.txt


# ─────────────────────────────
# PERMISSIONS
# ─────────────────────────────

ls -l
chmod +x script.sh
chmod 755 script.sh
chown user1 file.txt


# ─────────────────────────────
# USERS
# ─────────────────────────────

whoami
id
who
w
last
sudo lastb


# ─────────────────────────────
# PROCESSES
# ─────────────────────────────

ps aux
ps aux | grep ssh
top
htop
kill PID


# ─────────────────────────────
# SERVICES
# ─────────────────────────────

systemctl status ssh
systemctl start ssh
systemctl stop ssh
systemctl restart ssh
systemctl list-units --type=service --state=running


# ─────────────────────────────
# NETWORKING
# ─────────────────────────────

ip addr
ip route
hostname -I
ping 8.8.8.8
ss -tulnp
curl -I https://example.com


# ─────────────────────────────
# SEARCH
# ─────────────────────────────

grep "error" file.txt
grep -i "error" file.txt
grep -n "error" file.txt
find /home -name "*.txt"


# ─────────────────────────────
# LOGS
# ─────────────────────────────

sudo less /var/log/auth.log
sudo grep "Failed password" /var/log/auth.log
sudo grep "Accepted" /var/log/auth.log
sudo tail -f /var/log/auth.log
journalctl
journalctl -f
journalctl -u ssh


# ─────────────────────────────
# TEXT PROCESSING
# ─────────────────────────────

cut -d: -f1 /etc/passwd
sort file.txt
sort file.txt | uniq -c
awk '{print $1}' file.txt


# ─────────────────────────────
# FILE INTEGRITY
# ─────────────────────────────

sha256sum file.exe
md5sum file.txt


# ─────────────────────────────
# SYSTEM
# ─────────────────────────────

df -h
du -sh folder
free -h
```

---

# 📅 30-Day Kali Linux → SOC Learning Plan

## 🟢 Week 1 — Linux Fundamentals

Learn:

```text
pwd
ls
cd
mkdir
touch
cp
mv
rm
cat
nano
```

### Practice

Create:

```text
cyber-lab/
├── logs/
├── evidence/
├── scripts/
└── reports/
```

---

## 🟡 Week 2 — Users, Permissions & Processes

Learn:

```text
chmod
chown
whoami
id
who
w
last
ps
top
systemctl
```

Practice:

```text
Create users
Check permissions
Identify processes
Check running services
Review login history
```

---

## 🟠 Week 3 — Networking & Logs

Learn:

```text
ip
ping
ss
curl
grep
tail
journalctl
```

Practice:

```text
Find your IP
Check routes
Identify listening ports
Monitor authentication logs
Search failed logins
Search successful logins
```

---

## 🔴 Week 4 — SOC Investigation

Practice scenarios:

```text
1. Multiple failed SSH logins
2. Suspicious successful login
3. Unknown process
4. Unexpected listening port
5. Suspicious file
6. Recently modified files
7. High CPU process
8. Unexpected service
```

For every scenario:

```text
Identify
   ↓
Collect Evidence
   ↓
Analyze
   ↓
Determine Impact
   ↓
Document
   ↓
Escalate / Respond
```

---

# 🧠 Command Memory Map

```text
                    🐧 LINUX
                       │
        ┌──────────────┼──────────────┐
        │              │              │
      📂 Files       👤 Users       ⚙️ Processes
        │              │              │
   ls / cd / pwd    whoami / id    ps / top
   mkdir / touch    who / last     kill
   cp / mv / rm
        │
        ▼
   🔎 Analysis
        │
 cat / less / grep / find
 awk / cut / sort / uniq
        │
   ┌────┴─────┐
   ▼          ▼
🌐 Network   📰 Logs
   │          │
 ip / ss     grep
 ping        tail
 curl        journalctl
   │          │
   └────┬─────┘
        ▼
   🛡️ SOC ANALYSIS
        │
 Identify
        ↓
 Investigate
        ↓
 Analyze
        ↓
 Document
        ↓
 Escalate
```

---

# 🎓 The SOC Analyst Mindset

Don't learn Linux commands only by memorizing syntax.

Instead, understand:

```text
WHAT?
   ↓
What does this command do?

WHY?
   ↓
Why am I running it?

WHERE?
   ↓
Where is the evidence?

WHEN?
   ↓
When did the event happen?

WHO?
   ↓
Who performed the action?

HOW?
   ↓
How did the activity occur?

WHAT NEXT?
   ↓
Should I investigate or escalate?
```

For example, don't simply memorize:

```bash
grep "Failed password" /var/log/auth.log
```

Understand the investigation:

```text
🚨 Alert
   ↓
Multiple authentication failures
   ↓
Search auth.log
   ↓
Identify username
   ↓
Identify source IP
   ↓
Count attempts
   ↓
Check for successful login
   ↓
Check login history
   ↓
Check processes
   ↓
Check network connections
   ↓
Document findings
```

That is how you progress from:

```text
🐧 Linux Beginner
       ↓
🖥️ Linux User
       ↓
🔐 Security Learner
       ↓
🛡️ SOC Analyst
       ↓
🚨 Incident Responder
       ↓
🔎 Cyber Security Professional
```

---

# 🚀 Next-Level Learning Path

```text
🐧 Linux Fundamentals
        ↓
📂 Linux File System
        ↓
🔐 Permissions & Users
        ↓
⚙️ Processes & Services
        ↓
🌐 Networking
        ↓
📰 Linux Logs
        ↓
🔎 grep / awk / sed / cut
        ↓
🛡️ Security Fundamentals
        ↓
📊 SIEM
        ↓
🐺 Wazuh
        ↓
🚨 Alert Triage
        ↓
🔍 Log Analysis
        ↓
🧪 Incident Investigation
        ↓
📋 Incident Response
        ↓
🎯 SOC Analyst
```

---

## ⭐ Recommended Practice

Create a safe local Linux lab and practice commands on systems you own or are explicitly authorized to test.

> **Never use security commands against systems without authorization.**

---

# 👨‍💻 Author

**Ramcharan Singh Ramavath**

Learning:

```text
Linux
Cyber Security
SOC Monitoring
SIEM
Wazuh
Networking
Incident Response
```

---


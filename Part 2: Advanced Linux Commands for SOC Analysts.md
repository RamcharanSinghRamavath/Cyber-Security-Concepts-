
# 🛡️ Kali Linux — Part 2: Advanced Linux Commands for SOC Analysts

> Advanced Linux command reference for **SOC Analysts, Cyber Security Analysts, Incident Responders, and Blue Team learners**.

---

## 📚 Table of Contents

* [🎯 What You Will Learn](#-what-you-will-learn)
* [🧠 SOC Analyst Command Mindset](#-soc-analyst-command-mindset)
* [🔗 Pipes & Advanced Redirection](#-pipes--advanced-redirection)
* [🔎 Advanced grep](#-advanced-grep)
* [🧮 Advanced awk](#-advanced-awk)
* [✂️ cut, tr & sed](#️-cut-tr--sed)
* [📊 sort, uniq & wc](#-sort-uniq--wc)
* [🔍 Advanced find](#-advanced-find)
* [📁 File Metadata](#-file-metadata)
* [🔐 Permissions Investigation](#-permissions-investigation)
* [👤 User & Account Investigation](#-user--account-investigation)
* [⚙️ Process Investigation](#️-process-investigation)
* [🔧 Service Investigation](#-service-investigation)
* [🌐 Advanced Network Investigation](#-advanced-network-investigation)
* [🔌 Ports & Connections](#-ports--connections)
* [📰 Advanced Log Analysis](#-advanced-log-analysis)
* [🚨 SSH Investigation](#-ssh-investigation)
* [🧪 Suspicious File Investigation](#-suspicious-file-investigation)
* [🔒 File Hashing](#-file-hashing)
* [⏱️ Timeline Analysis](#️-timeline-analysis)
* [📦 Archives & Evidence](#-archives--evidence)
* [💾 Disk Investigation](#-disk-investigation)
* [🧠 Environment & Shell Investigation](#-environment--shell-investigation)
* [📜 Command History Investigation](#-command-history-investigation)
* [🛡️ Persistence Investigation](#️-persistence-investigation)
* [🚨 SOC Investigation Workflow](#-soc-investigation-workflow)
* [🎯 Practical SOC Scenarios](#-practical-soc-scenarios)
* [⭐ Advanced SOC Cheat Sheet](#-advanced-soc-cheat-sheet)
* [📅 30-Day Advanced Practice Plan](#-30-day-advanced-practice-plan)

---

# 🎯 What You Will Learn

Part 1 covered Linux fundamentals.

Part 2 focuses on using Linux as a **security investigation platform**.

You will learn how to investigate:

```text
🔐 Authentication
🌐 Network Connections
⚙️ Processes
🔧 Services
📁 Files
📰 Logs
👤 Users
⏱️ Timelines
🔒 File Integrity
🚨 Suspicious Activity
🛡️ Persistence
```

The goal is not simply to memorize commands.

The goal is:

```text
Command
   ↓
Evidence
   ↓
Analysis
   ↓
Security Decision
```

---

# 🧠 SOC Analyst Command Mindset

When an alert arrives, think in this order:

```text
WHO?
 ↓
WHAT?
 ↓
WHEN?
 ↓
WHERE?
 ↓
HOW?
 ↓
WHAT ELSE?
 ↓
IMPACT?
 ↓
ESCALATE?
```

Example:

```text
🚨 Multiple SSH failures

WHO?
→ Which username?

WHAT?
→ Authentication failures

WHEN?
→ What time?

WHERE?
→ Which source IP?

HOW?
→ SSH authentication

WHAT ELSE?
→ Was there a successful login?

IMPACT?
→ Did the account access anything?

ESCALATE?
→ Is compromise suspected?
```

---

# 🔗 Pipes & Advanced Redirection

Pipes are one of the most important Linux skills for SOC analysts.

## `|` — Pipe

```bash
ps aux | grep ssh
```

Flow:

```text
ps aux
   ↓
All processes
   ↓
grep ssh
   ↓
SSH-related processes
```

---

## Multiple Pipes

```bash
ps aux | grep ssh | grep -v grep
```

The final output removes the `grep ssh` process itself.

---

## Save Investigation Output

```bash
ps aux > processes.txt
```

Append:

```bash
ps aux >> investigation.txt
```

---

## Redirect Errors

```bash
find /etc -name "*.conf" 2> errors.txt
```

---

## Output + Error

```bash
command > output.txt 2>&1
```

---

## `tee` — Display and Save

```bash
ps aux | tee processes.txt
```

This:

```text
Displays output
      +
Saves output
```

Very useful during investigations.

Example:

```bash
sudo ss -tulnp | tee network_connections.txt
```

---

# 🔎 Advanced grep

`grep` is one of the most important SOC commands.

---

## Case-Insensitive Search

```bash
grep -i "failed" file.log
```

---

## Show Line Numbers

```bash
grep -n "Failed password" /var/log/auth.log
```

---

## Search Multiple Patterns

```bash
grep -E "failed|invalid|error" file.log
```

---

## Search Multiple Files

```bash
grep "Failed password" /var/log/*.log
```

---

## Recursive Search

```bash
grep -r "suspicious" /var/log/
```

---

## Show Lines Before Match

```bash
grep -B 3 "Failed password" file.log
```

---

## Show Lines After Match

```bash
grep -A 3 "Failed password" file.log
```

---

## Show Context

```bash
grep -C 3 "Failed password" file.log
```

---

## Invert Match

```bash
grep -v "INFO" file.log
```

Shows everything except lines containing `INFO`.

---

## Count Matches

```bash
grep -c "Failed password" file.log
```

---

## Exact Word Matching

```bash
grep -w "root" file.log
```

---

# 🧮 Advanced awk

`awk` is extremely useful for structured log analysis.

Basic example:

```bash
awk '{print $1}' file.log
```

Print first field.

---

## Print Multiple Fields

```bash
awk '{print $1, $2, $3}' file.log
```

---

## Filter by Field

```bash
awk '$3 == "ERROR" {print}' application.log
```

---

## Search for Specific IP

```bash
awk '$0 ~ /192.168.1.50/' file.log
```

---

## Count Values

Example:

```bash
awk '{print $1}' access.log | sort | uniq -c
```

Possible output:

```text
25 192.168.1.10
18 192.168.1.20
7  192.168.1.50
```

This can help identify frequently appearing source IPs.

---

# ✂️ cut, tr & sed

## `cut`

Extract a field:

```bash
cut -d: -f1 /etc/passwd
```

Explanation:

```text
-d: → delimiter is :
-f1 → first field
```

---

## Extract IP-related Fields

For structured text:

```bash
cut -d' ' -f1 access.log
```

> Always verify the actual log format before assuming a particular field contains an IP address.

---

# 🔄 tr

Translate characters:

```bash
echo "HELLO" | tr 'A-Z' 'a-z'
```

Output:

```text
hello
```

Remove characters:

```bash
echo "123-456-789" | tr -d '-'
```

Output:

```text
123456789
```

---

# 📝 sed

Display selected lines:

```bash
sed -n '1,10p' file.txt
```

Search and replace:

```bash
sed 's/old/new/g' file.txt
```

Remove blank lines:

```bash
sed '/^$/d' file.txt
```

> When investigating evidence, avoid modifying the original evidence file. Perform transformations on a copy.

---

# 📊 sort, uniq & wc

## `sort`

```bash
sort file.txt
```

Reverse:

```bash
sort -r file.txt
```

Numeric:

```bash
sort -n file.txt
```

---

## `uniq`

```bash
sort file.txt | uniq
```

Count duplicates:

```bash
sort file.txt | uniq -c
```

---

## Most Frequent Values

```bash
sort file.txt | uniq -c | sort -nr
```

This is a very useful SOC pattern.

Flow:

```text
Raw Data
   ↓
sort
   ↓
Group duplicates
   ↓
uniq -c
   ↓
Count
   ↓
sort -nr
   ↓
Most frequent first
```

---

## `wc`

Count lines:

```bash
wc -l file.log
```

Count words:

```bash
wc -w file.txt
```

Count characters:

```bash
wc -m file.txt
```

---

# 🔍 Advanced find

## Find Files by Name

```bash
find /home -name "*.log"
```

---

## Case-Insensitive Name Search

```bash
find /home -iname "*.LOG"
```

---

## Find Regular Files

```bash
find /tmp -type f
```

---

## Find Directories

```bash
find /tmp -type d
```

---

## Recently Modified Files

```bash
find /tmp -type f -mtime -1
```

---

## Recently Modified Within Minutes

```bash
find /tmp -type f -mmin -60
```

Find files modified within approximately the last hour.

---

## Large Files

```bash
find /home -type f -size +100M
```

---

## Empty Files

```bash
find /tmp -type f -empty
```

---

## Find Files with Specific Permissions

```bash
find /home -type f -perm -4000
```

This searches for files with the SUID bit set.

> SUID files are not automatically malicious. They should be reviewed against expected system configuration.

---

# 📁 File Metadata

## Detailed File Information

```bash
stat file.txt
```

Provides metadata such as:

```text
File
Size
Permissions
Owner
Access time
Modify time
Change time
```

---

## Why Metadata Matters

During incident response:

```text
Suspicious File
      ↓
stat
      ↓
Creation/modification-related timestamps
      ↓
Compare with incident timeline
```

> Linux filesystems do not universally expose a simple "creation time"; timestamp availability depends on filesystem and tooling. `stat` shows the timestamps supported by the filesystem.

---

# 🔐 Permissions Investigation

Check permissions:

```bash
ls -l suspicious_file
```

Check numeric permissions:

```bash
stat -c "%a %n" suspicious_file
```

Find SUID files:

```bash
sudo find / -type f -perm -4000 2>/dev/null
```

Find SGID files:

```bash
sudo find / -type f -perm -2000 2>/dev/null
```

Investigate unusual writable directories:

```bash
find /tmp -type f -writable
```

> Review findings carefully. Some writable files and SUID/SGID binaries are normal system components.

---

# 👤 User & Account Investigation

## Current User

```bash
whoami
```

---

## User ID

```bash
id
```

---

## Logged-In Users

```bash
who
```

---

## User Activity

```bash
w
```

---

## Login History

```bash
last
```

---

## Failed Login Attempts

```bash
sudo lastb
```

---

## List Usernames

```bash
cut -d: -f1 /etc/passwd
```

---

## Check Shells

```bash
cat /etc/shells
```

---

## Check Current User's Groups

```bash
groups
```

---

## Check sudo Configuration

```bash
sudo -l
```

Shows commands the current user is permitted to run through `sudo`.

> Use only on systems you are authorized to administer or investigate.

---

# ⚙️ Process Investigation

Processes are extremely important during incident response.

---

## List Processes

```bash
ps aux
```

---

## Full Process Tree

```bash
pstree
```

If installed:

```bash
pstree -p
```

This helps visualize parent-child relationships.

---

## Search for a Process

```bash
ps aux | grep nginx
```

---

## Find Process by Name

```bash
pgrep nginx
```

---

## Show Process Details

```bash
ps -p PID -f
```

Example:

```bash
ps -p 1234 -f
```

---

## Inspect Process Directory

```bash
sudo ls -l /proc/1234/
```

---

## Check Executable

```bash
sudo readlink -f /proc/1234/exe
```

---

## Check Process Command Line

```bash
sudo tr '\0' ' ' < /proc/1234/cmdline
```

---

## Check Process Environment

```bash
sudo tr '\0' '\n' < /proc/1234/environ
```

> Access to some `/proc` information may require elevated privileges.

---

# 🔧 Service Investigation

## List Running Services

```bash
systemctl list-units --type=service --state=running
```

---

## Check Service

```bash
systemctl status ssh
```

---

## View Service Logs

```bash
journalctl -u ssh
```

---

## List Failed Services

```bash
systemctl --failed
```

---

## Check Service Configuration

```bash
systemctl cat ssh
```

This can help identify:

```text
Executable
Arguments
User
Environment
Dependencies
```

---

# 🌐 Advanced Network Investigation

Networking is a major part of SOC analysis.

Important questions:

```text
What IP?
What port?
What protocol?
Which process?
Which user?
Inbound or outbound?
Expected or unexpected?
```

---

## Show Interfaces

```bash
ip addr
```

---

## Show Routing Table

```bash
ip route
```

---

## Show Neighbor Table

```bash
ip neigh
```

This can show nearby Layer-2/ARP neighbor information.

---

## Show Listening Ports

```bash
sudo ss -tulnp
```

---

## Show Established Connections

```bash
sudo ss -tunp
```

---

## Show TCP Connections

```bash
sudo ss -tnp
```

---

## Show UDP Sockets

```bash
sudo ss -unp
```

---

## Search for a Specific Port

```bash
sudo ss -tulnp | grep ':22'
```

---

## Search for a Specific IP

```bash
sudo ss -tunp | grep '192.168.1.50'
```

---

# 🔌 Ports & Connections

Common ports you should recognize:

| Port | Protocol / Service | Common Purpose               |
| ---: | ------------------ | ---------------------------- |
|   22 | SSH                | Secure remote administration |
|   23 | Telnet             | Remote terminal              |
|   25 | SMTP               | Email transfer               |
|   53 | DNS                | Name resolution              |
|   80 | HTTP               | Web traffic                  |
|  110 | POP3               | Email retrieval              |
|  143 | IMAP               | Email retrieval              |
|  443 | HTTPS              | Encrypted web traffic        |
|  445 | SMB                | Windows file sharing         |
| 3306 | MySQL              | Database                     |
| 3389 | RDP                | Remote Desktop               |
| 5432 | PostgreSQL         | Database                     |

> A port being open does **not** automatically mean the host is compromised. Always correlate the port with the expected service, process, host role, and network context.

---

# 📰 Advanced Log Analysis

Important locations:

```text
/var/log/
/var/log/auth.log
/var/log/syslog
/var/log/kern.log
```

Depending on your Linux distribution and configuration, filenames and log locations may differ.

---

## Search Errors

```bash
sudo grep -i "error" /var/log/*.log
```

---

## Search Authentication Failures

```bash
sudo grep -i "failed" /var/log/auth.log
```

---

## Search Successful Authentication

```bash
sudo grep -i "accepted" /var/log/auth.log
```

---

## Monitor Logs

```bash
sudo tail -f /var/log/auth.log
```

---

## Search by IP

```bash
sudo grep "192.168.1.50" /var/log/auth.log
```

---

## Search by Username

```bash
sudo grep "admin" /var/log/auth.log
```

---

# 📖 journalctl Advanced Usage

## Recent Logs

```bash
journalctl -n 100
```

---

## Follow Logs

```bash
journalctl -f
```

---

## Today's Logs

```bash
journalctl --since today
```

---

## Logs Since a Specific Time

```bash
journalctl --since "2026-09-01 10:00:00"
```

---

## Logs Before a Specific Time

```bash
journalctl --until "2026-09-01 12:00:00"
```

---

## Time Range

```bash
journalctl --since "2026-09-01 10:00:00" --until "2026-09-01 12:00:00"
```

---

## Specific Service

```bash
journalctl -u ssh
```

---

## Kernel Logs

```bash
journalctl -k
```

---

## Priority-Based Logs

```bash
journalctl -p warning
```

---

# 🚨 SSH Investigation

SSH is a common source of authentication events.

---

## Search Failed SSH Authentication

```bash
sudo grep "Failed password" /var/log/auth.log
```

---

## Search Successful SSH Authentication

```bash
sudo grep "Accepted" /var/log/auth.log
```

---

## Search Invalid Users

```bash
sudo grep "Invalid user" /var/log/auth.log
```

---

## Search a Specific Source IP

```bash
sudo grep "192.168.1.50" /var/log/auth.log
```

---

## Count Failed Attempts

```bash
sudo grep -c "Failed password" /var/log/auth.log
```

---

## Investigate an IP

```bash
sudo grep "192.168.1.50" /var/log/auth.log
```

Then ask:

```text
How many attempts?
Which username?
What timestamps?
Was authentication successful?
What happened afterward?
```

---

# 🧪 Suspicious File Investigation

Suppose you discover:

```text
/tmp/update
```

Do not immediately execute it.

Start with:

```bash
file /tmp/update
```

---

## Check Hash

```bash
sha256sum /tmp/update
```

---

## Check Permissions

```bash
ls -l /tmp/update
```

---

## Check Metadata

```bash
stat /tmp/update
```

---

## Check Strings

For an authorized defensive investigation:

```bash
strings /tmp/update | less
```

This may reveal readable strings such as:

```text
URLs
File paths
Error messages
Command names
Configuration strings
```

> `strings` output is only evidence, not proof of maliciousness.

---

## Check Dependencies for ELF Executables

```bash
ldd /tmp/update
```

> Avoid running an unknown executable merely to "see what it does." Static inspection and isolated analysis are safer starting points.

---

# 🔒 File Hashing

## SHA-256

```bash
sha256sum suspicious_file
```

---

## SHA-512

```bash
sha512sum suspicious_file
```

---

## MD5

```bash
md5sum suspicious_file
```

Use SHA-256 or stronger hashes for modern integrity workflows.

---

# ⏱️ Timeline Analysis

Incident response often requires building a timeline.

Important timestamps can include:

```text
Authentication
Process Start
File Modification
Service Start
Network Connection
Configuration Change
```

---

## File Timestamps

```bash
stat file.txt
```

---

## Recently Modified Files

```bash
find /etc -type f -mtime -1
```

---

## Recently Modified Files in `/tmp`

```bash
find /tmp -type f -mmin -60
```

---

## Combine with Metadata

```bash
find /tmp -type f -mmin -60 -exec stat {} \;
```

This can help collect metadata for recently modified files.

---

# 📦 Archives & Evidence

During investigations you may need to preserve collected evidence.

## Create a tar Archive

```bash
tar -cvf evidence.tar evidence/
```

---

## Compress with gzip

```bash
tar -czvf evidence.tar.gz evidence/
```

---

## List Archive Contents

```bash
tar -tzf evidence.tar.gz
```

---

## Extract Archive

```bash
tar -xzvf evidence.tar.gz
```

> Follow your organization's evidence-handling procedure. Preserve originals and record hashes when evidence integrity matters.

---

# 💾 Disk Investigation

## Disk Usage

```bash
df -h
```

---

## Directory Size

```bash
du -sh /var/log/
```

---

## Find Large Files

```bash
find /var -type f -size +100M
```

---

## Check Mounted File Systems

```bash
mount
```

or:

```bash
findmnt
```

---

## List Block Devices

```bash
lsblk
```

Useful during forensic or system investigations.

---

# 🧠 Environment & Shell Investigation

## Show Environment Variables

```bash
env
```

---

## Show Shell Variables

```bash
set
```

---

## Show Current Shell

```bash
echo $SHELL
```

---

## Show PATH

```bash
echo $PATH
```

---

## Current Working Directory

```bash
echo $PWD
```

---

## Current User

```bash
echo $USER
```

---

# 📜 Command History Investigation

View command history:

```bash
history
```

---

## Search History

```bash
history | grep ssh
```

---

## Search for Download Commands

```bash
history | grep -E "wget|curl"
```

---

## Search for Privilege Commands

```bash
history | grep sudo
```

> Shell history is useful evidence but is not complete or authoritative. History can be disabled, deleted, configured differently, or absent.

---

# 🛡️ Persistence Investigation

Attackers may attempt to establish persistence.

Common areas to investigate include:

```text
Cron
Systemd Services
SSH Keys
Shell Startup Files
User Accounts
Scheduled Tasks
```

---

## Check User Crontab

```bash
crontab -l
```

---

## Check Root Crontab

```bash
sudo crontab -l
```

---

## System Cron Locations

```bash
ls -la /etc/cron.d/
```

```bash
ls -la /etc/cron.daily/
```

```bash
ls -la /etc/cron.hourly/
```

---

## Check SSH Authorized Keys

For the current user:

```bash
cat ~/.ssh/authorized_keys
```

For another authorized account, inspect its home directory only when you have permission.

---

## Check Shell Startup Files

```bash
ls -la ~
```

Common files:

```text
.bashrc
.profile
.bash_profile
```

Review suspicious changes carefully.

---

# 🚨 SOC Investigation Workflow

A practical Linux investigation can follow this workflow:

```text
                  🚨 ALERT
                     │
                     ▼
             1️⃣ Identify Host
                     │
                     ▼
             2️⃣ Identify User
                     │
                     ▼
             3️⃣ Identify Time
                     │
                     ▼
             4️⃣ Identify Source IP
                     │
                     ▼
             5️⃣ Search Logs
                     │
                     ▼
             6️⃣ Check Processes
                     │
                     ▼
             7️⃣ Check Services
                     │
                     ▼
             8️⃣ Check Network
                     │
                     ▼
             9️⃣ Check Files
                     │
                     ▼
            🔟 Check Persistence
                     │
                     ▼
              🧠 Analyze Evidence
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
      Expected               Suspicious
          │                     │
          ▼                     ▼
       Close              Escalate
                                │
                                ▼
                         Incident Response
```

---

# 🎯 Practical SOC Scenario 1 — Brute-Force Investigation

### Alert

```text
🚨 Multiple SSH Authentication Failures

Source IP: 192.168.1.50
Target: Linux Server
Username: admin
```

---

## Step 1 — Search IP

```bash
sudo grep "192.168.1.50" /var/log/auth.log
```

---

## Step 2 — Search Failed Authentication

```bash
sudo grep "Failed password" /var/log/auth.log
```

---

## Step 3 — Count Events

```bash
sudo grep -c "192.168.1.50" /var/log/auth.log
```

---

## Step 4 — Check Successful Authentication

```bash
sudo grep "Accepted" /var/log/auth.log
```

---

## Step 5 — Check Login History

```bash
last
```

---

## Step 6 — Check Current Sessions

```bash
who
```

---

## Step 7 — Check Processes

```bash
ps aux
```

---

## Step 8 — Check Network Connections

```bash
sudo ss -tunp
```

---

## Investigation Questions

```text
❓ Were the attempts successful?

❓ Which account was targeted?

❓ Was the source IP expected?

❓ Did a successful login occur after failures?

❓ What happened after authentication?

❓ Are suspicious processes running?

❓ Are there unexpected network connections?
```

---

# 🎯 Practical SOC Scenario 2 — Suspicious Process

Alert:

```text
🚨 Suspicious Process Detected

PID: 2481
Process: unknown
```

---

## Step 1 — Identify Process

```bash
ps -p 2481 -f
```

---

## Step 2 — Find Executable

```bash
sudo readlink -f /proc/2481/exe
```

---

## Step 3 — Check Command Line

```bash
sudo tr '\0' ' ' < /proc/2481/cmdline
```

---

## Step 4 — Check Parent Process

```bash
pstree -p
```

---

## Step 5 — Check Network Connections

```bash
sudo ss -tunp
```

---

## Step 6 — Calculate Hash

If you identify the executable:

```bash
sha256sum /path/to/executable
```

---

## Step 7 — Check Metadata

```bash
stat /path/to/executable
```

---

# 🎯 Practical SOC Scenario 3 — Suspicious Listening Port

Alert:

```text
🚨 Unexpected Listening Port

Port: 4444
```

First investigate locally:

```bash
sudo ss -tulnp | grep ':4444'
```

Identify the process.

Then:

```bash
ps -p PID -f
```

Check executable:

```bash
sudo readlink -f /proc/PID/exe
```

Then investigate:

```text
Who owns the process?
Why is it running?
Which service launched it?
When did it start?
Is the port expected?
```

> An unusual port is an investigation lead, not by itself proof of compromise.

---

# 🎯 Practical SOC Scenario 4 — Suspicious File

Alert:

```text
🚨 Suspicious File

Location:
/tmp/update
```

Investigation:

```bash
file /tmp/update
```

```bash
ls -l /tmp/update
```

```bash
stat /tmp/update
```

```bash
sha256sum /tmp/update
```

```bash
strings /tmp/update | less
```

Then check:

```text
Who created it?
When was it modified?
What type of file is it?
What permissions does it have?
Is it executed by a process?
Is it referenced by a service or cron job?
```

---

# 🎯 Practical SOC Scenario 5 — Unexpected User

Alert:

```text
🚨 Unknown User Detected
```

Investigate:

```bash
cat /etc/passwd
```

Search username:

```bash
grep "username" /etc/passwd
```

Check groups:

```bash
groups username
```

Check login history:

```bash
last username
```

Check current sessions:

```bash
who
```

Check sudo permissions:

```bash
sudo -l -U username
```

> Use administrative commands only when authorized.

---

# 📊 SOC Evidence Collection Example

Create a dedicated directory:

```bash
mkdir -p ~/incident_001
```

Collect basic system information:

```bash
uname -a > ~/incident_001/system.txt
```

Collect hostname:

```bash
hostnamectl > ~/incident_001/hostname.txt
```

Collect users:

```bash
who > ~/incident_001/current_users.txt
```

Collect login history:

```bash
last > ~/incident_001/login_history.txt
```

Collect processes:

```bash
ps aux > ~/incident_001/processes.txt
```

Collect network connections:

```bash
sudo ss -tunap > ~/incident_001/network.txt
```

Collect running services:

```bash
systemctl list-units --type=service --state=running > ~/incident_001/services.txt
```

Collect recent journal entries:

```bash
journalctl -n 500 > ~/incident_001/journal.txt
```

Create a hash:

```bash
sha256sum ~/incident_001/* > ~/incident_001/hashes.txt
```

---

# 🔥 Powerful SOC Command Patterns

## Find Failed Authentication Counts

```bash
sudo grep "Failed password" /var/log/auth.log | wc -l
```

---

## Find Repeated Source IPs

For a known log format, extract the relevant field and count it:

```bash
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr
```

> **Important:** The field position can vary between log formats. Verify the actual log structure before using this in production.

---

## Search Multiple Security Indicators

```bash
sudo grep -Ei "failed|invalid|error|denied" /var/log/auth.log
```

---

## Find Recently Modified Files

```bash
find /tmp -type f -mmin -60
```

---

## Find Large Files

```bash
find /var -type f -size +100M 2>/dev/null
```

---

## Find SUID Files

```bash
sudo find / -type f -perm -4000 2>/dev/null
```

---

## Find SSH-Related Processes

```bash
ps aux | grep -i ssh
```

---

## Find SSH Listening Port

```bash
sudo ss -tulnp | grep ':22'
```

---

# 🧠 Advanced SOC Investigation Mind Map

```text
                       🛡️ SOC INVESTIGATION
                               │
             ┌─────────────────┼─────────────────┐
             │                 │                 │
          👤 USER           ⚙️ PROCESS        🌐 NETWORK
             │                 │                 │
          whoami              ps              ip addr
          id                  top             ip route
          who                 pstree          ss
          last                /proc           ping
             │                 │                 │
             └─────────────────┼─────────────────┘
                               │
                               ▼
                           📰 LOGS
                               │
                   ┌───────────┼───────────┐
                   │           │           │
                 grep         awk       journalctl
                   │           │           │
                   └───────────┼───────────┘
                               ▼
                         📁 FILES
                               │
                   ┌───────────┼───────────┐
                   │           │           │
                 find        stat       file
                   │           │           │
                   └───────────┼───────────┘
                               ▼
                         🔒 INTEGRITY
                               │
                          sha256sum
                               │
                               ▼
                         🚨 DECISION
                               │
                  ┌────────────┴────────────┐
                  ▼                         ▼
              LEGITIMATE                SUSPICIOUS
                  │                         │
                  ▼                         ▼
                CLOSE                   ESCALATE
                                            │
                                            ▼
                                      INCIDENT RESPONSE
```

---

# ⭐ Advanced SOC Cheat Sheet

```bash
# SYSTEM
uname -a
hostnamectl
uptime
env

# USERS
whoami
id
who
w
last
sudo lastb
groups
sudo -l

# FILES
ls -la
stat file
file file
find /path -type f
sha256sum file

# PERMISSIONS
ls -l
chmod
chown
stat -c "%a %n" file

# PROCESSES
ps aux
pstree -p
pgrep process
ps -p PID -f
readlink -f /proc/PID/exe

# SERVICES
systemctl status SERVICE
systemctl --failed
systemctl list-units --type=service --state=running
journalctl -u SERVICE

# NETWORK
ip addr
ip route
ip neigh
ss -tulnp
ss -tunp

# LOGS
grep
grep -Ei
tail -f
journalctl
journalctl -f
journalctl --since today

# TEXT PROCESSING
awk
cut
sed
tr
sort
uniq
wc

# INVESTIGATION
find
file
stat
strings
sha256sum
tar
tee

# PERSISTENCE
crontab -l
sudo crontab -l
ls -la /etc/cron.d/
ls -la ~/.ssh/
```

---

# 📅 30-Day Advanced SOC Linux Practice Plan

## 🟢 Days 1–5 — Advanced Text Processing

Practice:

```text
grep
awk
cut
sed
tr
sort
uniq
wc
```

Goal:

```text
Take raw log data
        ↓
Filter it
        ↓
Extract fields
        ↓
Count events
        ↓
Identify patterns
```

---

## 🟡 Days 6–10 — Process Investigation

Practice:

```text
ps
pstree
pgrep
/proc
top
```

Learn to answer:

```text
What is running?
Who started it?
What executable is running?
What is the parent process?
Is it expected?
```

---

## 🟠 Days 11–15 — Network Investigation

Practice:

```text
ip
ss
ping
```

Learn:

```text
IP
Port
Protocol
Process
Connection
```

---

## 🔵 Days 16–20 — Logs

Practice:

```text
grep
tail
journalctl
```

Investigate:

```text
SSH failures
Successful logins
Unknown users
Service events
System errors
```

---

## 🔴 Days 21–25 — File Investigation

Practice:

```text
find
file
stat
strings
sha256sum
```

Investigate:

```text
Suspicious files
Recently modified files
Unusual permissions
Unknown executables
File integrity
```

---

## 🟣 Days 26–30 — SOC Scenarios

Practice these scenarios:

```text
01 → SSH brute-force alert
02 → Suspicious successful login
03 → Unknown user
04 → Suspicious process
05 → Unexpected listening port
06 → Suspicious file
07 → Unexpected service
08 → Cron persistence
09 → Suspicious SSH key
10 → Multiple indicators on one host
```

For every scenario:

```text
Alert
 ↓
Identify
 ↓
Collect Evidence
 ↓
Analyze
 ↓
Determine Severity
 ↓
Document
 ↓
Escalate / Respond
```

---

# 🎓 Part 2 Key Concepts

By completing Part 2, you should be comfortable with:

```text
✅ Advanced Linux CLI
✅ Pipes and redirection
✅ Log filtering
✅ grep
✅ awk
✅ sed
✅ cut
✅ sort
✅ uniq
✅ find
✅ Process investigation
✅ /proc investigation
✅ Service investigation
✅ Network investigation
✅ Authentication investigation
✅ File metadata
✅ Hashing
✅ Timeline analysis
✅ Persistence checks
✅ Evidence collection
```

---

# 🚀 Part 3 — SOC & Wazuh

The next stage is moving from **Linux commands → actual SOC monitoring**.

```text
🐧 Linux
   ↓
📰 Linux Logs
   ↓
📊 SIEM
   ↓
🐺 Wazuh
   ↓
🚨 Alerts
   ↓
🔎 Alert Triage
   ↓
🧠 Investigation
   ↓
📋 Incident Documentation
   ↓
🛡️ Incident Response
```

### Part 3 Topics

```text
01 → What is a SIEM?
02 → What is Wazuh?
03 → Wazuh Architecture
04 → Wazuh Manager
05 → Wazuh Agent
06 → Wazuh Indexer
07 → Wazuh Dashboard
08 → Windows Agent
09 → Linux Agent
10 → Log Collection
11 → Rules
12 → Decoders
13 → Alerts
14 → Severity Levels
15 → MITRE ATT&CK
16 → Alert Triage
17 → False Positives
18 → Incident Investigation
19 → Custom Detection Rules
20 → Email / Teams Alerting
```

---

# 🛡️ Final SOC Mindset

The command itself is not the skill.

The skill is understanding the evidence.

```text
grep
 ↓
Find evidence

awk
 ↓
Extract information

sort + uniq
 ↓
Find patterns

find + stat
 ↓
Investigate files

ps + /proc
 ↓
Investigate processes

ss
 ↓
Investigate network

journalctl + logs
 ↓
Build timeline

sha256sum
 ↓
Verify file identity/integrity

ALL OF THEM
 ↓
      🧠
SOC INVESTIGATION
```

> **Remember:** A single unusual command, file, IP, process, or port does not automatically prove compromise. Good SOC analysis correlates multiple pieces of evidence, validates them against expected system behavior, preserves relevant evidence, and follows the organization's escalation and incident-response procedures.

---

## ⭐ Keep Learning

```text
Part 1 → Linux Fundamentals
Part 2 → Advanced Linux for SOC
Part 3 → Wazuh & SIEM
Part 4 → SOC Alert Investigation
Part 5 → Incident Response
Part 6 → Detection Engineering
Part 7 → Blue Team Labs
Part 8 → Real-World SOC Projects
```

---

## 👨‍💻 Author

**Ramcharan Singh Ramavath**

Learning:

```text
🐧 Linux
🛡️ Cyber Security
🚨 SOC Monitoring
📊 SIEM
🐺 Wazuh
🌐 Networking
🔎 Incident Response
```

---

⭐ **If this guide helps you, consider starring the repository and using it as your daily SOC/Linux reference.**

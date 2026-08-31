# All Should be Run IN """ Bash ""'

### Cybersecurity Foundation

These commands work on **Kali Linux, Ubuntu, Debian, Fedora, and other Linux distros**.

this guide is a quick reference while practicing. 🚀

---

## 🧭 01 — Navigation

### Move around the system

```bash
pwd                # Show current directory (Print Working Directory)
ls                 # List files/folders in current directory
ls -la             # Show hidden files with details
cd Desktop         # Move into Desktop folder
cd ..              # Go one step back
```

**Flow:**

`pwd` → `ls` → `cd Desktop` → `cd ..`

---

## 📁 02 — Directory Handling

### Work with folders

```bash
mkdir test         # Create a new folder named test
cd test            # Go inside the folder
```

**Flow:**

`mkdir` → Create folder → `cd` → Enter folder

---

## 📄 03 — File Handling

### Create → Read → Write → Append → Multiple Files

```bash
touch file1.txt    # Create an empty file
ls                 # Verify file creation
```

### 🟢 `cat` — Use Cases

**Read file content**

```bash
cat file1.txt
```

**Create + Write content**

```bash
cat > file1.txt
Hello Kali Linux
CTRL + D           # Save & exit
```

**Read file again**

```bash
cat file1.txt
```

**Append content to an existing file**

```bash
cat >> file1.txt
This is my first command practice
CTRL + D           # Save & exit
```

**Read updated file**

```bash
cat file1.txt
```

**Read multiple files at once**

```bash
cat file1.txt file2.txt
```

**File workflow:**

`touch` → Create → `cat` → Read → `cat >` → Write → `cat >>` → Append

---

## ✏️ 04 — File Editing

### Interactive Editor

```bash
nano file1.txt     # Open file in nano editor (write & edit)
```

**Flow:**

`nano` → Open → Edit → Save → Exit

---

## 🗑️ 05 — Delete Files & Folders

```bash
rm file1.txt       # Delete a file
rm -r test         # Delete folder + its contents
```

⚠️ **Be careful with `rm` commands**, especially when working with important files.

---

## 👤 06 — User & System Information

```bash
whoami             # Show current logged in user
hostname           # Show system hostname
uname -a           # Kernel + OS details
```

**Information flow:**

`whoami` → User
`hostname` → System name
`uname -a` → Kernel + OS details

---

## 🌐 07 — Networking Basics

```bash
ifconfig           # Show network interfaces (needs net-tools)
ip addr            # Alternative to ifconfig (modern Linux)
ping google.com    # Test connectivity
curl ifconfig.me   # Show your public IP
```

**Networking flow:**

`ifconfig` / `ip addr` → Network Interfaces

`ping` → Connectivity Test

`curl` → Public IP

---

## 📦 08 — Package Management

### Install / Update Tools

```bash
sudo apt update            # Update repositories
sudo apt upgrade           # Upgrade all packages
sudo apt install nmap      # Install a tool (e.g., Nmap)
nmap -v google.com         # Simple port scan
```

**Package workflow:**

`apt update` → Update repositories
↓
`apt upgrade` → Upgrade packages
↓
`apt install` → Install tools
↓
`nmap` → Use installed security tool

---

## ⚙️ 09 — Process Management

### Monitor & Kill Processes

```bash
ps aux              # Show running processes
top                 # Live process monitoring
kill -9 <PID>       # Kill a process by its ID
```

**Process workflow:**

`ps aux` → Find processes

`top` → Monitor processes

`kill -9 <PID>` → Terminate process

---

## 🔐 10 — Permissions & Ownership

```bash
ls -l               # Show file permissions
chmod 755 file1.txt # Change file permissions
chown user:user file1.txt  # Change file ownership
```

**Permission workflow:**

`ls -l` → Check permissions
↓
`chmod` → Change permissions
↓
`chown` → Change ownership

---

## 🔎 11 — Search & History

```bash
history             # Show previously used commands
grep "keyword" file1.txt   # Search for a word inside a file
man ls              # Manual/help for ls command
```

**Search workflow:**

`history` → Command history

`grep` → Search inside files

`man` → Command documentation

---

## 🧠 Quick Linux Mental Map

```text
🐧 Linux
   │
   ├── 🧭 Navigation
   │     ├── pwd
   │     ├── ls
   │     └── cd
   │
   ├── 📁 Directories
   │     └── mkdir
   │
   ├── 📄 Files
   │     ├── touch
   │     └── cat
   │
   ├── ✏️ Editing
   │     └── nano
   │
   ├── 🗑️ Deletion
   │     └── rm
   │
   ├── 👤 System
   │     ├── whoami
   │     ├── hostname
   │     └── uname
   │
   ├── 🌐 Networking
   │     ├── ifconfig
   │     ├── ip
   │     ├── ping
   │     └── curl
   │
   ├── 📦 Packages
   │     └── apt
   │
   ├── ⚙️ Processes
   │     ├── ps
   │     ├── top
   │     └── kill
   │
   ├── 🔐 Permissions
   │     ├── ls -l
   │     ├── chmod
   │     └── chown
   │
   └── 🔎 Search
         ├── history
         ├── grep
         └── man
```

---

## 🎯 Why These Commands?

These are **must-know Linux commands** for anyone starting in **Cyber Security & Ethical Hacking**.

Without Linux basics, you cannot effectively use tools like **Nmap, Hydra, Metasploit, Aircrack-ng**, etc.

---

## 🚀 Practice Path

```text
Linux Basics
     ↓
File & Directory Management
     ↓
Users & Permissions
     ↓
Processes
     ↓
Networking
     ↓
Package Management
     ↓
Security Tools
     ↓
Cybersecurity & Ethical Hacking
```

---

### 🐧 Learn Linux → 🔐 Understand Security → 🛡️ Build Cybersecurity Skills


A cyber attack is a deliberate attack attempt by hackers to steal, damage or disrupt computer systems.
Ex: sending fake bank emails to steal your login info...

## Types of Cyber Attacks...

* Phishing
* Malware
* Ransomware
* DDoS Attack
* Man-in-the-Middle Attack
* SQL Injection
* Password Attacks

### Phishing

Fake emails, messages, websites trick you into giving personal info.

Ex: You get an email, "Your bank account will be closed and you click to verify that link steals your credentials..."

### Malware

Malicious Software (virus, worm, trojan) installed secretly to harm your system, or steal data.

Ex: Downloading a free cracked game that secretly installs a keylogger.

### Ransomware

Hackers lock your files and demand money (ransom) to unlock them.

Ex: A hospital patient's data is encrypted and hackers ask millions to restore it.

### DDoS (Distributed Denial of Service) Attack

Flooding a website or server with huge traffic until it crashes.

Ex: An e-commerce site attacked during a big sale, making it unavailable to customers.

### Man-in-the-Middle Attack

Hackers secretly intercept communication between two parties.

Ex: Using free public Wi-Fi at a cafe, a hacker spies on your banking session.

### SQL Injection

Injecting malicious code into a website's database through forms or inputs.

Ex: A hacker types malicious commands in a login box and directly accesses all stored user data.

### Password Attacks

Guessing, stealing, cracking weak passwords.

Ex: Someone tries "12345" or "password" to break into your account.

---

## WHY UNDERSTANDING ALL THESE IS IMPORTANT?

Awareness helps you recognise threats early.

Prevention measures (strong passwords, antivirus, 2FA, not clicking suspicious links) reduce risks.

Cyber Security careers demand strong knowledge of these attack types.

---

# CIA Triad (Foundation of Security)

**Confidentiality, Integrity, Availability**

### Confidentiality

Ensures that sensitive information is only accessible to authorized individuals.

Protects against unauthorized individuals.

Using strong passwords and encryption so only you can access your online banking account.

### Integrity

Guarantees that information remains accurate, consistent and unaltered by unauthorized users.

Prevents unauthorized modification of data.

A medical record system ensures that no one can change a patient's prescription without doctor approval.

### Availability

Ensures that systems, applications and data are accessible when needed by authorized users.

Protects against downtime and service disruption.

Online banking remaining available 24/7 even during high traffic or cyberattacks.

---

# DAD TRIAD (Attacker's Goal)

### Disclosure

Unauthorized access or exposure of sensitive information.

Violates confidentiality.

A hacker leaks customer credit card details from an e-commerce database.

### Alteration

Unauthorized modification, manipulation, or corruption of data.

Violates integrity.

An attacker changes a patient's medical prescription in a hospital system.

### Denial

Disrupting or preventing legitimate access to systems, applications, or data.

Violates availability.

A DDoS (Distributed Denial of Service) attack makes an online banking service unavailable.

---

# CIA vs DAD

**CIA TRIAD = Defender's Goal**
(Protect Confidentiality, Integrity, Availability)

**DAD Triad = Attacker's Goal**
(Cause Disclosure, Alteration, Denial)

---

# Parkerian Hexad (SIX Elements Of Information Security)

## What is Parkerian Hexad?

It is an expanded model of information security that goes beyond the traditional CIA Triad.

Introduced by Donn B. Parker, Famous Security Researcher.

Instead of just 3 elements (Confidentiality, Integrity, Availability), it defines 6 essential attributes of information security.

## WHY IS IT IMPORTANT?

CIA triad is powerful, but sometimes too narrow for modern digital security challenges.

The Parkerian Hexad adds three more attributes (Possession, Authentication, Utility) which cover gaps left by CIA.

It gives a more complete framework for analyzing, understanding, and designing security policies, systems, and defenses.

**CONFIDENTIALITY, INTEGRITY, AVAILABILITY, POSSESSION**

### Possession (OR) Control

Refers to the ownership or control of information and physical media.

Having access to data doesn't always mean having legal/authorized possession.

If a hacker steals a USB with patient data, confidentiality might still be intact (if encrypted), but Possession is lost.

### Authenticity

Verifies that information, transactions and identities are genuine.

Prevents Impersonification and Forgery.

Digital Signatures on emails confirm that the sender is Authentic.

### Utility

Ensures that the data is useful, meaningful, and in a usable format.

Even if data is unavailable, if it's corrupted or unusable, its utility is lost.

A corrupted medical file that opens but shows unreadable text loses utility.

---

# Network Concepts For Cyber Security

### IP Address

A unique number label assigned to each device on a network.

**IPv4:** 192.168.1.1

**IPv6:** 2001:0db8:85a3:0000:0000:8a2e:0370:7334

Attackers trace IPs to launch attacks (e.g., DDoS, Scanning).

VPNs help hide IP addresses for privacy and protection.

### DNS — Domain Name System

The phonebook of the internet — translates human-friendly domain names into IP addresses.

**google.com → 142.250.190.14**

Vulnerable to DNS spoofing/poisoning (fake IP redirection).

DNSSEC provides a secure domain name resolution.

### HTTP — Hypertext Transfer Protocol

Transfers data without encryption.

### HTTPS — HTTP + SSL/TLS Encryption

Harder for attackers.

---

# VPN — Virtual Private Network

Creates a secure encrypted tunnel for internet traffic while masking your IP address.

* Hides IP (ensures anonymity).
* Encrypts traffic (safe on public Wi-Fi).
* Prevents attackers from tracing your identity.

**Risk:** Untrusted VPNs may log or track data.

---

# Firewall Basics

A security gatekeeper that monitors and controls network traffic based on allow/deny rules.

### Hardware Firewall

### Software Firewall

* Blocks unauthorized access.
* Prevents malware and hacking attempts.
* Works with IDS/IPS for advanced threat detection.

---

# What Is Cryptography?

Cryptography is the science of securing information by transforming it into an unreadable format, ensuring only authorized parties can access it.

It protects Confidentiality, Integrity, Authentication, and Non-Repudiation data.

Used in Secure communication, online transactions, digital identities and cybersecurity.

---

# CORE CONCEPTS OF CRYPTOGRAPHY

### Encryption

The process of converting Plain Text into Cipher Text using an algorithm and a key.

Ensures Confidentiality.

### Symmetric Encryption

Same key is used for both encryption and decryption.

Eg: AES, DES.

### Asymmetric Encryption

Different key is used.

Public key (encrypt)

and

Private key (Decrypt)

Eg: RSA, ECC.

Messaging apps (WhatsApp, Signal) use encryption to protect chats.

---

### Hashing

A one-way function that converts input data into a fixed-length string.

Ensures integrity and irreversible.

Even a small input change produces a completely different hash (avalanche effect).

Passwords are stored as hashes instead of plain text in databases.

---

### Digital Signature

A cryptographic mechanism that verifies the authenticity and integrity of digital data.

Sender hashes the message and encrypts the hash with their private key → creating a digital signature.

Receiver decrypts the signature using the sender's public key and verifies hash.

Authenticity and integrity.

Provides Non-Repudiation (sender cannot deny sending).

Used in Software Distribution, SSL Certificates, Blockchain Transactions.

---

# Public Key and Private Key

A pair of mathematically related cryptographic keys used in asymmetric encryption.

### Public Key

Shared openly; used to encrypt data or verify a digital signature.

### Private Key

Kept Secret; used to decrypt data or create a digital signature.

Data encrypted with a public key can only be decrypted with the corresponding private key.

Ensures secure communication without exchanging secret keys.

---

# Why Cryptography Is Important in Cybersecurity?

* Confidentiality
* Integrity
* Authentication
* Non-Repudiation

### Real-Life Applications:

Online Banking, E-commerce, VPNs, Cloud Storage, Digital Identity Verification...

---

# What is VirtualBox?

It is a FREE open-source virtualization software that allows you to run multiple operating systems on a single computer.

It creates a virtual environment (virtual machine) inside your main OS, so you can install and use another OS without affecting your actual computer.

We choose Kali Linux, a Debian-based Linux Distribution specially designed for cybersecurity.

Penetration Testing and Ethical Hacking.

It comes with Hundreds Of Pre-Installed tools for network security, forensics, and Vulnerability Testing.

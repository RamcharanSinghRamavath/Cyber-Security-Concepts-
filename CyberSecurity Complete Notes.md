A **cyber attack** is a deliberate attack attempt by hackers to steal, damage or disrupt computer systems. ex: sending fake bank emails to steal you login info...



Types of cyber Attack...



**phising**

**malware**

**Raansomware**

**DDOS Attack**

**man in the middle attack**

**SQL injection**

**Password Attacks**





**Phishing** --- Fake emails, msgs, websites trick you into giving personal iinfo



ex: you get an email, " your bank account will be closed and you click to verify that link steals your credentialss ...



**Malware** ---> Malicious SSoftware (virus, worm, trojan) installed secretly to harm ur system, or steal data.

ex: downloading a free cracked game that secretly installs a keylogger .





**Ransomware** ----> Hackers lock ur files and demand money (ransom) to unlock them..

ex: A hospital patients data is encrypted abd hackers ask millions to restore it.



**DDoS (Distributed denial of service ) attack** ----->  flooding a website or server with huge traffic until iit crashes.



ex : An ecommerce site attacked during big sale, making it unavailable to customers....



**Man in the middle attack** --->> hackers secretly intercepts communication b/w two parties.

ex: using free public wifi at a cafee  a hacker spies on your banking session...





**SQL injection** --->>injecting malicious code into a website's database through forms or inputs.



ex: a hacker types  malicious commands in a login box and directly accesses all storredd user data.



**Password AAttacks** --->

guessing, stealing, cracking weak passwords

ex: someone tries "12345" or " password" to break  into ur account.





WHY UNDERSTANDING ALL THESE IS IMP ??



awareness helps u recognise threats early.



prevention measures (strong passwords, antivirus, 2FA, not clicking suspicious links) reduce risks.'





Cyber Security careers demand strong noowlwdge of these attack types.



**CIA Triad (Foundation of Security) ---**



**confidential, integrity, Availability --**



**Confidential ---** Ensures that sensitive information is onky accessible to authorized indivisuals.

Protects against unauthorized individuals.

Using strong passwords and encryption so only you can access your online banking account.





**Integrity ---**  Garauntees  that information remains accrate, consistent and unaltered by unauthorized users.

Prevents unauthorized modification of data.

A medical record system ensures that no one can change a patients prescription without doctor approval.





**Availability ---** Ensures that systems, applications and data are accessible when needed by authorized users.



protects against downtime and service disruption.

online banking remaining available 24/7 even during high traffic or cyberattacks.







**DAD TRIAD (Attackers Goal)---->>**  

**Disclosure --** unauthorized access or exposure of sensitive information. 

violates confidentiality.

a hacker leaks customer credit card details from an e-commerce database  



**Alteration -->>**  unauthorized modification, manipulation, or corruption of data. 

violates integrity.

an attacker changes a patient's medical. prescription in a hospital system.



**Denial--->>** Disrupting or preventing legitimate access to systems, applications, or data.



violates availability.

A DDos (Distributed Denial of Service) attack, makes an Online Banking Service Unavailable.





**CIA vs DAD ---**



**CIA TRIAD** = Defender's Goal (Protect confidentiality, integrity, Availability)



**DAD Triad**  == Attacker's Goal( Cause Disclosure, Alteration, Denial).



**Parkerian Hexad (SIX Elements Of Information Security)**





**What is Parkerian Hexad ?**



It is an expanded model oof information security  that goes beyond the traditional CIA Triad. 

Introduced by Donn B. Parker 

Famous Security Researcher 

Instead of just  3 elements (confidentiality, integrity, Availability), it defines 6 essential attributes of  information security.





**WHY IS IT IMPORTANT?**



CIA triad is powerfull, but sometimes too narrow for modern digital security challenges. 



The pparkerain Hexad adds three more attributes (possession, Authentication, Utility) which cover gaps left by CIA.



It Gives a more complete framework for analyzing, understanding, and designing seurity policies, systems, and defenses. 



CONFIDENTIALITY, INTEGRITY, AVAILABILITY, POSSESSION



&#x20;**POSSESSION(OR) CONTROL --->>** refers to the ownership or control of information and physical media.

having access to data doesn't always mean having legal/ authorized possession.



If a Hacker steals a USB with patient data, confidentiality might still be  intact(if encrypted), but Possession is lost.





**Authenticity --->>>** verifies that information, transactions and identities are genuine.

Prevents Impersonification and Forgery.

Digital Signaures on emails confirm that the sender is Authentic.





Utility ---->>>

Ensures that the data is useful, meaningful, and in a usable format.

Even if data is unavailable. if it's corrupted oor unusable, its utility is lost.

A corrupted medical file that opens but shows unreadable text loses utility.





**Network Concepts For Cyber Security** 

&#x20;ip address --  a unique number label assigned to each device ona network 

IPV4 -->> 192.168.1.1



ipv6--->> 2001:0db8:85a3:0000:0000:8a2e:0370:7334



attackers trace ips to launch attacks(eg: DDos, Scanning)



Vpns help hide ip addresses for privacy and Protection.





**Dns -- Domain Name System.**

**The phonebook of the internet -- translates human friendly domain names into ip addresess.**



**google.com-->>>142.250.190.14**



**vulnerable to DNS spoofing/poisoning(fake IP redirection)**



**DNSSEC provides a secure domain name resolution.**





**HTTP --- HYPERTEXT TRANSFER PROTOCOL.(TRANSFERS DATA WITHHOUT ENCRYPTION)**

**HTTPS ----- HTTP+SSL/TLS ENCRYPTION.(HARDER FOR ATTACKERS** 





**VPN --- VIRTUAL PRIIVATE NETWORK.**

Creates a secure encrypted tunnel for internet traffic while masking your ip addresess.

hides ip(ensures anonymity).



encrypts traffic(safe on public wifi).



prevents attackers from tracing your identity.

RISK:  Untrusted VOPNS may log or track data.







**Farewall Basics...**



**a security gatekeeper that monitors and controls network traffic bbased on allow/deny rules.**



**Hardware firewall**

**software firewall**

**blocks unauthoorizedd access**

**prevents malware and hacking attempts.**

**works with IDS/IPS FOR ADVANCED Threat detection.**







**What Is Cryptography?**



cryptography is  the science of securing information by transforming it into an unreadable format, ensuring only authorized parties can access iit.

It protects  Confidentiality, integrity, authentication, and Non - Repudiation data. 

Used in Secure communication, online transactions, digital identities and cybersecurity.





**CORE CONCEPTS OF CRYPTOGRAPHY...**





**ENCRYPTION ---** THE PROCESS OF CONVERTING PLAIN TEXT INTO CIPHER TEXT USING AN ALGORITHM AND A KEY 

ENSURES CONFIDENTIALITY 

SYMMETRIC Encryption -->> same key is used for both encry and decryption ( eg:AES, DES).

ASSYMETRIC ENCRYPTION --->> DIFERENT KEY IS USED (public key(encrypt)



and Private key(Decrypt)(egg: RSA , ECC).



Messaging apps (WhatsApp signal) use encryption to protect chats.



**Hashing** --->>  A one way function that converts input datta into fixed length strnng.



ensures integrity and irreversible.

even a small input change produces a completely different hash(avalanche effect).



Passwords are stored as hashes instead of plain text in databases.





A cryptographic mechanism that verifies the authencity and integrity of digital data.



sender hashes the msg and encrypts the hash with their private key --> creating a digital signature.



Reciever decrypts the signature using the sender's public key and verifies hash.



Authencity and integrity Provides Non - Repudiation (sender cannot deny sending).

Used in Software Distribution, SSL Certificates, Blockchain Transactions. 





**Public key and Private Key :**



**A pair of mathematically related cryptographic keys used in asymmetric encryption.**



**public key--->> shared openly; used to encrypt data or verify a digital signature.**





**Private Key --->> Kept Secret; used to decrypt data or create a digital signature .**



**data encrypted with a public key can only be decrypted with the corresponding private key.**

**ensures secure ccommunication without exchanging secret keys.**





**Why cryptography is imp in Cybersecurity?**



confidentiality, integrity, authentication , non repudiation Real Life Applications: Online Banking, E-commerce, VPNs, Cloud Storage, Digital identity verification...



**What is Virtual Box ?**





it is A FREE Open source virtualization software that allows you too run multiple operationg systems on a single computer.





it creates a virtual environment(virtual machine) inside ur main OS, so you can install and use another os without affecting your actual computer..



We choose Kali Linux is a Debian - Based Linux Distribution specially designed for cybersecurity.



Penetration Testing, And Ethical Hacking.

It comes With Hundreds Of Pre Installed tools for network security, forensics, and Vulnerability Testing.











&#x20;






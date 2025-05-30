# 🌍 The Planets – Earth VM Walk-Through

A complete penetration-testing write-up for the **“The Planets – Earth”** VulnHub machine.  
This guide shows how to enumerate the target, exploit its web interface, escalate to root, and capture both user and root flags.

---

## Table of Contents
1. [Lab Setup](#lab-setup)  
2. [Reconnaissance](#reconnaissance)  
3. [Virtual-Host Enumeration](#virtual-host-enumeration)  
4. [Password Recovery (XOR Crack)](#password-recovery)  
5. [Initial Foothold (Web RCE)](#initial-foothold)  
6. [Privilege Escalation](#privilege-escalation)  
7. [Flags](#flags)  
8. [Screenshots](#screenshots)  
9. [Credits](#credits)

---

## Lab Setup
| Role              | Example IP | Notes                       |
|-------------------|-----------:|-----------------------------|
| Kali / Attacker   | `10.0.2.4` | Replace with your own       |
| Earth VM (Victim) | `10.0.2.11`| Discovered via `netdiscover`|

### Requirements
* VirtualBox / VMware  
* Kali Linux (or any pentest distro)  
* Earth VM OVA from VulnHub  

---

## Reconnaissance
```bash
# Identify hosts on the network
netdiscover -r 10.0.2.0/24

# Full TCP scan and service detection
nmap -sC -sV -p- -oA scans/full 10.0.2.11

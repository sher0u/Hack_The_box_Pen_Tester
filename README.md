# 🔴 Hack The Box — Penetration Tester Path

## 📋 Syllabus

### Introduction
1. Penetration Testing Process
2. Getting Started

### Reconnaissance, Enumeration & Attack Planning
3. Network Enumeration with Nmap
4. Footprinting
5. Information Gathering - Web Edition
6. Vulnerability Assessment
7. File Transfers
8. Shells & Payloads
9. Using the Metasploit Framework

### Exploitation & Lateral Movement
10. Password Attacks
11. Attacking Common Services
12. Pivoting, Tunneling, and Port Forwarding
13. Active Directory Enumeration & Attacks

### Web Exploitation
14. Using Web Proxies
15. Attacking Web Applications with Ffuf
16. Login Brute Forcing
17. SQL Injection Fundamentals
18. SQLMap Essentials
19. Cross-Site Scripting (XSS)
20. File Inclusion
21. File Upload Attacks
22. Command Injections
23. Web Attacks
24. Attacking Common Applications

### Post-Exploitation
25. Linux Privilege Escalation
26. Windows Privilege Escalation

### Reporting & Capstone
27. Documentation & Reporting
28. Attacking Enterprise Networks

---

## 🔑 Main Stages

| Stage | Description |
|---|---|
| **Pre-Engagement** | Define scope, rules of engagement, and contracts |
| **Information Gathering** | Collect target data passively and actively |
| **Vulnerability Assessment** | Identify weaknesses in systems and services |
| **Exploitation** | Gain initial access to the target |
| **Post-Exploitation** | Escalate privileges and collect sensitive data |
| **Lateral Movement** | Move across the internal network |
| **Proof of Concept** | Document how attacks were executed |
| **Post-Engagement** | Deliver report and clean up artifacts |

![Penetration Testing Process](https://github.com/user-attachments/assets/e5c9a62b-5186-4da0-a260-d2e660e8bccd)

---

## 🛰️ Service Scanning

### Commands Reference

| Command | Description |
|---|---|
| `nmap 10.129.42.253` | Run basic Nmap scan on an IP |
| `nmap -sV -sC -p- 10.129.42.253` | Run full script scan with version detection |
| `locate scripts/citrix` | List available Nmap scripts |
| `nmap --script smb-os-discovery.nse -p445 10.10.10.40` | Run a specific Nmap script |
| `netcat 10.10.10.10 22` | Grab banner of an open port |
| `smbclient -N -L \\\\10.129.42.253` | List SMB shares (no auth) |
| `smbclient \\\\10.129.42.253\\users` | Connect to an SMB share |
| `snmpwalk -v 2c -c public 10.129.42.253 1.3.6.1.2.1.1.5.0` | Scan SNMP on an IP |
| `onesixtyone -c dict.txt 10.129.42.254` | Brute force SNMP community string |

### Lab

**Q1: What does Nmap display as the version of the service running on port 8080?**

```bash
nmap -sV <target-ip>
```

> ✅ Answer: `Apache Tomcat`

---

**Q2: What non-default port is the Telnet service running on?**

```bash
nmap -sV <target-ip>
```

> ✅ Answer: `2323`

---

**Q3: List SMB shares, connect as `bob`, and retrieve `flag.txt` from the `flag` folder.**

```bash
smbclient -N -L //10.129.47.44              # List shares anonymously
smbclient -U bob //10.129.47.44/users       # Connect as bob
cd flag
get flag.txt
cat flag.txt
```

> ✅ Answer: `dceece590f3284c3866305eb2473d099`

---

## 🌐 Web Enumeration

### Commands Reference

| Command | Description |
|---|---|
| `gobuster dir -u http://10.10.10.121/ -w /usr/share/dirb/wordlists/common.txt` | Directory brute-force scan |
| `gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt` | Subdomain enumeration |
| `curl -IL https://www.inlanefreight.com` | Grab website banner/headers |
| `whatweb 10.10.10.121` | Identify webserver, CMS, and tech stack |
| `curl 10.10.10.121/robots.txt` | Check for hidden paths in robots.txt |
| `Ctrl + U` | View page source in Firefox |

### Lab

**Q: Enumerate the target and capture the flag.**

Target: `154.57.164.80:32036`

**Steps taken:**
1. Inspected page source — nothing useful initially
2. Ran `gobuster` for directory enumeration
3. Checked `robots.txt` → found `/admin` page
4. Inspected admin page source → found hardcoded credentials
5. Logged in and retrieved the flag

> ✅ Flag: `HTB{w3b_3num3r4710n_r3v34l5_53cr375}`

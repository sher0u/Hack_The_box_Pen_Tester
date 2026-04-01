# Hack_The_box_Pen_Tester
## Penetration Tester Path Syllabus
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

## 🔑 Main stages:
Pre-Engagement → define scope, rules, contract
Information Gathering → collect target data
Vulnerability Assessment → identify weaknesses
Exploitation → gain access
Post-Exploitation → escalate privileges & collect data
Lateral Movement → move across the network
Proof of Concept → document how attacks worked
Post-Engagement → report + clean up
<img width="2079" height="783" alt="image" src="https://github.com/user-attachments/assets/e5c9a62b-5186-4da0-a260-d2e660e8bccd" />


Q1:Perform an Nmap scan of the target. What does Nmap display as the version of the service running on port 8080?
Nmap -sV ip adress 
answer: Apache Tomcat

Q2:Perform an Nmap scan of the target and identify the non-default port that the telnet service is running on.
answer: 2323
Q3:List the SMB shares available on the target host. Connect to the available share as the bob user. Once connected, access the folder called 'flag' and submit the contents of the flag.txt file.
Steps:

smbclient -V
smbclient -N -L //10.129.47.44
smbclient //10.129.47.44/users
smbclient -U bob //10.129.47.44/users
cd flag
get flag.txt
cat flag.txt

asnwer:dceece590f3284c3866305eb2473d099



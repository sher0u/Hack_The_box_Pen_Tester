# Network Enumeration with Nmap

**Network Mapper (Nmap)** is an open-source network analysis and security auditing tool written in C, C++, Python, and Lua.

It is designed to:
- Scan networks using raw packets
- Identify available hosts on a network
- Detect services and applications (including names and versions)
- Identify operating systems and their versions

---

## 🔍 Use Cases

- Audit the security aspects of networks  
- Simulate penetration testing scenarios  
- Check firewall and IDS configurations  
- Analyze different types of network connections  
- Perform network mapping  
- Conduct response analysis  
- Identify open ports  
- Perform vulnerability assessments  

---

## ⚙️ Basic Syntax

```bash
nmap <scan_types> <options> <target>
nmap -sS -p 1-1000 192.168.1.1

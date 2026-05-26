# My Cybersecurity Journey
Started: April 2026
Goal: Entry-level cybersecurity role

## Study Log

## Day 1:
- Completed: OSI Model
- Lab: Drew the OSI model from memory
- What clicked: how data travels from one computer to another across a network
- What confused me: Layer 5, 6, 7,  encapsulation

## Day 2:
- Completed: IP Address and Subnetting basics
- Lab task: ran ip addr and ip route on my Linux machine. Identified my IP, subnet mask, default gateway, and confirmed I'm in a private range. Figured out why my broadcast address ends in .191 instead of .191 (the /20 boundary cuts through the third octet)
- What clicked: how an IP is structured across 4 octets, private vs public IP, a brief intro to IPv6, and why it exists
- What confused me: subnet mask, CIDR notation, subnetting calculations

## Day 3:
- Completed: DNS - How names become addresses
- Lab: nslookup google.com, nslookup google.com 8.8.8.8, also looked up other websites.
-  What clicked: how domain names get translated into IP addresses, recursive resolvers, authoritative nameservers, DNS Records (A, AAAA, CNAME, MX) 

## Day 4:
- Completed: TCP/IP - how data travels
- Lab Task: ss -tuln (Ubuntu) and netstat -an (Windows PowerShell), local IP, remote IP, port, and state (LISTEN, ESTABLISHED, etc)
- What clicked: the difference between TCP and UDP, TCP 3-way handshake, well-known ports, TCP teardown
- What confused me: open Gmail expecting to see ESTABLISHED connection in WSL2, but got nothing. Turns out Chrome runs on Windows, not inside WSL2, so its connections are invisible to the Linux ss command. had to run netstat -an on the Windows Powershell side instead, where I finally saw real ESTABLISHED connections all on port 443.

## Day 5: 
- Completed: HTTP, HTTPS & Application Protocols
- Lab Task: I used Browser DevTools to watch HTTP requests on Wikipedia, where I encountered a 304 Not Modified response, gzip compression, a no-cache directive, and a DNT privacy header.
- What clicked: GET, PUT, POST, DELETE, status code, the difference between HTTP and HTTPS, how TLS encryption secures connections, and how SSL certificates verify a website's identity. Application Protocols: SMTP for email, FTP for file transfer, SSH for encrypted remote access, and DHCP for automatic IP address assignment, including the full DORA process.
- What confused me: memorizing the different types of acronyms for the application protocol

  ## Day 6:
  - Completed: Switches, Routers and Network Devices
  - Lab Task: ran arp -a on Ubuntu, saw my actual ARP cache pointing to my Hyper-V virtual gateway, then ran traceroute google.com and watched my packets travel through my home router and deep into ISP's backbone network before hitting Google's infrastructure at around 34ms.
  - What Clicked: Hubs, Switches,a nd routers and how each one handles traffic differently. how switches use MAC address tables to deliver frames only to the right device (Layer 2), while routers use IP addresses and routing tables to forward packets between different networks (Layer 3). how the default gateway acts as the exit door out of a local network.
  - What confused me: ARP, VLANs and Spanning Tree Protocol
## DAY 7:
- Completed: Wireshark
- Lab Task: ran my first live packet capture on my Wi-Fi Interface. Filtered by dns and watched real-time DNS queries flying off my machine to Google and other background services, also tcp.port==443 and found the TLS handshake in the wild: spotted Client Hello packets with SNI, Change Cipher Spec, and Application Data rows
What clicked: once encryption switches on, Wireshark can see the packet but cannot read inside them. The biggest insight today was realising my computer is constantly chattering on the network without me doing anything

## Day 8:
- Completed: Firewalls and Networking Security Devices
- Lab Task: ran sudo iptables -L on Linux to read live firewall rules, manually wrote and applied a rule to accept TCP traffic on port 22, then flushed the table clean. Also explored Windows Defender Firewall's Advanced Settings, reading real inbound and outbound rules and identifying entries from installed apps
- What clicked: stateful vs stateless firewalls, packet filtering, ACLs, next-generation firewalls with deep packet inspection, IDS vs IPS, UTMs.
- What confused me: DMZs, network segmentation, and proxy servers

## Day 9:
- Completed: VPNs & Encryption
- Lab Tasks: used Wireshark to capture a live TLS 1.3 handshake with Spotify servers. Observed the Client Hello with 20 cipher suites and SNI extension, the Server Hello selecting TLS_AES_256_GCM_SHA384, the x25519 Diffie-Hellman key exchange, Change Cipher Spec, and finally fully encrypted application data that Wireshark could not decode. Watched PKI and TLS do their job in real time — every field from theory appeared live in the capture.
- What clicked: symmetric (one shared key, fast but vulnerable to interception during sharing) and asymmetric (public/private key pair, solves the key distribution problem). Learned how VPNs work — tunneling, encapsulation, IPSec vs SSL/TLS VPN, split tunneling, and the difference between site-to-site and remote access VPNs. Studied digital certificates, Certificate Authorities, and PKI — understanding how the entire HTTPS trust system depends on CAs verifying that public keys genuinely belong to who they claim to. Walked through the TLS handshake step by step (Client Hello → Server 
Hello → certificate verification → key exchange → encrypted session).

## Day 10:
- Completed: Common Network Attacks
- Lab Task: TryHackMe Pre-Security Path (in progress)
- What Clicked: ARP spoofing/poisoning, DNS spoofing, Man-in-the-Middle, DoS vs DDoS, SYN flood, VLAN hopping, packet sniffing, rogue access points, evil twin, and MAC flooding. 


## Day 11:
**Completed**: Wireless Networks & Security
- Lab Task: Performed a passive wireless scan of the local RF environment.
- What Clicked: 802.11 Standards, 2.4GHz vs 5GHz, WEP/WPA/WPA2/WPA3, SSID, BSSID, Authentication Modes, WPS Vulnerabilities, Evil Twin Attack, Captive Portals, RADIUS

## Day 12:
- Completed: Network Monitoring & Log Analysis
- Lab Task:
    - Windows — Event Viewer: Opened Event Viewer and navigated to Windows Logs → Security. Filtered for Event IDs 4624 and 4625. Found 37,009 total security events on the machine; all visible events after filtering were Audit Success (4624). Clicked into an individual event and read the full details: Security ID SYSTEM, Logon Type 5 (Service), Computer SHM. Learned that SYSTEM and Logon Type 5 are normal Windows background activity — services authenticating automatically.
    - Linux — Auth Log: Ran sudo cat /var/log/auth.log | tail -50 on an Ubuntu virtual machine. Read the output line by line: saw a successful session opened for user salma (uid=1000), systemd session creation, and, most interestingly, the sudo command itself being recorded in real time. The log captured the exact command we ran, the terminal session (TTY=pts/0), the working directory, and the fact that we temporarily acted as root. This demonstrated how sudo logging creates accountability and how attackers get caught: rm -rf /var/log in a sudo log entry means an attacker deleted evidence and the log caught it just before being wiped.
- Topics: Syslog, SNMP, NetFlow, Log Formats, SIEM Basics, Alert Triage, Baseline vs Anomaly, Event IDs, Windows Security Logs, Linux Auth Logs


## Day 13:
- Completed: Network Troubleshooting Tools
- Lab Task: run ping -c 4 8.8.8.8, traceroute 8.8.8.8, nslookup cloudflare.com, netstat -an, ip a
- Topics:  ping, traceroute, nslookup, dig, netstat, nmap, ipconfig/ifconfig/ip a, curl, and telnet. each designed to answer a specific diagnostic question about a network or connection. 

## Day 14:
- Completed: Wireshark Deep Dive
- Lab Task: Analysed three real .pcap files from Wireshark's official sample capture library.
  1. In telnet-cooked.pcap, credentials (username: fake, password: user) were recovered directly from a TCP stream with no decryption required. The entire post-login session including commands run and files listed was readable in plain text, demonstrating exactly why Telnet is banned in any security-conscious environment.
  2. In http.cap, an unencrypted 2004 browser session to www.ethereal.com was analysed. The full HTML source of the visited page was recoverable, and request headers revealed the user's OS (Windows XP), browser, and browsing history.
  3. In arp-storm.pcap, 622 ARP packets all identical in size (60 bytes) were observed rapidly targeting dozens of different IP addresses without waiting for responses. A pattern consistent with either a denial-of-service flood or automated network reconnaissance.
- Covered: four main interface panels (filter bar, packet list, packet details, and packet bytes), how to write display filters to narrow down traffic, and how to use Follow TCP Stream to reassemble entire conversations between two computers into a readable window. Protocol identification was covered in depth — understanding that protocols like Telnet, FTP, and HTTP send data in plaintext while HTTPS and SSH encrypt it, and knowing what attack patterns look like in captured traffic (ARP floods, port scans, credential exposure).


## ISC2 CC -  DOMAIN 1: SECURITY PRINCIPLES
- Completed: ISC2 CC Domain 1 in full
- Topics covered:
   - CIA Triad (Confidentiality, Integrity, Availability)
   - Privacy & GDPR
   - PII and the Aggregation Problem
   - Introduction to Risk Management
   - Threats, Vulnerabilities & Likelihood
   - Risk in Our Lives
   - Protecting Information
   - Making Connections (CIA + real-world scenarios)
   - Privacy in the Working Environment (HIPAA, GDPR)
   - Risk Management Terminology (Asset, Vulnerability, Threat)
   - Decision Making Based on Risk Priorities
   - Importance of Risk Management
   - Importance of Governance Elements
   - Risk Identification
   - What are Security Controls (Physical, Technical, Administrative)
   - Code of Ethics — Theoretical Examples
   - Professional Code of Conduct & Canons
   - Authentication (3 Factors, MFA)
   - Governance Elements (Regulations, Standards, Policies, Procedures)
- Weak Areas: Physical Controls (tangible hardware (walls/fences) vs processes), Risk transfer scenarios, CIA Triad confidence.

## ISC2 CC - DOMAIN 2: INCIDENT RESPONSE, BC & DR
- Key Topics covered:
    - Incident Terminology (Event, Incident, Breach, Exploit, Intrusion, Threat, Vulnerability and Zero Day)
    - IR / BC / DR Relationship
    - Business Continuity
    - Disaster Recovery
- Weak Area: Red Book question: the defining feature is location (outside the facility), not the content (procedures). The exam tests why, not what.

## ISC2 CC - DOMAIN 3: ACCESS CONTROL CONCEPTS
- Key Topics Covered
    - Security Controls & Access Elements
    - Defense in Depth
    - Physical vs Logical Controls
    - Least Privilege
    - Controls and Risks
    - RBAC
    - PAM & Just-in-Time Access
    - Privileged Accounts
    - Monitoring
 - Weak Area: Static admin = always on = maximum blast radius if compromised and JIT = privileges activate only for the specific task being performed

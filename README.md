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
Completed: IP Address and Subnetting basics
Lab task: ran ip addr and ip route on my Linux machine. Identified my IP, subnet mask, default gateway, and confirmed I'm in a private range. Figured out why my broadcast address ends in .191 instead of .191 (the /20 boundary cuts through the third octet)
What clicked: how an IP is structured across 4 octets, private vs public IP, a brief intro to IPv6, and why it exists
What confused me: subnet mask, CIDR notation, subnetting calculations

## Day 3:
Completed: DNS - How names become addresses
Lab: nslookup google.com, nslookup google.com 8.8.8.8, also looked up other websites.
What clicked: how domain names get translated into IP addresses, recursive resolvers, authoritative nameservers, DNS Records (A, AAAA, CNAME, MX) 

## Day 4:
Completed: TCP/IP - how data travels
Lab Task: ss -tuln (Ubuntu) and netstat -an (Windows PowerShell), local IP, remote IP, port, and state (LISTEN, ESTABLISHED, etc)
What clicked: the difference between TCP and UDP, TCP 3-way handshake, well-known ports, TCP teardown
What confused me: open Gmail expecting to see ESTABLISHED connection in WSL2, but got nothing. Turns out Chrome runs on Windows, not inside WSL2, so its connections are invisible to the Linux ss command. had to run netstat -an on the Windows Powershell side instead, where I finally saw real ESTABLISHED connections all on port 443.

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
  - What confused: ARP, VLANs and Spanning Tree Protocol
## DAY 7:
- Completed: Wireshark
- Lab Task: ran my first live packet capture on my Wi-Fi Interface. Filtered by dns and watched real-time DNS queries flying off my machine to Google and other background services, also tcp.port==443 and found the TLS handshake in the wild: spotted Client Hello packets with SNI, Change Cipher Spec, and Application Data rows
What clicked: once encryption switches on, Wireshark can see the packet but cannot read inside them. The biggest insight today was realising my computer is constantly chattering on the network without me doing anything

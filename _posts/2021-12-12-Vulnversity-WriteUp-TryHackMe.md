---
layout: post
title: "Vulnversity WriteUp TryHackMe"
date: 2021-12-12 15:45:15 CET
categories: jekyll update
---

In this writeup I'll review my walkthrough on the [Vulnversity room](https://tryhackme.com/room/vulnversity) 
from TryHackMe. It's a beginner level CTF, with questions that guide the steps
to take in order to hack the machine. It also gives tips when using tools like
`nmap` or `GoBuster`.



## Deploy the machine

# Reconnaissance


| nmap flag     | Description                                                                         |
| :-----------: | :---------------------------------------------------------------------------------: |
| -sV           | Attempts to determine the version of the services running                           |
| -p <x> or -p- | Por scan for port <x> or scan all ports                                             |
| -Pn           | Disable host discovery and just scan for open ports                                 |
| -A            | Enables OS and version detection, executes in-build scripts for further enumeration |
| -sC           | Scan with the default nmap scripts                                                  |
| -v            | Vervose mode                                                                        |
| -sU           | UDP port scan                                                                       |
| -sS           | TCP SYN port scan                                                                   |


- Scan the box, how many ports are open?
> Answer: `6`
- What version of the squid proxy is running on the machine?
> Answer: `3.5.12`
- How many ports will nmap scan if the flag -p-400 was used?
> Answer: `400`
- Using the nmap flag -n what will it not resolve?
> Answer: `DNS`
- What is the most likely operating system this machine is running?
> Answer: `Ubuntu`
- What port is the web server running on?
> Answer: `3333`

## Locating directories using GoBuster


- What is the directory that has an upload form page?
> Answer: `/internal/`



## Compromise the webserver


- Try upload a few file types to the server, what common extension seems to be blocked?
> Answer: `.php`
- Run this attack, what extension is allowed?
> Answer: `.phtml`
- What is the name of the user who manages the webserver?
> Answer: `Bill`
- What is the user flag?
> Answer: `******************`



## Privilege escalation


- On the system, search for all SUID files. What file stands out?
> Answer: `/bin/systemctl`
- Become root and get the last flag (/root/root.txt)
> Answer: `******************`

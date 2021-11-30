---
layout: post
title: "Simple CTF WriteUp TryHackMe"
date: 2021-11-30 15:45:15 CET
categories: jekyll update
---

Simple CTF is a beginner level room on TryHackMe. There are few questions that
guide you in which steps have to be done. It took me few hours to complete it as
I found problems running the exploit, a python script. First I needed to solve
some dependencies, I also modified the code to adapt it to Python3 and finally
it worked till the moment of cracking the password.

Firs, as always, I started enumerating the system. Here is the output of this
nmap command:

``` bash
nmap -sCV <ip-address>
```

![nmap](img/simpleCTF/nmap.png)

Whith this information I could answer some of the questions.

- How many services are running under port 1000?
> Answer: `2`
- What is running on the higher port?
> Answer: `ssh`

It has the port 80 open, so I typed the ip in my browser and it displayed the
default's apache page. So I run **gobuster** to find hidden directories.

``` bash
gobuster dir -u http://<ip-address> -x -.txt,.php,.html -w /usr/share/wordlists/dirb/common.txt -t 64 -q
```

![gobuster](img/simpleCTF/gobuster.png)

It shows the `/simple` directory, which could be exploited. Here's a 

Here the point is that this site is using a CMS called `CMS made simple`,
version 2.2.8. I when to [exploit DB](https://www.exploit-db.com/) and search
for exploits for this application. There's one for that version, and I could
answer the next question:

![exploitDB](img/simpleCTF/exploitDB.png)

- What's the CVE you're using against the application?
> Answer: `CVE-2019-9053`
- To what kind of vulnerability is the application vulnerable?
> Answer: `SQLi`

This exploit is the 46635.py and I tried to run it with this command:

``` bash
python /usr/share/exploitdb/exploits/php/webapps/46635.py -u http://<ip-address>/simple --crack -w /usr/share/seclists/Passwords/Common-Credentials/best110.txt
```

There's a hint in the web to recommend using the best110.txt dictionary instead of the
classic rockyou.txt. It makes the process faster since is way shorter.

At this point I could answer the next two questions:

- What's the password?
> Answer: `secret`
- Where can you login with the details obtained?
> Answer: `ssh`

Having the user and his password I was able to ssh into the machine and read the
user's flag. Also they ask if there's another user in the home directory

- What's the user flag?
> Answer: `G00d j0b, keep up!`
- Is there any other user in the home directory? What's its name?
> Answer: `sunbath`

In order to escalate privileges I tried with `sudo -l` and found that you can
run vim as root without the password. That's an easy one, so in vim as root I
executed the command `:!sh` and immediately had a root shell. I could read the
root flag and answer the last questions to complete the room.

![ssh](img/simpleCTF/root.png)

- What can you leverage to spawn a privileged shell?
> Answer: `vim`
- What's the root flag?
> Answer: `W3ll d0n3. You made it!`

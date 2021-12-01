---
layout: post
title: "Hydra WriteUp TryHackMe"
date: 2021-11-28 15:45:15 CET
categories: jekyll update
---

This room is very short comared to others and very straightforward. It's part
of the **Comptia Pentest+** path. Hydra is a pentest tool for cracking paswords
with brute force.  The first task of the room is about what is that tool for and
how to install it.  As it says, Hydra *bruteforces* authentication in SSH, Web
Application Forms, FTP and SNMP. Also there's a long list of protocols Hydra has
the ability to crack. It's an essential tool for the pentester.

Hydra is preinstalled in Kali Linux, so I could execute it from a
Kali Docker container on my Mac machine. 

On the second task there are few examples of the usage of this tool and an
explanation of what the parameters mean. It is more or less what we are going to
use to get the flags.  This is my walkthrough on this room.


## Task 1: Hydra Introduction

Read the above and have Hydra at the ready.

## Task 2: Using Hydra

I first deployed the machine and executed nmap for a quick recognisement. Nmap
shows that has 2 ports open, 22 and 80. Then I type the IP in the browser and it
appears a login form with an image of Hydra, the many-headed snake from the
greek mythology.

- Use Hydra to bruteforce molly's web password. What is flag 1? 

The same question gives us the username which we are going to attempt to get its
password. I used the same command given before with one difference, the
directory Hydra will bruteforce is `/login` instead of `/`, as when I browsed
the IP it redirected me to that directory. The dictionary used waw the
`rockyou.txt`, like always I try to crack passwords, and as you can see in the
image it worked after very few attempts.

``` bash
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.166.99 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V
```

![Hydra output](/img/output_post.png)

Then I logged in with that credentials and got the flag 1.

![login](/img/login.png)

- Use Hydra to bruteforce molly's SSH password. What is flag 2?

Port 22 is also open so knowing the user **molly** we can try to crack the
password and ssh into the machine. The command I used this time was this:

``` bash
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.166.99 -t 4 ssh
```

![Hydra output](/img/output_ssh.png)

It didn't take long and after cracking the password I could ssh into the machine and
the flag was the content of the file `flag2.txt`.

![ssh login](/img/ssh.png)

As you can see, this room is very short and fast to do, but so useful since
**Hydra** it's an important tool for password cracking. It also shows the
importance of using strong passwords because it's so easy to crack the
most predictable ones.

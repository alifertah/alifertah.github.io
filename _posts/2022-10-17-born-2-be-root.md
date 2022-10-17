---
layout: post
title: Born 2 Be Root
tags: programming IT
date: 17-10-2022
author: Ali Fertah
---

# Born2beroot

## 42 school project

# 1. Installation

The installation guide is at the end of the article.

# 2. Configuration

## 2.1. Installing sudo

Login as root

$ su -

Install sudo

$ apt-get update -y  
$ apt-get upgrade -y  
$ apt install sudo

Adding user in sudo group

$ su -  
$ usermod -aG sudo your_username

Check if user is in sudo group

$ getent group sudo

Give privilege as a su.

Open sudoers file:

$ sudo visudo

Add this line in file:

your_username    ALL=(ALL) ALL

## 2.2. Installing tools

Installing git

$ apt-get update -y  
$ apt-get upgrade -y  
$ apt-get install git -y

Check git version

$ git --version

Installing wget  _(wget is a free and open source tool for downloading files from web repositories.)_

$ sudo apt-get install wget

Installing Vim

$ sudo apt-get install vim

Installing Oh my zsh (because it is easier to use)

$ sudo apt-get install zsh  
$ zsh --version  
$ sh -c "$(wget [https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh](https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh) -O -)"

## 2.3. Installing SSH and configuring SSH service

$ sudo apt-get update  
$ sudo apt install openssh-server

Check the SSH server status

$ sudo systemctl status ssh

Restart the SSH service

$ service ssh restart

Changing default port (22) to 4242

$ sudo nano _/etc/ssh/sshd_config_

Edit the file change the line #Port22 to Port 4242

_Find thid line:_

#Port 22

_Change it like this:_

Port 4242

Check if port settings got right

$ sudo grep Port /etc/ssh/sshd_config

Restart the SSH service

$ sudo service ssh restart

## 2.4. Installing and configuring UFW (Uncomplicated Firewall)

Install UFW

$ apt-get install ufw

Enable

$ sudo ufw enable

Check the status

$ sudo ufw status numbered

Configure the rules

$ sudo ufw allow ssh

Configure the port rules

$ sudo ufw allow 4242

Delete the new rule: (This is for when you defend your Born2beroot)

$ sudo ufw status numbered  
$ sudo ufw delete (that number, for example 5 or 6)

## 2.5. Connecting SSH server

Add forward rule for VirtualBox

1. Go to VirtualBox-> Choose the VM->Select Settings

2. Choose “Network”-> “Adapter 1"->”Advanced”->”Port Forwarding”

![](https://miro.medium.com/max/671/1*rCj_FeuZ5Rm2abz48qhulg.png)

3. Enter the values as shown:

![](https://miro.medium.com/max/700/1*61-KSUCFcerO1wPqBcYISg.png)

4. Restart SSH server (go to the your VM machine)

$ sudo systemctl restart ssh

5. Check ssh status:

$ sudo service sshd status

6. From host side from iTerm2 or Terminal enter as shown below:

$ ssh your_username@127.0.0.1 -p 4242

7. Quit the connection:

$ exit

## 2.6. Set password policy ([source](https://ostechnix.com/how-to-set-password-policies-in-linux/))

This setting enforces how many classes, i.e upper-case, lower-case, and other characters, should be in a password, also the length of the password.

> “To set up a strong password policy, you have to comply with the following requirements:
> 
> • Your password must be at least 10 characters long. It must contain an uppercase letter and a number. Also, it must not contain more than 3 consecutive identical characters. 6 Born2beRoot
> 
> Your password has to expire every 30 days.
> 
> • The minimum number of days allowed before the modification of a password will be set to 2.
> 
> • The user has to receive a warning message 7 days before their password expires.
> 
> • The password must not include the name of the user.
> 
> • The following rule does not apply to the root password: The password must have at least 7 characters that are not part of the former password.
> 
> • Of course, your root password has to comply with this policy.”

Installing password quality checking library (libpam-pwquality):

$ sudo apt-get install libpam-pwquality

Change the length

$ sudo nano /etc/pam.d/common-password

Find the following line:

password [success=2 default=ignore] pam_unix.so obscure sha512

And add an extra word: minlen=10 at the end.

password [success=2 default=ignore] pam_unix.so obscure sha512 minlen=10

To set at least one upper-case letter in the password, add a word ‘**ucredit=-1**’ at the end of the following line.

Find this line:

password    requisite         pam_pwquality.so retry=3 

Add these values (min lower-case 1 letter, min upper-case 1 letter, min digit 1, max same letter repetition 3, whether to check if the password contains the user name in some form (enabled if the value is not 0), the minimum number of characters that must be different from the old password=7, enforce_for_root: same policy for root users):

password    requisite         pam_pwquality.so retry=3 **lcredit =-1** **ucredit=-1 dcredit=-1 maxrepeat=3 usercheck=0 difok=7 enforce_for_root**

It will look like this:

![](https://miro.medium.com/max/700/1*kEDIaQbWGJqO_JbDpPMZgw.png)

/etc/pam.d/common-password

Password expiration:

$ sudo nano /etc/login.defs

Find this part

PASS_MAX_DAYS 9999  
PASS_MIN_DAYS 0  
PASS_WARN_AGE 7

Change it like this:(max 30 days, min number of days(2) allowed before the modification, receive a notification before expiration at least 7 days before)

PASS_MAX_DAYS 30  
PASS_MIN_DAYS 2  
PASS_WARN_AGE 7

Reboot the change affects:

$ sudo reboot

## 2.7. Create group

$ sudo groupadd user42  
$ sudo groupadd evaluating

Check if group created:

$ getent group

## 2.8. Create user and assign into group

Check the all local users:

$ cut -d: -f1 /etc/passwd

Create the user

$ sudo adduser _new_username_

Assign an user into “evaluating” group (This is for when you defend)

$ sudo usermod -aG user42 your_username  
$ sudo usermod -aG evaluating your_new_username

Check if the user is in group

$ getent group user42  
$ getent group evaluating

Check which groups user account belongs:

$ groups

Check if password rules working in users:

$ chage -l your_new_username

## 2.9. Configuring sudoers group

Go to file:

$ sudo nano /etc/sudoers

Add following for authentication using sudo has to be limited to 3 attempts in the event of an incorrect password:

Defaults     secure_path="..."  
Defaults     passwd_tries=3

For wrong password warning message, add:

Defaults     badpass_message="Password is wrong, please try again!"

Each action log file has to be saved in the /var/log/sudo/ folder:

(If there is no “/var/log/sudo” folder, create the sudo folder inside of “/var/log”)

Defaults	logfile="/var/log/sudo/sudo.log"  
Defaults	log_input,log_output

Require tty: (_Why use tty? If some non-root code is exploited (a PHP script, for example), the_ `_requiretty_` _option means that the exploit code won't be able to directly upgrade its privileges by running_ `_sudo_`_._)

Defaults        requiretty

For security reasons too, the paths that can be used by sudo must be restricted. Example : /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

(It was already set there)

Defaults   _secure_path="_/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"

Now my /etc/sudoers file looks like this

![](https://miro.medium.com/max/700/1*N4Ad-9k0vfvnWKNC5q6MjQ.png)

## 2.10. Change hostname (!!!This is for when you defend!!!)

Check current hostname

$ hostnamectl

Change the hostname

$ hostnamectl set-hostname new_hostname

Change /etc/hosts file

$ sudo nano /etc/hosts

Change old_hostname with new_hostname:

127.0.0.1       localhost  
127.0.0.1       new_hostname

Reboot and check the change

$ sudo reboot

## 2.11. Crontab configuration

> “A  **crontab**  file contains instructions for the cron(8) daemon in the following simplified manner: “run this command at this time on this date”

1.  Install the netstat tools

$ sudo apt-get update -y  
$ sudo apt-get install -y net-tools

1.  Place monitoring.sh in /usr/local/bin/

#!/bin/bash  
wall $'#Architecture: ' `hostnamectl | grep "Operating System" | cut -d ' ' -f5- ` `awk -F':' '/^model name/ {print $2}' /proc/cpuinfo | uniq | sed -e 's/^[ \t]*//'` `arch` \  
$'\n#CPU physical: '`cat /proc/cpuinfo | grep processor | wc -l` \  
$'\n#vCPU:  '`cat /proc/cpuinfo | grep processor | wc -l` \  
$'\n'`free -m | awk 'NR==2{printf "#Memory Usage: %s/%sMB (%.2f%%)", $3,$2,$3*100/$2 }'` \  
$'\n'`df -h | awk '$NF=="/"{printf "#Disk Usage: %d/%dGB (%s)", $3,$2,$5}'` \  
$'\n'`top -bn1 | grep load | awk '{printf "#CPU Load: %.2f\n", $(NF-2)}'` \  
$'\n#Last boot: ' `who -b | awk '{print $3" "$4" "$5}'` \  
$'\n#LVM use: ' `lsblk |grep lvm | awk '{if ($1) {print "yes";exit;} else {print "no"} }'` \  
$'\n#Connection TCP:' `netstat -an | grep ESTABLISHED |  wc -l` \  
$'\n#User log: ' `who | cut -d " " -f 1 | sort -u | wc -l` \  
$'\nNetwork: IP ' `hostname -I`"("`ip a | grep link/ether | awk '{print $2}'`")" \  
$'\n#Sudo:  ' `grep 'sudo ' /var/log/auth.log | wc -l`

2. Add the rule that script would execute without sudo password:

Open sudoers file:

$ sudo visudo

Add this line:

your_username ALL=(ALL) NOPASSWD: /usr/local/bin/monitoring.sh

sudoers will look like:

![](https://miro.medium.com/max/700/1*l-7LtAqCon1gRkV3dY3qiQ.png)

sudoers

3. Reboot

$ sudo reboot

4. Execute the script as su:

$ sudo /usr/local/bin/monitoring.sh

5. Open crontab and add the rule:

$ sudo crontab -u root -e

Add at end as follows: (*/10 means every 10 mins the script will show)

*/10 * * * * /usr/local/bin/monitoring.sh

#Tips

1.  If you have this error when you reboot your VM, change the Display settings in your VirtualBox settings. See the solution  [here](https://unix.stackexchange.com/questions/502540/why-does-drmvmw-host-log-vmwgfx-error-failed-to-send-host-log-message-sh).

$ drm:vmw_host_log *ERROR* Failed to send host log message.

# 3. Defense

1.  The basic difference of CentOS and Debian is shown as below.

![](https://miro.medium.com/max/482/1*EUhkzOMoiT_KEF3j402O6g.png)

It is from  [here](https://1gbits.com/blog/debian-vs-centos-comparison/)

2. What is the difference between aptitude and apt?

“Apart from main difference being that  **Aptitude**  is a high-level package manager while  **APT**  is lower-level package manager which can be used by other higher-level package managers, other main highlights that separate these two package managers are:

1.  **Aptitude**  is vaster in functionality than  **apt-get**  and integrates functionalities of apt-get and its other variants including  **apt-mark**  and  **apt-cache**.

While  **apt-get**  handles all the package installation, up-gradation, system-upgradation, purging package, resolving dependencies etc., Aptitude handles lot more stuff than apt, including functionalities of  **apt-mark**  and  **apt-cache**  i.e. searching for a package in list of installed packages, marking a package to be automatically or manually installed, holding a package making it unavailable for up-gradation and so on.” ([source](https://www.tecmint.com/difference-between-apt-and-aptitude/))

![](https://miro.medium.com/max/700/1*vRgjWvlyZsTHhO3_4Qsvlg.png)

[source](https://www.oreilly.com/library/view/implementing-devops-with/9781787120532/8dfaa49e-7885-48f1-8d71-a3535c90aff8.xhtml)

3. Difference between SELinux and APPArmor?

“These security systems provide tools to isolate applications from each other and in turn isolate an attacker from the rest of the system when an application is compromised.

**SELinux**  rule sets are incredibly complex but with this complexity you have more control over how processes are isolated. Generating these policies  [can be automated](http://magazine.redhat.com/2007/08/21/a-step-by-step-guide-to-building-a-new-selinux-policy-module/). A strike against this security system is that its very difficult to independently verify.

**AppArmor**  (and SMACK) is very straight forward. The profiles can be hand written by humans, or generated using  `aa-logprof`. AppArmor uses path based control, making the system more transparent so it can be independently verified.” ([source](https://security.stackexchange.com/questions/29378/comparison-between-apparmor-and-selinux))

![](https://miro.medium.com/max/700/1*wJLXOmrC5eJg_kLZakN9Fg.png)

[source](https://www.slideshare.net/albertspijkers/apparmor-overview-23108025)

# 1. Installation

If you already have installed the OS, you can skip this part.

1.  1. Get the Debian installer image from  [here](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/).

_ISO The_ `_netinst_` _CD is a small CD image that contains just the core Debian installer code and a small core set of text-mode programs (known as "standard" in Debian)._

I chose the standard debian-10.10.0-amd64-netinst.

[](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/)

## Index of /debian-cd/current/amd64/iso-cd

### These are files containing the installer and other software for the Debian GNU/Linux operating system. The files in…

cdimage.debian.org

Put the image in sgoinfre (/sgoinfre/goinfre/Perso/your_login) if you are installing at school.

0. Choose “Save link as” and open the folder as above (sgoinfre…).

1.  2. Installing the Debian 10.

![](https://miro.medium.com/max/700/1*tkjZEbnHKqPGN24HQw_kRA.png)

Choose ”New”

![](https://miro.medium.com/max/678/1*WyFDl98AZfft999XCKD6kA.png)

If you are installing at school environment, choose “sgoinfre”

![](https://miro.medium.com/max/675/1*SoVNIKT340ARlLvQ7RuwDA.png)

Select all as default

![](https://miro.medium.com/max/674/1*PzVboJLyLTs7qJmgbdoBYA.png)

![](https://miro.medium.com/max/694/1*6_D9jIyOW0jE3a6vF_UzXg.png)

![](https://miro.medium.com/max/697/1*HagpR-UD0HWCb7zRTeSQXQ.png)

![](https://miro.medium.com/max/700/1*rYdYJbPswCVCUa5pwKcRZA.png)

![](https://miro.medium.com/max/700/1*V2wtat5wJyBjSEoXatkG0A.png)

Choose “Settings”->”Storage”

![](https://miro.medium.com/max/646/1*je75kGWjXl0M6PlqEzHgoA.png)

Click on Optical Drive’s far right blue small box

![](https://miro.medium.com/max/700/1*VDy31g0tePnUOuJ1cZQsxQ.png)

Choose a ISO image that you already have download

![](https://miro.medium.com/max/700/1*FOldzHFaQ2JS_phe6z6T4g.png)

![](https://miro.medium.com/max/700/1*Evj7Z2EOq102A1zUVgUnQg.png)

![](https://miro.medium.com/max/700/1*Yg53c1-01g4VzTqhcVEEcA.png)

Click “Start” green arrow to start the VM

![](https://miro.medium.com/max/638/1*-tV-M-4g6MH8h6pWJ27bCg.png)

Choose “Install”

![](https://miro.medium.com/max/700/1*xeb8quQ-ccd5X51d8ToZRw.png)

![](https://miro.medium.com/max/700/1*WixFq3GJF9OjeH-zTBTN7Q.png)

![](https://miro.medium.com/max/700/1*zKUk6R9tls_jiyY81ue8kA.png)

![](https://miro.medium.com/max/700/1*r0fzgkzXOjK2DfsBCh7wEQ.png)

Enter the hostname as your login+42

![](https://miro.medium.com/max/700/1*81XjZBZg2bbNXunuxgnFPQ.png)

Leave it as default

![](https://miro.medium.com/max/700/1*ft498oj7syh4zVjI48U_tw.png)

![](https://miro.medium.com/max/700/1*rhJWnMKN0TPBZwqRey9OeQ.png)

![](https://miro.medium.com/max/700/1*fJFibR-WkevpF3fLwyZiag.png)

![](https://miro.medium.com/max/700/1*z4BtcP_BS8UmUzbZNgcCqA.png)

![](https://miro.medium.com/max/700/1*2i7svoURih_UIlRJ87rj5w.png)

![](https://miro.medium.com/max/700/1*CsSx-ALmn8mMxvWicsNVAQ.png)

![](https://miro.medium.com/max/700/1*BTLz5sT6noL_SVQ7eq3u-A.png)

![](https://miro.medium.com/max/700/1*r5zFPA7R_9BtIqwyOpCCVw.png)

![](https://miro.medium.com/max/700/1*NHdo3JbApICz0Co2epPLFA.png)

![](https://miro.medium.com/max/700/1*KHmnCUJUWhf1minIdHNS4g.png)

![](https://miro.medium.com/max/700/1*B0QL-gX7rZW5-RJyTD1uWw.png)

![](https://miro.medium.com/max/700/1*xE1owXa0ttpvcioaEwnutA.png)

![](https://miro.medium.com/max/700/1*SUFMu-qy3rBwIe9B0Bq3kg.png)

![](https://miro.medium.com/max/700/1*yfXpHyGD37OGAOX7qs1Avw.png)

![](https://miro.medium.com/max/700/1*Mfb1YHt4K3pZJ12TF2dXAw.png)

![](https://miro.medium.com/max/700/1*vqV-bN3zDMqTBAKz_u548w.png)

![](https://miro.medium.com/max/700/1*bLnFC6MebhW1-YZlI2n9_A.png)

![](https://miro.medium.com/max/700/1*e08pS8shLNmhZuFUrmuBwA.png)

Leave it blank

![](https://miro.medium.com/max/700/1*1I6fHG3MHuovrarqj9PNnA.png)

![](https://miro.medium.com/max/700/1*lGsuAQEwT0WBhb4kdUMp9g.png)

Deselect “SSH server”, “standard system utilities”. We’ll install it later manually.(To deselect, just hit SPACE key)

![](https://miro.medium.com/max/700/1*b2qXPye_kX8EudSvbO4yww.png)

![](https://miro.medium.com/max/700/1*s3S7D1c1t98nowFfDvJfgg.png)

![](https://miro.medium.com/max/700/1*riuXLYYgESxdq-lpkivFXQ.png)

![](https://miro.medium.com/max/651/1*aLyQeWzQ1etZHbQVQepjBA.png)

![](https://miro.medium.com/max/628/1*frU-8y-PY8aUFo70AGApHw.png)

![](https://miro.medium.com/max/700/1*FlHR1WFfu-Hwmspd2WXNGA.png)

Enter your encryption password

![](https://miro.medium.com/max/700/1*5ynsRmWt6HteSbOWYPxeZw.png)

login as your_username

![](https://miro.medium.com/max/700/1*Y_bimgjp7w49TR4hek3n3g.png)

Run “lsblk” to see the partition
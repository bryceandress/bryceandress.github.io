---
layout: post
title: Quaoar CTF
---

Quaoar is a CTF hosted on VulnHub. This CTF was developed by Viper for Hackfest 2016 and is rated at an easy challenge. As always thank you to VulnHub for hosting these images and Viper for his work on this one.

These machines told you the I.P. pulled when booted. On my network this grabbed a 192.168.1.179 address.

After locating the machine I ran an Nmap scan to see which ports were open and got the following

To start things off I ran Nmap. It found the following ports open
    - 22 which was running SSH
	- 53 which was a Domain Name Server
	- 80 which was running apache
	- 110 pop3
	- 139 netbios-ssn
	- 143 imap
	- 445 Microsoft-ds
	- 993 imap
	- 995 Pop3s

At this point I decided to take a look at the website for this machine. I was greeted with a picture and
a link to another picture. robots.txt had an allow for /wordpress/ so I decided to check that out.

I started with enumerating users with wpscan and found an admin and wpuser accounts. Realizing this was probably
a default install of Wordpress I tried logging in with admin/admin.

Once admin access to wordpress is gained I fired up Metasploit and fired off the /exploit/unix/webapp/wp_admin_shell_upload
payload which gives me a shell on the system as www-data. I then decided to cat the wp-config.php file.
In this file there is MySQL password **rootpassword**. Hoping the password was reused I tried to ssh into the box
with these credentials and luckily I got access. 

In the root directory I found my first flag which was **8e3f9ec016e3598c5eec11fd3d73f6fb**. Realizing I 
probably missed one in the Wordpress install I went back over there and found a flag in the wpadmin directory **2bafe61f03117ac66a73c3c514de796e**.

I could not however find the third flag that was supposed to be on the system and looking at other walkthroughs it
appears others could not as well.

Hopefully this walkthrough gives you enough help to get through the machine without giving you every step, which is
my goal for writing this.

Enjoy!
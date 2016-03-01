---
layout: post
title: Cowrie-Findings
categories: project
---
At the end of the last [post](https://bryceandress.github.io/2016/02/25/HoneyPot-Shenanigans-with-Cowrie/)
 I stated that I would report my findings if anything interesting did happen. I left the server run for 
48 hours with a custom userdb.txt file that allowed a couple of usernames and almost all passwords for the listed usernames. My userdb.txt file
can be found below.

```
root:x:!root
root:x:123456
root:x:*
richard:x:*
richard:x:fout
system:x:*
git:x:*
administrator:x:*
*:x:*
git:x:mafiotsiciliancatasmk112119
root:x:samp
```
Note: The final two passwords were added by cowrie because the attackers
changed the root password to them,

Some other background information if you did not read the first post or the cowrie setup guide, this tool
creates a vulnerable SSH server on port 22 allowing any SSH connection that matches the userdb.txt file.

During the course of the 48 hours this server was running I had 1,204 connection attempts and 521 of the connection attempts
ended up being successful. The majority of these attempts did nothing once connected besides close the connection. It is safe
to assume in these scenarios the bots that were doing the scanning of open SSH ports were just programmed to report a list of IPs
and username/password combinations and nothing else. Of the 1,204 connections attempts  509 of them attempted to use root to gain access to
the machine. Looking back at my userdb.txt file we can see that the only password root did not accept was root. 488 of the successful connections
came from root being the username. 29 of the successful connections came when git was the username and 3 came when system was the username.

The attacks came from 73 different IPs with one IP clocking in 469 attempts, the next closest IP had 240, and the third only had 80. After this the attempt
per IP fall drastically. None of the finally 70 IPs broke 50 attempts.

The userdb.txt did not include very many usernames, some of the most attempted usernames consisted of test, admin, oracle, postgres,
teamspeak, and guest. The full list of attempted usernames can be found [here](https://gist.github.com/bryceandress/1044ddbf27798eacb313).

This is a nice list of what usernames should not be used for SSH but how about the most common passwords that were attempted? This list did not have many
surprises just like the usernames did not. The most frequently attempted passwords consisted of 123456, password, and !@. The full list of
attempted passwords can be found [here](https://gist.github.com/bryceandress/e964e2a0ad1d0d59d652).

The most frequently used username and password combinations consisted of root and user123, test and test, and admin and password. The full list can be
found [here](https://gist.github.com/bryceandress/12971432e0b65b875908).

17 different clients were used to attempted and make connections:

1. SSH-2.0-libssh-0.2

2. SSH-2.0-PuTTY_KiTTY                    
3. SSH-2.0-PuTTY_Release_0.65             
4. SSH-2.0-OpenSSH_7.1                    
5. SSH-2.0-libssh-0.1                     
6. SSH-2.0-PuTTY_Release_0.63             
7. SSH-2.0-PuTTY_Release_0.66             
8. SSH-2.0-libssh2_1.4.2                  
9. SSH-2.0-libssh2_1.4.3                  
10. SSH-2.0-JSCH-0.1.51                 
11. SSH-2.0-libssh-0.6.0                   
12. SSH-2.0-libssh2_1.6.0                  
13. SSH-2.0-Granados-1.0                   
14. SSH-2.0-phpseclib_0.3 (mcrypt, bcmath) 
15. SSH-2.0-PUTTY
16. SSH-2.0-paramiko_1.8.1
17. SSH-2.0-OpenSSH_5.3

However, this list really does not mean anything since these can be spoofed fairly easily.

Of all the successful connections only 13 tried to transfer anything and all 13 seem to make a call to a personal server. I will not post any of the urls
for security and privacy reasons; however, if anyone is interested in looking at the scripts reach out to me. I will say that most of the scripts
tried downloading busybox, which is a collection of *nix utilities which will help the attackers run various other scripts once installed.
Unfortunately since my cowrie user did not have sudo access busybox never successfully installed so most of the scripts terminated before they completely
finished. The only other nifty attempt transfer was a file disguised as a jpg that was actually a tarball inside a zip file. Inside the zip/tarball
there were a couple scripts mostly consisting of port scans on the local network, and lists of username/password combos presumably used to gain access
to other user accounts on the local machine and possibly the network. This looks to be the most advanced attack I encountered and I will most likely do a
write up on what the script does in its entirety at some point.

The most common commands once the attacker gained access to the machine consisted of "ls", "cat /proc/cpuinfo/", and "cd..". The list of commands attempted
can be found [here](https://gist.github.com/bryceandress/7ca2f996b12271c5ca6f). NOTE: Commands that showed an IP were removed from this list and that richard
is the only user on the machine with a simple install of cowrie.

In conclussion,the results are nothing groundbreaking and a good admin should know to avoid using root, any program name, or any service as a username.
Most admins should also know to not use simple passwords especially the ones on this list. Finally, changing the SSH port to something besides 22 will greatly reduce
the number attacks that target you. Following these techniques will greatly increase your chances of not having a server compromised. However, it is important to remember
that these results are only for SSH. The same rules should apply though for other programs that have open ports.


[![Analytics](https://ga-beacon.appspot.com/UA-74486839-1/cowire-findings)](https://github.com/igrigorik/ga-beacon)

---
layout: post
title: Honeypot Shenanigans with Cowrie
---

After reading the latest article in Linux Voice about setting up a honey
pot to monitor incoming attacks I decided to give it a go for myself. Since I do
not have a RaspPi I couldn't follow their article to a T so I did some
research and found [cowrie.](https://github.com/micheloosterhof/cowrie)
Cowrie is a python script that makes ssh vulnerable but still allows the
admin to configure it so he can log back in to check out logs. The install process was very simple I started by going to Digital Ocean
and creating a droplet that would be used for nothing else but this, for
obvious safety reasons. After the droplet was created I ssh'd into the
machine and got to work. The cowrie install.md file has all the
information you will need to get it up and running, but if you runn into
any issues this [article](https://sehque.wordpress.com/2015/07/23/how-to-configure-and-deploy-a-cowrie-ssh-honeypot-for-beginners) should be able to help. The only mistake I made was closing my ssh connection while cowrie was running without an
admin port to allow myself back in. After destroying the droplet
and getting everything to the point right before running I created a
snapshot just incase mistakes were made again. I let cowrie run for about 8 hours before I let myself look at
the logs and when I finally did take a look I was quite surprised at the
amount connections that were made or attempted. The logs are stored inside the
cowrie/logs/tty/ and any files that the attacker tries to move to the
honeypot are stored in cowrie/dl. Unfortunately upon further investigation most of the connections were made by bots and did not really do anything once they gained access to the honeypot, whether this was because they realized it was one or they just simply wanted to document open servers I am not sure. Upon writing this post I have had 45 connection attempts where 28 of them have been successful. If you try this and do not have the same results try allowing more passwords in the userdb file, I allowed any root password to be accepted and that is the account the majority of my connections are taking place on. None of the connections have tried to run any files on my honeypot yet which is rather unfortuante and I will probably keep tabs on this project until I have atleast one file to check out. The last thing I want to take note of is the wonderful MySQL support cowrie has, I set it up and it makes keeping track of who tried to connect super easy. I hope everyone enjoyed this post and if you think about giving this project a try please let me know how it goes.


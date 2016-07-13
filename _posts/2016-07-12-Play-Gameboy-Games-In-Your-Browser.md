---
layout: post
title: Play GameBoy Games in Your Browser
---
This tutorial is going to teach you how to setup a GameBoy emulator that runs in your
browser. First things first you are going to need a box to host this on. I personally
am using a $5 a month DigitalOcean droplet running Ubuntu 16.04 and that is what this
tutorial will assume you have. However, this setup should run on any machine including
Windows but with heavy modifications.

After heading over to DigitalOcean follow this [guide](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04)
 to setup and secure your machine. After that is complete you will want to install
Apache which can be done with.

```
sudo apt-get install apache2
```

After Apache is installed you may want to create a user just for your web directory if
you plan on using this server for other things. However, we are just going to use
the user you created.

Next you want to browse to your web directory and get a copy of
GameBoy-Online files. The commands below should do this for you.

NOTE: git might need to be installed.

```
cd /var/www/html
sudo git clone https://github.com/taisel/GameBoy-Online
sudo chown -R $USER:$USER /var/www/html/
sudo chmod -R 755 /var/www

```
NOTE: $USER:$USER should either be your user or the one you created just for the
GameBoy emulator.

All that is left now is to go and get yourself a copy of your favorite GameBoy game in
ROM format. I would recommend getting your ROMs from [CoolRom](http://www.coolrom.com)
and going to http://yourip/GameBoy-Online

This concludes this quick little tutorial and hopefully everyone can now enjoy their
favorite GameBoy games in their browser.

If you do not want to go through the process of setting this up feel
free to use [mine.](http://104.131.54.214/GameBoy-Online/)

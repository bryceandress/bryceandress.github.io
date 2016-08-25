---
layout: post
title: IceCTF 2016 Corrupt Transmission Writeup
---

Corrupt Transmission, 50 pts, Forensics

This challenge we are given a png file that appears to be corrupted.

After opening this up in Bless Hex Editor and pulling up the PNG Header
info on Wikipedia it is easy to see that they are not the same.

The correct PNG header is 89 50 4E 47 0D 0A 1A 0A so we can go ahead and
edit this in and open it up in our favorite image viewer and see our flag
is

IceCTF{t1s_but_4_5scr4tch}

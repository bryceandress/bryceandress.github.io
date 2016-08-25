---
layout: post
title: IceCTF 2016 Complacent Writeup
---

Complacent, 40 points, reconnaissance

This challenge was the first of stage 2 however, it is still a quite simple problem.

First you want to go to (http://complacent.vuln.icec.tf)

For this challenge I used Google Chrome. Once at the site I noticed the SSL
cert was red telling me something was wrong. So I clicked on the https://
lock and in the pop up clicked details.

This opens another window. In this window there is a place to view the cert and hidden in the General portion of the cert you see the flag
**IceCTF{this_1nformation_wasnt_h1dd3n_at_a11}**

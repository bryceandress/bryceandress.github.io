---
layout: post
title: When in Rome Writeup
---

10 points, cryptography

When in Rome is the first challengeof the 2016 sctf and at 10 points it is the perfect
starting challenge. To begin you are given the string "Nvctfdv kf jTKW! Nv yfgv pfl veafp kyv gifscvdj nv yrmv nizkkve wfi kyv wzijk hlrikvi fw 2016. Yviv zj pfli wzijk fw (yfgvwlccp) drep wcrxj! jtkw{ny3e_1e_tkw_u0_r5_tkw3i5_u0}"

Judging by the name and my basic understanding of crypto I figured this was a Rot probelm.

Now you can do this by hand but I decide to go to [planetcalc](http://www.planetcalc.com/1434)

This website allows you to enter a string and it figures out all the ROTs for you.
After going through all the possiblities it is really easy to see that ROT9 is what we are looking for.

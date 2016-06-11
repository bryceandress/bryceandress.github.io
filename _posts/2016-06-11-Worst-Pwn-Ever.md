---
layout: post
title: Worst-Pwn-Ever Backdoor2016
---

Worst-Pwn-Ever was a 100 point pwn challenge from Backdoor2016. Here is the description:

```
tocttou is an enviornmentalist. But some say he has a vicious motive and he uses nature to hide his dark side. We found a weird shell on his amazon (pun inteded) web services. Can you tell us what is he upto? Tip: he might shut down the machine if he notices you - and he will (maybe in 45 seconds).
Access: nc hack.bckdr.in 9008
Created by: Ashish Chaudhary
```

The binary for this challenge can be found on Backdoor's website.

When this challenge is run you are launched into what looks to be a limited shell. After
running a couple misc. linux commands (I should have documented which it was but I did not)
including I was able to get a NameError: error which led me to believe this was a python program.
At this point I tried a import os command, which is a python library that can run system
commands like "cat flag" but that also led to a NameError.

After a couple other failed ideas and a night of sleep I tried a __builtins__ function,
which was:

```
input(__builtins__.__import__('os'))
```
which worked!

Great, now we know how to import system we just need to locate the flag. Luckily the
title is a big clue for this Pwn sounds a lot like pun. So I reread the description
and realized it said enviromentalist so I thought lets check the enviroment variables,
with os this is easy enough! The finally working code was then this:

```
input(__builtins__.__import__('os').system("printenv"))
```

which got us our flag!


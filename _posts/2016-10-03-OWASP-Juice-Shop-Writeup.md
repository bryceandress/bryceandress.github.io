---
layout: post
title: OWASP Juice Shop Walkthrough
---

Hello all, it has been quite a while since I posted a writeup on anything so today I am going to start a post about the OWASP Juice Shop.
This is a newer VM put out by OWASP that includes vulnerabilities from their top 10 list. I am going to start with the first one on the 
scoreboard which is insanely easy! 

Scoreboard:

Juice Shop comes with a scoreboard but it is not easily accessible from somewhere on the website. In order to get this challenge you need 
read through the source on the homepage and about 2/3 of the way down you will find a commented out link which brings you to the 
scoreboard gaining you your first points.

Provoke and Error:

This challenge is second the scoreboard and just like the first very easy to solve. After a little searching I decided to search with a 
leading ' I threw some junk behind it and ended up with 'adk312fd triggering the scoreboard to award me the points. I believe this could be accomplished with just the ' or anything after it but I need to reset the machine to find out for sure.

Log in to Admin Account:

This is the first real "hacking" challenge but is still not incredibly difficult. To solve this one I fired up burp and captured a test b
post packet. I then went to the intruder tab and editted the positionis to just the email. I then went to payloads and passed it the 
fuzzdb xplatform.txt file. Let intruder do its thing and you eventually get a 200 response with a' or 1=1 You can then use this on the 
web form and get the admin scoreboard to trigger.
TO BE CONTINUED.

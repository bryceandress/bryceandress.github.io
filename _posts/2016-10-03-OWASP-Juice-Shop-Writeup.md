---
layout: post
title: OWASP Juice Shop Walkthrough
---

Hello all, it has been quite a while since I posted a writeup on anything so today I am going to start a post about the OWASP Juice Shop.
This is a newer VM put out by OWASP that includes vulnerabilities from their top 10 list. I am going to start with the first one on the 
scoreboard which is insanely easy! 

**Scoreboard:**

Juice Shop comes with a scoreboard but it is not easily accessible from somewhere on the website. In order to get this challenge you need 
read through the source on the homepage and about 2/3 of the way down you will find a commented out link which brings you to the 
scoreboard gaining you your first points.

**Provoke and Error:**

This challenge is second the scoreboard and just like the first very easy to solve. After a little searching I decided to search with a 
leading ' I threw some junk behind it and ended up with 'adk312fd triggering the scoreboard to award me the points. I believe this could be accomplished with just the ' or anything after it but I need to reset the machine to find out for sure.

**Log into Admin Account:**

This is the first real "hacking" challenge but is still not incredibly difficult. To solve this one I fired up burp and captured a test b
post packet. I then went to the intruder tab and editted the positionis to just the email. I then went to payloads and passed it the 
fuzzdb xplatform.txt file. Let intruder do its thing and you eventually get a 200 response with a' or 1=1 You can then use this on the 
web form and get the admin scoreboard to trigger.

**XSS Tier 1:**

This is a rather simple challenge. When you look at the scoreboard it wants <script>alert("XSS1")</script> to execute. Normally for xss you place it in some input area for this challenge I chose the search bar and that executed it. I am sure there are some other places on the site to also do this.

** Log into Admin Account without SQLi:**

For this challenge we are going to harness the power of Burp Intruder again. Inside the positions tab edit the request so this time it says admin@juice-sh.op and make the password variable. Then go into the payloads tab load your rockyou.txt file that can be found online pretty simply (If you need it email me) and fire away. Itll take a couple minutes but you will eventually get a 200 request with the result being password123.


TO BE CONTINUED.

---
layout: post
title: OWASP Juice Shop Walkthrough
---

Hello all, it has been quite a while since I posted a writeup on anything so today I am going to start a post about the OWASP Juice Shop.
This is a newer VM put out by OWASP that includes vulnerabilities from their top 10 list. I am going to start with the first one on the 
scoreboard which is insanely easy! 

#Scoreboard:

Juice Shop comes with a scoreboard but it is not easily accessible from somewhere on the website. In order to get this challenge you need 
read through the source on the homepage and about 2/3 of the way down you will find a commented out link which brings you to the 
scoreboard gaining you your first points.

#Provoke and Error:

This challenge is second the scoreboard and just like the first very easy to solve. After a little searching I decided to search with a 
leading ' I threw some junk behind it and ended up with 'adk312fd triggering the scoreboard to award me the points. I believe this could be accomplished with just the ' or anything after it but I need to reset the machine to find out for sure.

#Log into Admin Account:

This is the first real "hacking" challenge but is still not incredibly difficult. To solve this one I fired up burp and captured a test b
post packet. I then went to the intruder tab and editted the positionis to just the email. I then went to payloads and passed it the 
fuzzdb xplatform.txt file. Let intruder do its thing and you eventually get a 200 response with a' or 1=1 You can then use this on the 
web form and get the admin scoreboard to trigger.

#XSS Tier 1:

This is a rather simple challenge. When you look at the scoreboard it wants `<script>alert("XSS1")</script>` to execute. Normally for xss you place it in some input area for this challenge I chose the search bar and that executed it. I am sure there are some other places on the site to also do this.

#Log into Admin Account without SQLi:

For this challenge we are going to harness the power of Burp Intruder again. Inside the positions tab edit the request so this time it says admin@juice-sh.op and make the password variable. Then go into the payloads tab load go to /usr/share/dirb/big.txt  (If you need it email me) and fire away. Itll take a couple minutes but you will eventually get a 200 request with the result being admin123.

#Give a Devastating 0 Star Review & Leave a Review with Someone Elses Account:

I decided to combine these 2 challenges because they are pretty similiar and why would you want to tamper with a site with your own account? So to get this one rolling you need to go back to the website go to the Feedback tab and leave a review with any stars and with your email (admin). Then go into Burp and send the packet you just sent to the Juice Shop to repeater by right clinking and clicking Send to Repeater. Once in repeater go ahead and edit the id from 0 to 1 and the stars to 0. Then go ahead and send this packet. If you go back to the site you should see the notifications for both challenges.

#Access Someone Else's Basket

Following suit with the packet injections this one you make a request to your basket. Then go into Burp find that packet send it to repeater and modify the GET request from /rest/basket/1 to /rest/basket/2 and hit Go. If you go back to Juice-Shop you should have the notification waiting for you that you got the challenge.

#Place an Order that Makes You Rich:

I believe I did this challenge wrong but hey it works. So add a bunch of items to your cart. Then go into Burp and look at one of the requests. There will be a quantity, change this value to a very small negative number like -100000 and forward the packet. Now forwarding the packet should just place it in your basket but mine actually redirected me to past the checkout button where you get your receipt. I am not sure if this was designed or I found another bug. Regardless you should be able to press Checkout after changing the quantity and get the correct result.

#Access a Hidden File, find the Easter Egg, Access a Salesman's Backup, and Access a Developer's Backup 
I grouped all these challenges together because they all follow the same basic format. First we need to do something you should normally do in the beginning and that is ennumerate the website. To do this I ran the command dirb http://127.0.0.1:3000. This gave me a result of all the hidden directories on the server. Browsing to 127.0.0.1:3000/ftp (which was a result) brings us to a page which lists a bunch of files. You can access legal.md and acquisitions.md but all the other files you get errors. At this point if you were to look at the scoreboard you would see that you have scored the Access a Hidden File challenge but known of the others. 

This is where a technique called Null-Byte Injection comes in. To do this you click on a file, lets say eastere.gg. It will bring you to an error page, this is alright. Now go to the url bar and add %2500.pdf and you should be able to download a copy of eastere.gg. If you go to the scoreboard now you will see you scored the Easter Egg challenge. Do this for the rest of the files on the ftp page and you will also get Access a Salesman's Backup and Access a Developer's Backup. 



#If you have any questions or need further explanation on any challenges please let me know

#TO BE CONTINUED.

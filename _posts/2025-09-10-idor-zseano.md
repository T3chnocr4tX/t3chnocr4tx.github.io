---
title: Check out these HackerPhotos! Nothings wrong here.
description: >-
  We've created a basic web application called "HackerPhotos" to hightlight some awesome hacker-tagged photography. It is just in BETA and we'd love for you to give it a try and make sure we've not made any mistakes!
date: 2025-09-10 20:55:00 +0800
categories: [Labs]
tags: [IDOR]
image:
  path: assets\img\bug1.png
  alt:  IDOR
pin: true
---


# Bug Bounty Hunter

## Check out these HackerPhotos! Nothings wrong here

***
This afternoon, I was like, "Let me practice some labs on IDOR." I just opened my laptop and searched for some IDOR stuff. Then I found these bug bounty hunter labs by Zseano on IDOR. So, I solved the labs, and let’s take a look at ‘em. To be honest, the labs just give you some description—they don’t even give you pointers like “look for flags” or anything, kinda similar to Hacker101 CTF. I think the purpose of the labs is to teach manual testing. So, let’s leave that rant aside. Here’s the lab description if you wanna follow along...... [idor](https://www.bugbountyhunter.com/challenge?id=10)
***


**_We've created a basic web application called "HackerPhotos" to hightlight some awesome hacker-tagged photography. It is just in BETA and we'd love for you to give it a try and make sure we've not made any mistakes!_**


With that being said, log in to your account. At first, when I logged in, I tried to look for some button where I could click but found nothing. I was just like, "What the...?"

![bug11](https://github.com/user-attachments/assets/57e139a3-8e11-458c-b859-39ce1bbe3334)

So, I checked my web proxy and found a JS extension. So, let’s take a look at it.

![bug4](https://github.com/user-attachments/assets/83676803-0fe4-4b6b-9fc3-cf4eb525cb08)

Then I found a path in the JS file where it appears that the web application retrieves a user ID from a cookie and uses it to fetch user data from a server.

![3](https://github.com/user-attachments/assets/98c3b6cc-24be-41ad-b006-7a0187c75c88)

- So, I checked my cookies and saw some long value in the user ID, but how can this be guessable?
But, you know, thinking in my head, let me just copy this path and add a numerical value. then it appeared I could see some information.


Then I sent the request to automate enumeration, thinking maybe I could get other users' information. Then I found 7 people. Wow, what an IDOR!

![bug62](https://github.com/user-attachments/assets/f6211f72-a2c6-4936-b391-62f2610d4862)

So, that’s it, guys. The tip is to just use the application like a normal user, then check the JS file to understand the application.
Catch you guys later, I’ll be dropping more blogs.

Here is my Twitter account @[T3chnocr4tX](https://x.com/T3chnocr4tx)

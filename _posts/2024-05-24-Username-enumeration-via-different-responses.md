---
title: Username enumeration via different responses
description: This lab is vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password.
date: 2024-05-24 11:33:00 +0800
categories: [Web Security Academy Labs]
tags: [username enumeration, Authentication]
pin: true
math: true
mermaid: true
image:
  path: https://static.vecteezy.com/system/resources/previews/025/463/773/non_2x/hacker-logo-design-a-mysterious-and-dangerous-hacker-illustration-vector.jpg
  alt: password-reset-poisoning
---


***
# Authentication
### Lab#: Username enumeration via different responses
***

Hola 👋, welcome back! Here is my write-up on [Username Enumeration via Different Responses](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses) on Web Security Academy, where I will go through how I approached it. This lab is vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password.


***
### End Goal :#
- Solve the lab, enumerate a valid username, brute-force the user's password
- Then access the account page.

### Username enumeration
**_Username enumeration is when an attacker is able to observe changes in the website's behavior in order to identify whether a given username is valid._**

***
### Testing for vulnerabilities
We are given a wordlists for the username and password:

[Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)

[Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

- Accessing the lab, let's check for the features and functionality of the web app to know what type of vulnerabilities to look for. It is a blog site 😎

![1](https://github.com/T3chnocr4t/T3chnocr4t.github.io/assets/115868619/69ac04d5-8bec-4a6f-9ffe-054cc1d102a9)

- Let's go to the login page and submit an invalid username and password and see if we get an 'invalid username' message.

![2](https://github.com/T3chnocr4t/T3chnocr4t.github.io/assets/115868619/b3fd2771-27fa-4597-b9ad-f7d8c9e112ae)

- In Burp, go to Proxy > HTTP history tab and find the POST /login request. Send it to the Repeater tab so we can see it clearly there.

![3](https://github.com/T3chnocr4t/T3chnocr4t.github.io/assets/115868619/79843416-420f-4713-bc31-7e551b408077)

- Highlight the value of the username parameter in the request and send it to Burp Intruder. Go to Burp Intruder in the Positions tab. We can see that the username parameter is automatically set as a payload position, indicated by two § symbols. And select the attack type to sniper.

![4](https://github.com/T3chnocr4t/T3chnocr4t.github.io/assets/115868619/dcfa48b5-2543-4580-bd30-75f906872ebd)

- After that, go to the Payloads tab and make sure that the Simple list payload type is selected. Under Payload settings, paste the list of candidate usernames. and, click Start attack.

![5](https://github.com/T3chnocr4t/T3chnocr4t.github.io/assets/115868619/1ecd1812-1058-4a27-abd6-3dd7ac1f0f82)

- When the attack is complete, on the Results tab, check the Length column. Notice that one of the entries is longer than the others. Compare the response to this payload with the other responses. Notice that the other responses contain the message 'Invalid username,' but this response says 'Incorrect password,' i.e., we now know the username.

![6](https://github.com/T3chnocr4t/T3chnocr4t.github.io/assets/115868619/2d01de38-ea14-4417-8e63-b9c59194786a)

- So, let's close the attack and go back to the Positions tab. Click Clear, then change the value of the username parameter to the username we found. Add a payload position to the password parameter.
- On the Payloads tab, clear the list of usernames and replace it with the list of candidate passwords. Then click Start attack.
- When the attack is finished, let's look at the Status column. Notice that each request received a response with a 200 status code except for one, which got a 302 response. This indicates that the login was successful.

![7](https://github.com/T3chnocr4t/T3chnocr4t.github.io/assets/115868619/20e27afa-5c21-48d4-b627-16b2adbc91e5)

- Now that we know the username and password, let's log in to access the account and solve the labs.
- Note: yours might be different because it unpredictable.

![giphy](https://github.com/T3chnocr4t/T3chnocr4t.github.io/assets/115868619/f676abd6-e5a8-4e9c-9f44-fa3f9c7408e0)

![8](https://github.com/T3chnocr4t/T3chnocr4t.github.io/assets/115868619/93d3fd11-55f6-42ec-9c2a-2edc07eee44c)

That's all, friends. Thank you for reading up to this point. I would like to hear your feedback on anything not clear here. Here is my Twitter account @[T3chnocr4t](https://twitter.com/T3chnocr4tx). Feel free to DM me if you have any issues with my write-up. Thanks!

[Go Back Home](https://t3chnocr4tx.github.io/)
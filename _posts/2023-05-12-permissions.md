---
title: Pico CTF (Permissions)
author: josephkimiri
date: 2023-05-12 20:22:00 +0300
categories: [CTFs, Web]
tags: [picoctf, ctfs, web, cybersecurity]
render_with_liquid: false
image: /assets/img/blog/permissions.png
---

## Permissions

AUTHOR: GEOFFREY NJOGU

Description
Can you read files in the root file?
Additional details will be available after launching your challenge instance.

After starting the challenge we get more info
The system admin has provisioned an account for you on the main server:
ssh -p 56038 picoplayer@saturn.picoctf.net
Password: Sd9KYTm5kr
Can you login and read the root file?

## Solution
Remember the challenge `chrono`, well this also tests the same concept.
1. First ssh to the server 
`ssh -p 56038 picoplayer@saturn.picoctf.net`
![image](https://user-images.githubusercontent.com/98275198/237027427-21a17fc5-a7e5-4e85-b004-5f6ca9c8471c.png)
2. Navigate to root folders `cd ../..`
3. We see a folder `challenge`
4. On the folder there is a file `metadata.json`
5. When we cat the file, we get our flag.
![image](https://user-images.githubusercontent.com/98275198/237028324-64f2b1c5-6b0b-4b30-bd19-9ab989e548e8.png)


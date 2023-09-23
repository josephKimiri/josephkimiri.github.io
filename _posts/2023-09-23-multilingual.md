---
title: Multilingual
author: josephkimiri
date: 2023-09-23 22:27:00 +0300
categories: [CTFs, Web]
tags: [SheHacks Intervarsity CTF, mobile, cybersecurity]
render_with_liquid: false
image: /assets/img/blog/multi.png
---

# SheHacks Intervarsity CTF

Over the weekend, I had the opportunity of attending the Intervarsity CTF organized by Shehacks Kenya 
whith my school's CTF team @Dumb1d0r3♾️🟰♾️

![image](https://user-images.githubusercontent.com/98275198/270124581-f07bcdb0-aecb-4667-a1b3-99a28083c024.png)
I and my team solved some few challenges and we had fun playing and learning.

I'll take you through some of the challenges we solved.

# Android
## Multilingual
The first challenge was called `Multilingual` and was pretty easy.

*I can't seem to pick out the hidden message. Can you assit? [multilingual.apk](https://shehacks.ciphercode.dev/files/301764f949fdfc5c86d24e1ee7bac16d/multilingual.apk)*

## solution
I solved this one quite easy. We get an android APK file and we are to find the flag.

![image](https://user-images.githubusercontent.com/98275198/270125053-1720c4d7-f9fb-41fb-9542-5c3274f11b1b.png)

I first decompile the application with `apktool`.

![image](https://user-images.githubusercontent.com/98275198/270125136-4c2f5015-4391-44f5-b164-2b7350e98ecf.png)

I then went ahead to grep the strings with words like `flag` and was able to capture interesting encoded strings.

![image](https://user-images.githubusercontent.com/98275198/270125232-be3cc680-2ee8-4e4d-a9ef-bc742901ef2f.png)

I then went ahead to arrange the identified parts in the order `part1`,`part2`,`part3` to form `ZmxhZ3tDNGxsX00zX011bHQxbDFuZ3U0bH0=`

This been base64 encoded, I decoded it using `echo "ZmxhZ3tDNGxsX00zX011bHQxbDFuZ3U0bH0" | base64 -d` and we got our flag.

![image](https://user-images.githubusercontent.com/98275198/270125429-2add6c3a-1ce4-42ac-a312-199b92b3eb7e.png)

That was it for that challenge.

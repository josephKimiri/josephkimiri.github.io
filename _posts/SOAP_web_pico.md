---
title: SOAP Pico-CTF
author: josephKimiri
date: 2023-05-12 10:07:00 +0800
categories: [CTF, Cybersecurity]
tags: [ctfs, picoctf, web]
math: true
mermaid: true
---
## SOAP
CHALLENGE AUTHOR: GEOFFREY NJOGU

Description
The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?
Web Portal

## Solution
Well this challenge reminded me of LFI (local File Inclusion). It was an interesting challenge, I loved it.
Let's get started, shall we?

1. Connect to the challenge via the provided url.
![image](https://user-images.githubusercontent.com/98275198/237692084-0bdda3b2-d458-4413-ba69-fe393c7f890e.png)

2. It looks very much static, I try the `Detail` buttons to check what they load and I proxy my requests through burp.

![image](https://user-images.githubusercontent.com/98275198/237692586-ecf18beb-fb3b-4326-9a64-44a1f1246aea.png)

3. We get a path `/data` that appends an xml code snippet with the id parameter.

![image](https://user-images.githubusercontent.com/98275198/237693087-03360966-968c-4adf-ac71-f802819bc0ba.png)

4. I immediately start crafting xml PoCs to dump the `/etc/passwd`
5. I come up with

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE data [
  <!ENTITY readfile SYSTEM "file:///etc/passwd">
]>
<data>
  <ID>&readfile;</ID>
</data>
```
6. I remove the existing xml and replace it with my crafted xml.

![image](https://user-images.githubusercontent.com/98275198/237694007-782e85e1-d1d3-405d-b0db-093752f408fe.png)

7. Sending the request, we get a response dumping the `/etc/passwd` and at the end of it we get our flag.

![image](https://user-images.githubusercontent.com/98275198/237694521-4640f0d1-0421-46dd-9cc7-dbea8c657f5a.png)

That is it. Stay vigilant in the digital wild west. Happy Hacking
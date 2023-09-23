---
title: Secured Notes
author: josephkimiri
date: 2023-09-23 22:27:00 +0300
categories: [CTFs, Web]
tags: [SheHacks Intervarsity CTF, ctfs, mobile, cybersecurity]
render_with_liquid: false
image: /assets/img/blog/secured-notes.png
---

## Secured Notes 
*I created an application to retrieve my secrets. Is it realy secured?*
[SecuredNotes.apk](https://shehacks.ciphercode.dev/files/eb87b76700359036b1bc6ae2ad7f01da/SecuredNotes.apk?token=eyJ1c2VyX2lkIjoxMCwidGVhbV9pZCI6NywiZmlsZV9pZCI6MTF9.ZQ8vSQ.NzsB7kKBpwgGlfyBS368JHpKAxE)

## Solution
Here, we were given an apkfile and we were tasked into finding whether the app was handling secrets well. 
I decompiled the app using `apktool` using the command `apktool d SecuredNotes.apk`

![image](https://user-images.githubusercontent.com/98275198/270125873-5035f2a0-cf44-4fc8-a3a4-342fd5cf7289.png)

I then went into the folder containing the application and grepped for the key words **secret** & **flag**

![image](https://user-images.githubusercontent.com/98275198/270125976-dcdec05f-c4d7-4607-89d5-895e1b8cd3d6.png)

We get a base64 like string `DQkYFA8aWxkBCFUdQBAtHB8XWgseACtGXgURNBZKEAZBGxgY`, but after decoding it we realize it is messed up somehow.

![image](https://user-images.githubusercontent.com/98275198/270126074-c1674a58-3fda-4ae2-8ed6-f8b6f32c83c3.png)

We then grep for `secret` and we immediately get a hit.

![image](https://user-images.githubusercontent.com/98275198/270126136-2f94ec52-5eed-491c-8458-331bd614d8a0.png)

Trying to decode it, we get a string `ekortsyek` that initially I thought was the password for the notes app.

![image](https://user-images.githubusercontent.com/98275198/270126988-6f2467ed-48de-4d11-accb-e84b91813ba2.png)

Now we need a script to help us read the flag and secret.
```python3
#!/usr/bin/python3

import base64

def decode_base64(data):
    return base64.b64decode(data).decode('utf-8')

def xor_strings(s1, s2):
    return ''.join(chr(a ^ b) for a, b in zip(s1, s2))

decoded_secret = decode_base64("ZWtvcnRzeWVr")[::-1]

decoded_flag = decode_base64("DQkYFA8aWxkBCFUdQBAtHB8XWgseACtGXgURNBZKEAZBGxgY")


flag = xor_strings(decoded_flag.encode('utf-8'), (decoded_secret * len(decoded_flag)).encode('utf-8'))

print(flag)
          
```
Running the script, we get our flag.

![image](https://user-images.githubusercontent.com/98275198/270127902-d452c949-dfcb-48e9-a06f-7d8cf2e040e3.png)

I was not able to solve the other Android challenges during the CTF but will definitely look into them later.

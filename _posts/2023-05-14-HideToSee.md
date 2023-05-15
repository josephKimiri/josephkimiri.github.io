---
title: Pico CTF (HideToSee)
author: josephkimiri
date: 2023-05-14 10:46:00 +0300
categories: [CTFs, Cryptography]
tags: [picoctf, ctfs, cryptography, cybersecurity]
render_with_liquid: false
image: /assets/img/blog/atbash.jpg
---

## HideToSee

AUTHOR: SUNDAY JACOB NWANYIM

Description
How about some hide and seek heh?
Look at this image [here](https://artifacts.picoctf.net/c/237/atbash.jpg).

## Solution

This challenge was tricky as it required some forensics and then understanding atbash cipher.
Let's get started, shall we?
1. Download the given image.
2. As I said, this challenge required some forensics skills.
3. Since the hint said we extract the image, I went to my forensics toolkit and chose `stegseek`.\
Stegseek is a powerful command-line tool designed to detect and extract hidden messages or data concealed within various digital media files, such as images or audio files. It utilizes a technique called steganography, which involves hiding information within another file without arousing suspicion.
4. I used stegseek to bruteforce the image by running `stegseek atbash.jpg` 
![image](https://user-images.githubusercontent.com/98275198/238173319-bd774d57-86c6-4d7b-b0e3-808fd6f5b133.png)
5. Lucky us, we find the encrypted text and it is stored in `atbash.jpg.out`.
6. Let's now cat the encrypted text by running `cat atbash.jpg.out`.
![image](https://user-images.githubusercontent.com/98275198/238173437-09c2bb26-96d7-4a35-be8a-fd137a948be9.png)
7. We get an atbash encrypted text. `krxlXGU{zgyzhs_xizxp_05y2z65z}`
The Atbash cipher is a simple substitution cipher that operates by reversing the alphabet. It is one of the oldest known encryption techniques, dating back to ancient times. In this cipher, each letter of the alphabet is replaced with its corresponding letter from the opposite end.
8. I now head over to [cyberchef](https://gchq.github.io/) which is a simple, intuitive web app for analysing and decoding data without having to deal with complex tools or programming languages.
9. Search for atbash cipher and place your encrypted text on the input box. 
![image](https://user-images.githubusercontent.com/98275198/238173672-d6bafd8a-758f-4a85-892f-3d7ce4e0a23d.png)

We finally get our flag. That's it read my other writeups and hack ethically.



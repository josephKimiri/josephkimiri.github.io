---
title: PcapPoisoning
author: josephkimiri
date: 2023-05-12 11:45:00 +0300
categories: [CTFs, Forensics]
tags: [picoctf, ctfs, forensics, cybersecurity]
render_with_liquid: false
---

## PcapPoisoning

AUTHOR: MUBARAK MIKAIL

Description
How about some hide and seek heh?
Download this file and find the flag.

## Solution
1. This challenge was pretty easy, Download the packet capture [file](https://artifacts.picoctf.net/c/371/trace.pcap)
2. Then even without firing `wireshark`, we use strings and grep and look for the flag format `picoCTF{}`
`strings trace.pcap | grep -E "pico"`
3. We immedietely get the flag.
![image](https://user-images.githubusercontent.com/98275198/237201868-5a01fc94-260f-4460-8b72-dfc8d19b0c77.png)

Eazy Peazy
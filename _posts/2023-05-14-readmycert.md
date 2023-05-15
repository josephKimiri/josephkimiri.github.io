---
title: Pico CTF (ReadMyCert)
author: josephkimiri
date: 2023-05-14 18:33:00 +0300
categories: [CTFs, Cryptography]
tags: [picoctf, ctfs, cryptography, cybersecurity]
render_with_liquid: false
image: /assets/img/blog/ReadMyCert.png
---

## ReadMyCert

AUTHOR: SUNDAY JACOB NWANYIM

Description
How about we take you on an adventure on exploring certificate signing requests
Take a look at this CSR file [here](https://artifacts.picoctf.net/c/422/readmycert.csr)

## Solution

In this challenge, we shall learn how to read CSR(certificate signing requests) using `openssl`
OpenSSL is a widely-used cryptographic library that includes a command-line tool for working with CSRs.
Let's solve this challenge, shall we?
1. Download the given `readmycert.csr`. 
2. Use the `file` to read the certificates properties.
![image](https://user-images.githubusercontent.com/98275198/238194166-eeef8f47-cdde-4d50-9f01-8d64c68a162d.png)
3. Let's view the contents of the certificate by running `cat readmycert.csr`
![image](https://user-images.githubusercontent.com/98275198/238194243-944fbb77-e5e0-47e4-92e1-adf230112f20.png)
4. Now, lets get all details of the CSR using the command `openssl req -in readmycert.csr -noout -text` which will display the CSR details, including the subject, organization, common name, and other relevant information.
5. Lets understand the commands in details.
  - Flag/Option: `openssl`
    : This is the command-line tool used to perform various cryptographic operations using the OpenSSL library.
  - Flag/Option: `req`
    : It is a subcommand of OpenSSL specifically used for working with certificate requests, including CSRs.
  - Flag/Option: `-in your_csr_file.csr`
    : This flag specifies the input file for the CSR. Replace your_csr_file.csr with the actual path and filename of your CSR file.
  - Flag/Option: `-noout`
    : This flag instructs OpenSSL not to output the actual certificate but only display the CSR's text representation. It prevents generating any output other than the textual information.
  - Flag/Option: `-text`
    : This flag tells OpenSSL to display the CSR details in a human-readable format. It provides a comprehensive view of the CSR's contents, including the subject's distinguished name (DN), public key information, and any other attributes included in the request.
6. We get our flag in the subject of the certificate.
![image](https://user-images.githubusercontent.com/98275198/238194704-d37bcdde-2d83-45d8-8066-d7b9543edba8.png)
That is it, I hope you learnt a thing or two from this challenge.
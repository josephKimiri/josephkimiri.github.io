---
title: Pico CTF (Specialer)
author: josephkimiri
date: 2023-05-12 11:50:00 +0300
categories: [CTFs, General]
tags: [picoctf, ctfs, general, cybersecurity]
render_with_liquid: false
image: /assets/img/blog/Specialer.png
---
## Specialer
AUTHOR: LT 'SYREAL' JONES, ET AL.

Description
Reception of Special has been cool to say the least. That's why we made an exclusive version of Special, called Secure Comprehensive Interface for Affecting Linux Empirically Rad, or just 'Specialer'. With Specialer, we really tried to remove the distractions from using a shell. Yes, we took out spell checker because of everybody's complaining. But we think you will be excited about our new, reduced feature set for keeping you focused on what needs it the most. Please start an instance to test your very own copy of Specialer.
ssh -p 59255 ctf-player@saturn.picoctf.net. The password is 483e80d4

## Solution
This was a fun challenge, I enjoyed playing this one. Let's get started, shall we? 

1. First we connect to the server via ssh `ssh -p 59255 ctf-player@saturn.picoctf.net` 
![image](https://user-images.githubusercontent.com/98275198/237124488-5858c0e1-f6b7-4ab5-a089-445516f93b24.png)
2. I try using normal linux commands but most of the commands don't work exept for some.
![image](https://user-images.githubusercontent.com/98275198/237125215-2573c7a2-f548-49ab-a2f1-7a55aa8fa167.png)
3. To list all the commands that the system allows, I press `tab` twice.
![image](https://user-images.githubusercontent.com/98275198/237125612-e116eb56-8fc1-435f-838e-70d87b16663b.png)
4. Now, lets try see how we can use the `echo` command to cat items.
5. Assuming the flag is in `flag.txt`, I will need to improvice how I can read the file since the `cat` command is not available.
6. The following command `echo $(<flag.txt)` can be used to print out the contents of `flag.txt`
7. Back to the challenge, I now need to figure out where the flag is stored.
8. I use `cd ../..` and press `tab` twice to execute.
![image](https://user-images.githubusercontent.com/98275198/237127521-6d29bbdd-2437-463e-9369-75fa98b1f3d4.png)
9. Now, let's navigate to the home directory to see what is there. `cd home/` and again press `tab` twice to execute.
10. Here we get into another directory called `ctf-player` which has several files and folders
![image](https://user-images.githubusercontent.com/98275198/237129150-786bdcbe-c3f9-45dd-9d46-6e6b9882c436.png)
11. Let us try printing the contents of each folder.
12. I start with the `abra` folder and cat the contents of the two txt files. `echo $(<cadabra.txt)`
![image](https://user-images.githubusercontent.com/98275198/237130646-6b5b6917-bad2-4e66-8694-e3ef27d8edc4.png)
13. I then cat `cadaniel.txt` using `echo $(<cadaniel.txt)`
![image](https://user-images.githubusercontent.com/98275198/237131004-15cc4adc-8653-43c4-ad04-c0b1fd997548.png)
14. I then proceed to the `ala` folder by backtracking one step, `cd ../ala` from the current folder.
15. I then cat the `kazam.txt` that is there and luckily enough, that file has our flag.
![image](https://user-images.githubusercontent.com/98275198/237131860-389ffcb0-8f16-477b-850b-129dc37930cd.png)

Thank you for reading through, hope you learnt something new.
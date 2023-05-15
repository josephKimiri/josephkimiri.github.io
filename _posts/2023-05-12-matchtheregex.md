---
title: MatchTheRegex
author: josephkimiri
date: 2023-05-12 11:35:00 +0300
categories: [CTFs, Web]
tags: [picoctf, ctfs, web, cybersecurity]
render_with_liquid: false
---

## MatchTheRegex

How about trying to match a regular expression
The website is running here.

## Solution
1. First we access the challenge using the provided url.
2. We then get a web page asking for a valid input with input being parsed through a text box.
![image](https://user-images.githubusercontent.com/98275198/237683027-080c0ea2-0abf-450b-83d4-a109bbe85629.png)
3. Now, lets try random strings.
![image](https://user-images.githubusercontent.com/98275198/237683229-d45d8c07-7aab-4ac6-b8c7-ed1fb98003f4.png)
4. The next step would be checking the source code to understand how the input is parsed.
5. Press `ctrl+u` to view page source. 
6. Navigate to the javascript where the logic is coded.
![image](https://user-images.githubusercontent.com/98275198/237683784-2ff9f635-ffb9-444b-a1ee-92a7835afadc.png)
7. The code has a function `send_request()` which retrieves the value entered in the input field with the id "name", it then sends it as a query parameter in a fetch request to the `/flag` endpoint, and displays the value of the "flag" property from the response in an alert box.
8. As the title suggests, the input should match a particular regex to pop out the flag. 
9. Checking the code again, we get a javascript comment that shows the regex `^p.....F!?` 
![image](https://user-images.githubusercontent.com/98275198/237684844-0fde1a0c-2bf4-49e9-822b-1e14f750eec1.png)
10. The comment shows a regex of a string with `8` characters that starts with p and ends with `F` and the `!` is optional.
11. I then come up with a random string `piqwerF` that I use to pop out the flag.
![image](https://user-images.githubusercontent.com/98275198/237685799-7713baed-232a-47d1-a176-2b792fc50a97.png)

Eazy Peazy. Remember to stay vigilant in the digital wild west. Happy Hacking.
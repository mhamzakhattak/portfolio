---
title: AirTech CTF '24 Final - Web - HideOut
date: '2024-03-02'
tags: ['AIRTECH24', 'WEB','PHP', 'HideOut','LOGINBYPASS']
draft: false
---
> “This challenge was pritty good”

![challenge discription](static/writeups/airtech/HideOut/chall_discription.png)

### First Challenge that I solve was this USB100.
First things first, i downloaded the challenge file and unziped it using the follwing command

```bash
 7z e USB100.zip
```
and found out it’s a pcapng file as follows:
![send.pacapng](/static/writeups/blackhat2023/usb100/send.png)

Now, normally i would open this with Wireshark and try to analyze it but i aimed for a deferent approach this time and chose the easy way.

I ran Binwalk to see what kind of information and files are stored in send.pcapng, and i found the following.

![binwalk_command](/static/writeups/blackhat2023/usb100/binwalk_command.png)

There is a windows executable stored inside of this file and now all we need to do is extract it and it’s hexadecimal is AC723, So i wrote down the following command.

```bash
binwalk -e --dd=".*" send.pcapng
```
and ended up with the following files with the executable among them.
![windows_executable](/static/writeups/blackhat2023/usb100/windows_executable.png)

So i immediately copied the executable to my windows desktop and ran it on Powershell and Bingo….. WE GOT A FLAG.

![FLAG_Imgae](/static/writeups/blackhat2023/usb100/FLAG.png)

Thanks a lot for reading along to the end.
### ***kh4tt4k***

### Peace! 👋👋👋

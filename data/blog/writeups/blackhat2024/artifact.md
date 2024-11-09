---
title: Blackhat MEA '24 Quals - Forensics - Artifact
date: '2024-09-11'
tags: ['BLACKCTF2024', 'BLACKHATMEA','FORENSICS', 'Artifact','Windows Artifact']
draft: false
---
> BlackHat Conference is a renowned cybersecurity event where experts discuss the latest trends and research in the field. It includes a challenging Capture The Flag (CTF) competition that tests participants’ hacking and security skills. I personally experienced the Online Qualifying Round, which was both challenging and fun, and it further highlights the high caliber of the BlackHat CTF

![blackhatlogo](/static/writeups/blackhat2023/usb100/blackhat.png)


### Challenge Name: Artifact (Easy)

**Description:**  
During the investigation of a compromised machine, it was discovered that an impersonation tool had been executed. The Digital Forensics and Incident Response (DFIR) team provided a specific registry hive for analysis. Your task is to identify the name of the executable associated with the impersonation tool and determine its earliest suspected execution time on the affected machine.  
**Flag format/example:** `BHFlagY{cmd.exe_29/12/1992_22:33:13}`

---

![artifact](/static/writeups/blackhat2024/artifact/1.PNG)

### Solution Walkthrough

For this challenge, we were given a Registry Hive file as the primary artifact. I began my analysis using **RegRipper**, a popular tool for extracting and parsing critical information from Windows registry files.

Once RegRipper completed its scan, I focused on locating executable files, with the goal of identifying anything suspicious. During this process, I found a notable entry:  
**DeadPotato-NET4.exe**  
This file was located in the following registry path:

```bash
ControlSet001\Control\Session Manager\AppCompatCache
```

The **AppCompatCache** key is known for storing details about executables that have been run on the system, including their execution timestamps. According to the data extracted, **DeadPotato-NET4.exe** was executed on **09/08/2024 at 22:42:13**, which matched the format needed to solve the flag.

![data_extracted](/static/writeups/blackhat2024/artifact/1.PNG)

### Final Flag:
`BHFlagY{DeadPotato-NET4.exe_09/08/2024_22:42:13}`

This challenge underscores the significance of registry forensics in detecting and investigating suspicious activities on a system. By utilizing tools like **RegRipper**, forensic analysts can swiftly extract crucial evidence from registry hives, aiding in their overall investigation.



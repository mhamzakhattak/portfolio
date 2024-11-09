# Forensics Writeups | BlackHat MEA CTF Qualification 2024

![title](/static/writeups/blackhat2024/artifact/1.png)

### Challenge Name: Artifact (Easy)

**Description:**  
During the investigation of a compromised machine, it was discovered that an impersonation tool had been executed. The Digital Forensics and Incident Response (DFIR) team provided a specific registry hive for analysis. Your task is to identify the name of the executable associated with the impersonation tool and determine its earliest suspected execution time on the affected machine.  
**Flag format/example:** `BHFlagY{cmd.exe_29/12/1992_22:33:13}`

---

### Solution Walkthrough

For this challenge, we were given a Registry Hive file as the primary artifact. I began my analysis using **RegRipper**, a popular tool for extracting and parsing critical information from Windows registry files.

Once RegRipper completed its scan, I focused on locating executable files, with the goal of identifying anything suspicious. During this process, I found a notable entry:  
**DeadPotato-NET4.exe**  
This file was located in the following registry path:
`ControlSet001\Control\Session Manager\AppCompatCache`


The **AppCompatCache** key is known for storing details about executables that have been run on the system, including their execution timestamps. According to the data extracted, **DeadPotato-NET4.exe** was executed on **09/08/2024 at 22:42:13**, which matched the format needed to solve the flag.

![output](/static/writeups/blackhat2024/artifact/2.png)

### Final Flag:
BHFlagY{DeadPotato-NET4.exe_09/08/2024_22:42:13}

This challenge underscores the significance of registry forensics in detecting and investigating suspicious activities on a system. By utilizing tools like **RegRipper**, forensic analysts can swiftly extract crucial evidence from registry hives, aiding in their overall investigation.

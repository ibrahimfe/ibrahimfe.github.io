---
title: PicoCTF 2024 Writeups
date: 2024-07-13 22:59 +0700
categories: [CTF, Writeup]
tags: [Writeup]
author: <author_id>
---

This is a writeup for all CTF challenges i solved in the PicoCTF 2024 event. I hope it helped you learn about my way of thinking and troubleshooting.

## Time Machine [General Skills]

**Description**
What was I last working on? I remember writing a note to help me remember...

**Hints**
1. The `cat` command will let you read a file, but that won't help you here!
2. Read the chapter on Git from the picoPrimer [here](https://primer.picoctf.org/#_git_version_control)
3. When committing a file with git, a message can (and should) be included.

**How i solved it**

Inside there is a txt file which have this paragraph :
This is what I was working on, but I'd need to look at my commit history to know why...

The first thing i do when seeing the text in txt file is use `git log` command in the terminal in the current directory and voila i got the flag in the commit message

Flag : **picoCTF{t1m3m@ch1n3_e8c98b3a}**

## Verify [Forensics]

**Description**
People keep trying to trick my players with imitation flags. I want to make sure they get the real thing! I'm going to provide the SHA-256 hash and a decrypt script to help you know that my flags are legitimate. You can download the challenge files here:
[Challenge.zip](https://artifacts.picoctf.net/c_rhea/10/challenge.zip)

**Hints**
1. Checksums let you tell if a file is complete and from the original distributor. If the hash doesn't match, it's a different file.
2. You can create a SHA checksum of a file with `sha256sum <file>` or all files in a directory with `sha256sum <directory>/*`.
3. Remember you can pipe the output of one command to another with `|`. Try practicing with the 'First Grep' challenge if you're stuck!

Note : you have to connect to the instance of the challenge to actually see the flag

**How i solved it:**
After launching the instance and list all the files and folder with `ls`, inside there is a decrypt.sh, checksum.txt and a files/ folder which contain all of the SHA-256 Hash file. To look inside the checksum.txt file i use `cat checksum.txt` and it contain some Hash String

    467a10447deb3d4e17634cacc2a68ba6c2bb62a6637dad9145ea673bf0be5e02

the challennges wants us to verify the correct hash file with this hash string. so using the linux terminal i use `sha256sum files/*` to list all of the hash string inside the `files/` folder. To match the hash string in the checksum.txt pipe the output of `sha256sum files/*` use `grep`, and it will look like this `sha256sum files/* | grep <hash string>`. switch the `hash string` with the actual hash string and it will show the actual file which is `c6c8b911`. type `./decrypt.sh files/c6c8b911` and it will output the actual flag.

Flag : **picoCTF{trust_but_verify_c6c8b911}**

## Scan Surprise [Forensics]

**Description** 
I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead? You can download the challenge files here:

[Challenge.zip](https://artifacts.picoctf.net/c_atlas/1/challenge.zip)


**Hints**
1. QR codes are a way of encoding data. While they're most known for storing URLs, they can store other things too.
2. Mobile phones have included native QR code scanners in their cameras since version 8 (Oreo) and iOS 11
3. If you don't have access to a phone, you can also use zbar-tools to convert an image to text

Literally scan the file and you will get the flag.

Flag : **picoCTF{p33k_@_b00_3f7cf1ae}**


## Binary Search [General Skills]

**Description**
Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses. Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools! You can download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_atlas/4/challenge.zip)

**Hints**
1. Have you ever played hot or cold? Binary search is a bit like that.
2. You have a very limited number of guesses. Try larger jumps between numbers!
3. The program will randomly choose a new number each time you connect. You can always try again, but you should start your binary search over from the beginning - try around 500. Can you think of why?

**How i solved it**
The strategy to solve this challenge is to always guess in the middle of a number. For example you start with 500, if lower try 250, if higher try 750. Continue doing this strategy until the 7th or 8th guess. Now you can try you lucky day in the 9th and 10th guesses.

Flag : **picoCTF{g00d_gu355_ee8225d0}**

## WebDecode [Web Exploitation]

**Description** 
Do you know how to use the web inspector?
Start searching here to find the flag

**Hints**
1. Use the web inspector on other files included by the web page.
2. The flag may or may not be encoded

**How i solved it**
I inspect all of the 3 html page and found a suspicious string in about.html page. It looks something like this `cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfMWY4MzI2MTV9`. So i open up the [cyberchef.org](https://cyberchef.org), put the string in the input box and use **Base64** recipe to decode the string. 


Flag : **picoCTF{web_succ3ssfully_d3c0ded_1f832615}**

## Unminify [Web Exploitation]

**Description**
I don't like scrolling down to read the code of my website, so I've squished it. As a bonus, my pages load faster!

**Hints**
1. Try CTRL+U / ⌘+U in your browser to view the page source. You can also add 'view-source:' before the URL, or try `curl <URL>` in your shell.
2. Minification reduces the size of code, but does not change its functionality.
3. What tools do developers use when working on a website? Many text editors and browsers include formatting

**How i Solved It**
After i connected to the instance and open the webpage, and open the page source with the rigth click. After that i use CTRL + F to search the keyword picoCTF{} to find the flag. And there you go.

Flag : **picoCTF{pr3tty_c0d3_b99eb82e}**

## Super SSH [General Skills]

**Description**
Using a Secure Shell (SSH) is going to be pretty important.
Can you ssh as ctf-player to titan.picoctf.net at port 64549 to get the flag? You'll also need the password 1ad5be0d. If asked, accept the fingerprint with yes. If your device doesn't have a shell, you can use: [PicoCTF Webshell](https://webshell.picoctf.org) If you're not sure what a shell is, check out our Primer: [Primer PicoCTF](https://primer.picoctf.com/#_the_shell)

**Hints**
1. [man ssh](https://linux.die.net/man/1/ssh)
2. You can try logging in 'as' someone with `<user>`@titan.picoctf.net
3. How could you specify the port?
4. Remember, passwords are hidden when typed into the shell

**How I Solved It**
Connect to the ssh with `ssh ctf-player@titan.picoctf.net -p 64549`. Put the password given and you will get the flag.

Flag : **picoCTF{s3cur3_c0nn3ct10n_8306c99d}**

## Secret of the Polyglot [Forensics]

**Description**
The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file? Download the suspicious file [here](https://artifacts.picoctf.net/c_titan/97/flag2of2-final.pdf). 

**Hints**
1. This problem can be solved by just opening the file in different ways

**How i solved it**
First thing i do is open the pdf file given and got this strange string `1n_pn9_&_pdf_724b1287}` most likely the second part of the flag. Looking at the string we know the current file is in pdf format, but there is a `pn9` text that most likely translate to **png** which is an image file. So i rename the extension of the file to png and open it and we got `picoCTF{f1u3n7_` string as an image for the first part of the flag.

Flag : **picoCTF{f1u3n7_1n_pn9_&_pdf_724b1287}**
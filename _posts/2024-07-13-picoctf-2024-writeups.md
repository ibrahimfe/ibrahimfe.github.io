---
title: PicoCTF 2024 Writeups
date: 2024-07-13 22:59 +0700
categories: [CTF, Writeup]
tags: [Writeup]
author: <author_id>
---

This is a writeup for all CTF challenges i solved in the PicoCTF 2024 event. I hope it helped you learn about my way of thinking and troubleshooting.

## Time Machine [General Skills]

Question :
What was I last working on? I remember writing a note to help me remember...

- Hint 1 : The `cat` command will let you read a file, but that won't help you here!
- Hint 2 : Read the chapter on Git from the picoPrimer [here](https://primer.picoctf.org/#_git_version_control)
- Hint 3 : When committing a file with git, a message can (and should) be included.

Inside there is a txt file which have this paragraph :
This is what I was working on, but I'd need to look at my commit history to know why...

The first thing i do when seeing the text in txt file is use `git log` command in the terminal in the current directory and voila i got the flag in the commit message

Flag : **picoCTF{t1m3m@ch1n3_e8c98b3a}**

## Verify [Forensics]

Description :
People keep trying to trick my players with imitation flags. I want to make sure they get the real thing! I'm going to provide the SHA-256 hash and a decrypt script to help you know that my flags are legitimate. You can download the challenge files here:
[Challenge.zip](https://artifacts.picoctf.net/c_rhea/10/challenge.zip)

1. Hint 1 : Checksums let you tell if a file is complete and from the original distributor. If the hash doesn't match, it's a different file.
2. You can create a SHA checksum of a file with `sha256sum <file>` or all files in a directory with `sha256sum <directory>/*`.
3. Remember you can pipe the output of one command to another with `|`. Try practicing with the 'First Grep' challenge if you're stuck!

Note : you have to connect to the instance of the challenge to actually see the flag

**How i solved it:**
After launching the instance and list all the files and folder with `ls`, inside there is a decrypt.sh, checksum.txt and a files/ folder which contain all of the SHA-256 Hash file. To look inside the checksum.txt file i use `cat checksum.txt` and it contain some Hash String

    467a10447deb3d4e17634cacc2a68ba6c2bb62a6637dad9145ea673bf0be5e02

the challennges wants us to verify the correct hash file with this hash string. so using the linux terminal i use `sha256sum files/*` to list all of the hash string inside the `files/` folder. To match the hash string in the checksum.txt pipe the output of `sha256sum files/*` use `grep`, and it will look like this `sha256sum files/* | grep <hash string>`. switch the `hash string` with the actual hash string and it will show the actual file which is `c6c8b911`. type `./decrypt.sh files/c6c8b911` and it will output the actual flag.

Flag : **picoCTF{trust_but_verify_c6c8b911}**

## Scan Surprise [Forensics]

**Challenge Description** : I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead? You can download the challenge files here:

[Challenge.zip](https://artifacts.picoctf.net/c_atlas/1/challenge.zip)

- Hint 1 : QR codes are a way of encoding data. While they're most known for storing URLs, they can store other things too.
- Hint 2 : Mobile phones have included native QR code scanners in their cameras since version 8 (Oreo) and iOS 11
- Hint 3 : If you don't have access to a phone, you can also use zbar-tools to convert an image to text

Literally scan the file and you will get the flag.

Flag : **picoCTF{p33k_@_b00_3f7cf1ae}**

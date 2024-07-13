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

- Hint 1 : The 'cat' command will let you read a file, but that won't help you here!
- Hint 2 : Read the chapter on Git from the picoPrimer [here](https://primer.picoctf.org/#_git_version_control)
- Hint 3 : When committing a file with git, a message can (and should) be included.

Inside there is a txt file which have this paragraph :
This is what I was working on, but I'd need to look at my commit history to know why...

The first thing i do when seeing the text in txt file is use 'git log' command in the terminal in the current directory and voila i got the flag in the commit message

Flag : **picoCTF{t1m3m@ch1n3_e8c98b3a}**

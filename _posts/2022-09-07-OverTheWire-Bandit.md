---
layout: single
title: OverTheWire Bandit Writeup
excerpt: "As my first experience with Infosec I started with OverTheWire , a CTF for beginners in cybersec. In this article I will be posting a writeup step by step about levels 1-33 of Bandit wargame with some extra info about tools I've used and learnt in the way"
date: 2022-09-07
classes: wide
header:
  teaser: /assets/images/overthewire-writeup/logo.png
  teaser_home_page: true
categories:
  - overthewire
  - writeup
tags:  
  - ctf
  - bash
  - wargame
  - overthewire
---

## Bandit 0->1

This is the first Bandit Wargame level , to log in we just need to ssh into the OverTheWire server with the following command.

- ssh bandit0@bandit.labs.overthewire.org -p2220

We will be logging in through port "2220" and once the connection is made we will be asked to enter it's password whose for the level 0 is just "bandit0"

![image-center](/assets/images/overthewire-writeup/bandit0_0.png){: .align-center}

Once logged in the description says :

"The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game"

By default , in the description they lend you a hand and give you some clues about tools/commands you can use to solve the levels.

This time they are telling we could use:

- [ls](https://man7.org/linux/man-pages/man1/ls.1.html)
- [cd](https://man7.org/linux/man-pages/man1/cd.1p.html)
- [cat](https://man7.org/linux/man-pages/man1/cat.1.html)
- [file](https://man7.org/linux/man-pages/man1/file.1.html)
- [du](https://man7.org/linux/man-pages/man1/du.1.html)
- [find](https://man7.org/linux/man-pages/man1/find.1.html)


So , to solve this level , we will be using "ls" to list the files in our current directory and cat to output it's content.


![image-center](/assets/images/overthewire-writeup/bandit0_1.png){: .align-center}

And just like this we got the password for the next level.

## Bandit 1->2

As we did for bandit0 we need to log in into bandit1 with the password we got in bandit0 (Remember to store the passwords as you will probably need them further on).

The description for this level says :

"The password for the next level is stored in a file called - located in the home directory"

Our task is the same as the last one , we just need to cat the file named "-" and that's it. Easy , isn't it?

![image-center](/assets/images/overthewire-writeup/bandit1_0.png){: .align-center}

Woops! cat didn't output anything! This is because cat isn't reading it as a file name. So the fix for this is either , doing cat to the whole directory ( We have only one file so it will only output it's content) or , using the absolute path.

![image-center](/assets/images/overthewire-writeup/bandit1_1.png){: .align-center}

As you guys can see , this time we got the right ouput , and thus the password for the next level , Bandit 2. Let's login and continue the game!







 
    

        

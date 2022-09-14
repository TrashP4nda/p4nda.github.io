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

## Bandit 2->3

Okay , so once logged in Bandit 2 we got a simmilar problem.

"The password for the next level is stored in a file called spaces in this filename located in the home directory"


![image-center](/assets/images/overthewire-writeup/bandit2_0.png){: .align-center}

So , as in Bandit 1 there is a problem when trying to use cat with certain filenames , this time the solution is the following one.

Okay , so we got the password for Bandit 3 , let's login.

## Bandit 3->4

"The password for the next level is stored in a hidden file in the inhere directory."

This is the clue for Bandit3.

We can find hidden files using ls flags , read the manual. 

ls -la / -all can list all the hidden files in the directory and list their attributes.

So we loggin , use ls and then cd into the directory called hidden ( You can also write ls + the path to the directory and don't need to cd)

Once inside use ls -la and a .hidden file appears.

I used file to list the file type and then cat to list it's content.

![image-center](/assets/images/overthewire-writeup/bandit3_0.png){: .align-center}

And as you can see the there is the password for the next level.

## Bandit 4->5

"The password for the next level is stored in the only human-readable file in the inhere directory"

Our new clue.. 

This time we need to find the only human readable file in the directory.

I used file so I could list the file type of the files inside. The only readable one as you can see in the picture is "-file07" and by using what we learnt about previous Bandit levels we can list it's content. Which is , the password for Bandit 5.

![image-center](/assets/images/overthewire-writeup/bandit4_0.png){: .align-center}

## Bandit 5->6

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

    human-readable
    1033 bytes in size
    not executable


This time we will need to use "find". They ask for a file with three attributes.

So after reading the find manual for some time I managed to solve the issue. Using find , and xargs which "applies" a command for each result of find , in which in this case is file , to list the file type and then grep to filter by ASCII. 

As can be seen there are a lot of directories with their own files.

![image-center](/assets/images/overthewire-writeup/bandit5_1.png){: .align-center}

![image-center](/assets/images/overthewire-writeup/bandit5_0.png){: .align-center}

After getting the result the first time I concatenated it , was listed with a lot of white spaces , so I used "awk" to remove them.

## Bandit 6->7

The password for the next level is stored somewhere on the server and has all of the following properties:

    owned by user bandit7
    owned by group bandit6
    33 bytes in size

We will need to use find again.

![image-center](/assets/images/overthewire-writeup/bandit6_0.png){: .align-center}

Sooo , what's this now?

We got a lot of errors and can't see anything at all. But , the password is there.

We just need to redirect stdout to /dev/null which is kinda like a black hole. 

- [What are stdin , stderr and stdout in Bash](https://linuxhint.com/bash_stdin_stderr_stdout/)
- [Redirecting stdout/in/err](https://www.devdungeon.com/content/stdin-stdout-stderr-piping-and-redirecting)

And after filtering all of this we got a file path.

![image-center](/assets/images/overthewire-writeup/bandit6_1.png){: .align-center}

So after doing a cat onto the file path we got the password.

![image-center](/assets/images/overthewire-writeup/bandit6_2.png){: .align-center}

## Bandit 7->8

"The password for the next level is stored in the file data.txt next to the word millionth"

This one was pretty easy , just grep the file and search for millionth. 

![image-center](/assets/images/overthewire-writeup/bandit7_0.png){: .align-center}

## Bandit 8->9

"The password for the next level is stored in the file data.txt and is the only line of text that occurs only once"

This time we will need to use new tools like sort and uniq.

- [sort](https://man7.org/linux/man-pages/man1/sort.1.html)
- [uniq](https://man7.org/linux/man-pages/man1/uniq.1.html)

Okay so after using uniq we notice that nothing is happening , we are getting all the content in data.txt. The key is that for uniq to work first we must sort the content.

![image-center](/assets/images/overthewire-writeup/bandit8_0.png){: .align-center}

![image-center](/assets/images/overthewire-writeup/bandit8_1.png){: .align-center}

## Bandit 9->10

"The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters."

![image-center](/assets/images/overthewire-writeup/bandit9_0.png){: .align-center}

The first thing after we cat the file is unreadable chaos. So this time we will use a new tool.

- [strings](https://linux.die.net/man/1/strings)

Strings prints readable character sequences that are at least 4 char long. With this we can get strings to fileter using grep and search for "====" as they mentioned that the password is next to several "=" characters.

![image-center](/assets/images/overthewire-writeup/bandit9_1.png){: .align-center}


## Bandit 10->11

"The password for the next level is stored in the file data.txt, which contains base64 encoded data"

UNDER CONSTRUCTION******


 
    

        

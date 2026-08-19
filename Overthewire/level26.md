# Overthewire - level 26

## Overview

### Category: General skill

### Description:
>Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.
>NOTE: if you’re a Windows user and typically use Powershell to ssh into bandit: Powershell is known to cause issues with the intended solution to this level. You should use command prompt instead.

## Exploitation
We can get the sshkey to level 26 fairly easy with *ls*
```bash
bandit25@bandit:~$ ls
bandit26.sshkey
```
Then we'll use it to connect to level 26

So our shell now isn't */bin/bash*, after trying to connect, we can see that we're restricted from making commands. 

We can log in as another user to check what we can do using *cat /etc/passwd*, then we can see that it is using /usr/bin/showtext
```bash
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```
After reading the file, we can see that it uses *more* to display the welcome text
```bash
bandit0@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```
We can shrink our terminal to 3-5 lines, then it will let us input in the middle of displaying, instead of instantly log us out

When it is displaying *--More-- (33%)*, we can press *v* to enter *vim*, then we rewrite our default bash path and then call a new shell
```bash
:set shell=/bin/bash
:shell
```
Now we've escaped the limited shell and reset it to the normal shell


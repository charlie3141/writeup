# Overthewire - level 28

## Overview

### Category: General skill

### Description:
>There is a git repository at ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27.
>From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

## Exploitation
First we git clone the respiratory at port 2220
```bash
root@DESKTOP-5UQIQJM:~# git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```
Then we navigate into */repo* and *cat* the README file inside to get the password
```bash
root@DESKTOP-5UQIQJM:~/repo# cat README
The password to the next level is: 
```
### Password
y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ
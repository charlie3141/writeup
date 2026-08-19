# Overthewire - level 27

## Overview

### Category: General skill

### Description:
>Good job getting a shell! Now hurry and grab the password for bandit27!

## Exploitation
First we *ls* to see the files inside
```bash
bandit26@bandit:~$ ls
bandit27-do  text.txt
```
text.txt is the welcome decorative bandit text, we then try the other file to see what it does
```bash
bandit26@bandit:~$ ./bandit27-do
Run a command as another user.
  Example: ./bandit27-do id
```
We can get the next level's password with the same method we did a few challenges ago, which is to use it to cat the password file
```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```
### Password
STJLJBRRphMxKB392CT4iOr5CbzPU9ER
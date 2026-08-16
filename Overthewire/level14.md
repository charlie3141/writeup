# Overthewire - level 14

## Overview

### Category: pwn

### Description:
>The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.
If you need help with this level: a hint file can be found in the home directory.
Make sure to read the error messages as they are informative.

## Exploitation
First, we download the private sshkey file from bandit13 back to linux *~//* using this command:
```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220 "cat sshkey.private" > ~/s.private
```
then we check the file's status with 
```bash
root@DESKTOP-5UQIQJM:~# ls -la | grep -n "s.private"
23:-rw-------  1 root root  2602 Aug 15 21:39 s.private
```
(if the first part isn't *-rw-------*, we use *chmod 600 filename* to set access to user 6(rw-: read, write), group 0(---: can't read/write), others 0(---:can't read/write))

Then we connect to level 14 with the flag -i (identity file) for our new sshkey 
```bash
root@DESKTOP-5UQIQJM:~# ssh -i s.private bandit14@bandit.labs.overthewire.org -p 2220

                      This is an OverTheWire game server.
...
  Enjoy your stay!

bandit14@bandit:~$
```
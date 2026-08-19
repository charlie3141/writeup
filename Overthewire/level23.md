# Overthewire - level 23

## Overview

### Category: General skill

### Description:
>A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
>NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

## Exploitation
We'll read what program is executing in */etc/cron.d* just like what we did in the lastest level, then we'll see the content inside this program
```bash
bandit22@bandit:~$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
If we run the file, it will give us the path to our **current** user-bandit22, but we're trying to get password to the user bandit23

We need to manually change the variable *$myname* to *bandit23* and run the *echo* command seperately
```bash
bandit22@bandit:/etc/cron.d$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```
### Password
gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw
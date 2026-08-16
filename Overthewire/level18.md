# Overthewire - level 18

## Overview

### Category: General skill

### Description:
>There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

## Exploitation
If you have trouble connecting to this problem with the previous openssh key, you can use this command to download it, chmod 600 it and then use it to connect this problem
```bash
ssh bandit16@bandit.labs.overthewire.org -p 2220 "cat /etc/bandit_pass/bandit16 | openssl s_client -quiet -connect localhost:31790 2>/dev/null | tail -n +2" > bandit17.private
```
Then we use *diff* to find the different line
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< qOg5pVOjPx9x9VccyYBADiT4xxyoUB8D
---
/> OQxXZjELndr90zuhOTDYBEomI0SZITXI
### Password
OQxXZjELndr90zuhOTDYBEomI0SZITXI
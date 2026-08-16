# Overthewire - level 15

## Overview

### Category: General skill

### Description:
>The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

## Exploitation
We can read the current password in */etc/bandit_pass/bandit14* and then send the password to port 30000 on localhost using *nc*
```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14 | nc localhost 30000
Correct!
```
### Password
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
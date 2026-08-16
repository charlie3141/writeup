# Overthewire - level 20

## Overview

### Category: General skill

### Description:
>To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

## Exploitation
We'll figure that bandit20-do run command as another user, then we know it runs as level 20's user with these commands
```bash
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do whoami
bandit19@bandit:~$ ./bandit20-do whoami
bandit20
```
Then we can use bandit20 user to access our usual password directory with
```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```
### Password
4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
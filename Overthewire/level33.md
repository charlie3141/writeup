# Overthewire - level 33

## Overview

### Category: General skill

### Description:
>After all this git stuff, it’s time for another escape. Good luck!

## Exploitation
This level we're put in *UPPERCASE SHELL*. It will turn all of our input into uppercase, essentially making almost all of bash commands unusable
```bash
WELCOME TO THE UPPERCASE SHELL
>> ls

sh: 1: LS: Permission denied
```
In this problem, we will use *$0* because they have no uppercase counterpart so they can run smoothly.

With the positional parameter *$0*, the shell expands to */bin/sh* so that we can freely use bash commands inside this newly created subshell
```bash
WELCOME TO THE UPPERCASE SHELL
> $0

$ whoami
bandit33
$ cat /etc/bandit_pass/bandit33
```
### Password
u4P2CyPOwPGLe94RdD9Uo2FxFwvnFswM
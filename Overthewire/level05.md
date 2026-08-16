# Overthewire - level 5

## Overview

### Category: General skill

### Description:
>The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

## Exploitation
First, we'll list the files in *inhere* and see that there are 10 files in total
```bash
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls -la
total 48
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file00
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file01
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file02
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file03
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file04
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file05
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file06
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file07
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file08
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file09
drwxr-xr-x 2 root    root    4096 Jun 24 14:59 .
drwxr-xr-x 3 root    root    4096 Jun 24 14:59 ..
```
All of the files contain 33 bytes so we can't differentiate them by file size

In order to find the right file, we use the command *file* 
```bash
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: OpenPGP Secret Key
./-file03: data
./-file04: data
./-file05: data
./-file06: Non-ISO extended-ASCII text, with NEL line terminators
./-file07: ASCII text
./-file08: data
./-file09: data
```
File number 7 is in ascii - the only human-readable file in the inhere directory, so we read it and get the password
```bash
cat ./-file07
```
### Password:
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
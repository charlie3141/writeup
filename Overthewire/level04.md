# Overthewire - level 4

## Overview

### Category: General skill

### Description:
>The password for the next level is stored in a hidden file in the inhere directory.

## Exploitation
We can use this command to list all entries:
```bash
bandit4@bandit:~$ ls -la
drwxr-xr-x   2 root root 4096 Jun 24 14:59 inhere
```
The output starts with a *d* so it's a directory (if it starts with a dash then it's a file)

Using the same command, we can see our target file
```bash
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 Jun 24 14:59 .
drwxr-xr-x 3 root    root    4096 Jun 24 14:59 ..
-rw-r----- 1 bandit4 bandit3   33 Jun 24 14:59 ...Hiding-From-You
bandit3@bandit:~/inhere$ cd ...Hiding-From-You
-bash: cd: ...Hiding-From-You: Not a directory
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
```
### Password:
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
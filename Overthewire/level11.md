# Overthewire - level 11

## Overview

### Category: pwn

### Description:
>The password for the next level is stored in the file data.txt, which contains base64 encoded data

## Exploitation
We use *base64* with the flag *-d* for decoding
```bash
bandit10@bandit:~$ base64 -d data.txt
The password is 
```
### Password:
pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
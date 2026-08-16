# Overthewire - level 8

## Overview

### Category: pwn

### Description:
>The password for the next level is stored in the file data.txt next to the word millionth

## Exploitation
We use grep with the flag *-n* to get the whole line
```bash
cat data.txt | grep -n "millionth"
```
### Password:
VR1ljMayciFxbnUokuQmJFw6QC9VKtub
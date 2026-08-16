# Overthewire - level 0

## Overview

### Category: pwn

### Description:
>The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

## Exploitation
We will use the command **ssh** with the flag -p (port) 2220 to connect to Overthewire bandit
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

### Password:
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
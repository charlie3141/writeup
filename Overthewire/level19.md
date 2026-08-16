# Overthewire - level 19

## Overview

### Category: General skill

### Description:
>The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

## Exploitation
We can append our command right after the *ssh* to get the content of the *readme* file
```bash
root@DESKTOP-5UQIQJM:~# ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme" > test18.txt
                         _                     _ _ _
                        | |__   _ _ _ _   _| () |_
                        | '_ \ / _ | '_ \ / _ | | __|
                        | |_) | (| | | | | (_| | | |
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
bandit18@bandit.labs.overthewire.org's password:
root@DESKTOP-5UQIQJM:~# cat test18.txt
```
### Password
KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI
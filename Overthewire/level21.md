# Overthewire - level 21

## Overview

### Category: General skill

### Description:
>There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).
>NOTE: Try connecting to your own network daemon to see if it works as you think

## Exploitation
First, we'll see a file called *suconnect* after doing *ls*
```bash
bandit20@bandit:~$ ls
suconnect
```
We'll set a *nc* in the background that will send the password if it catches any connections
```bash
bandit20@bandit:~$ nc -l -p 12345 < /etc/bandit_pass/bandit20 &
[1] 36
```
This command contains *-l* as in *listener* an *&* to make it run in the background, so that our next command will not stop it

Then we'll just need to specify the port *12345* we're using to get the flag
```bash
bandit20@bandit:~$ ./suconnect 12345
Read: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
Password matches, sending next password
```
### Password
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY

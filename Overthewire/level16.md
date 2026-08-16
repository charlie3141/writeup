# Overthewire - level 16

## Overview

### Category: General skill

### Description:
>The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

## Exploitation
We can read the current password in */etc/bandit_pass/bandit15* and then send the password to port 30000 on localhost using SSL/TLS encryption with *openssl s_client -connect* (We can add *-quiet* to discard the handshake output)
```bash
bandit15@bandit:~$ cat /etc/bandit_pass/bandit15 | openssl s_client -quiet -connect localhost:30001
Connecting to 127.0.0.1
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
Correct!
```
### Password
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
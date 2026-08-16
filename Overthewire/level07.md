# Overthewire - level 7

## Overview

### Category: pwn

### Description:
>The password for the next level is stored somewhere on the server and has all of the following properties:
>
>owned by user bandit7
>
>owned by group bandit6
>
>33 bytes in size

## Exploitation
Because it's on the entire server, we navigate to root directory *//*
```bash
cd /
```
Then we use *find* with *-size 33c* for 33 bytes, *-user bandit7* for the user owner, *-group bandit6* for the group owner
```bash
bandit6@bandit:/$ find . -size 33c -group bandit6 -user bandit7 2>/dev/null
./var/lib/dpkg/info/bandit7.password
```
We append *2>/dev/null* to redirect stderr (standard error) to /dev/null to discard all errors
```bash
cat ./var/lib/dpkg/info/bandit7.password
```
### Password:
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
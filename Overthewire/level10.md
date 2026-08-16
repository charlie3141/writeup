# Overthewire - level 10

## Overview

### Category: General skill

### Description:
>The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

## Exploitation
We can use *strings* to get human-readable text, to get the words after several *=* characters, we use grep with the flag *-E* for regex, then *+* for the rest of the line
```bash
bandit9@bandit:~$ strings data.txt | grep -E '==='+
========== the
========== password
========== is
```

### Password:
B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
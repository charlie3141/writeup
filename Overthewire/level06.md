# Overthewire - level 6

## Overview

### Category: General skill

### Description:
>The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
>
>human-readable
>
>1033 bytes in size
>
>not executable

## Exploitation
We can search for the file using the command *find* with three flags, including *-type f* for files, *-size 1033c* for 1033 bytes, *! - executable* for non-executable files
```bash
bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable
./maybehere07/.file2
cat ./maybehere07/.file2
```

### Password:
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
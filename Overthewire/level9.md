# Overthewire - level 9

## Overview

### Category: pwn

### Description:
>The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

## Exploitation
We first use *sort* to get all the same lines adjacent, then we use *uniq -u* to get the unique line
```bash
sort data.txt | uniq -u
```

### Password:
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
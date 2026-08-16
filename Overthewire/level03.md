# Overthewire - level 3

## Overview

### Category: General skill

### Description: 
>The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

## Exploitation
This filename begins with a dash, so we'll use *./* to specify our folder at the beginning. It also has spaces, so we'll put *\\* before the spaces to read the file
```bash
cat ./--spaces\ in\ this\ filename--
```
There is a faster way, which is to write the beginning of the filename *./--spaces* then we press *Tab* and it will complete the rest of the filename for us

### Password:
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
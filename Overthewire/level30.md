# Overthewire - level 30

## Overview

### Category: General skill

### Description:
>There is a git repository at ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo via the port 2220. The password for the user bandit29-git is the same as for the user bandit29.
>From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine


## Exploitation
First, we read the README.md file
```bash
root@DESKTOP-5UQIQJM:~/repo# ls -la
total 16
drwxr-xr-x  3 root root 4096 Aug 18 19:46 .
drwx------ 15 root root 4096 Aug 18 19:46 ..
drwxr-xr-x  8 root root 4096 Aug 18 19:46 .git
-rw-r--r--  1 root root  131 Aug 18 19:46 README.md
root@DESKTOP-5UQIQJM:~/repo# cat README.md
/# Bandit Notes
Some notes for bandit30 of bandit.

/## credentials

- username: bandit30
- password: <no passwords in production!>
```
We can view the branches to see where the password was leaked
```bash
root@DESKTOP-5UQIQJM:~/repo# git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
```
After checking every branches with *git log -p {branch}* we can see that it was in origin/dev
```bash
root@DESKTOP-5UQIQJM:~/repo# git log -p origin/dev
commit d36874ce7e88201c326bb596ba47a4cd063a023e (origin/dev)
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:08 2026 +0000

    add data needed for development

diff --git a/README.md b/README.md
index 1af21d3..d395d04 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for bandit30 of bandit.
 ## credentials

 - username: bandit30
-- password: <no passwords in production!>
+- password: jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX


commit 2dcc91e34c5f8df1cfdea2e685d5faa6408f62d2
Author: Ben Dover <noone@overthewire.org>
Date:   Wed Jun 24 14:59:08 2026 +0000

    add gif2ascii

diff --git a/code/gif2ascii.py b/code/gif2ascii.py
new file mode 100644
index 0000000..8b13789
--- /dev/null
+++ b/code/gif2ascii.py
@@ -0,0 +1 @@
+

commit a9c5d1c2b43890809f3077bb9ec65c30ced242fb (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Wed Jun 24 14:59:08 2026 +0000

    fix username

diff --git a/README.md b/README.md
index 2da2f39..1af21d3 100644
--- a/README.md
+++ b/README.md
@@ -3,6 +3,6 @@ Some notes for bandit30 of bandit.

 ## credentials

-- username: bandit29
+- username: bandit30
:
```
### Password
jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX
# Overthewire - level 29

## Overview

### Category: General skill

### Description:
>There is a git repository at ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo via the port 2220. The password for the user bandit28-git is the same as for the user bandit28.
>From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.


## Exploitation
After delete the old */repo* and clone level 28, we try to read the README.md file
```bash
root@DESKTOP-5UQIQJM:~# cd repo
root@DESKTOP-5UQIQJM:~/repo# ls -la
total 16
drwxr-xr-x  3 root root 4096 Aug 18 19:41 .
drwx------ 15 root root 4096 Aug 18 19:41 ..
drwxr-xr-x  8 root root 4096 Aug 18 19:41 .git
-rw-r--r--  1 root root  111 Aug 18 19:41 README.md
root@DESKTOP-5UQIQJM:~/repo# cat README.md
/# Bandit Notes
Some notes for level29 of bandit.

/## credentials

- username: bandit29
- password: xxxxxxxxxx
```
We can try to see the commit history with this command
```bash
root@DESKTOP-5UQIQJM:~/repo# git log
commit 83d77407b76c9f86ac4e691a47618641c9d527ba (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:06 2026 +0000

    fix info leak

commit 13bbc4d2414ffe0439b8ee4f5e5c2949780cf4b3
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:06 2026 +0000

    add missing data

commit f3334fbccbf9446a6af88a3c71021c2f57163322
Author: Ben Dover <noone@overthewire.org>
Date:   Wed Jun 24 14:59:06 2026 +0000

    initial commit of README.md
root@DESKTOP-5UQIQJM:~/repo# git log -p
commit 83d77407b76c9f86ac4e691a47618641c9d527ba (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:06 2026 +0000

    fix info leak

diff --git a/README.md b/README.md
index 42331d9..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials

 - username: bandit29
-- password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
+- password: xxxxxxxxxx


commit 13bbc4d2414ffe0439b8ee4f5e5c2949780cf4b3
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:06 2026 +0000

    add missing data

diff --git a/README.md b/README.md
index 7ba2d2f..42331d9 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials

 - username: bandit29
-- password: <TBD>
+- password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0


commit f3334fbccbf9446a6af88a3c71021c2f57163322
Author: Ben Dover <noone@overthewire.org>
Date:   Wed Jun 24 14:59:06 2026 +0000

    initial commit of README.md

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..7ba2d2f
--- /dev/null
+++ b/README.md
@@ -0,0 +1,8 @@
:
```
We can see that the password was commited and deleted later
### Password
Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
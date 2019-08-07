---
title:  "scourcetree  总是需要输入密码"
---



git: 'credential-cache' is not a git command. See 'git --help'.



"This [git-credential-cache] doesn’t work for Windows systems as git-credential-cache communicates through a Unix socket."


Still using msysgit? For msysgit versions 1.8.1 and above
The wincred helper was added in msysgit 1.8.1. Use it as follows:

git config --global credential.helper wincred
For msysgit versions older than 1.8.1
First, download [git-credential-winstore](https://github.com/anurse/git-credential-winstore/downloads) and install it in your git bin directory.

Next, make sure that the directory containing git.cmd is in your Path environment variable. The default directory for this is C:\Program Files (x86)\Git\cmd on a 64-bit system or C:\Program Files\Git\cmd on a 32-bit system. An easy way to test this is to launch a command prompt and type git. If you don't get a list of git commands, then it's not set up correctly.

Finally, launch a command prompt and type:

git config --global credential.helper winstore
Or you can edit your .gitconfig file manually:

[credential]
    helper = winstore






-----------------------------------










[https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%87%AD%E8%AF%81%E5%AD%98%E5%82%A8](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%87%AD%E8%AF%81%E5%AD%98%E5%82%A8)
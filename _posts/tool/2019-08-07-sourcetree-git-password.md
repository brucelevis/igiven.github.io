---
title:  "scourcetree  总是需要输入密码"
---

## Git密钥存储相关

幸运的是，Git 拥有一个凭证系统来处理这个事情。 下面有一些 Git 的选项：

- 默认所有都不缓存。 每一次连接都会询问你的用户名和密码。
- “cache” 模式会将凭证存放在内存中一段时间。 密码永远不会被存储在磁盘中，并且在15分钟后从内存中清除。
- “store” 模式会将凭证用明文的形式存放在磁盘中，并且永不过期。 这意味着除非你修改了你在 Git 服务器上的密码，否则你永远不需要再次输入你的凭证信息。 这种方式的缺点是你的密码是用明文的方式存放在你的 home 目录下。
- 如果你使用的是 Mac，Git 还有一种 “osxkeychain” 模式，它会将凭证缓存到你系统用户的钥匙串中。 这种方式将凭证存放在磁盘中，并且永不过期，但是是被加密的，这种加密方式与存放 HTTPS 凭证以及 Safari 的自动填写是相同的。
- 如果你使用的是 Windows，你可以安装一个叫做 “winstore” 的辅助工具。 这和上面说的 “osxkeychain” 十分类似，但是是使用 Windows Credential Store 来控制敏感信息。 可以在 [https://gitcredentialstore.codeplex.com](https://gitcredentialstore.codeplex.com/) 下载。

`git config --global credential.helper store `

“store” 模式可以接受一个 `--file <path>` 参数，可以自定义存放密码的文件路径（默认是 `~/.git-credentials` ）

WINDOS部分版本的GIT会提示

```
git: 'credential-cache' is not a git command. See 'get --help'.
```

实际上是缺少微软的 Git Credential Manager

安裝 Git Credential Manager for Windows即可解决该问题

最新的下载地址为：

https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/latest

下载安装完后可以通过命令进行查看是否生效

```
git config --global credential.helper
git config --global credential.helper manager
返回
manager
```



 ## 同网站多账号的问题

如果同一个网站有多个账号..查看->选项->验证

- 编辑那个网站的账号,就会新建一个用户名@xxx.com的账号
- 然后把那个公用的删除



# SourceTree删除GIT密码

当GIT服务器修改密码后，sourcetree本地记住的密码，会导致提交代码失败。
本地删除当前用户目录下保存密码的文件，文件路径：
C:\Users\wuxiaoyuan\AppData\Local\Atlassian\SourceTree\passwd
清空文件内容即可

## 相关链接

- [https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%87%AD%E8%AF%81%E5%AD%98%E5%82%A8](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%87%AD%E8%AF%81%E5%AD%98%E5%82%A8)


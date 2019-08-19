---
title:  "powershell 常用命令"
---


- Get-PSDrive  Windows PowerShell 驱动器是一个数据存储位置，你可以像访问 Windows PowerShell 中的文件系统驱动器那样访问它。
- Get-Alias 和   ls Alias:(驱动器)     列出所有alias
- ls Env:(驱动器)    列出所有的环境变量
- ls Variable:(驱动器) 和 Get-Variable 列出所有的变量
- ls Function:(驱动器)  列出所有的函数
- get-command   查看命令信息 可以查看某个命令的path  get-command mysqldump
- invoke-item  向windows桌面双击操作一样打开某个文件或者目录
- $env:path -split ";"  列出所有path


---
title:  "Linux部署dotnetcore记录"
---

## Daemon

Linux Daemon（守护进程）是运行在后台的一种特殊进程。它独立于控制终端并且周期性地执行某种任务或等待处理某些发生的事件。它不需要用户输入就能运行而且提供某种服务，不是对整个系统就是对某个用户程序提供服务。Linux系统的大多数服务器就是通过守护进程实现的。常见的守护进程包括系统日志进程syslogd、 web服务器httpd、邮件服务器sendmail和数据库服务器mysqld等...

### 配置文件
```
sudo nano /etc/systemd/system/KestrelDemoSer.service
```
```
[Unit]
Description=KestrelDemo running on CentOS
[Service]
WorkingDirectory=/cusD/wwwroot/KesPublish
Type=simple
User=root
Group=root
ExecStart=/usr/bin/dotnet /cusD/wwwroot/KesPublish/KestrelDemo.dll
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
SyslogIdentifier=dotnet-example
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false
[Install]
WantedBy=multi-user.target

```

### 命令
```
systemctl enable KestrelDemoSer.service
systemctl start KestrelDemoSer.service
systemctl status KestrelDemoSer.service
sudo journalctl -fu KestrelDemoSer.service  //查看日志
```

## jenkins
```
sudo systemctl stop edu
dotnet publish -c Release ${WORKSPACE}/src/Edu.Web/Edu.Web.csproj -o /usr/local/src/edu
sudo systemctl start edu
```

不能使用sudo的解决办法

```
sudo visudo

jenkins ALL=(ALL) NOPASSWD: ALL


systemctl restart jenkins

```
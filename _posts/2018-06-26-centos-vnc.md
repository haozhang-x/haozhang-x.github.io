---
layout: post
title: macOS通过VNC连接Linux Gnome桌面
subtitle: Remote desktop service (VNC)
date: 2018-06-26 22:51:52       
author: ZhangHao
header-img: "img/post-bg-2015.jpg"
tags: linux
---

### 1.安装X-Window
```
yum check-update
yum groupinstall "X Window System"
yum install gnome-classic-session gnome-terminal nautilus-open-terminal control-center liberation-mono-fonts
unlink /etc/systemd/system/default.target
ln -sf /lib/systemd/system/graphical.target /etc/systemd/system/default.target
reboot #重启机器
```

### 2.安装VNC
```
yum install tigervnc-server -y
```

### 3.复制VNC service文件到系统service服务管理目录下
```
cp /lib/systemd/system/vncserver@.service /etc/systemd/system/vncserver@:1.service  
#复制并被重命名为vncserver@:1.service
```


### 4.修改vncserver@:1.service文件

```
[Unit]
Description=Remote desktop service (VNC)
After=syslog.target network.target
[Service]
Type=forking
User=root
ExecStartPre=-/usr/bin/vncserver -kill %i
ExecStart=/sbin/runuser -l root -c "/usr/bin/vncserver %i"
PIDFile=/root/.vnc/%H%i.pid
ExecStop=-/usr/bin/vncserver -kill %i
[Install]
WantedBy=multi-user.target
```

### 5.修改文件使配置生效：

```
systemctl daemon-reload
```

### 6.为vncserver@:1.service设置密码<br>
```
vncpasswd
```
### 7.启动VNC
```
systemctl enable vncserver@:1.service #设置开机启动
systemctl start vncserver@:1.service #启动vnc会话服务
systemctl status vncserver@:1.service #查看nvc会话服务状态
systemctl stop vncserver@:1.service #关闭nvc会话服务
netstat -lnt | grep 590*      #查看端口
```
### 8.通过Finder访问
打开Finder(访达)
输入Command+K,输入vnc的地址vnc://mycloudx.cn:5901,然后输入之前通过vncpasswd命令设置的密码，连接成功。出现gnome桌面。

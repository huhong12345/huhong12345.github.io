---
title: Linux清理系统内存&&QB相关
date: 2024-01-3 22:56:01
categories:
- 编程
- Linux
tags:
- 摘抄
- Linux
---
QB系统占用内存非常大，本篇主要在不中断任何进程或服务的情况下清除缓存。
## 单次清理
### 仅清除页面缓存(Clear PageCache only)
``` bash
sync; echo 1 > /proc/sys/vm/drop_caches
``` 
### 清除目录项和inode(Clear dentries and inodes)
``` bash
sync; echo 2 > /proc/sys/vm/drop_caches
``` 
### 清理三者(Clear PageCache, dentries and inodes)
``` bash
sync; echo 3 > /proc/sys/vm/drop_caches
``` 
同步 (sync) 将刷新文件系统缓冲区。命令以 “;” 分隔依次运行。在执行序列中的下一个命令之前，shell 等待每个命令终止。正如内核文档中提到的，写入 drop_cache 将清除缓存而不杀死任何应用程序/服务，命令 echo 正在执行写入文件的工作。

如果您必须清除磁盘缓存，第一个命令在企业和生产中是最安全的“…echo 1 > …”。只会清除 PageCache。不建议在生产中使用“…echo 3 >”上方的第三个选项，直到您知道自己在做什么，因为它会清除 PageCache、dentries 和 inode。

## 定时清理缓存
``` bash
sudo su
vim clearcache.sh
``` 
写下如下内容：
``` bash
#!/bin/bash
# Note, we are using "echo 3", but it is not recommended in production instead use "echo 1"
sync
echo 3 > /proc/sys/vm/drop_caches
``` 
``` bash
chmod 755 clearcache.sh
``` 
以 root 身份创建定时清理任务
``` bash
crontab -e
``` 
写入如下内容，每天0点，12点，18点的0分清理缓存
``` bash
0  0,12,18  *  *  *  /path/to/clearcache.sh
``` 
一般来说，不建议定时清理RAM。还有一下替代方法：

## 清除Linux交换空间
如果想清除掉Swap空间，可以运行下面的命令：
``` bash
swapoff -a && swapon -a
``` 
此外，了解有关风险后，您可以将上面的命令添加到cron中。现在，我们将上面两种命令结合成一个命令，写成正确的脚本来同时清除RAM缓存和交换空间。
``` bash
echo 3 > /proc/sys/vm/drop_caches && swapoff -a && swapon -a && printf '\n%s\n' 'Ram-cache and Swap Cleared'
``` 
或：
``` bash
su -c 'echo 3 > /proc/sys/vm/drop_caches' && swapoff -a && swapon -a && printf '\n%s\n' 'Ram-cache and Swap Cleared'
``` 
在测试上面的命令之前，我们在执行脚本前后运行“free -m” 来检查缓存。

## QB相关代码
### 安装
``` bash
sudo add-apt-repository -y ppa:qbittorrent-team/qbittorrent-stable
sudo apt install -y qbittorrent-nox
qbittorrent-nox --version
``` 
### 自启动
``` bash
sudo vim /etc/systemd/system/qbittorrent-nox.service
``` 
写入：
``` bash
[Unit]
Description=qBittorrent client
After=network.target

[Service]
ExecStart=/usr/bin/qbittorrent-nox --webui-port=8080
Restart=always

[Install]
WantedBy=multi-user.target
``` 
### 指令
``` bash
sudo service qbittorrent-nox start
sudo service qbittorrent-nox status
sudo service qbittorrent-nox stop
sudo service qbittorrent-nox restart
sudo systemctl enable qbittorrent-nox
``` 
### 卸载
停止服务，删除系统文件
``` bash
sudo service qbittorrent-nox stop
sudo systemctl disable qbittorrent-nox
sudo rm -rf /etc/systemd/system/qbittorrent-nox.service
sudo systemctl daemon-reload
sudo systemctl reset-failed
``` 
卸载：
``` bash
sudo apt purge --autoremove -y qbittorrent-nox
``` 
如果有GPK key和 repository:
``` bash
sudo rm -rf /etc/apt/trusted.gpg.d/qbittorrent-team_ubuntu_qbittorrent-stable.gpg
sudo rm -rf /etc/apt/sources.list.d/qbittorrent-team-ubuntu-qbittorrent-stable-focal.list
``` 
删除其他目录：
``` bash
sudo rm -rf /.config/qBittorrent
sudo rm -rf /.local/share/qBittorrent
sudo rm -rf /.cache/qBittorrent
rm -rf ~/.config/qBittorrent
rm -rf ~/.local/share/qBittorrent
rm -rf ~/.cache/qBittorrent
``` 
## 参考文献
1、https://colobu.com/2015/10/31/How-to-Clear-RAM-Memory-Cache-Buffer-and-Swap-Space-on-Linux/
2、https://xujinzh.github.io/2021/06/20/clear-linux-memory-cache/index.html
3、https://www.tecmint.com/clear-ram-memory-cache-buffer-and-swap-space-on-linux/
4、https://lindevs.com/install-qbittorrent-nox-on-ubuntu




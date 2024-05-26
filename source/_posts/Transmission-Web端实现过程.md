---
title: Transmission Web端实现过程
tags:
  - 远程
  - Ubuntu
  - 服务器
categories:
  - 编程
  - Linux
date: 2023-01-05 09:40:23
---
Transmission是Ubuntu服务器默认的下载工具，但对于服务器开启远程桌面很不方便，这里说明如何安装Web端远程控制。

部署完成后，使用网页http://ip:9091  的形式访问ip为你服务器的公网地址，内网下则是局域网ip。

安装过程可以用sudo - i

## 安装Transmission
```bash
sudo apt-get install software-properties-common -y
sudo add-apt-repository ppa:transmissionbt/ppa
sudo apt-get install transmission-daemon -y
```
## 修改配置文件
```bash
#停止Transmisson后台服务
systemctl stop transmission-daemon.service
#修改配置文件
vi /var/lib/transmission-daemon/.config/transmission-daemon/settings.json
```
在第51行附近修改以下4处
```bash
  "rpc-password": "填写你的登陆密码",
  "rpc-port": 9091, #外网访问端口可以自行更改
  "rpc-username": "填写你的登陆账号",
  "rpc-whitelist-enabled": false, #默认为true, 如需外网访问最好关
```

## 更换Transmission Web Control美化主题
### 获取最新的安装脚本：（使用国内镜像）
```bash
wget https://gitee.com/culturist/transmission-web-control/raw/master/release/install-tr-control-gitee.sh
```

如果提示 https 获取失败，请使用以下命令获取安装脚本：
```bash
wget https://github.com/ronggang/transmission-web-control/raw/master/release/install-tr-control-cn.sh --no-check-certificate
```
如果提示文件已存在，可以通过 rm install-tr-control-cn.sh 进行删除后再执行下载；或者在 wget 后面添加 -N 参数，如：
```bash
wget -N https://github.com/ronggang/transmission-web-control/raw/master/release/install-tr-control-cn.sh --no-check-certificate
```
### 执行安装脚本
添加权限，运行脚本：
```bash
chmod +x install-tr-control-cn.sh
bash install-tr-control-cn.sh
```
这里运行脚本时我出现了报错：
```bash
【cp: cannot stat '/tmp/tr-web-control/transmission- web-control/src/.': No such file or directory】
```
检查后发现错误原因在install-tr-control-gitee.sh中185行来源地址与实际地址不符，临时的解决办法是修改install-tr-control-gitee.sh中185行代码：
```bash
##修改前：
cp -r "$TMP_FOLDER/transmission-web-control/src/." "$WEB_FOLDER/"
##修改后：
cp -r "$TMP_FOLDER/transmission-web-control-v1.6.1-update1/src/." “$WEB_FOLDER/”
```
脚本运行正常，输入1，安装最新发布版本。

安装完成后，用浏览器访问 Transmission Web Interface（如：http://your_ip:9091/ ）即可看到新的界面；如果无法看到新界面，可能是浏览器缓存了，请按 Ctrl + F5 强制刷新页面或 清空缓存 后再重新打开；

## 启动Transmission后台服务
```bash
#启动服务
systemctl start transmission-daemon.service
#停止服务
systemctl stop transmission-daemon.service
#查询运行状态
systemctl status transmission-daemon.service
#开机自启动
systemctl enable transmission-daemon.service
#关闭开机自启
systemctl disable transmission-daemon.service
```
到这里博客就结束了。
![](tr.png)

## 参考
[1] https://zhuanlan.zhihu.com/p/465136042
[2] https://mathpretty.com/15094.html
[3] https://github.com/ronggang/transmission-web-control/wiki/Linux-Installation-CN
[4] https://github.com/ronggang/transmission-web-control/issues/583
---
title: Code-server配置方法
date: 2022-08-30 17:07:30
categories:
- 编程
- Code
tags:
- Code Online
- 配置
---
## 开始
一般来说，Vscode可由https://vscode.dev ，在浏览器中运行一个轻量化的编辑器，支持在本地机器打开文件夹并开始工作。这里支持文件系统访问 API（目前的 Edge 和 Chrome）的现代浏览器允许网页访问本地文件系统（在你的许可下）。（图片来自官网）

![](code.png)

这个简单的本地机器网关，快速打开了一些使用 VS Code for the Web 作为零安装本地开发工具的有趣场景，例如：

1、本地文件查看和编辑。在 Markdown 中快速记笔记（和预览！）。即使你在无法安装完整 VS Code 的受限机器上，仍然可以使用 vscode.dev 查看和编辑本地文件。

2、结合浏览器工具构建客户端 HTML、JavaScript 和 CSS 应用程序以进行调试。

3、在 Chromebook 等低功率机器上编辑代码，因为你无法（或者说 “轻松地”）在 Chromebook 安装 VS Code。

4、在 iPad 上开发。你可以上传 / 下载文件（甚至使用 Files 应用程序将它们存储在云中），以及使用内置的 GitHub 存储库扩展远程打开存储库。
而且，如果浏览器不支持本地文件系统 API，仍然可以通过浏览器上传和下载单个文件来打开它们。

##  在线部署
如果需要在服务器上部署VSCode服务端，可实现无论什么环境，只需要一台可以上网具有浏览器的设备，也可以方便使用VSCode编辑和运行代码的功能。

例如针对iPad，它没有Mac上的Code应用程序，但由此即可完成随时随地写代码、维护服务器文件、博客等桌面级功能。VSCode的各种插件甚至可以让它成为一个简易的IDE

Code-server的Github地址为https://github.com/coder/code-server
上面强调了其优点是：

1、在具有一致开发环境的任何设备上编写代码

2、使用云服务器加速测试、编译、下载等

3、在旅途中保持电池寿命；所有密集型任务都在您的服务器上运行

## 安装方法
具体安装教程可参考：https://coder.com/docs/code-server/latest/install，官网上提供了四种方式：

1、使用安装脚本，它可以自动执行大部分过程，但对网络条件有要求
```bash
curl -fsSL https://code-server.dev/install.sh | sh
```
2、手动安装代码服务器

3、使用coder/coder将代码服务器部署到团队

4、使用一键式按钮和指南将代码服务器部署到云提供商
https://github.com/coder/deploy-code-server

本文主要介绍离线安装包安装。

## 具体过程
最新安装包下载地址https://github.com/coder/code-server/releases

下载完成后，在目录下安装
```bash
sudo dpkg -i code-server_4.6.0_amd64.deb
```

先试运行一次，生成配置文件：
```bash
code-server
```

修改个人的配置文件
```bash
vim ~/.config/code-server/config.yaml
```
端口、密码可自行更改，地址写为0.0.0.0，这样网页可直接访问服务器公网ip:端口号即可访问。
```bash
# 远程访问需要把127.0.0.1换成0.0.0.0，端口也可设置
bind-addr: 0.0.0.0:8080
 
# 保持默认
auth: password
 
# 设置登入密码
password: ****

# 保持默认
cert: false
```
修改配置文件后，需要重启服务。

开启服务
```bash
sudo systemctl start code-server@huhong
```

开机自启
```bash
sudo systemctl enable code-server@huhong
```

到这里就完成了，非常简单。

## 其他事项
1、Code-server相关命令
``` py
#启动
systemctl --user enable --now code-server

# 重启
systemctl --user restart code-server

# 查看code-server状态
systemctl status code-server@root.service
 
# 查看code-server进程
ps -aux | grep code-server
 
# 停止code-server服务
systemctl stop code-server@root.service
 
# 杀死code-server进程
kill <pid>
```

2、如果要迁移插件目录

不同系统下目录分别为：

Ubuntu+code-server：	~/.local/share/code-server/extensions/

linux：	~/.vscode/extensions,不同发行版可能不同

windows：	C:/Users/（你的用户名）/.vscode/extensions

Mac	：User/（你的用户名）/.vscode/extensions

将对应目录的插件迁移过去即可
```bash
#先将插件打包（全选各个插件文件夹然后打包），再使用scp上传
scp extensions.zip user@host:~/local/share/code-server/extensions/

#解压
unzip extensions.zip
```

3、开机自启服务相关的参考
https://zhuanlan.zhihu.com/p/496990810
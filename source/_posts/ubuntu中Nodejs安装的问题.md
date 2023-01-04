---
title: ubuntu中Nodejs安装的问题
date: 2021-07-03 17:19:25
categories:
- 博客
- Nodejs
tags:
- Linux
- Nodejs
---
## 方法零(2023年1月5日更新)
使用nvm安装nodejs，这是一个非常好的node.js版本管理器，例如
```bash
nvm use 16
#Now using node v16.9.1 (npm v7.21.1)
node -v
#v16.9.1
nvm use 14
#Now using node v14.18.0 (npm v6.14.15)
node -v
#v14.18.0
nvm install 12
#Now using node v12.22.6 (npm v6.14.5)
node -v
#v12.22.6
```
NVM的仓库在https://github.com/nvm-sh/nvm 上，安装方法为：
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
#或者
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```
如果下载不动，可能是GitHub的raw.githubusercontent.com域名解析被污染了，通过修改hosts解决此问题。可在https://www.ipaddress.com/ 查询raw.githubusercontent.com的真实IP。

修改hosts：
```shell
sudo vim /etc/hosts
```
输入：
```shell
199.232.96.133 raw.githubusercontent.com
```

查看nvm是否安好：
```shell
nvm --version
```
确认安好后，输入下命令即可：
```shell
sudo apt-get remove nodejs
nvm install 16.15.1
```
参考：https://stackoverflow.com/questions/72921215/getting-glibc-2-28-not-found

## 方法一：下载源码，直接软连接
目前Node最新版本为16.15.1，npm 8.11.0。但通过：

```shell
$ sudo apt install nodejs
```
安装的并不是最新版（目前安装下来的Node为v8.10.0，npm为3.5.2）。此时可以选择下下来后去进行软连接的思路。

登陆官网https://nodejs.org/en/download/    ，下载源码
![](node.png)

接下来解压，cd进目录检查此包内node版本
```shell
$ tar xf  node-v16.15.1-linux-x64.tar.xz       // 解压
$ cd node-v16.15.1-linux-x64/                  // 进入解压目录
$  ./bin/node -v                               // 执行node命令 查看版本
// bin目录下有执行文件npm和node 做软链接
```

注意软连接需要写绝对路径，软连接到/usr/local/bin/下：

```shell
$ ln -s  /home/huhong/Downloads/node-v16.15.1-linux-x64/bin/node  /usr/local/bin/
$ ln -s /home/huhong/Downloads/node-v16.15.1-linux-x64/bin/npm  /usr/local/bin/
// 注意要写文件的绝对路径
```

如果创建软连的时候，出现npm已经存在,node 已经存在，解决方案是删除 /usr/local/bin/目录下的node，npm：

```shell
$ rm -rf /usr/local/bin/node
$ rm -rf /usr/local/bin/npm
```

之后创建软连接，即可（不了解rm含义慎用）。

## 方法二：通过更新工具
也可以考虑通过n这个用于更新node 版本的工具，并通过n下载最新的稳定版本

```shell
$ sudo npm install n -g
$ sudo n stable
```

结果为：

```shell
$ sudo n stable
  installing : node-v16.15.1
       mkdir : /usr/local/n/versions/node/16.15.1
       fetch : https://nodejs.org/dist/v16.15.1/node-v16.15.1-linux-x64.tar.xz
     copying : node/16.15.1
   installed : v16.15.1 (with npm 8.11.0)
```

可见，最新版本为v16.15.1。

## 几个坑点：
#### 1、shell不显示更新
如果经过以上方法后，使用node-v依然是先前的版本，可考虑根据不同的shell执行hash -r。

我使用的是zsh，执行hash -r 后显示正确。

```shell
$ node -v
v8.10.0
$ npm -v
3.5.2
$ hash -r
$ node -v
v16.15.1
$ npm -v
8.11.0
```
#### 2、watchers超过限制
我在启动hexo -s 时遇到err: Error: ENOSPC: System limit for number of file watchers reached
具体为：
```shell
$ hexo s
INFO  Validating config
WARN  Deprecated config detected: "use_date_for_updated" is deprecated, please use "updated_option" instead. See https://hexo.io/docs/configuration for more details.
INFO  Start processing
FATAL {
  err: Error: ENOSPC: System limit for number of file watchers reached, watch '/home/huhong/My_Blog/themes/aria/'
      at FSWatcher.<computed> (node:internal/fs/watchers:244:19)
      at Object.watch (node:fs:2264:34)
      at createFsWatchInstance (/home/huhong/My_Blog/node_modules/chokidar/lib/nodefs-handler.js:119:15)
      at setFsWatchListener (/home/huhong/My_Blog/node_modules/chokidar/lib/nodefs-handler.js:166:15)
      at NodeFsHandler._watchWithNodeFs (/home/huhong/My_Blog/node_modules/chokidar/lib/nodefs-handler.js:331:14)
      at NodeFsHandler._handleDir (/home/huhong/My_Blog/node_modules/chokidar/lib/nodefs-handler.js:567:19)
      at processTicksAndRejections (node:internal/process/task_queues:96:5)
      at async NodeFsHandler._addToNodeFs (/home/huhong/My_Blog/node_modules/chokidar/lib/nodefs-handler.js:617:16)
      at async /home/huhong/My_Blog/node_modules/chokidar/index.js:451:21
      at async Promise.all (index 0) {
    errno: -28,
    syscall: 'watch',
    code: 'ENOSPC',
    path: '/home/huhong/My_Blog/themes/aria/',
    filename: '/home/huhong/My_Blog/themes/aria/'
  }
} Something's wrong. Maybe you can find the solution here: %s https://hexo.io/docs/troubleshooting.html
```
参考博客[1]后，了解是watch的文件数问题，通过以下命令扩大成果解决。
```shell
$ echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

#### 3、ubuntu防火墙问题
本人没有遇到过防火墙问题，但发现较多在ubuntu上配置hexo都会出现此问题，提供一些相关命令参考[2]。
```shell
$ sudo ufw enable
$ sudo ufw allow 4000
$ sudo ufw allow http
$ sudo ufw allow https
$ sudo ufw status
```

#### 4、报错gnutls_handshake() failed
具体体现为：gnutls_handshake() failed: The TLS connection was non-properly terminated.
此时为代理设置的问题，可重置代理：
```shell
$ git config --global  --unset https.https://github.com.proxy 
$ git config --global  --unset http.https://github.com.proxy 
```
若需使用代理，以8080端口为例,http协议和socket协议的配置分别如下：
```shell
//http
git config --global http.https://github.com.proxy http://127.0.0.1:8080
git config --global https.https://github.com.proxy https://127.0.0.1:8080
//socket
git config --global http.proxy 'socks5://127.0.0.1:8080'
git config --global https.proxy 'socks5://127.0.0.1:8080'
```

## 参考文献：
[1] https://www.jianshu.com/p/faff1b74bd37
[2] https://www.niuqi360.com/linux/install-and-create-blog-with-hexo-on-ubuntu-20-04/
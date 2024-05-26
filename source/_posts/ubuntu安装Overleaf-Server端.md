---
title: ubuntu安装Overleaf Server端
tags:
  - 服务器
  - ubuntu 
  - Overleaf
categories:
  - 编程
  - Linux
date: 2023-05-12 17:20:41
---
本博客的核心在于通过docker拉取完整版的texlive环境，即：
```bash
docker pull tuetenk0pp/sharelatex-full
```
‍具体为：

## 安装docker

打开 /etc/apt/sources.list.d/docker.list​，添加内容：

```bash
sudo vi /etc/apt/sources.list.d/docker.list
deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable
```

更新并安装docker-ce：

```bash
sudo apt-get update
sudo apt-get install docker-ce
```

查看是否安装成功：
```bash
docker --version
```
出现Docker version 20.10.7, build f0df350字样，即安装成功。此处也可参照清华镜像站等手段安装docker:

https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/
## 安装 docker-Compose

进入 https://github.com/docker/compose/releases`​查看最新版本，当前版本为1.29.2

```bash
sudo curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```

设置权限:

```bash
sudo chmod +x /usr/local/bin/docker-compose
```
一般来说，无科学环境github上得较慢，故也可以用pip安装
```bash
sudo pip install docker-compose
```
若显示sudo下没有pip，则sudo apt install  python-pip

查看是否安装成功:

```bash
docker-compose --version
```
出现类似docker-compose version 1.29.2, build 5becea4c即可。

## 安装Overleaf的完整docker镜像

docker权限问题，添加docker用户组：
```bash
#添加docker用户组
sudo groupadd docker
      
#将登陆用户加入到docker用户组中
sudo gpasswd -a $USER docker 
      
#更新用户组
newgrp docker 
```
接着从https://raw.githubusercontent.com/Tuetenk0pp/sharelatex-full/master/docker-compose.yml 下载Overleaf配置文件：

```bash
wget https://github.com/Tuetenk0pp/sharelatex-full/blob/master/docker-compose.yml
vi docker-compose.yml
```
需要修改的就是ports: - 80:80​，一般80端口都被apache或nginx占用了，改用其他端口如：ports: - 62728:80。同时记得更新ufw防火墙。

其他可根据需要修改，如项目名称（SHARELATEX_APP_NAME）、挂载位置等。

如果已经通过docker安装Overleaf的开源版本sharelatex，可以接着安装完整texlive，即先进入docker容器，在docker中安装编译所需的完整的texlive:
```bash
docker pull sharelatex/sharelatex
docker exec -it sharelatex bash
tlmgr option repository https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/
tlmgr update --self --all
tlmgr install scheme-full &
```

安装过程较长漫长，为了避免shell断掉加上 &，回车后可以看到安装过程。可重复再执行update和install。

## 启动Overleaf

在docker-compose.yml​所在路径下执行

```bash
docker-compose up -d
```



## 使用Overleaf

打开浏览器访问 http://hostname:5000/launchpad

创建完成Admin账户，即可。

‍
## 参考文献

1、原始配置文件：https://raw.githubusercontent.com/sharelatex/sharelatex/master/docker-compose.yml

2、https://www.xiaoledeng.com/2021/06/03/ubuntu-install-overleaf-sharelatex/

3、https://junbin.gitbook.io/studynotes/overleaf-da-jian

4、https://zhuanlan.zhihu.com/p/593690031

5、https://xlz.pub/2023/01/10/Ubuntu%E4%BD%BF%E7%94%A8Docker%E6%90%AD%E5%BB%BASharelatex-Overleaf%E5%BC%80%E6%BA%90%E7%89%88%E6%9C%AC-%E5%B9%B6%E9%85%8D%E7%BD%AENginx%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86/

‍
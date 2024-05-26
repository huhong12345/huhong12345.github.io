---
title: nodejs版本管理与hexo多终端重新部署
tags:
  - 生活
  - Nodejs
  - hexo
categories:
  - 博客
  - hexo
date: 2024-05-26 22:38:00
---

## nodejs安装与版本管理
由于涉及到windows下部署hexo环境，先要安装nodejs，并通过nvm来切换版本。

node官网：
https://nodejs.org/en

我安装到了C://My_Program/nodejs目录下。

nvm可到github下载，地址如下，选nvm-setup.exe
https://github.com/coreybutler/nvm-windows/releases

我安装到了C://My_Program/nvm目录下，在选择nodejs时目录时选择了刚刚的地址。

这里就可以使用：
``` bash
nvm list
nvm list available
nvm install 16.15.1
nvm use 16.15.1
npm install -g hexo-cli
``` 
等方式安装特定的node版本并使用。

后续安装hexo就同理：

``` bash
npm install -g hexo-cli
```
注意在nvm install时需要使用管理员运行cmd方式安装。

相关链接：

1、git下载链接：https://git-scm.com/download/win

2、node多版本下载链接：https://nodejs.org/en/download/package-manager

3、hexo主题：https://hexo.io/themes/

## git分支进行多终端部署
如果需要在多终端都进行部署，即完成hexo源文件备份，可使用git的分支系统进行多终端工作。这样每次打开不一样的电脑，只需要进行简单的配置和在github上把文件同步下来，就可以无缝操作。

### 原理
hexo d上传部署到github的其实是hexo编译后的文件，是用来生成网页的，不包含源文件。也就是上传的是在本地目录里自动生成的.deploy_git里面。而我们本地文件的source、配置文件、主题文件都没有上传上去。所以可以利用git的分支管理，将源文件上传到github的另一个分支即可。

### 创建新分支

首先，在我们的github中的blog库中添加新分支hexo，在仓库的settings中，将hexo设置为默认分支(之前为master)。

### 将源文件上传到hexo分支中
在本地的任意目录下，打开git bash，将该分支git clone下来。此时，因为默认分支已经设置成了hexo，所以clone时，只clone了hexo。

之后，在克隆到本地的文件夹中，把除了.git文件夹外所有的文件都删掉。然后把之前我们写的博客源文件全部复制过来，除了.deploy_git。

注意：如果之前clone过theme的主题文件，则应该将主题文件中的.git文件夹也删掉。而且，我们复制过来的文件应该有一个.gitignore文件，这个文件包括了git时要忽略提交的文件，如果没有，自己创建一个，添加上如下内容：
``` bash
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
``` 
之后运行命令：
``` bash
git add .
git commit -m "add branch hexo"
git push
``` 
### 新设备操作
跟之前一样搭建好环境，安装好git、node.js、设置好ssh、安装hexo，但注意此时不需要再对hexo初始化了。
``` bash
npm install hexo-cli -g
``` 
之后，将该库，clone到任意文件夹下。进入到该文件夹，安装一些配置：
``` bash
npm install
npm install hexo-deployer-git --save
hexo g
hexo d
``` 
之后就可以写博客了。最好每次写完博客，都将源文件上传一下：
``` bash
git add .
git commit -m "new push"
git push
``` 

参考文章：

1、https://blog.csdn.net/qq_43657442/article/details/120523934

2、https://blog.csdn.net/qq_43657442/article/details/120522180

3、http://baidinghub.github.io/2020/03/02/Windows%E4%B8%8B%E4%BD%BF%E7%94%A8hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/
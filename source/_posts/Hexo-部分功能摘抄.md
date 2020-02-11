---
title: Hexo部分功能摘抄
date: 2019-11-29 22:10:33
tags: 
- 摘抄
- Hexo
categories:
- 编程
- Hexo
---

### 先放几个有用的博客：
https://zhuanlan.zhihu.com/p/26625249
https://tengj.github.io/categories/hexo%E5%B9%B2%E8%B4%A7%E7%B3%BB%E5%88%97/
https://tengj.github.io/2016/03/06/hexo4/

### 常用的Hexo 命令
``` py
npm install hexo -g #安装Hexo
npm update hexo -g #升级
hexo init #初始化博客

简写命令
hexo n "我的博客" == hexo new "我的博客" #新建文章
hexo g == hexo generate #生成
hexo s == hexo server #启动服务预览
hexo d == hexo deploy #部署

hexo server #Hexo会监视文件变动并自动更新，无须重启服务器
hexo server -s #静态模式
hexo server -p 5000 #更改端口
hexo server -i 192.168.1.1 #自定义 IP
hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令
```
这三个命令依次为新建一篇博客文章、生成网页、在本地预览的操作。
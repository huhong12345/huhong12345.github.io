---
title: Github-Pages+CheapName域名配置
date: 2021-08-02 17:19:25
categories:
- 博客
- 域名
tags:
- Github
- 域名
---
## 整体思路

个人Blog是使用Hexo+Github Pages搭建的。Pages的域名都是默认https://github.com/XXX/XXX.github.io。 如果要绑定域名，需要在域名解析服务商和Github两边都完成操作。具体思路为：
1、在域名解析商处注册个人域名，并配置域名解析，将域名绑定到个人的XXX.github.io
2、在github pages设置页面配置CNAME文件重定向到解析商得到的域名。
类似于双向握手，两边信息匹配握手成功即可。



## 域名解析配置

这里使用的是Namecheap上注册的域名，官网是https://www.namecheap.com/ 。 如果有Github认证学生身份，可以在GitHub Student Developer Pack里找到。感觉这家的域名足够的短，最终注册了huhong.me的个人域名。
![](name.png)

通过学生身份，可以得到一年的域名和SSL认证 https://education.github.com/pack/offers。
如果不需要SSL认证（即使用HTTPS），只需要在Domain List-Advanced DNS处增加三条内容即可：
![](dns.png)
第三条根据自己的情况填写。需要注意的是，github.io.后面有个点，不能省略。
到这里，保存后即完成域名解析的配置。

## CNAME文件配置

配置CNAME文件是为了使得 GitHub Page个人网站.github.io解析到个人申请购买的云服务器域名，也就是当你输入.github.io时会自动DNS解析访问至云服务器域名。

知道思路配置非常简单，直接在自己github.io仓库的Settings-Pages项里，设置Custom domain。设置完后系统会自动在你的仓库里添加一个CNAME文件
![](pages.png)

如果不配置SSL的强制HTTPS，到这里就结束了（配置SSL证书在NameCheap官网里有教程）。

## 其他问题
#### 1、连接Github连不上或访问慢
如果出现了github有时连不上或者访问慢的情况，通常的方法是修改hosts文件：

```bash
#修改 /etc/hosts
sudo vim /etc/hosts
```

hosts里添加Github的ip地址

```bash
140.82.113.4 github.com
199.232.5.194 github.global.ssl.fastly.net
54.231.114.219 github-cloud.s3.amazonaws.com
```

也可以尝试访问下https://ipaddress.com/website/www.github.com 去查看目前Github的实际IP。
```bash
#更新一下hosts
source /etc/hosts
```
也使用Github国内镜像网站的方法，在clone某个项目的时候将github.com替换为github.com.cnpmjs.org或git.sdut.me即可。个人没有试过，供参考：
```bash
//这是我们要clone的
git clone https://github.com/Hackergeek/architecture-samples
//使用镜像
git clone https://github.com.cnpmjs.org/Hackergeek/architecture-samples
//或者使用镜像
git clone https://git.sdut.me/Hackergeek/architecture-samples
```

#### 2、CNAME文件每次被覆盖
如果发现hexo 每次Deploy后需要手动在 Github Pages 的 Setting 里重新设置自定义域名，具体有四个解决方法：

方法一（最推荐）：在source文件夹里将CNAME内容改为huhong.me （即你自己网站的域名）。

方法二：每次 hexo d 之后，去 GitHub 仓库根目录新建 CNAME文件

方法三：每次 hexo d 之后，按照上述CNAME文件配置处，重新在自己github.io仓库的Settings-Pages项里，设置一遍Custom domain

方法四：通过安装插件（不太推荐）：
```bash
npm install hexo-generator-cname --save
```
然后在_config.yml中添加一条
```bash
Plugins: - hexo-generator-cname
```
#### 3、README.md文件每次被覆盖
同理，若想避免 README.md 文件被解析，可在执行hexo deploy前把在本地写好的README.md文件复制到.deploy文件夹中，再去执行hexo deploy。

因为Hexo原理就是hexo在执行hexo generate时会在本地先把博客生成的一套静态站点放到public文件夹中，在执行hexo deploy时将其复制到.deploy文件夹中。Github的版本库通常建议同时附上README.md说明文件，但是hexo默认情况下会把所有md文件解析成html文件，所以即使你在线生成了 README. md，它也会在你下一次部署时被删去。


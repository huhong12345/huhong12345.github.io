---
title: PT&NAS梳理
tags:
  - 生活
  - PT站
  - NAS
categories:
  - 生活
  - PT站
date: 2023-11-15 16:15:48
---

## 介绍
PT (Private Tracker) 是一种基于私有 BT Tracker 服务器的资源传播形式，经授权的用户使用受允许的客户端进行种子制作与下载。相较于传统 BT 和 emule，PT 站往往采取了严格的邀请制度以及免责制度来规避法律风险，同时要求用户客户端开启传输加密以绕过运营商的检测策略。实际上来说， PT 站的运营、使用仍然是违反了各国版权法的。

PT是BT的改进版，拥有约束机制，下载速度有保证，相当于是一个会员制拥有内部圈子的BT，对站点的贡献体现为上传量、等级、魔力等。由于PT站是在私密范围内进行种子分享，所以在PT站内下载种子至少需要满足2个条件，即PT站注册帐号和专用下载软件。其实，每一个PT站点，都有自己独一无二的属性，不是千篇一律的，根据你的需要可选择加入不同的PT站点。PT站就是一个在网络上的虚拟组织，有注册用户、管理员和资源种子，也有行为规则和考核机制，是一个“人人为我，我为人人”的资源共享圈子。

过去（十年前的PT黄金期）主要是高清爱好者聚集在 PT 站，发布翻录的蓝光原盘、CD 资源以及录制的高清电视视频；近期，得益于 Netflix、HBO、Apple TV 等高清流媒体在线视频平台的发展，近年也出现了一些 WEB-DL (Download from Web) 资源。目前国内使用的 PT 站源码大部分为基于浙江大学 xiazuojie 团队所开发的开源整站项目 NexusPHP，基于 PHP + MySQL + memcached。部分站点使用 Discuz! 进行二次开发。建议谨慎选择注册用户数小于 1 万或每周活跃用户数小于 1 千的 PT 站。

根据网络环境和用户群体，国内 PT 站可以划分为两个系别：公网 PT 站和教育网 PT 站。

## 公网 PT 站点
过去中国五大公网 PT 站：HDS、TTG、HDC、CHD、HDR，也有三大 PT 站的说法，即 CHDbits、HDChina、TTG。后来经过世界版权日风波（即被称作“中国版权第一案”的思路网侵权案），HDStar（思路网）管理组被捕入狱，剩下的站点也多多少少受到了一些影响，有些直接关闭了，有的则隐没了。

现在国内论坛主要流传五大站、十二大的说法，其中：
五大（馒空岛瓷套）： **馒头（MTeam）、天空（HDSky）、彩虹岛（CHDbits）、HDChina（瓷）、TTG（套）**。
九大（堡家朋春）：五大+**我堡（Ourbits）、家园（HDHome）、朋友（KeepFRDS）、春天（SSD）**。
十二大（猫观憨）：九大+**猫（Pter）、观众（Audiences）、憨憨（HHClub）**。

五大里，**TTG**发展很快；九大里，**春天**比较隐秘，十二大里，**猫站（PTer）**发展最快。
<img src="/image/pt.jpg" width="60%" height="60%">
图中，柠檬23年5月无了，通常把新来的主打WEB资源站点**憨憨**补充进去，成为新十二大。

五大站里。瓷器的特色是高清电视的录制，空的特色是同一资源各种分辨率的种子都有（PAD版本也有），岛的特色是UHD原盘DIY 公映国语/台配 国配简繁/简繁英特效四字幕 BDJ菜单修改（sGnb），TTG特色是游戏和韩剧。

## 教育网 PT 站点
据说，教育网 PT 站或多或少获得了学校网络中心的技术和政策支持，所以才能存留至今。部分教育网 PT 站仅允许 IPv6 或仅归属于教育网单位的 IPv6 访问，因此对于公众来说访问有些难度。可以通过 Hurricane Electric 提供的 IPv6 TunnelBroker 隧道，或者基于有 IPv6 网络的 VPS 搭建代理来中转 tracker 的流量。

高校校园网提供的 IPv4 网络一般是有计费及限速策略的，由校方向电信、联通、移动、鹏博士等运营商采购带宽并在出口实施自动分流。而为了推广 IPv6 业务，各高校所接入的中国教育网（CERNET）的 IPv6 网络一般是不计费且不限速的，因此组建一个依托于 IPv6 的免费资源分享网络有着很大意义。一般来说，教育网 PT 站的原创影视资源较少，大部分为转载资源。Coursera、Udacity 等公开课资源（WEB-DL）、考研视频、电子书等内容较多，此外，北邮人等站点还提供一些诸如 Steam 游戏数据备份文件。

从分享率和发种规范来看，教育网 PT 站十分宽松，以北邮人（北京邮电大学）、蒲公英（西北工业大学）、极速之星（北京理工大学）和六维空间（东北大学）为主。但保种率可能不如公网 PT 站高，资源也没那么丰富。但对于追热门电影和美剧的轻度用户来说还是足够了。建议初次接触 PT 的用户先从教育网 PT 站（如北邮人、蒲公英）养号，之后通过官方邀请帖等渠道间接进入公网 PT 站。部分 tracker 可能仅允许教育网或 IPv6 连接。入站门槛较低，可以凭借 edu 教育域名的邮箱进行注册，也可以通过校内用户发起邀请。对分享率和种子规范的限制比较宽松。

目前主要的教育网PT站有：
BYR 北邮人：北京邮电大学 PT 站，仅对 IPv6 开放
TJUPT 北洋园：天津大学 PT 站
NanyangPT 南洋：西安交通大学 PT 站
葡萄 PT：上海交通大学 PT 站
NPUPT 蒲公英：西北工业大学 PT 站
BITPT 极速之星：北京理工大学 PT 站
六维空间：东北大学 PT 站
NexusHD：浙江大学 PT 站，仅供校内用户访问
MTPT 麦田 PT: 西北农林科技大学 PT 站
西电睿思：西安电子科技大学 PT 站


## 站点介绍
### 五大
1、馒头（M-team）
成立时间非常长了，采用老用户邀请的方式入站，站内有电影、电视剧、音乐、记录片、4K专区，当然，大家也喜欢馒头的一个不可描述的分享，知道的都懂，站内电影比较多，保种人数也比较多，让你下载资源可达到带宽满速，上传量也非常好刷，每周在不可描述区域下载大包就可以刷几百G的流量。官方提供付费邀请码购买渠道。

2、天空（HDsky）
也是老站了，综合性站点，对于国内的电影和电视剧更新比较快，有官方压制、录制等小组，新资源更新很快，高清影视资源比较多，也是通过邀请进入的，不过天空比较难进，在其他站的官窑也有官方直接邀请的贴子，不过要求非常高，不过只要你玩几个月，自然会变成有缘人进入了的。不过2022 年年中，HDSky 突然修改了账号等级制度和保号政策，并上调 VIP 价格，吃相有点难看。

3、彩虹岛（CHDbits）
近 10 年的老站点，影视资源很丰富。主打特效字幕，很多电影都有相应的特效字幕，如果你有这方面的爱好，可以到这个站点，其实进站的难度也是比较高的，除了官窑进入，普通会员需要使用50W的魔力才可以买一个邀请，而且还有可能被连累，所以一般没有人邀请。

4、瓷器（HDChina）
近 10 年的老站，用户数据继承自原先的 HDWinG 和 HDStar。资源方面，官方制作组（HDCTV 和 HDChina）的 Netflix、HBO 剧集，原盘，录制的电视剧比较多。

5、TTG（totheglory）
totheglory在PT界被称为TTG，2014年成立，资源以高清影视、游戏资源为主，老牌特色PT站，圈内名气比较大，TTG 由原 GameGui(GG)演变而成，2010 年 4 月份，Wiki小组加盟后网站改版为TTG,从原来的单一游戏 PT 站，转型为集众多高清影视、游戏、音乐、动漫资源的综合PT站，目前在国内PT中居于前列，影片、游戏、剧集更新速度快。

### 其他大站
1、我堡（Ourbits）
2016/11/1成立，相对来说比较有特色的的一个影视网站，资源主要涵盖影视、动漫、纪录片、综艺及无损音乐等资源。可以说是仅次于五大站（hdsky/chdbits/mteam/hdchina/ttg）的一个PT站点。官方制作组作品特效字幕是一大亮点，有些资源下载完还没有来得及看就出了特效字幕版本的话，强烈建议洗版，观影体验会极佳。站内有一个保种专区，应该是做种人数低于特定数值后就进入该区，区内种子都是2xFREE的，激励用户下载，特别是新人做任务，同时也有利于减少网站死种。整体资源数量和质量都不错，如果有机会的话不管手里是否有其他pt站，我堡都值得收割。

2、家园（HDHome）
家园PT站的主要资源在蓝光原盘，官方有专门的压制团队，为一些高清蓝光电影增加字幕等进行二次DIY，站内几乎都是影视资源，小种也只有音轨，如果你的设备比较齐全，非常喜欢看高清蓝光电影，可以入这个站，进入相对容易一些，会转种的话上传量刷的会比较快。

3、猫站（PT之友PTer）
综合性的站点，而且是一些比较轻松的站群，进入相对容易一些，而且几乎是一个玩不死的站点，要求比较低，资源也比较丰富，尤其是新剧更新非常快，各大影视站出了马上就会更新，从猫站的官窑可以进入很多大中型PT站。主打游戏和MV资源。

4、朋友（KEEPFRDS）
KEEPFRDS官方解释为Let us keep friends forever，大家都叫朋友，这个站主要就是影视，主打高清小体积的影视资源，全站都是官种，下些资源几乎都是满速，保种非常好，进入全靠邀请，从猫站、北洋官窑比较容易进入。

5、春天（SSD，CMCT）
2010 年创建的老站点，前身为 CMCT 触摸春天。这个站对于宣传非常严格，不允许任何人去宣传，因此进站不太容易。


### 其他中小站
BT School 比特校园：2019 年刚创建的新站点，门槛相对比较低。
HD Time 高清时间：老站点，但是没什么名气。
52PT 我爱 PT：新站点。
PTHome 铂金家：2018 年左右成立的新站，没啥特色。
HDCity 城市：2016 年底成立的新站（相对来说）。
NicePT 老师站：又称为小馒头（相对于 M-Team 来说），2019 年建站。
CCFBits 精品高清：挺老的大站了，资源很丰富也很低调。
HDR (HDRoute)：前身为 HDRoad 思路高清，历史悠久。
LeagueHD LemonHD 柠檬：小站中发展的还算不错的，2019 年成立。已于 2023 年 5 月 20 日永久关闭。
Haidan 海胆之家：2020 年刚成立的小站。
Great Poster Wall (GPW) 海豹: 基于 Gazelle 开发的国内 PT 站，2021 年刚开，没啥特色。
HDU 好多油: 2014 年 12 月 27日创建的老站，距今也快 10 年了。知名度很低，资源一般，没什么原创种。
还有以动漫资源为主的特色站：
U2 动漫花园 幼儿园：老牌动漫 PT 站。各种上古资源都能找到。
Skyey Snow 天雪动漫：基于 Discuz! 构建的 PT 站点，相对来说新一些。
以音乐资源为主的特色站：
OpenCD 皇后 PT：小体积种子比较多，基本靠攒魔力值来保号。
DICMusic 海豚音乐: 基于 Gazelle 开发的国内音乐 PT 站，前身是空耳 PT。

根据@土爹爹整理https://www.tudiedie.com/pt-websites.html， 可参考如下分类：
![](tu2.png)

## 站点数据
1、最新的数据可以参考https://api.rhilip.info/ptanalytics.html
### 五大站：
馒头MTeam：2022: Total Online days: 246 (67.40 %), With Recorded Torrents: 41914, Average 170.38 (Online days), 114.83 (Total Year) torrents per day
天空HDSky：2023: Total Online days: 309 (84.66 %), With Recorded Torrents: 56731, Average 183.60 (Online days), 155.43 (Total Year) torrents per day
彩虹岛CHDBits：2023: Total Online days: 308 (84.38 %), With Recorded Torrents: 67788, Average 220.09 (Online days), 185.72 (Total Year) torrents per day
瓷器HDChina：2023: Total Online days: 305 (83.56 %), With Recorded Torrents: 33475, Average 109.75 (Online days), 91.71 (Total Year) torrents per day
套TTG：2023: Total Online days: 310 (84.93 %), With Recorded Torrents: 32989, Average 106.42 (Online days), 90.38 (Total Year) torrents per day
### 其他大站
我堡（Ourbits）：2023: Total Online days: 310 (84.93 %), With Recorded Torrents: 29111, Average 93.91 (Online days), 79.76 (Total Year) torrents per day
家园（HDHome）：2021: Total Online days: 213 (58.36 %), With Recorded Torrents: 12405, Average 58.24 (Online days), 33.99 (Total Year) torrents per day
春天（SSD）：2023: Total Online days: 308 (84.38 %), With Recorded Torrents: 31592, Average 102.57 (Online days), 86.55 (Total Year) torrents per day
猫站（PTer）：2022: Total Online days: 277 (75.89 %), With Recorded Torrents: 48146, Average 173.81 (Online days), 131.91 (Total Year) torrents per day
学校（BTSChool）：2022: Total Online days: 284 (77.81 %), With Recorded Torrents: 16950, Average 59.68 (Online days), 46.44 (Total Year) torrents per day
### 教育网
北邮BYR：2022: Total Online days: 365 (100.00 %), With Recorded Torrents: 12147, Average 33.28 (Online days), 33.28 (Total Year) torrents per day
北洋TJUPT：2023: Total Online days: 316 (86.58 %), With Recorded Torrents: 40647, Average 128.63 (Online days), 111.36 (Total Year) torrents per day

2、根据 @Rhilip 的分析，对按官方种占比排序。数据源日期为 2018/4/10https://blog.rhilip.info/archives/839/
![](sj.jpg)

## PT 下载客户端选择
不同网站对于 BT 客户端的兼容性不同。尤其是 BitTorrent v2 协议推出后，与旧版本的客户端均不兼容。因此部分 PT 站会拒绝较新版本的 BT 软件。此外，普通的 PT 下载器如 Free Download Manager (FDM)、迅雷、Aria2c 以及 qBittorrent-enhanced 是被严格禁止的。

- 99.9% 的 seedbox 用户选择 Rtorrent/Rutorrent，因为有些 seedbox provider 只提供这些。
- 大部分 Windows 用户选择了 µTorrent (uTorrent)。但是 uTorrent 3.x/4.x 并不稳定，性能也不好，内置了浏览器、工具栏等奇怪的插件。另外一部分用户选择了 qBittorrent。
- 大部分群晖用户会选择 Synology Download Station；而由于糟糕的兼容性，大部分威联通用户会选择封装好的 qBittorrent。还有一部分人用 Transmission。这里更推荐使用 qBittorrent 的 Docker 镜像，方便迁移数据和版本升级等。
- Linux 用户可能会选择 libtorrent 或 qBittorrent-nox。

## 硬盘选择
推荐购买 WD Ultrastar 和 希捷银河 (Seagate Exos) 这两个系列的硬盘，国行经销商（非京东、淘宝官方店）的购买价格约为 110-130 元/TB。几家圈内知名代理商的淘宝店。这几家店价格基本一致，哪家售后好买哪家就行：
- 南京梵多
- 北京硬盘之家
- 上海硬盘公园
- 上海坤心
个人购买的是希捷银河18T（放服务器），和四个4T海康威视的VX0015监控盘（放NAS里）。



## NAS选择
### 成品NAS
1、群晖 (Synology) 和威联通 (QNAP) 总部都位于台湾，但前者的本地化 (localization) 做的明显比后者好，无论是帮助文档、软件的 UI/UX 还是云中转隧道服务。特别需要注意的是，群晖在大陆的销售活动实施控价销售，在非官方促销活动时，从淘宝、天猫和京东等平台查看的售价要高于实际经销商售价的几百至几千不等。

2、群晖在亚马逊美国（美亚）的价格比国内低 20-30%，即使算上关税和运费也比国内目录价便宜几百上千。但需要注意的是海淘群晖无法在大陆享受保修服务，部分淘宝商家可以代为邮寄至香港保修。

3、威联通 QTS 现在有第三方应用商店 Qnapclub Store，资源相当丰富，更新也很及时。https://qnapclub.eu/en

4、本人目前使用的是威联通464C，CPU是5095内存8G，4个4T硬盘组的raid0；同时有一个N5105的软路由，内置2T固态，有一个黑群晖。平时的照片备份、笔记之类的都还是用UI更好一些的群晖，威联通主要用来存数据和干一些粗活（如PT），相当于双持党。同时照片等一些重要数据，通过内网传输，在两台NAS上做了双备份，最重要的数据，定期上传到云盘或冷备份。个人还是不太相信所谓的Raid。


### 替代方案
只需要本地文件存储的用户，选购移动硬盘配合 OpenWrt 路由的 SMB 共享。
有转码、Docker 容器和 KVM 虚拟机等需求的用户，尽量选择自己组装 TrueNAS、UNRAID 等平台。
有充足预算，需要代维护的小企业和 SOHO 用户，可以考虑群晖 Synology。
傻瓜方案：安装 Ubuntu Server，用 docker 跑 qbittorrent-nox，再装一份 Plex Media Server 就可以了。GPU 转码没什么必要，TV 端和移动端的 Plex 支持本地解码。文件存储用 Seafile 或 NextCloud。备份通过 rclone 同步至 OneDrive 或 Backblaze B2。
替代方案有：
照片备份 => OneDrive/iCloud/Google Drive/…
PT 下载 => qBittorrent/libtorrent/rtorrent/…
数据备份 => rclone/rsync/btrfs-send/…
文件同步 => OwnCloud/NextCloud/…
文件读写 => Samba/nfs-kernel-server/…
VPN 访问 => ZeroTier/WireGuard/OpenVPN/…
虚拟化 => ESXi/Docker/LXC/LXD/…
## 注意事项
除非在特定板块，不要在某个 PT 站提到其他 PT 站点的名字。
有些网站管理员非常介意用户流失，或者与其他站点发生过不愉快的事情，因此会对触犯此条例的用户执行封禁。
尽可能地尊重发布者，不要在评论区发表不积极的意见。
尊重资源发布者是一种美德。触犯此条例可能会获得警告信或者永久封禁。
遇到技术问题应先使用搜索引擎检索，而不是当伸手党。
网站管理员一般非常反感小白用户的问题。
不要作弊
由于圈子很小，可能会遭受连锁封禁（被多个站点同时封禁）。你也可以理解为国内 PT 站点有着一个类似 John Wick 里的 High Table（高桌会）组织，会就行为恶劣的事件达成共识。
不要持有小号（马甲）
管理员一般会基于以下规则来判断马甲账号
用户的登录、注册 IP
用户客户端上报 Tracker 所使用的 IP
用户名及邮箱的命名规律
匿名举报
谨慎选择邀请人，不要随意向陌生人发送邀请。
部分站点对于违反某些规则的用户会采取连坐措施，封禁整个邀请链（树）。
不要在公共场合发送、索求邀请码，或者提到网站网址和名称。
这个“传统”已经持续近十年了，只不过是自我安慰。

## 站点链接(摘抄自互联网)
序号	英文名	中文名	网址	主要资源类型
### 五大
1	Mteam	馒头	https://kp.m-team.cc/	影视、XXX、音乐
2	HDSky	天空	https://hdsky.me/	影视
3	CHDBits	彩虹岛	https://ptchdbits.co/	影视
4	TTG	听听歌	https://totheglory.im/	影视、游戏
5	HDChina	瓷器	https://hdchina.org/	影视
### 九大
6	Ourbits	我堡	https://ourbits.club/	影视
7	HDHome	家园	https://hdhome.org/	影视
8	SSD/cmct	春天	https://springsunday.net/	影视
9 FRDS	朋友	https://pt.keepfrds.com/	影视
### 十二大
10 HHCLUB	憨憨	https://hhanclub.top/	WEB
11 PTerclub	猫站/PT之友	https://pterclub.com/	影视
12 Audiences	观众	https://audiences.me/	影视
### 中型站
13	BTSchool	学校	https://pt.btschool.club/	影视
14	TCCF/torrentccf	他吹吹风	https://et8.org/	学习
15	Soulvoice	聆音	https://pt.soulvoice.club/	电子书、学习
16	HDCity	城市	https://hdcity.leniter.org/	影视
17	UB	优堡	https://ubits.club/ 	影视
18	PTTime	PTT	https://www.pttime.org/	综合
19	RL 红叶	https://leaves.red/ 	综合，有声书
20	TLFBits/eastgame	吐鲁番	https://pt.eastgame.org/	影视
### 外站
21 IPT https://iptorrents.com/ 综合
22 TTL https://www.torrentleech.me/ 综合
23 Jpo https://jpopsuki.eu/ 音乐
### 教育网
24	TJUPT	北洋园(天津大学)	https://tjupt.org/	影视、学习
25	BYRBT	北邮人（北京邮电大学）	https://bt.byr.cn/	影视、学习
26	SJTU	葡萄（上海交通大学）	https://pt.sjtu.edu.cn/	影视、学习
27	HUD	蝴蝶（华中电子科技大学）	https://hudbt.hust.edu.cn/	影视、学习
### 音乐站&特色站
28	DICMusic	海豚音乐	https://dicmusic.club/	音乐
29	GPW	海豹	https://greatposterwall.com/	电影
30	Opencd	皇后	https://open.cd/	音乐
31	U2 动漫花园	https://u2.dmhy.org/ 	动漫
32	Dajiao 打胶	https://dajiao.cyou/ 	纪录片
33	Rousi 肉丝 https://rousi.zip/ 9KG
34	PTLSP	https://www.ptlsp.com/ 	影视
### 其他
10 lemonhd	柠檬	https://lemonhd.org/	影视
11	HDTime	时间	https://hdtime.org/	影视
14	HD Dolby	杜比	https://www.hddolby.com/	影视
15	Pthome	铂金家	https://www.pthome.net/	影视
16	dmhy/U2	幼儿园	https://u2.dmhy.org/	动漫
17	HDArea	视界	https://www.hdarea.co/	影视
18	HD4Fans	兽站	https://pt.hd4fans.org/	影视
27	HDU	好多油（杭州电子科技大学）	https://pt.hdupt.com/	影视、学习
28	NPU	蒲公英（西工大）	https://npupt.com/	影视、学习
29	neu6	六维空间（东北大学）	http://bt.neu6.edu.cn/	影视、学习
30	HITPT	百川（哈尔滨工业大学）	https://www.hitpt.com/	影视、学习
31	nanyangpt	南洋（西安交通大学）	http://nanyangpt.com/	影视、学习
32	ccfbits	吹吹风	https://ccfbits.org/	影视
33	JoyHD	JoyHD	https://www.joyhd.net/	影视
34	Ptsbao	烧包	https://ptsbao.club	影视
35	Beitai	备胎	https://www.beitai.pt/	影视
36	PTMSG	马杀鸡	https://pt.msg.vg/	影视
37	52PT	我爱PT	https://52pt.site/	影视
38	HDFans	红豆饭	https://hdfans.org/	影视
39	HDZone	空间	https://hdzone.me/	影视
40	HaiDan	海胆	https://www.haidan.video/	影视
41	1ptba	壹PT	https://1ptba.com/	影视
43	hdatmos	全景声	https://hdatmos.club/	影视
44	Soulvoice	聆音	https://pt.soulvoice.club/	电子书、学习
47	NicePT	老师	https://www.nicept.net/	XXX
48	AVGV	艾薇网	https://avgv.cc/	XXX
49	HDbd	伊甸园	https://pt.hdbd.us/	XXX
50	SkyeySnow	天雪	https://www.skyey2.com/	动漫
51	DiscFan	港知堂	https://discfan.net/	影视
54	htpt	海棠PT	https://www.htpt.cc/	曲艺,小品,有声小说
56	HDPOST	HDPOST	https://pt.hdpost.top/	电影,电视剧

参考：
[1] 站点：https://iecho.cc/2019/01/09/PT-%E4%B8%8B%E8%BD%BD%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%85%BB%E8%80%81/
[2] NAS和硬盘选择：https://iecho.cc/2022/02/06/beginners-guide-to-private-tracker-3/
[3] 药丸论坛：https://invites.fun/
[4] 保种：https://reseed.tongyifan.me/
[5] QnapClub：https://qnapclub.eu/en
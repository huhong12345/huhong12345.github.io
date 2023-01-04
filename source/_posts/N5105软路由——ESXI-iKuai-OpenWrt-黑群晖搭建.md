---
title: N5105软路由——ESXI+iKuai+OpenWrt+黑群晖搭建
date: 2022-09-08 11:51:26
tags:
  - 生活
  - 软路由
  - ESXi
categories:
  - 生活
  - 软路由
---
发发发最近刚刚接触软路由，记录一下All in One的思路。我的方案其实已经算目前圈子里较为成熟的选择，主要是跟着其他博客大佬，看他们设计自己All in One主机的过程、思路，选择一套属于自己需求和未来需求的主机。整个过程中，思考和思路的借鉴似乎可以值得记录，毕竟这属于DIY圈，不同人需求差异还是较大的。

## 总述
All in One主机一般来说是一个虚拟机底层系统，集成众多针对特定需求建立的子系统，形成的一整套个人服务器。

然而，由于虚拟机硬件转化率低，同时集成度高的耦合系统很容易出现，All in One， All in Boom的现象，All in One方案始终被诟病。很多人更倾向于将软路由只作为拨号与插件使用，通过购买NAS、独立服务器实现其他功能。

随着x86软路由性能逐渐提高，从J1900到J4125和N5015，软路由只装个Openwrt性能远远过剩。同时显卡直通、内网穿透等手段让All in One方案对垃圾佬来说具有很大吸引力。
## 底层架构
一个底层虚拟机系统，其稳定性、可维护性、容错性、硬件性能转化率，很大程度上决定了All in One主机的使用体验。具体而言，有以下四种方案：

1·安装Windows，使用Hyper-v虚拟机安装其他系统

2·安装Ubuntu/Debian等Linux内核系统，在Liunx环境下使用Docker或安装虚拟机运行其他系统。

3、安装支持Docker的系统平台（unRAID、群晖/威联通Nas系统、Liunx），通过Docker完成虚拟机部署。

4、安装底层虚拟机（ESXI/PVE/unRAID），其他系统全部运行在底层虚拟机上。

### Windows+Hyper （Windows+虚拟机）
这种方案最大优势是熟悉和便利。最突出的缺陷是性能转化率太低。机制使然，Windows系统下虚拟机的性能转化率相对(太)低。且Windows系统本身就会占用了（很大）部分的硬件资源。抑制了虚拟机对硬件性能的利用。

同时，其性能转换率、运行稳定性都不尽人意。显然，这不是虚拟机的可靠环境，更不是组All in One主机的理想选择。但Hyper几乎Windows原生。通常安装了Windows的计算机在现有条件下、无需安装其他软件即可着手虚拟机的部署。另一方面，以Windows的普及率和保有量，在安装、交互操作等方面几乎没有学习成本。这样的属性也让Windows+Hyper成为很多初学者最先上手的方案。所以这种方案通常用于一些简单测试、功能调试等临时任务。以及学习部署虚拟机、了解虚拟机的运行机制。

### Linux系统（Ubuntu/Debian等）上安装虚拟机环境。
这个方案的优点是在硬件性能转化率上相对Windows要好很多，甚至很多虚拟机的内核本身就是基于Liunx系统开发。在兼容性、可维护性上，Liunx平台对虚拟机也更加友好。尤其在某些调试上，Liunx作为根系统有不可替代的优势。最具代表性的就是Liunx作为根系统，直接为Docker提供了环境。

但其缺点是虚拟机直接部署在Linux系统上需要对Linux交互有一定基础，这导致其大概率不会是一个首选方案，而是一个可学习、调试和实践的方案。

### 3、Nas/liunx+Docker
这种方案的最大优势是Docker容器轻量化、高效率、扩展性强的天然优势。开源平台从不缺少方方面面的扩展，具象需求几乎都能找到对应趁手的工具。且Docker机制决定了其在部署的便利性上有着其他系统(方案)不可比拟的优越性。

对于已经有成品NAS，通过NAS+Docker的方案，让现有NAS具备更多功能，即在已经成型的Linux环境下进行拓展和加强，实现个人需求。Nas性能一般运行一个Op也足足够用。

然而，其缺点是成品NAS价格昂贵，同时其性能也具有一定瓶颈。同时，NAS+Docker实现底层系统的核心在Docker，而Docker依然具有一定局限性，如不支持32位，不完全虚拟、隔离不彻底等。

所以其实可以直接将NAS作为一个子系统而不是根系统，让Docker存在于虚拟机中的虚拟机，这样不失Docker功能及实现上的便利，又不拘泥于Docker而封堵其他系统并存的实现。当硬件配置足够(至少强过成品Nas整机)时，不舍弃Docker，但不围绕、局限于Docker，才可以为更加宽旷的可能性提供更包容的扩展环境。

### 4、直接安装底层虚拟机
这个目前是目前All in One主机的最优解决方案，底层系统可以是ESXi、PVE、UnRaid，子系统可以是iKuai、Openwrt、Nas或两两组合，有时还会加一个Windows用于下载或远程桌面等粗活。

这种方案拥有最高的硬件性能转化率。底层部署，由于不依托其他系统，没有多余的资源消耗。进而硬件直通，尤其是网卡、硬盘实现直通，不仅性能提升明显。且能够大幅减少虚拟机对宿主机的性能资源消耗。


## 硬件
All in One主机属性注定要7*24小时值守工作，所以功耗和散热是两个最重要的问题，虽然也有自组的想法，但最后觉得第一台还是成品机较好。

机器的选择上，首先肯定排除Arm阵营的软路由（R4S、R5S、R68S等）系列，它们性能太差，拓展性太差适合只作为软路由，连接交换机使用。且目前来说，四五百的价格性价比较低。最便宜的R2S甚至带不起千兆。

x86平台，目前来看，J1900宝刀已老，J4125是最稳定的。其散热控制，和性能表现，对于AIO非常合适。且其出来也有一段时间，各项BUG和解决方法在网上也都能找得到。

不过，在我购买的时候N5105准系统大约650，而J4125也需要550。本着买新不买旧的想法，和对M2接口的需求，本人最后选择了11代10nmCPU的N5105平台。其实两者性能也就相差30%左右，只是N5105新平台，对内存频率容量和扩展性好一些。特色大致如下：
<img src="/image/tese.png" width="40%" height="40%">

这个机器主要的问题在于散热，感觉磨具和J4125差不多，但性能提高就稍微有点压不住了。本人提前买了一个USB小风扇准备辅助散热，不过目前不拿它跑太大的东西，暂时被动散热也还可以。
<img src="/image/cemian.png" width="40%" height="40%">
<img src="/image/zhuban.png" width="80%" height="80%">

650的准系统+闲鱼125收的英睿达8G 3200内存+129京东买了个垃圾固态爱国者P2000 256G ，总共花了900。硬件方面暂时不会有太大新的需求，后期会把笔记本的2T 2.5寸硬盘接上预留的SATA口（随机附赠了SATA线）。

AP方面用的是华为AX3 Pro，一个普通的Wifi6路由器。（最一开始就是因为这玩意固件不开源没法刷系统装插件，才开始关注的软路由），就是硬件的全部了。




## 软件
本人最终装的系统是ESXi主系统，内置iKuai主路由+OpenWrt旁路由+NAS。下面尽量省略，主要说下思路。

### 安装ESXi系统
1、接通电源，电脑连eth0（未来的lan口），hdmi连显示器，接上USB鼠标键盘。

2、使用Ventoy制作PE启动盘，里面放上ESXi主系统和WePE64防止需要部分操作。
<img src="/image/ventoy.png" width="40%" height="40%">

3、进入ESXi安装界面，可能会出现识别不了NVME硬盘的现象，原因是6.7版本以后新的ESXi删除了部分消费级NVME驱动，可在先前的版本把驱动复制过去或直接使用论坛上已经集成好NVME驱动的ESXi固件。

4、安装好固件后设置密码，这里密码要求比较高，要有大小写和特殊符号（后面可通过重置系统删除掉这个密码）。

5、重启后，F2进入菜单，输入密码，Configure Management Network-IPv4 Configuration，设置
<img src="/image/shezhi.png" width="80%" height="80%">
这里我没有采集卡，参考了别人的截图。我的网关是123，所以IPv4地址是192.168.123.3，网关是192.168.123.1（未来的iKuai主路由）

6、转到电脑，设置为123网段，进入192.168.123.3虚拟机主界面，网卡直通，重新引导。
<img src="/image/zhitong.png" width="80%" height="80%">

7、ESXi转到网络-虚拟交换机-编辑设置-安全-接受混杂模式，重新引导。

### 安装IKuai
1、ESXi创建新新虚拟机，给2两个CPU，2个插槽，2G内存，2G备用，4G硬盘，CD挂载iKuai固件iso。添加三次PCI设备（eth1-3三个网卡）
<img src="/image/ik.png" width="80%" height="80%">
2、ESXi双击启动iKuai，1将系统安装到硬盘1。1设置网卡绑定，set wan1 eth3；2设置LAN地址192.168.123.1
<img src="/image/ik2.png" width="80%" height="80%">
3、电脑输入192.168.123.1，进爱快后台。如果需要连外网就wan1设置PPPoE拨号（家用宽带）或DHCP（校园网）。也可以将内网三个lan口链路桥接。ikuai设置自动启动。

### 安装Openwrt
1、首先需要将img文件转换为虚拟机识别的引导镜像，即使用StarWindConverter，Image format选择VMWare ESXI server image，得到两个vmdk文件。

2、ESXi建立新虚拟机，分配1个CPU，2G内存 ，删掉USB控制器、CD驱动器等。（作为旁路由不需要添加PCI设备，作为主路由需要），虚拟机选项引导选择BIOS；

3、添加现有硬盘，新建一个叫OP的文件夹，分别上传两个vmdk文件
<img src="/image/op.png" width="80%" height="80%">

4、安装好后，修改配置文件 vi etc/config/network ，将lan的ip从192.168.5.1修改成主路由的网关下的地址，如192.168.123.2；

5、进入OP后台-网络-接口-Lan修改-网关设置为192.168.123.1，基本设置-忽略此接口

### 安装NAS
1、使用StartWindConverter将synoboot.img转换为两个vmdk文件。

2、部署服务器的时候，服务器操作版本选择Red Hat Enterprise Linux7 64位，CPU给2个，内存给2G，删除掉硬盘+SCSI控制器+CD驱动器，在网络适配器-类型选择E1000e，完成。
<img src="/image/nas.png" width="80%" height="80%">

3、编辑NAS设置-添加现有硬盘-建立NAS文件夹-上传两个vmdk文件；

4、添加 新标准硬盘-设置为80G左右-磁盘模式选独立持久；

5、打开电源-通过iKuai后台查到NAS地址，进去。设置-浏览-DSM_DS918+.pat-安装系统;

6、进入NAS系统，存储空间管理员-存储空间-新增-  快速-选择硬盘80G-应用；共享文件夹也可以新建一个，编辑文件夹权限涉资为可读写。 

参考：https://www.right.com.cn/forum/forum.php?mod=viewthread&tid=8238423&extra=&highlight=n5105&page=1

### 硬盘直通
1、关机，断开SATA盘与主机的连接，然后再开机. 注意：**不断开会使直通设置过程出错**.

2、主机 -> 管理 -> 硬件 -> PCI设备，找到“Intel(R) SATA controller”，找到SATA设备的“设备ID”与“供应商ID”.

3、右键菜单启动TSM-SSH：主机 -> 管理 -> 服务 -> TSM-SSH

4、putty通过SSH连接exsi，密码同网页端的登录密码，登录后编辑直通配置文件.
输入命令：

``` bash
vi /etc/vmware/passthru.map
``` 
在文件末尾增加下面2行数据。8086为“供应商ID”，4dd3为“设备ID”，可根据第1步找到的值进行修改。

``` bash
# Intel(R) SATA controller
8086  4dd3  d3d0     default
``` 
按":"进行命令模式，输入"wq"两个字符保存退出.

5、重新exsi主机使修改生效. 再进入系统后，可看到sata能设置为直通，手动把sata切换为直通.

6、关机，连接上SATA硬盘.

参考：https://www.bilibili.com/video/BV1da411J7zF/?spm_id_from=333.999.0.0&vd_source=cf9bf18d8cd9c4647e5513862d2eb7aa

到这一个简易的iKuai+OpenWrt+NAS@ESXi主机就大概搭建完成了。
## 最终拓扑图
最终放上我的网络拓扑图，方便理解。
![](tuopu.png)

## 参考
1、https://www.right.com.cn/forum/forum.php?mod=viewthread&tid=8219610&highlight=N5105 （固件下载）
2、https://www.right.com.cn/forum/forum.php?mod=viewthread&tid=8249615&highlight=N5105 （畅网套装）
3、https://www.bilibili.com/video/BV185411o7gY?spm_id_from=333.880.my_history.page.click&vd_source=cf9bf18d8cd9c4647e5513862d2eb7aa （向北J4125视频）
4、https://www.bilibili.com/video/BV1LN4y1379g/?spm_id_from=333.788.recommend_more_video.0&vd_source=cf9bf18d8cd9c4647e5513862d2eb7aa （向北N5105视频）
5、https://www.bilibili.com/video/BV1NT4y16799/?spm_id_from=333.788.recommend_more_video.2&vd_source=cf9bf18d8cd9c4647e5513862d2eb7aa （阿雷课堂视频）


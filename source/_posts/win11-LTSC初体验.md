---
title: win11 LTSC初体验
tags:
  - 生活
  - win11
  - 系统
categories:
  - 硬件
  - 装机
date: 2024-05-26 21:05:50
---
由于装新电脑，尝试了一下2024年4月刚出的win11 LTSC泄露版。

目前时全英文的，不过后续可以汉化，问题不大。
### 1、安装
在安装这步选择lot版本，该版本可以跳过win11系统的硬件检测，同时有10年的超长支持期（虽然也没啥啥用）
![](1.png)

这里如果没有联网，就可以直接使用本地账户。

如果选了普通版，也可以通过以下方式跳过：

安装按Shift+F10，打开命令行界面，输入regedit打开注册表，然后定位到HKEY_LOCAL_MACHINESYSTEMSetup，接着创建一个名为“LabConfig”的项

接着在“LabConfig”下创建两个DWORD值：键为“BypassTPMCheck”，值为“00000001”，键为“BypassSecureBootCheck”，值为“00000001”

安装完后系统显示Version 24H2，OS build为26100.1

### 2、汉化
如下图，添加语言
![](2.png)
下载中文并设为首选语言。

![](3.png)

在下面的区域设置(Country or region) 中，把国家和地区改为中国。

在管理语言设置（Administrative language settings），把下面两个勾都打上，能改成中文的都改了。
![](4.png)

同时在Change system location处把地址改为中国，重启后，就为中文了。

重启后可能会出现简体中文输入法问题，下载“基本输入法”即可。

如果将 Win11 设置成中文后界面出现中英文混杂的情况，可以尝试在语言和区域设置中将系统语言改回英文，然后删掉刚才下载的中文语言包。 重启过后再进行一遍汉化的步骤即可。
### 3、优化
此处，可使用HEU KMS Activate数字激活。

#### 恢复windows应用商店
按下win+R，输入命令：
``` bash
wsreset -i
```
系统就会自动下载。

#### 释放保留的存储空间
管理员身份进入powershell，输入：
``` bash
DISM.exe /Online /Set-ReservedStorageState /State:Disabled
```
### 参考
1、原帖镜像：archive.org/details/26100-ltsc-x64-enus

2、系统镜像：https://www.bilibili.com/video/BV1pT421C7f1/?spm_id_from=333.337.search-card.all.click&vd_source=cf9bf18d8cd9c4647e5513862d2eb7aa

3、安装教程：https://www.bilibili.com/video/BV1pT421C7f1/?spm_id_from=333.337.search-card.all.click&vd_source=cf9bf18d8cd9c4647e5513862d2eb7aa


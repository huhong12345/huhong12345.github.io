---
title: 整合一下深度学习caffe基本环境的配置
date: 2019-11-29 22:34:28
tags: 
- DL
- 配环境
- 心情
categories: 
- 科研
- DL
---
**本帖为一个回忆贴，最初写于2016年11月，大二上学期**
2016年11月，经历了数模校赛，培训，国赛等一系列折磨后，最终结果是拿到了个不好不坏的成绩：国二。虽然还是有些不甘心，但仔细想觉得数模也就那么回事，随缘就好，便申请负责了一个国创项目，间接进入导师实验室开始做科研训练。（这里还是要感谢电院较好的学术氛围和师资）

当时因为在院里实验班，自己成绩和竞赛也还不错，就找到了学校里一个挺不错的图像组的大佬当导师。那时候感觉DL没有现在那么火，自己也是第一次接触它当然，那时候第一次看这相关paper还是蛮难的，第一次接触“深度学习”这个词，但又被它各种玄幻但又挺符合常理的操作所折服。现在回忆起来，对本科生来说，多自学，早日将数学和英语水平提高到一定层次进组做科研比一味做一些所谓加分的竞赛对个人实力提升要有用得多。

说回来，当时国创项目还是偏工程一些，主要关于衣物的目标检测与识别的内容。由于前期没有任何学长的帮助，一开始在配环境上就花了很长时间。那时候做目标检测还是Caffe的天下。（配过的同学应该知道这玩意有多恶心）不过后来问问基本都是这样过来的，格十几次系统不算大事。本blog主要记录的是配环境的总结。应该算是最后一种非常完善普适的方法了。（后期进实验室才发现，实验室框环境都配好的，从老的faster-RCNN到SSD、resnet等等都有学长给弄好的，需要做的只是安心看paper，带着数据去跑即可）

本来也参考了很多CSDN前辈的教程，也按照《深度学习——２１天实战caffe》这本书来配过，但是都不成功。Caffe不像现在TensorFlow，Pytorch这种兼容性那么强，它于各种电脑的配置、环境都极大相关，且修复较难，牵一发而动全身。加上后来配GPU版的时，才发现只能先装Cuda等驱动才能在在其基础上装Caffe-gpu，又得推翻重来。（可能也是因为自己菜，当时大二上也没怎么有很多Linux的基础）故仅凭一篇教程来配置caffe是欠妥当的。建议后面的朋友主要看看每篇教程有什么不同，配的时候多带着些思考，哪些依赖包是教程没有提及但自己电脑又确实没有的。
　　
Caffe依赖多且复杂，历来被人诟病，但是配置编译完成后caffe所带来的欣喜与便捷也足以回报先前的煞费苦心。相信自己的能力也会随配环境这个过程逐步提高，而慢慢入门。希望未来看到这篇博客的你不要灰心丧气、半途而废！

　　正文开始：
　　由于选择的是CPU训练，所以暂时没有配置Cuda和CuDNN两个环境。

　　计算机配置：
　　Ubuntu 16.04 LTS
　　i7-4720HQ
　　8G内存



## 安装依赖库
　　在终端输入

``` python
sudo apt-get install libprotobuf-dev   
sudo apt-get install libleveldb-dev   
sudo apt-get install libsnappy-dev   
sudo apt-get install libopencv-dev   
sudo apt-get install libhdf5-serial-dev   
sudo apt-get install protobuf-compiler  
sudo apt-get install --no-install-recommends libboost-all-dev
```


　　接下来安装BALS(基本线性代数子库)

``` python
  sudo apt-get install libatlas-base-dev
```


　　使用默认Python来建立pycaffe接口，需要安装：

``` python
sudo apt-get install python-dev  
##另一些兼容依赖库
sudo apt-get install libgflags-dev  
sudo apt-get install libgoogle-glog-dev   
sudo apt-get install liblmdb-dev 
```



## 下载Caffe源码

安装git

``` python
sudo apt-get install git
```

下载caffe 源代码

``` python
git clone https://github.com/BVLC/caffe.git
```

在终端下载可能会有些慢，而且容易掉线，还不支持断点续传，所以我们也可以访问上面的网站，在网站下载ｚｉｐ格式的文件，再解压到/home 就可以了。

这里多说一句，在终端下载源文件时系统会自动在/home 下生成一个名叫caffe 的文件夹，当遇到了下载不成功的情况时，我们需要找到这个文件夹，把它删除，当然里面什么也没有。这样下次再用命令行下载才不会报错。

如果需要Caffe的Python接口，切换到caffe下的python目录下，输入以下命令下载python依赖库（先安装pip）：

``` python
cd /caffe/python
sudo apt-get install python-pip
for req in (catrequirements.txt);dopipinstall(catrequirements.txt);dopipinstallreq; done
```



## 编译Caffe

开始编译之前，建议输入以下命令：

``` python
make clean
```

我们来到caffe 文件夹中，将Makefile.config.example 文件复制一份，改名为Makefile.config，然后我们打开这个复本文件，做一些必要的修改。

将原文本如下：

``` python
＃CPU-only switch (uncomment to build without GPU support).
# cpu_only :=1
```

改为如下形式：

``` python
＃CPU-only switch (uncomment to build without GPU support).
cpu_only :=1
```

将原文本如下：

``` python
＃Whatever else you find you need goes here.
INCLUDE_DIRS :=(PYTHONINCLUDE)/usr/local/includeLIBRARYDIRS:=(PYTHONINCLUDE)/usr/local/includeLIBRARYDIRS:=(PYTHON_LIB) /usr/local/lib /usr/lib
```

改为如下形式：

``` python
＃Whatever else you find you need goes here.
INCLUDE_DIRS :=(PYTHONINCLUDE)/usr/local/include　/usr/include/hdf5/serialLIBRARYDIRS:=(PYTHONINCLUDE)/usr/local/include　/usr/include/hdf5/serialLIBRARYDIRS:=(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial
```

将原文本如下：

``` python
＃NOTE: this is required only if you will compile the python interface.
#
We need to be able to find Python.h and numpy/arrayobject.h.
PYTHON_INCLUDE := /usr/include/python2.7 \
/usr/lib/python2.7/dist-packages/numpy/core/include
```

改为如下形式：

``` python
＃NOTE: this is required only if you will compile the python interface.
#
We need to be able to find Python.h and numpy/arrayobject.h.
PYTHON_INCLUDE := /usr/include/python2.7 \
/usr/local/lib/python2.7/dist-packages/numpy/core/include
```

接下来是编译。
这里需要注意四点：
１、这些命令要在caffe路径下执行；
２、若编译报错与numpy有关，往往需要安装numpy:

``` python
sudo apt-get install python-numpy
```

若报错与matplotlib相关，则需要相应安装这个package;
３、若编译出现失败，需要执行make clean 命令，然后重新将四条编译命令再依次执行。
４、在每条编译命令后面加上 -j8 -j16 的命令对提高编译速度很有帮助，将会调用尽可能多的ＣＰＵ资源进行编译。
下面是编译命令：

``` python
make pycaffe
make all
make test
make runtest
```

## 测试
测试Caffe的Python接口，切换到caffe/python文件目录下，记录下来当前路径，输入以下命令：

``` python
export PYTHONPATH=/path/to/caffe/python:$PYTHONPATH
```

进入Python环境，输入

``` python
import caffe
```


若没有出现异常，就说明编译成功了。
如果没有报错，证明安装成功。

上面的方法，一旦关闭终端或者打开新终端则失效，如果放到配置文件中，可以永久有效果，命令操作如下：

``` python
#A.把环境变量路径放到 ~/.bashrc文件中  
sudo echo export PYTHONPATH="~/caffe/python" >> ~/.bashrc  
#B.使环境变量生效  
source ~/.bashrc 
```



非常感谢这位前辈的博文对配置环境的帮助

http://blog.csdn.net/muzilinxi90/article/details/53673184

github也有一篇文档很好，篇幅原因不再翻译，感兴趣的朋友可以参考一下。

https://github.com/BVLC/caffe/wiki/Ubuntu-16.04-or-15.10-Installation-Guide

import caffe 出现问题也可以参考这个网站：

http://www.linuxdiyf.com/linux/23093.html

caffe官网给出的教程，第一手的资料，建议阅读：

http://caffe.berkeleyvision.org/installation.html



基本上完成CPU only的caffe配置后，并且在不断摸索中，对linux系统和基本依赖包就已经很熟了。之后开始真正做项目需要用cuda，GPU的配置其实也很容易上手。

**另外我们发现，其实与其去看那么多的博客，不如自己去读英文的官方文件，或者github下下来后的readme文件，那才是最权威的第一手资料**




下为cuda官方文件的翻译

##NVIDIA CUDA Installation Guide for Linux
###Linux 系统下的NVIDIA CUDA 安装指南

http://blog.csdn.net/hhy_csdn/article/details/64440406

到了这里基本就结束了。


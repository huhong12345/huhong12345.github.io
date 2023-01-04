---
title: Linux常用命令
date: 2022-09-16 22:56:01
categories:
- 科研
- Linux
tags:
- 摘抄
- Linux
---
# 常用命令
## cd命令
这是一个非常基本，也是大家经常需要使用的命令，它用于切换当前目录，它的参数是要切换到的目录的路径，可以是绝对路径，也可以是相对路径。如：
``` bash
cd /root/Docements # 切换到目录/root/Docements
cd ./path          # 切换到当前目录下的path目录中，“.”表示当前目录  
cd ../path         # 切换到上层目录中的path目录中，“..”表示上一层目录
``` 

## ls命令
这是一个非常有用的查看文件与目录的命令，list之意，它的参数非常多，也可以组合使用，如下：
``` bash
-l #列出长数据串，包含文件的属性与权限数据等
-a #列出全部的文件，连同隐藏文件（开头为.的文件）一起列出来（常用）
-d #仅列出目录本身，而不是列出目录的文件数据
-h #将文件容量以较易读的方式（GB，kB等）列出来
-R #连同子目录的内容一起列出（递归列出），等于该目录下的所有文件都会显示出来
ls -l #以长数据串的形式列出当前目录下的数据文件和目录
ls -lR #以长数据串的形式列出当前目录下的所有文件
``` 
## grep命令
该命令常用于分析一行的信息，若当中有我们所需要的信息，就将该行显示出来，该命令通常与管道命令一起使用，用于对一些命令的输出进行筛选加工等等，它的简单语法为
``` bash
grep [-acinv] [--color=auto] '查找字符串' filename
``` 

它的常用参数为
``` bash
-a ：将binary文件以text文件的方式查找数据
-c ：计算找到‘查找字符串’的次数
-i ：忽略大小写的区别，即把大小写视为相同
-v ：反向选择，即显示出没有‘查找字符串’内容的那一行
# 例如：
# 取出文件/etc/man.config中包含MANPATH的行，并把找到的关键字加上颜色
grep --color=auto 'MANPATH' /etc/man.config
# 把ls -l的输出中包含字母file（不区分大小写）的内容输出
``` 

## find命令
find是一个基于查找的功能非常强大的命令，相对而言，它的使用也相对较为复杂，参数也比较多，所以在这里将给把它们分类列出，它的基本语法如下：
``` bash
find [PATH] [option] [action]

# 与时间有关的参数：
-mtime n : n为数字，意思为在n天之前的“一天内”被更改过的文件；
-mtime +n : 列出在n天之前（不含n天本身）被更改过的文件名；
-mtime -n : 列出在n天之内（含n天本身）被更改过的文件名；
-newer file : 列出比file还要新的文件名
# 例如：
find /root -mtime 0 # 在当前目录下查找今天之内有改动的文件

# 与用户或用户组名有关的参数：
-user name : 列出文件所有者为name的文件
-group name : 列出文件所属用户组为name的文件
-uid n : 列出文件所有者为用户ID为n的文件
-gid n : 列出文件所属用户组为用户组ID为n的文件
# 例如：
find /home/ljianhui -user ljianhui # 在目录/home/ljianhui中找出所有者为ljianhui的文件

# 与文件权限及名称有关的参数：
-name filename ：找出文件名为filename的文件
-size [+-]SIZE ：找出比SIZE还要大（+）或小（-）的文件
-tpye TYPE ：查找文件的类型为TYPE的文件，TYPE的值主要有：一般文件（f)、设备文件（b、c）、
             目录（d）、连接文件（l）、socket（s）、FIFO管道文件（p）；
-perm mode ：查找文件权限刚好等于mode的文件，mode用数字表示，如0755；
-perm -mode ：查找文件权限必须要全部包括mode权限的文件，mode用数字表示
-perm +mode ：查找文件权限包含任一mode的权限的文件，mode用数字表示
# 例如：
find / -name passwd # 查找文件名为passwd的文件
find . -perm 0755 # 查找当前目录中文件权限的0755的文件
find . -size +12k # 查找当前目录中大于12KB的文件，注意c表示byte
``` 
## cp命令
该命令用于复制文件，copy之意，它还可以把多个文件一次性地复制到一个目录下， 它的常用参数如下：
``` bash
-a ：将文件的特性一起复制
-p ：连同文件的属性一起复制，而非使用默认方式，与-a相似，常用于备份
-i ：若目标文件已经存在时，在覆盖时会先询问操作的进行
-r ：递归持续复制，用于目录的复制行为
-u ：目标文件与源文件有差异时才会复制
``` 
例如：
``` bash
cp -a file1 file2 #连同文件的所有特性把文件file1复制成文件file2
cp file1 file2 file3 dir #把文件file1、file2、file3复制到目录dir中
``` 
## mv命令
该命令用于移动文件、目录或更名，move之意，它的常用参数如下：
``` bash
-f ：force强制的意思，如果目标文件已经存在，不会询问而直接覆盖
-i ：若目标文件已经存在，就会询问是否覆盖
-u ：若目标文件已经存在，且比目标文件新，才会更新
``` 
注：该命令可以把一个文件或多个文件一次移动一个文件夹中，但是最后一个目标文件一定要是“目录”。例如：
``` bash
mv file1 file2 file3 dir # 把文件file1、file2、file3移动到目录dir中
mv file1 file2 # 把文件file1重命名为file2
``` 

## rm命令
该命令用于删除文件或目录，remove之间，它的常用参数如下：
``` bash
-f ：就是force的意思，忽略不存在的文件，不会出现警告消息
-i ：互动模式，在删除前会询问用户是否操作
-r ：递归删除，最常用于目录删除，它是一个非常危险的参数
``` 
例如：
``` bash 
rm -i file # 删除文件file，在删除之前会询问是否进行该操作
rm -fr dir # 强制删除目录dir中的所有文件
``` 
## ps命令
该命令用于将某个时间点的进程运行情况选取下来并输出，process之意，它的常用参数如下：
``` bash
-A ：所有的进程均显示出来
-a ：不与terminal有关的所有进程
-u ：有效用户的相关进程
-x ：一般与a参数一起使用，可列出较完整的信息
-l ：较长，较详细地将PID的信息列出
``` 
其实我们只要记住ps一般使用的命令参数搭配即可，它们并不多，如下：
``` bash
ps aux # 查看系统所有的进程数据
ps ax # 查看不与terminal有关的所有进程
ps -lA # 查看系统所有的进程数据
ps axjf # 查看连同一部分进程树状态
``` 
## kill命令
该命令用于向某个工作（%jobnumber）或者是某个PID（数字）传送一个信号，它通常与ps和jobs命令一起使用，它的基本语法如下：
``` bash
kill -signal PID
``` 
signal的常用参数如下：
注：最前面的数字为信号的代号，使用时可以用代号代替相应的信号。
``` bash
1：SIGHUP，启动被终止的进程
2：SIGINT，相当于输入ctrl+c，中断一个程序的进行
9：SIGKILL，强制中断一个进程的进行
15：SIGTERM，以正常的结束进程方式来终止进程
17：SIGSTOP，相当于输入ctrl+z，暂停一个进程的进行
``` 
例如：
``` bash
# 以正常的结束进程方式来终于第一个后台工作，可用jobs命令查看后台中的第一个工作进程
kill -SIGTERM %1 
# 重新改动进程ID为PID的进程，PID可用ps命令通过管道命令加上grep命令进行筛选获得
kill -SIGHUP PID
```
## killall命令
该命令用于向一个命令启动的进程发送一个信号，它的一般语法如下：
``` bash
killall [-iIe] [command name]
``` 
它的参数如下：
``` bash
-i ：交互式的意思，若需要删除时，会询问用户
-e ：表示后面接的command name要一致，但command name不能超过15个字符
-I ：命令名称忽略大小写
# 例如：
killall -SIGHUP syslogd # 重新启动syslogd
``` 
## file命令
该命令用于判断接在file命令后的文件的基本数据，因为在Linux下文件的类型并不是以后缀为分的，所以这个命令对我们来说就很有用了，它的用法非常简单，基本语法如下：
``` bash
file filename
#例如：
file ./test
``` 
## tar命令
该命令用于对文件进行打包，默认情况并不会压缩，如果指定了相应的参数，它还会调用相应的压缩程序（如gzip和bzip等）进行压缩和解压。它的常用参数如下：
``` bash
-c ：新建打包文件
-t ：查看打包文件的内容含有哪些文件名
-x ：解打包或解压缩的功能，可以搭配-C（大写）指定解压的目录，注意-c,-t,-x不能同时出现在同一条命令中
-j ：通过bzip2的支持进行压缩/解压缩
-z ：通过gzip的支持进行压缩/解压缩
-v ：在压缩/解压缩过程中，将正在处理的文件名显示出来
-f filename ：filename为要处理的文件
-C dir ：指定压缩/解压缩的目录dir
``` 
通常记住以下三条：
``` bash
压缩：tar -jcv -f filename.tar.bz2 要被处理的文件或目录名称
查询：tar -jtv -f filename.tar.bz2
解压：tar -jxv -f filename.tar.bz2 -C 欲解压缩的目录
``` 
注：文件名并不定要以后缀tar.bz2结尾，这里主要是为了说明使用的压缩程序为bzip2

## cat命令
该命令用于查看文本文件的内容，后接要查看的文件名，通常可用管道与more和less一起使用，从而可以一页页地查看数据。例如：
``` bash
cat text | less # 查看text文件中的内容
# 注：这条命令也可以使用less text来代替
``` 
## chgrp命令
该命令用于改变文件所属用户组，它的使用非常简单，它的基本用法如下：
``` bash
chgrp [-R] dirname/filename
-R ：进行递归的持续对所有文件和子目录更改
# 例如：
chgrp users -R ./dir # 递归地把dir目录下中的所有文件和子目录下所有文件的用户组修改为users
``` 
## chmod命令
该命令用于改变文件的权限，一般的用法如下：
``` bash
chmod [-R] xyz 文件或目录
-R：进行递归的持续更改，即连同子目录下的所有文件都会更改
``` 
同时，chmod还可以使用u（user）、g（group）、o（other）、a（all）和+（加入）、-（删除）、=（设置）跟rwx搭配来对文件的权限进行更改。
``` bash
# 例如：
chmod 0755 file # 把file的文件权限改变为-rxwr-xr-x
chmod g+w file # 向file的文件权限中加入用户组可写权限
``` 
## gcc命令
对于一个用Linux开发C程序的人来说，这个命令就非常重要了，它用于把C语言的源程序文件，编译成可执行程序，由于g++的很多参数跟它非常相似，所以这里只介绍gcc的参数，它的常用参数如下：
``` bash
-o ：output之意，用于指定生成一个可执行文件的文件名
-c ：用于把源文件生成目标文件（.o)，并阻止编译器创建一个完整的程序
-I ：增加编译时搜索头文件的路径
-L ：增加编译时搜索静态连接库的路径
-S ：把源文件生成汇编代码文件
-lm：表示标准库的目录中名为libm.a的函数库
-lpthread ：连接NPTL实现的线程库
-std= ：用于指定把使用的C语言的版本

# 例如：
# 把源文件test.c按照c99标准编译成可执行程序test
gcc -o test test.c -lm -std=c99
#把源文件test.c转换为相应的汇编程序源文件test.s
gcc -S test.c
``` 
## time命令
该命令用于测算一个命令（即程序）的执行时间。它的使用非常简单，就像平时输入命令一样，不过在命令的前面加入一个time即可，例如：
``` bash
time ./process
time ps aux
``` 
在程序或命令运行结束后，在最后输出了三个时间，它们分别是：

user：用户CPU时间，命令执行完成花费的用户CPU时间，即命令在用户态中执行时间总和；

system：系统CPU时间，命令执行完成花费的系统CPU时间，即命令在核心态中执行时间总和；

real：实际时间，从command命令行开始执行到运行终止的消逝时间；

注：用户CPU时间和系统CPU时间之和为CPU时间，即命令占用CPU执行的时间总和。实际时间要大于CPU时间，因为Linux是多任务操作系统，往往在执行一条命令时，系统还要处理其它任务。另一个需要注意的问题是即使每次执行相同命令，但所花费的时间也是不一样，其花费时间是与系统运行相关的。

# 详细命令
## 文件操作
### 切换、查看、删除、移动、链接
``` bash
cd /home 进入 '/ home' 目录
cd .. 返回上一级目录 
cd ../.. 返回上两级目录 
cd 进入个人的主目录 
cd ~user1 进入个人的主目录 
cd - 返回上次所在的目录 
pwd 显示工作路径 
ls 查看目录中的文件 
ls -F 查看目录中的文件 
ls -l 显示文件和目录的详细资料 
ls -a 显示隐藏文件 
ls *[0-9]* 显示包含数字的文件名和目录名 
tree 显示文件和目录由根目录开始的树形结构
lstree 显示文件和目录由根目录开始的树形结构
mkdir dir1 创建一个叫做 'dir1' 的目录
mkdir dir1 dir2 同时创建两个目录 
mkdir -p /tmp/dir1/dir2 创建一个目录树 
rm -f file1 删除一个叫做 'file1' 的文件
rmdir dir1 删除一个叫做 'dir1' 的目录
rm -rf dir1 删除一个叫做 'dir1' 的目录并同时删除其内容 
rm -rf dir1 dir2 同时删除两个目录及它们的内容 
mv dir1 new_dir 重命名/移动 一个目录 
cp file1 file2 复制一个文件 
cp dir/* . 复制一个目录下的所有文件到当前工作目录 
cp -a /tmp/dir1 . 复制一个目录到当前工作目录 
cp -a dir1 dir2 复制一个目录 
cp -r dir1 dir2 复制一个目录及子目录
ln -s file1 lnk1 创建一个指向文件或目录的软链接 
ln file1 lnk1 创建一个指向文件或目录的物理链接 
touch -t 0712250000 file1 修改一个文件或目录的时间戳 - (YYMMDDhhmm) 
file file1 outputs the mime type of the file as text 
iconv -l 列出已知的编码
``` 

### 文件授权
``` bash
文件的权限 —— 使用 "+" 设置权限，使用 "-" 用于取消 
ls -lh 显示权限 
ls /tmp | pr -T5 -W$COLUMNS 将终端划分成5栏显示 
chmod ugo+rwx directory1 设置目录的所有人(u)、群组(g)以及其他人(o)以读（r ）、写(w)和执行(x)的权限 
chmod go-rwx directory1 删除群组(g)与其他人(o)对目录的读写执行权限 
chown user1 file1 改变一个文件的所有人属性 
chown -R user1 directory1 改变一个目录的所有人属性并同时改变改目录下所有文件的属性 
chgrp group1 file1 改变文件的群组 
chown user1:group1 file1 改变一个文件的所有人和群组属性 
find / -perm -u+s 罗列一个系统中所有使用了SUID控制的文件 
chmod u+s /bin/file1 设置一个二进制文件的 SUID 位 - 运行该文件的用户也被赋予和所有者同样的权限 
chmod u-s /bin/file1 禁用一个二进制文件的 SUID位 
chmod g+s /home/public 设置一个目录的SGID 位 - 类似SUID ，不过这是针对目录的 
chmod g-s /home/public 禁用一个目录的 SGID 位 
chmod o+t /home/public 设置一个文件的 STIKY 位 - 只允许合法所有人删除文件 
chmod o-t /home/public 禁用一个目录的 STIKY 位 s
``` 


### chmod使用

``` bash
chmod [可选项] <mode> <file...>

可选项：
  -c, --changes          like verbose but report only when a change is made (若该档案权限确实已经更改，才显示其更改动作)
  -f, --silent, --quiet  suppress most error messages  （若该档案权限无法被更改也不要显示错误讯息）
  -v, --verbose          output a diagnostic for every file processed（显示权限变更的详细资料）
       --no-preserve-root  do not treat '/' specially (the default)
       --preserve-root    fail to operate recursively on '/'
       --reference=RFILE  use RFILEs mode instead of MODE values
  -R, --recursive        change files and directories recursively （以递归的方式对目前目录下的所有档案与子目录进行相同的权限变更)
       --help   显示此帮助信息
       --version    显示版本信息
mode ：权限设定字串，详细格式如下：
[ugoa...][[+-=][rwxX]...][,...]，其中
[ugoa...]
u 表示该档案的拥有者，g 表示与该档案的拥有者属于同一个群体(group)者，o 表示其他以外的人，a 表示所有（包含上面三者）。
[+-=]
+ 表示增加权限，- 表示取消权限，= 表示唯一设定权限。
[rwxX]
r 表示可读取，w 表示可写入，x 表示可执行，X 表示只有当该档案是个子目录或者该档案已经被设定过为可执行。
``` 



### 数字权限使用格式
在这种使用方式中，首先我们需要了解数字如何表示权限。 首先，我们规定 数字 4 、2 和 1表示读、写、执行权限（具体原因可见下节权限详解内容），即 r=4，w=2，x=1 。此时其他的权限组合也可以用其他的八进制数字表示出来，如： rwx = 4 + 2 + 1 = 7 rw = 4 + 2 = 6 rx = 4 +1 = 5 即

若要同时设置 rwx (可读写运行） 权限则将该权限位 设置 为 4 + 2 + 1 = 7 若要同时设置 rw- （可读写不可运行）权限则将该权限位 设置 为 4 + 2 = 6 若要同时设置 r-x （可读可运行不可写）权限则将该权限位 设置 为 4 +1 = 5

上面我们提到，每个文件都可以针对三个粒度，设置不同的rwx(读写执行)权限。即我们可以用用三个8进制数字分别表示 拥有者 、群组 、其它组( u、 g 、o)的权限详情，并用chmod直接加三个8进制数字的方式直接改变文件权限。

### 文件搜索
``` bash
find / -name file1 从 '/' 开始进入根文件系统搜索文件和目录 
find / -user user1 搜索属于用户 'user1' 的文件和目录 
find /home/user1 -name \*.bin 在目录 '/ home/user1' 中搜索带有'.bin' 结尾的文件 
find /usr/bin -type f -atime +100 搜索在过去100天内未被使用过的执行文件 
find /usr/bin -type f -mtime -10 搜索在10天内被创建或者修改过的文件 
find / -name \*.rpm -exec chmod 755 '{}' \; 搜索以 '.rpm' 结尾的文件并定义其权限 
find / -xdev -name \*.rpm 搜索以 '.rpm' 结尾的文件，忽略光驱、捷盘等可移动设备 
locate \*.ps 寻找以 '.ps' 结尾的文件 - 先运行 'updatedb' 命令 
whereis halt 显示一个二进制文件、源码或man的位置 
which halt 显示一个二进制文件或可执行文件的完整路径
``` 



### 文件特殊属性
``` bash
文件的特殊属性 - 使用 "+" 设置权限，使用 "-" 用于取消 
chattr +a file1 只允许以追加方式读写文件 
chattr +c file1 允许这个文件能被内核自动压缩/解压 
chattr +d file1 在进行文件系统备份时，dump程序将忽略这个文件 
chattr +i file1 设置成不可变的文件，不能被删除、修改、重命名或者链接 
chattr +s file1 允许一个文件被安全地删除 
chattr +S file1 一旦应用程序对这个文件执行了写操作，使系统立刻把修改的结果写到磁盘 
chattr +u file1 若文件被删除，系统会允许你在以后恢复这个被删除的文件 
lsattr 显示特殊的属性
``` 


### 文本处理
``` bash
cat file1 file2 ... | command <> file1_in.txt_or_file1_out.txt general syntax for text manipulation using PIPE, STDIN and STDOUT 
cat file1 | command( sed, grep, awk, grep, etc...) > result.txt 合并一个文件的详细说明文本，并将简介写入一个新文件中 
cat file1 | command( sed, grep, awk, grep, etc...) >> result.txt 合并一个文件的详细说明文本，并将简介写入一个已有的文件中 
grep Aug /var/log/messages 在文件 '/var/log/messages'中查找关键词"Aug" 
grep ^Aug /var/log/messages 在文件 '/var/log/messages'中查找以"Aug"开始的词汇 
grep [0-9] /var/log/messages 选择 '/var/log/messages' 文件中所有包含数字的行 
grep Aug -R /var/log/* 在目录 '/var/log' 及随后的目录中搜索字符串"Aug" 
sed 's/stringa1/stringa2/g' example.txt 将example.txt文件中的 "string1" 替换成 "string2" 
sed '/^$/d' example.txt 从example.txt文件中删除所有空白行 
sed '/ *#/d; /^$/d' example.txt 从example.txt文件中删除所有注释和空白行 
echo 'esempio' | tr '[:lower:]' '[:upper:]' 合并上下单元格内容 
sed -e '1d' result.txt 从文件example.txt 中排除第一行 
sed -n '/stringa1/p' 查看只包含词汇 "string1"的行 
sed -e 's/ *$//' example.txt 删除每一行最后的空白字符 
sed -e 's/stringa1//g' example.txt 从文档中只删除词汇 "string1" 并保留剩余全部 
sed -n '1,5p;5q' example.txt 查看从第一行到第5行内容 
sed -n '5p;5q' example.txt 查看第5行 
sed -e 's/00*/0/g' example.txt 用单个零替换多个零 
cat -n file1 标示文件的行数 
cat example.txt | awk 'NR%2==1' 删除example.txt文件中的所有偶数行 
echo a b c | awk '{print $1}' 查看一行第一栏 
echo a b c | awk '{print $1,$3}' 查看一行的第一和第三栏 
paste file1 file2 合并两个文件或两栏的内容 
paste -d '+' file1 file2 合并两个文件或两栏的内容，中间用"+"区分 
sort file1 file2 排序两个文件的内容 
sort file1 file2 | uniq 取出两个文件的并集(重复的行只保留一份) 
sort file1 file2 | uniq -u 删除交集，留下其他的行 
sort file1 file2 | uniq -d 取出两个文件的交集(只留下同时存在于两个文件中的文件) 
comm -1 file1 file2 比较两个文件的内容只删除 'file1' 所包含的内容 
comm -2 file1 file2 比较两个文件的内容只删除 'file2' 所包含的内容 
comm -3 file1 file2 比较两个文件的内容只删除两个文件共有的部分
``` 


### 字符设置和文件格式转换
``` bash
dos2unix filedos.txt fileunix.txt 将一个文本文件的格式从MSDOS转换成UNIX 
unix2dos fileunix.txt filedos.txt 将一个文本文件的格式从UNIX转换成MSDOS 
recode ..HTML < page.txt > page.html 将一个文本文件转换成html 
recode -l | more 显示所有允许的转换格式
``` 


### 文件系统分析
``` bash
badblocks -v /dev/hda1 检查磁盘hda1上的坏磁块 
fsck /dev/hda1 修复/检查hda1磁盘上linux文件系统的完整性 
fsck.ext2 /dev/hda1 修复/检查hda1磁盘上ext2文件系统的完整性 
e2fsck /dev/hda1 修复/检查hda1磁盘上ext2文件系统的完整性 
e2fsck -j /dev/hda1 修复/检查hda1磁盘上ext3文件系统的完整性 
fsck.ext3 /dev/hda1 修复/检查hda1磁盘上ext3文件系统的完整性 
fsck.vfat /dev/hda1 修复/检查hda1磁盘上fat文件系统的完整性 
fsck.msdos /dev/hda1 修复/检查hda1磁盘上dos文件系统的完整性 
dosfsck /dev/hda1 修复/检查hda1磁盘上dos文件系统的完整性
``` 



### 挂载一个文件系统
``` bash
mount /dev/hda2 /mnt/hda2 挂载一个叫做hda2的盘 - 确定目录 '/ mnt/hda2' 已经存在 
umount /dev/hda2 卸载一个叫做hda2的盘 - 先从挂载点 '/ mnt/hda2' 退出 
fuser -km /mnt/hda2 当设备繁忙时强制卸载 
umount -n /mnt/hda2 运行卸载操作而不写入 /etc/mtab 文件- 当文件为只读或当磁盘写满时非常有用 
mount /dev/fd0 /mnt/floppy 挂载一个软盘 
mount /dev/cdrom /mnt/cdrom 挂载一个cdrom或dvdrom 
mount /dev/hdc /mnt/cdrecorder 挂载一个cdrw或dvdrom 
mount /dev/hdb /mnt/cdrecorder 挂载一个cdrw或dvdrom 
mount -o loop file.iso /mnt/cdrom 挂载一个文件或ISO镜像文件 
mount -t vfat /dev/hda5 /mnt/hda5 挂载一个Windows FAT32文件系统 
mount /dev/sda1 /mnt/usbdisk 挂载一个usb 捷盘或闪存设备 
mount -t smbfs -o username=user,password=pass //WinClient/share /mnt/share 挂载一个windows网络共享
``` 

### 初始化一个文件系统
``` bash
mkfs /dev/hda1 在hda1分区创建一个文件系统 
mke2fs /dev/hda1 在hda1分区创建一个linux ext2的文件系统 
mke2fs -j /dev/hda1 在hda1分区创建一个linux ext3(日志型)的文件系统 
mkfs -t vfat 32 -F /dev/hda1 创建一个 FAT32 文件系统 
fdformat -n /dev/fd0 格式化一个软盘 
mkswap /dev/hda3 创建一个swap文件系统
``` 

### SWAP文件系统
``` bash
mkswap /dev/hda3 创建一个swap文件系统 
swapon /dev/hda3 启用一个新的swap文件系统 
swapon /dev/hda2 /dev/hdb3 启用两个swap分区
``` 

### 备份
``` bash
dump -0aj -f /tmp/home0.bak /home 制作一个 '/home' 目录的完整备份 
dump -1aj -f /tmp/home0.bak /home 制作一个 '/home' 目录的交互式备份 
restore -if /tmp/home0.bak 还原一个交互式备份 
rsync -rogpav --delete /home /tmp 同步两边的目录 
rsync -rogpav -e ssh --delete /home ip_address:/tmp 通过SSH通道rsync 
rsync -az -e ssh --delete ip_addr:/home/public /home/local 通过ssh和压缩将一个远程目录同步到本地目录 
rsync -az -e ssh --delete /home/local ip_addr:/home/public 通过ssh和压缩将本地目录同步到远程目录 
dd bs=1M if=/dev/hda | gzip | ssh user@ip_addr 'dd of=hda.gz' 通过ssh在远程主机上执行一次备份本地磁盘的操作 
dd if=/dev/sda of=/tmp/file1 备份磁盘内容到一个文件 
tar -Puf backup.tar /home/user 执行一次对 '/home/user' 目录的交互式备份操作 
( cd /tmp/local/ && tar c . ) | ssh -C user@ip_addr 'cd /home/share/ && tar x -p' 通过ssh在远程目录中复制一个目录内容 
( tar c /home ) | ssh -C user@ip_addr 'cd /home/backup-home && tar x -p' 通过ssh在远程目录中复制一个本地目录 
tar cf - . | (cd /tmp/backup ; tar xf - ) 本地将一个目录复制到另一个地方，保留原有权限及链接 
find /home/user1 -name '*.txt' | xargs cp -av --target-directory=/home/backup/ --parents 从一个目录查找并复制所有以 '.txt' 结尾的文件到另一个目录 
find /var/log -name '*.log' | tar cv --files-from=- | bzip2 > log.tar.bz2 查找所有以 '.log' 结尾的文件并做成一个bzip包 
dd if=/dev/hda of=/dev/fd0 bs=512 count=1 做一个将 MBR (Master Boot Record)内容复制到软盘的动作 
dd if=/dev/fd0 of=/dev/hda bs=512 count=1 从已经保存到软盘的备份中恢复MBR内容
``` 
## 系统操作
### 系统信息
``` bash
arch 显示机器的处理器架构
uname -m 显示机器的处理器架构
uname -r 显示正在使用的内核版本 
dmidecode -q 显示硬件系统部件 - (SMBIOS / DMI) 
hdparm -i /dev/hda 罗列一个磁盘的架构特性 
hdparm -tT /dev/sda 在磁盘上执行测试性读取操作 
cat /proc/cpuinfo 显示CPU info的信息 
cat /proc/interrupts 显示中断 
cat /proc/meminfo 校验内存使用 
cat /proc/swaps 显示哪些swap被使用 
cat /proc/version 显示内核的版本 
cat /proc/net/dev 显示网络适配器及统计 
cat /proc/mounts 显示已加载的文件系统 
lspci -tv 罗列 PCI 设备 
lsusb -tv 显示 USB 设备 
date 显示系统日期 
cal 2007 显示2007年的日历表 
date 041217002007.00 设置日期和时间 - 月日时分年.秒 
clock -w 将时间修改保存到 BIOS
``` 

### 用户和群组
``` bash
groupadd group_name 创建一个新用户组 
groupdel group_name 删除一个用户组 
groupmod -n new_group_name old_group_name 重命名一个用户组 
useradd -c "Name Surname " -g admin -d /home/user1 -s /bin/bash user1 创建一个属于 "admin" 用户组的用户 
useradd user1 创建一个新用户 
userdel -r user1 删除一个用户 ( '-r' 排除主目录) 
usermod -c "User FTP" -g system -d /ftp/user1 -s /bin/nologin user1 修改用户属性 
passwd 修改口令 
passwd user1 修改一个用户的口令 (只允许root执行) 
chage -E 2005-12-31 user1 设置用户口令的失效期限 
pwck 检查 '/etc/passwd' 的文件格式和语法修正以及存在的用户 
grpck 检查 '/etc/passwd' 的文件格式和语法修正以及存在的群组 
newgrp group_name 登陆进一个新的群组以改变新创建文件的预设群组
``` 

### 磁盘空间
``` bash
磁盘空间 
df -h 显示已经挂载的分区列表 
ls -lSr |more 以尺寸大小排列文件和目录 
du -sh dir1 估算目录 'dir1' 已经使用的磁盘空间' 
du -sk * | sort -rn 以容量大小为依据依次显示文件和目录的大小 
rpm -q -a --qf '%10{SIZE}t%{NAME}n' | sort -k1,1n 以大小为依据依次显示已安装的rpm包所使用的空间 (fedora, redhat类系统) 
dpkg-query -W -f='${Installed-Size;10}t${Package}n' | sort -k1,1n 以大小为依据显示已安装的deb包所使用的空间 (ubuntu, debian类系统)
``` 

### 关机、重启、登出
``` bash
shutdown -h now 关闭系统
init 0 关闭系统
telinit 0 关闭系统
shutdown -h hours:minutes & 按预定时间关闭系统 
shutdown -c 取消按预定时间关闭系统 
shutdown -r now 重启
reboot 重启
logout 注销
``` 
### yum 软件包
``` bash
YUM 软件包升级器 - （Fedora, RedHat及类似系统） 
yum install package_name 下载并安装一个rpm包 
yum localinstall package_name.rpm 将安装一个rpm包，使用你自己的软件仓库为你解决所有依赖关系 
yum update package_name.rpm 更新当前系统中所有安装的rpm包 
yum update package_name 更新一个rpm包 
yum remove package_name 删除一个rpm包 
yum list 列出当前系统中安装的所有包 
yum search package_name 在rpm仓库中搜寻软件包 
yum clean packages 清理rpm缓存删除下载的包 
yum clean headers 删除所有头文件 
yum clean all 删除所有缓存的包和头文件
``` 
### DEB包 dpkg
``` bash
DEB 包 (Debian, Ubuntu 以及类似系统) 
dpkg -i package.deb 安装/更新一个 deb 包 
dpkg -r package_name 从系统删除一个 deb 包 
dpkg -l 显示系统中所有已经安装的 deb 包 
dpkg -l | grep httpd 显示所有名称中包含 "httpd" 字样的deb包 
dpkg -s package_name 获得已经安装在系统中一个特殊包的信息 
dpkg -L package_name 显示系统中已经安装的一个deb包所提供的文件列表 
dpkg --contents package.deb 显示尚未安装的一个包所提供的文件列表 
dpkg -S /bin/ping 确认所给的文件由哪个deb包提供
``` 
### apt软件包
``` bash
APT 软件工具 (Debian, Ubuntu 以及类似系统) 
apt-get install package_name 安装/更新一个 deb 包 
apt-cdrom install package_name 从光盘安装/更新一个 deb 包 
apt-get update 升级列表中的软件包 
apt-get upgrade 升级所有已安装的软件 
apt-get remove package_name 从系统删除一个deb包 
apt-get check 确认依赖的软件仓库正确 
apt-get clean 从下载的软件包中清理缓存 
apt-cache search searched-package 返回包含所要搜索字符串的软件包名称
``` 

## 系统进程
### linux查看端口占用
``` bash
# 查看端口进程
netstat -tunlp | grep 端口号
# 查看端口占用
lsof -i:端口号
# 查看TCP的listen的端口
ss -tln 
# 查看哪些进程使用了监听端口
ss -tlnp
``` 
### ps命令
``` bash
ps命令常用用法（方便查看系统进程）

ps a 显示现行终端机下的所有程序，包括其他用户的程序。
ps -A 显示所有进程。
ps c 列出程序时，显示每个程序真正的指令名称，而不包含路径，参数或常驻服务的标示。
ps -e 此参数的效果和指定"A"参数相同。
ps e 列出程序时，显示每个程序所使用的环境变量。
ps f 用ASCII字符显示树状结构，表达程序间的相互关系。
ps -H 显示树状结构，表示程序间的相互关系。
ps -N 显示所有的程序，除了执行ps指令终端机下的程序之外。
ps s 采用程序信号的格式显示程序状况。
ps S 列出程序时，包括已中断的子程序资料。
ps -t<终端机编号> 　指定终端机编号，并列出属于该终端机的程序的状况。
ps u 　以用户为主的格式来显示程序状况。
ps x 　显示所有程序，不以终端机来区分。
``` 
常用指令组合 ：ps aux,然后再通过管道使用grep命令过滤查找特定的进程,然后再对特定的进程进行操作。
``` bash
ps aux | grep program_filter_word,ps -ef |grep tomcat
ps -ef|grep java|grep -v grep 显示出所有的java进程，去处掉当前的grep进程。
``` 

## 网络
### ifconfig命令
``` bash
#作用：
ifconfig命令用于显示或设置网络设备。
#说明： 
与windows下的ipconfig命令类似,linux下使用ifconfig命令查看
#格式
ifconfig [网络设备][down up -allmulti -arp -promisc][add<地址>][del<地址>][<hw<网络设备类型><硬件地址>][io_addr<I/O地址>][irq<IRQ地址>][media<网络媒介类型>][mem_start<内存地址>][metric<数目>][mtu<字节>][netmask<子网掩码>][tunnel<地址>][-broadcast<地址>][-pointopoint<地址>][IP地址]

#参数
add<地址> 设置网络设备IPv6的IP地址。
del<地址> 删除网络设备IPv6的IP地址。
down 关闭指定的网络设备。
<hw<网络设备类型><硬件地址> 设置网络设备的类型与硬件地址。
io_addr<I/O地址> 设置网络设备的I/O地址。
irq<IRQ地址> 设置网络设备的IRQ。
media<网络媒介类型> 设置网络设备的媒介类型。
mem_start<内存地址> 设置网络设备在主内存所占用的起始地址。
metric<数目> 指定在计算数据包的转送次数时，所要加上的数目。
mtu<字节> 设置网络设备的MTU。
netmask<子网掩码> 设置网络设备的子网掩码。
tunnel<地址> 建立IPv4与IPv6之间的隧道通信地址。
up 启动指定的网络设备。
-broadcast<地址> 将要送往指定地址的数据包当成广播数据包来处理。
-pointopoint<地址> 与指定地址的网络设备建立直接连线，此模式具有保密功能。
-promisc 关闭或启动指定网络设备的promiscuous模式。
[IP地址] 指定网络设备的IP地址。
[网络设备] 指定网络设备的名称。

#实例
显示网络设备信息

# ifconfig        
eth0   Link encap:Ethernet HWaddr 00:50:56:0A:0B:0C 
     inet addr:192.168.0.3 Bcast:192.168.0.255 Mask:255.255.255.0
     inet6 addr: fe80::250:56ff:fe0a:b0c/64 Scope:Link
     UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
     RX packets:172220 errors:0 dropped:0 overruns:0 frame:0
     TX packets:132379 errors:0 dropped:0 overruns:0 carrier:0
     collisions:0 txqueuelen:1000 
     RX bytes:87101880 (83.0 MiB) TX bytes:41576123 (39.6 MiB)
     Interrupt:185 Base address:0x2024 

lo    Link encap:Local Loopback 
     inet addr:127.0.0.1 Mask:255.0.0.0
     inet6 addr: ::1/128 Scope:Host
     UP LOOPBACK RUNNING MTU:16436 Metric:1
     RX packets:2022 errors:0 dropped:0 overruns:0 frame:0
     TX packets:2022 errors:0 dropped:0 overruns:0 carrier:0
     collisions:0 txqueuelen:0 
     RX bytes:2459063 (2.3 MiB) TX bytes:2459063 (2.3 MiB)
启动关闭指定网卡

# ifconfig eth0 down
# ifconfig eth0 up
为网卡配置和删除IPv6地址

# ifconfig eth0 add 33ffe:3240:800:1005::2/ 64 //为网卡诶之IPv6地址

# ifconfig eth0 del 33ffe:3240:800:1005::2/ 64 //为网卡删除IPv6地址
用ifconfig修改MAC地址

# ifconfig eth0 down //关闭网卡
# ifconfig eth0 hw ether 00:AA:BB:CC:DD:EE //修改MAC地址
# ifconfig eth0 up //启动网卡
# ifconfig eth1 hw ether 00:1D:1C:1D:1E //关闭网卡并修改MAC地址 
# ifconfig eth1 up //启动网卡
配置IP地址

# ifconfig eth0 192.168.1.56 
//给eth0网卡配置IP地址
# ifconfig eth0 192.168.1.56 netmask 255.255.255.0 
// 给eth0网卡配置IP地址,并加上子掩码
# ifconfig eth0 192.168.1.56 netmask 255.255.255.0 broadcast 192.168.1.255
// 给eth0网卡配置IP地址,加上子掩码,加上个广播地址
启用和关闭ARP协议

# ifconfig eth0 arp  //开启
# ifconfig eth0 -arp  //关闭
设置最大传输单元

# ifconfig eth0 mtu 1500 
//设置能通过的最大数据包大小为 1500 bytes
```


### ping命令
``` bash
#作用
用于检测主机。若远端主机的网络功能没有问题，就会回应该信息，因而得知该主机运作正常。
#格式
ping [-dfnqrRv][-c<完成次数>][-i<间隔秒数>][-I<网络界面>][-l<前置载入>][-p<范本样式>][-s<数据包大小>][-t<存活数值>][主机名称或IP地址]
#参数
-d 使用Socket的SO_DEBUG功能。
-c<完成次数> 设置完成要求回应的次数。
-f 极限检测。
-i<间隔秒数> 指定收发信息的间隔时间。
-I<网络界面> 使用指定的网络界面送出数据包。
-l<前置载入> 设置在送出要求信息之前，先行发出的数据包。
-n 只输出数值。
-p<范本样式> 设置填满数据包的范本样式。
-q 不显示指令执行过程，开头和结尾的相关信息除外。
-r 忽略普通的Routing Table，直接将数据包送到远端主机上。
-R 记录路由过程。
-s<数据包大小> 设置数据包的大小。
-t<存活数值> 设置存活数值TTL的大小。
-v 详细显示指令的执行过程。
#实例
检测是否与主机连通
ping www.baidu.com
//需要终止按ctrl +c
指定接收包的次数
ping -c 2 www.baidu.com
//收到两次包后，自动退出
``` 
### nslookup命令
``` bash
#作用：
查看dns信息用的，linux系统不自带，需要手动安装
如果你的Linux系统没有nslookup命令，那么八成是你没有安装bind-utils包。
直接yum install bind-utils就可以解决问题了。

#格式：
        进入非交互模式       nslookup 域名（www.baidu.com）
非交互模式nslookup会连接到默认的域名服务器
（即/etc/resolv.conf的第一个dns地#址）。
        进入交互模式         nslookup

#交互模式常用命令：
exit        退出交互模式
set all 列出nslookup工具常用选项设置值

#返回值说明
返回值一共分为两部分，第一部分是本机的DNS信息，包括服务器和地址

第二部分非权威应答对应的英文是：Non-authoritative answer。什么叫非权威应答？假设某个DNS server没有域名test.com的记录信息，当有客户端通过它请求获取test.com的域名信息，此DNS Server会通过迭代递归的方式从test公司实际存储此记录信息的DNS server中获取test.com的域名信息，反馈给发出请求的客户端，同时会把test.com的记录信息放在自身缓存中放置一段时间，当又有客户端请求test.com域名解析时，此DNS server直接从自身缓存中提取返回给客户端，这个回答叫“非权威回答”，简言之凡是从非实际记录存储DNS server中获取的域名解析回答，都叫“非权威回答”。

[root@localhost ~]# nslookup www.baidu.com
Server:     114.114.114.114
Address:    114.114.114.114#53

Non-authoritative answer:
www.baidu.com   canonical name = www.a.shifen.com.
Name:   www.a.shifen.com
Address: 61.135.169.121
Name:   www.a.shifen.com
Address: 61.135.169.125

#www.a.shifen.com.指代www.baidu.com对应的dns主机名记录
``` 
### traceroute
``` bash
#作用：
显示数据包到主机间的路径。
对应window下的tracert命令

#格式： 
Traceroute [options] <IP-address or domain-name> [data size]

#参数
  -d   使用Socket层级的排错功能。
  -f<存活数值>   设置第一个检测数据包的存活数值TTL的大小。
  -F   设置勿离断位。
  -g<网关>   设置来源路由网关，最多可设置8个。
  -i<网络界面>   使用指定的网络界面送出数据包。
  -I   使用ICMP回应取代UDP资料信息。
  -m<存活数值>   设置检测数据包的最大存活数值TTL的大小。
  -n   直接使用IP地址而非主机名称。
  -p<通信端口>   设置UDP传输协议的通信端口。(缺省为33434)

  -q  设置TTL测试数目(缺省为3)
  -r   忽略普通的Routing Table，直接将数据包送到远端主机上。
  -s<来源地址>   设置本地主机送出数据包的IP地址。
  -t<服务类型>   设置检测数据包的TOS数值。
  -v   详细显示指令的执行过程。
  -w<超时秒数>   设置等待远端主机回报的时间。
  -x   开启或关闭数据包的正确性检验。  
[data size]:每次测试包的数据字节长度(缺省为38)
#返回值说明
显示到达目的地的数据包路由
[root@localhost ~]# traceroute www.baidu.com
traceroute to www.baidu.com (61.135.169.125), 30 hops max, 60 byte packets
 1  10.20.35.254 (10.20.35.254)  0.626 ms  1.205 ms  1.476 ms
 2  10.20.0.1 (10.20.0.1)  0.365 ms  0.453 ms  0.463 ms
 3  124.160.189.213 (124.160.189.213)  2.377 ms  2.226 ms  2.250 ms
 4  124.160.188.101 (124.160.188.101)  2.253 ms 124.160.188.105 (124.160.188.105)  2.396 ms  2.518 ms
 5  124.160.189.89 (124.160.189.89)  8.592 ms 124.160.189.97 (124.160.189.97)  11.756 ms 124.160.189.105 (124.160.189.105)  7.020 ms
 6  219.158.96.133 (219.158.96.133)  28.295 ms  27.595 ms 219.158.96.129 (219.158.96.129)  27.675 ms
 7  202.96.12.114 (202.96.12.114)  29.006 ms  28.724 ms 124.65.194.154 (124.65.194.154)  30.519 ms
 8  61.148.155.50 (61.148.155.50)  31.042 ms 124.65.58.198 (124.65.58.198)  28.132 ms 124.65.58.54 (124.65.58.54)  27.523 ms
 9  202.106.48.18 (202.106.48.18)  27.811 ms 123.125.248.102 (123.125.248.102)  26.961 ms 123.125.248.46 (123.125.248.46)  50.428 ms
``` 

## 其他
### 打包和压缩文件
``` bash
bunzip2 file1.bz2 解压一个叫做 'file1.bz2'的文件 
bzip2 file1 压缩一个叫做 'file1' 的文件 
gunzip file1.gz 解压一个叫做 'file1.gz'的文件 
gzip file1 压缩一个叫做 'file1'的文件 
gzip -9 file1 最大程度压缩 
rar a file1.rar test_file 创建一个叫做 'file1.rar' 的包 
rar a file1.rar file1 file2 dir1 同时压缩 'file1', 'file2' 以及目录 'dir1' 
rar x file1.rar 解压rar包 
unrar x file1.rar 解压rar包 
tar -cvf archive.tar file1 创建一个非压缩的 tarball 
tar -cvf archive.tar file1 file2 dir1 创建一个包含了 'file1', 'file2' 以及 'dir1'的档案文件 
tar -tf archive.tar 显示一个包中的内容 
tar -xvf archive.tar 释放一个包 
tar -xvf archive.tar -C /tmp 将压缩包释放到 /tmp目录下 
tar -cvfj archive.tar.bz2 dir1 创建一个bzip2格式的压缩包 
tar -jxvf archive.tar.bz2 解压一个bzip2格式的压缩包 
tar -cvfz archive.tar.gz dir1 创建一个gzip格式的压缩包 
tar -zxvf archive.tar.gz 解压一个gzip格式的压缩包 
zip file1.zip file1 创建一个zip格式的压缩包 
zip -r file1.zip file1 file2 dir1 将几个文件和目录同时压缩成一个zip格式的压缩包 
unzip file1.zip 解压一个zip格式压缩包
``` 


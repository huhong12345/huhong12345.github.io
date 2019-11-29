---
title: Python is For Fun
Date: 2019-11-29 21:55:33
categories:
- 编程
- Python
tags:
- Python
- 编程
- 练习
- DL

---

# Read after me, Python is for Fun!   :)


**简单的人名对话**

``` py
name = input("输入姓名:")
print("%s 同学，学好Python，前途无量！"%name)
print("%s 大侠，学好Python，大展拳脚！"%name[0])
print("%s 哥哥，学好Python，人见人爱！"%name[1:])
```

输入长者后，依次回显示江大侠和民哥哥
{% img [class names] /image/a.png %}

**九九乘法表输出**

``` py
for i in range(1,10):
    for j in range(1,i+1):
        print("{}*{}={:2} ".format(j,i,i*j), end='')
    print('')
```

**绘制太阳花**
``` py
from turtle import *
color('red', 'yellow')
begin_fill()
while True:
    forward(200)
    left(170)
    if abs(pos()) < 1:
       break
end_fill()
done()
```
结果为

{% img [class names] /image/b.png %}

**再来画个大蟒蛇吧:**

``` py
#e2.2DrawPython.py
from turtle import *
setup(650, 350, 200, 200)
penup()
fd(-250)
pendown()
pensize(25)
pencolor("purple")
seth(-40)
for i in range(4):
    circle(40, 80)
    circle(-40, 80)
circle(40, 80/2)
fd(40)
circle(16, 180)
fd(40 * 2/3)

```
然后画出个大蟒蛇。。。。
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMTcwNzI3Mzg1?x-oss-process=image/format,png)

贴一段这样的代码：（表示华氏度和摄氏度的转换），很有参考意义

``` py
#e1.1TempConvert.py
TempStr = input("请输入带有符号的温度值: ")
if TempStr[-1] in ['F','f']:
    C = (eval(TempStr[0:-1]) - 32)/1.8
    print("转换后的温度是{:.2f}C".format(C))
elif TempStr[-1] in ['C','c']:
    F = 1.8*eval(TempStr[0:-1]) + 32
    print("转换后的温度是{:.2f}F".format(F))
else:
    print("输入格式错误")
```
**对于注释而言，**
``` py
#可以表示单行注释
print(pow(2,10))#也可以这样注释
'''
fneifi
feisf
fneisn
'''       这样中间就全是注释了
```
**对于python的字符串而言**

``` py
>>> aaa="110C"
>>> print(aaa[-1])
C
>>> print(aaa[1])
1
>>> print(aaa[0:-1])
110
>>> print(aaa[0])
1
>>> aaa="123456789C"
>>> print(aaa[0])
1
>>> print(aaa[1])
2
>>> print(aaa[5])
6
>>> print(aaa[-1])
C
>>> print(aaa[9])
C
>>> print(aaa[0:-1])
123456789
>>> print(aaa[0:5])
12345
```
应该还是很容易看懂我是什么意思吧，[0：-1]表示从第一个字符到最后一个（不包括最后一个）

**对输入：**

``` py
TempStr=input("请输入带有符号的温度值：")
```
也是很有参考意义的

**对分支:**

``` py
if TempStr[-1] in ['F','f']:
elif TempStr[-1] in ['C','c']:
```
查找最后一个字符

**另外，eval函数表示已python表达式的方式去解释并执行字符串**

最后，该程序还能转化为函数形式：
 
``` py
#*******************************e1.3TempConvert.py***********************************************
def tempConvert(ValueStr):
    if ValueStr[-1] in ['F','f']:
        C = (eval(ValueStr[0:-1]) - 32)/1.8
        print("转换后的温度是{:.2f}C".format(C))
    elif ValueStr[-1] in ['C','c']:
        F = 1.8*eval(ValueStr[0:-1]) + 32
        print("转换后的温度是{:.2f}F".format(F))
    else:
        print("输入格式错误")
TempStr = input("请输入带有符号的温度值: ")
tempConvert(TempStr)
```
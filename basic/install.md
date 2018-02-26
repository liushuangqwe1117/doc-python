## python3安装与运行

### 下载python安装包
---
1. 访问地址：https://www.python.org/downloads/
2. 选择windows系统进入下载页面
3. 现在用户一般使用的是window-x64的的操作系统，所以选择“Windows x86-64 executable installer”进行下载，下载完成后的文件名为“python-3.6.4-amd64.exe”

### 安装python
---
1. 点击“python-3.6.4-amd64.exe”进行安装

### 安装环境变量
---
1. 添加python的安装目录到path中
` PATH=PATH;D:\soft\Python\Python36;D:\soft\Python\Python36\Scripts;`
2. 进入cmd窗口，输入python命令，会输出如下信息：
```
C:\Users\LS>python
Python 3.6.4 (v3.6.4:d48eceb, Dec 19 2017, 06:54:40) [MSC v.1900 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>exit()
```
exit()：退出命令行  
在Windows上运行Python时，启动命令行，然后运行python
在Mac和Linux上运行Python时，打开终端，然后运行python3

### python编辑器
---

#### IDLE编译器运行

1. 打开python自带的编辑器“IDLE”
![](images/idle.png)
2. 至此就可以进行python开发了
3. 在">>>"提示符下只能执行单行语句
4. 选择"File>new file"打开一个新的文件，就可以进行多行语句开发.写完语句后选择"Run>Run Module"执行语句

#### 运行python文件
在Windows上执行：`C:\work>python calc.py`  
在Mac和Linux上执行：`[root@root home]# python3 calc.py`

#### 直接运行python文件
&emsp;&emsp;有同学问，能不能像.exe文件那样直接运行.py文件呢？在Windows上是不行的，但是，在Mac和Linux上是可以的方法是在.py文件的第一行加上一个特殊的注释：
```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

print('hello, world')
```
然后，通过命令给hello.py以执行权限：
```
$ chmod a+x hello.py
```
就可以直接运行hello.py了
```
[root@root home]# ./hello.py
hello,world
```

扩展知识：  
`# -*- coding: utf-8 -*-`的作用：  
Python 作为高级语言的一种，不可避免的会接触到各种各样的编码，为了避免因为编码产生的问题，最好对源码设置统一编码。
只要满足正则表示`coding[:=]\s*([-\w.]+)`都可以，所以如下的编码设置方式效果是相同的：
```
# -*- coding: utf-8 -*- 推荐是用此种方式，符合Emacs(著名的集成开发环境和文本编辑器)风格
#coding=utf8
# encoding: utf-8
```

## python模块
---
### 什么是模块
- 模块是按照需求类别将一些常见的功能（函数）组合在一起。模块中的函数叫做模块的方法
- 系统中自带的模块在安装目录的Lib目录或Lib/site-packages目录下
- 第三方模块
- 自定义模块

### 模块导入
import 模块名
```
import cgi
cgi.print_environ()
```
from 模块名 import 方法名
```
from cgi import print_environ
print_environ()
```

### 第三方模块安装
1. pip方式安装(也称网络安装，要求网络良好)

  进入cmd窗口

  pip install 模块名

  `pip install scrapy`

2. whl下载安装的方式

  一般都是在“LFD python”中去查找
  https://www.lfd.uci.edu/~gohlke/pythonlibs/

  下载对应操作系统版本的文件，例如：ad3-2.1-cp36-cp36m-win_amd64.whl

  ```
  C:\Users\LS\Desktop>pip install ad3-2.1-cp36-cp36m-win_amd64.whl
    Processing c:\users\ls\desktop\ad3-2.1-cp36-cp36m-win_amd64.whl
    Installing collected packages: ad3
    Successfully installed ad3-2.1
  ```
3. 直接复制的方式

  直接从已经安装模块电脑中拷贝到自己电脑上，并放到Lib目录下

4. anaconda方式安装


### 自定义模块
1. 直接将自己编写的python文件放到python安装目录的Lib下，就可以作为模块被调用

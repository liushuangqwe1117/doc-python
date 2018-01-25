## 正则表达式
---

### 原子
> 原子是正则表达式中最基本的组成单位，每个正则表达式中至少要包含一个原子。常见的原子类型有：

1. 普通字符作为原子
2. 非打印字符作为原子
3. 通用字符作为原子
4. 原子表

```
#导入正则模块
import re
#普通字符作为原子
str="taoyunjiaoyu"
reg="yun"
rst=re.search(reg,str)
print(rst)

#非打印字符作为原子
#\n : 换行符号
#\t : 制表符
str='''baidu.com
qq.com
'''
reg="\n"
rst=re.search(reg,str)
print(rst)

#通用字符作为原子
'''
\w : 字母、数字、下划线
\W : 除了字母、数字、下划线的字符
\d : 十进制数字
\D : 除了十进制数字
\s : 空白字符
\S : 除了空白字符
'''
str="abcd1 234def"
reg="\w\d\s\d"
rst=re.search(reg,str)
print(rst)

#原子表:[]
str="abcd1 234def"
reg="ab[ckg]"
reg2="ab[^ckg]"
rst=re.search(reg2,str)
print(rst)
```

### 元字符
> 元字符就是正则表达式中具有一些特殊含义的字符，比如重复N次前面的字符等

```
#导入正则模块
import re
#元字符
'''
. : 除换行外的任意一个字符
^ ：在原子表中表示非，不在原子表中则表示开始位置
$ : 结束位置
* ：出现0次、1次、多次
？：出现0次、1次
+ : 出现1次、多次
{n}:只出现n次
{n,}:至少出现n次
{n,m}:至少出现n此，至多出现m次
| : 模式选择符或
(): 模式单元
'''

str="taoooyunjiaoyu"
reg="^tao.*"
reg="^tao+"
reg="^tao{1,3}"
rst=re.search(reg,str)
print(rst)
```

### 模式修饰符
> 模式修饰符是在不改变正则表达式的情况下，通过模式修正符改变正则表达式的含义，从而实现一些匹配结果的调整等功能

```
#导入正则模块
import re
#模式修正符
'''
I : 匹配时忽略大小写，默认不忽略大小写
M : 多行匹配
L :(L)本地化识别匹配
U : unicode
S : 让.匹配包括换行符
'''

str="Python"
reg="pyt"
rst=re.search(reg,str,re.I)
print(rst)
```

### 贪婪模式与懒惰模式
> 贪婪模式就是尽可能多的匹配，懒惰模式就是尽可能少的匹配

```
#导入正则模块
import re
#贪婪模式与懒惰模式
str="poythonyabc"
reg="p.*y" #贪婪模式
reg2="p.*?y" #懒惰模式,加一个？表示懒惰模式匹配，懒惰模式相对精准
rst=re.search(reg,str,re.I)
rst2=re.search(reg2,str,re.I)
print(rst)
print(rst2)
```

### 正则表达式函数
> 正则表达式函数有re.match()函数,re.search()函数,全局匹配函数,re.sub()函数

```
#导入正则模块
import re
#正则表达式函数
#match只能从头开始配
#search可以从任意地方开始匹配

str="poythonyabc"
reg1="p.*?y"
reg2="o.*?y"
rst=re.match(reg1,str,re.I)
rst2=re.search(reg1,str,re.I)
print(rst)
print(rst2)

rst=re.match(reg2,str,re.I)
rst2=re.search(reg2,str,re.I)
print(rst)
print(rst2)

#全局匹配函数
str="poythonyapdybcpdfagy"
reg="p.*?y"
rst=re.compile(reg).findall(str)
print(rst)
```

### 常见正则实例
> 匹配网址、电话号码等

```
#导入正则模块
import re
#常见正则实例
#匹配网址
string="<a href='http://www.baidu.com'>百度</a>"
reg="[a-zA-Z]+://[^\s]*[.com|.cn]"
rst=re.compile(reg).findall(string)
print(rst)

#匹配电话号码
string="tel:020-78762764 other:7632-8766234"
reg="\d{4}-\d{7}|\d{3}-\d{8}"
rst=re.compile(reg).findall(string)
print(rst)
```

### 简单爬虫的编写
```
#自动提取QQ群
#分析网页源码查找要提取内容的规律
import urllib.request
import re
data = urllib.request.urlopen("https://edu.csdn.net/huiyiCourse/detail/253").read().decode("UTF-8");
pat="<p>(\d{7,})</p>"
res=re.compile(pat).findall(data)
print(res)
```

```
#提取出版社信息并写入文件中
#分析网页源码查找要提取内容的规律
import urllib.request
import re
data = urllib.request.urlopen("https://read.douban.com/provider/all").read().decode("UTF-8");
pat="<div class=\"name\">(.*?)</div>"
res=re.compile(pat).findall(data)
file=open("C:/Users/LS/Desktop/publisher.txt","w",encoding="utf-8")
for name in res:
    file.write(name + "\n")
file.close()
```

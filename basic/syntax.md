## 基本语法
** 内容目录： **  
[输入和输出](#inout)  
[注释](#note)  
[标识符](#identifier)  
[常量/变量](#variable)  
[数据类型](#dataType)  

### <span id="inout">输入和输出<span>
---
#### 输入
Python提供了一个input()，可以让用户输入字符串，并存放到一个变量里：
```
>>> name = input()
abc
>>> name
'abc'
>>>
```
这样显得很不友好。input()可以让你显示一个字符串来提示用户
```
>>> name = input('please enter your name: ')
please enter your name: def
>>> name
'def'
>>>
```

#### 输出
用print()在括号中加上字符串，就可以向屏幕上输出指定的文字
```
print("hello world")
```
print()函数也可以接受多个字符串，用逗号“,”隔开，就可以连成一串输出（遇到逗号“,”会输出一个空格）：
```
>>> print('The quick brown fox', 'jumps over', 'the lazy dog')
The quick brown fox jumps over the lazy dog
```

print()也可以打印整数，或者计算结果：
```
>>> print(300)
300
>>> print(100 + 200)
300
>>> print('100 + 200 =', 100 + 200)
100 + 200 = 300
```

### <span id="note">注释<span>
---
1. #注释

  `#print("hello world!")`

2. 三引号注释(三个单引号或三个双引号都可以)

```

'''
print("hello world!")

print("hello world!")

print("hello world!")

'''
```

### <span id="identifier">标识符<span>
---
1. 命名规则：第一个字符为字母或下划线，其他字符可以是字母、下划线或数字.
2. 大小写敏感

### <span id="variable">变量/常量<span>
---
`a = 1`变量a是一个整数。  
`t_007 = 'T007'`变量t_007是一个字符串。  
`Answer = True`变量Answer是一个布尔值True。  
在Python中，等号=是赋值语句，可以把任意数据类型赋值给变量，同一个变量可以反复赋值，而且可以是不同类型的变量，例如：
```
a = 123 # a是整数
print(a)
a = 'ABC' # a变为字符串
print(a)
```
这种变量本身类型不固定的语言称之为动态语言，与之对应的是静态语言。静态语言在定义变量时必须指定变量类型，如果赋值的时候类型不匹配，就会报错。例如Java是静态语言

**变量作用域**
```
i=1 #全局变量
def func():
    j=2 #局部变量
    print(i)
    print(j)
func()
print(i)
print(j) #报错
```

**常量**  
&emsp;&emsp;所谓常量就是不能变的变量，比如常用的数学常数π就是一个常量。在Python中，通常用全部大写的变量名表示常量：
```
PI = 3.14159265359
```
但事实上PI仍然是一个变量，Python根本没有任何机制保证PI不会被改变，所以，用全部大写的变量名表示常量只是一个习惯上的用法。

### <span id="dataType">数据类型<span>
---
#### 基本数据类型：
> 整数、浮点数、字符串、布尔值、空值

**整数**
- Python可以处理任意大小的整数，包括负整数:例如：1，100，-8080，0
- 十六进制用0x前缀和0-9，a-f表示，例如：0xff00，0xa5b4c3d2
- Python的整数没有大小限制，而某些语言的整数根据其存储长度是有大小限制的，例如Java对32位整数的范围限制在-2147483648-2147483647。



**浮点数**  
- 浮点数也就是小数，之所以称为浮点数，是因为按照科学记数法表示时，一个浮点数的小数点位置是可变的，比如，1.23x109和12.3x108是完全相等的。
- 浮点数可以用数学写法，如1.23，3.14，-9.01，等等。但是对于很大或很小的浮点数，就必须用科学计数法表示，把10用e替代，1.23x109就是1.23e9，或者12.3e8，0.000012可以写成1.2e-5，等等。
- Python的浮点数也没有大小限制，但是超出一定范围就直接表示为inf（无限大）。

**字符串**  
字符串是以单引号'或双引号"或三个单引号括起来的任意文本，例如：
```
a1='abc'
a2="abc"
a3='''abc''' #支持字符串换行
```
&emsp;&emsp;请注意，''或""本身只是一种表示方式，不是字符串的一部分，因此，字符串'abc'只有a，b，c这3个字符。如果'本身也是一个字符，那就可以用""括起来，比如"I'm OK"包含的字符是I，'，m，空格，O，K这6个字符。  
&emsp;&emsp;如果字符串内部既包含'又包含"怎么办？可以用转义字符\来标识，比如：
```
'I\'m \"OK\"!'
```
表示的字符串内容是：
```
I'm "OK"!
```
&emsp;&emsp;转义字符\可以转义很多字符，比如\n表示换行，\t表示制表符，字符\本身也要转义，所以\\表示的字符就是\。
```
>>> print('\\\n\\')
\
\
```
&emsp;&emsp;如果字符串里面有很多字符都需要转义，就需要加很多\，为了简化，Python还允许用r''表示''内部的字符串默认不转义，可以试试：
```
>>> print('\\\t\\')
\       \
>>> print(r'\\\t\\')
\\\t\\
```
多行字符串'''...'''也可以在前面加上r使用
```
>>> print(r'''hello,\n
world''')

hello,\n
world
>>>
```

**布尔值**  
&emsp;&emsp;布尔值和布尔代数的表示完全一致，一个布尔值只有True、False两种值，要么是True，要么是False，在Python中，可以直接用True、False表示布尔值（请注意大小写），也可以通过布尔运算计算出来：
```
>>> True
True
>>> False
False
>>> 3 > 2
True
>>> 3 > 5
False
```
布尔值可以用and、or和not运算。
```
>>> True and True
True
>>> True and False
False

>>> True or True
True
>>> True or False
True
>>> False or False
False

>>> not True
False
>>> not False
True
>>> not 1 > 2
True
```
布尔值经常用在条件判断中，比如：
```
if age >= 18:
    print('adult')
else:
    print('teenager')
```

**空值**
&emsp;&emsp;空值是Python里一个特殊的值，用None表示。None不能理解为0，因为0是有意义的，而None是一个特殊的空值。


#### 复杂数据类型：
> 列表(list)、元组(tuple)、集合(set)、字典(dictionary)


3. 列表(下标从0开始)
  - b=[7,"cd",9]
  - 取值：print(b[0])
  - 设值：b[2]='def'
4. 元组(不能重新赋值)
  - b=(7,"cd",9)
  - 取值：print(b[0])
  - 设值：b[2]='def' #报错
5. 集合(去重)
  - b=set("abcdabc")  #最终结果只有abcd四个字符
  - c=set("cdef")
  - g=b-c #结果为ab即求差集，b集合中有c集合中没有的元素
6. 字典
  - 格式：{key1:value1,key2:value2,...}
  - data={"abc":7,"def":"hello"}
  - 取值：data["abc"]
  - 设值：data["abc"]="world"

### 运算符
1. 常见运算符：`+、-、*、/、%`

在Python中，有两种除法，一种除法是`/`
```
>>> 10 / 3
3.3333333333333335
```
`/`除法计算结果是浮点数，即使是两个整数恰好整除，结果也是浮点数：
```
>>> 9 / 3
3.0
```
还有一种除法是`//`，称为地板除，两个整数的除法仍然是整数：
```
>>> 10 // 3
3
```
你没有看错，整数的地板除`//`永远是整数，即使除不尽。要做精确的除法，使用`/`就可以。
因为//除法只取结果的整数部分，所以Python还提供一个余数运算，可以得到两个整数相除的余数：
```
>>> 10 % 3
1
```

2. 优先级：

### 缩进
python是一门强制缩进的语言，同一层次的代码必须处于同一个缩进幅度上。下一层次的代码要相对于上一层次的代码进行缩进，建议使用tab建进行缩进(tab缩进设置为4个空格)

### 分支流程
```
a=10
b=1
if(a>9):
  print(a)
  if(b<9):
    print(b)
elif(a>5 and b<5):
  print("a>5 and b<5")
else:
  print("over")
```

### 循环语句
#### while语句
```
a=0
while(a<10):
  print("hello" + str(a))
  a+=1
```

#### for语句
- 遍历列表
```
arr=["a","b","c","d"]
for i in arr:
    print(i)
```
- 常规循环
```
for j in range(0,10):
    print(j)
```

#### 乘法口诀实例（end=""表示不换行输出）
```
for i in range(1,10):
    for j in range(1,i+1):
        print(str(i) + "*" + str(j) +"=" +str(i*j), end="   ")
    print()
```
** 逆向输出乘法口诀(range第三个参数为步长) **
```
for i in range(9,0,-1):
    for j in range(i,0,-1):
        print(str(i) + "*" + str(j) +"=" +str(i*j),end="    ")
    print()
```

### 中断语句
- continue
```
for j in range(0,10):
    if(j>5 and j<8):
        continue
    print(j)
```
- break
```
for j in range(0,10):
    if(j>5 and j<8):
        break
    print(j)
```

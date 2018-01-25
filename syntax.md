## 基本语法
---

### 输出
- python2.x  
print "hello world"
- python3.x  
print("hello world")

### 注释
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

### 标识符
1. 命名规则：第一个字符为字母或下划线，其他字符可以是字母、下划线或数字.

### 变量/常量
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

### 数据类型

常见数据类型：
  数字、字符串、列表(list)、元组(tuple)、集合(set)、字典(dictionary)

1. 数字
  - abc=9
2. 字符串
  - a1='abc'
  - a2="abc"
  - a3='''abc'''
  - a4=a1+a2+a3
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

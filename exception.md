## python异常处理
---

### 基本语法
```
异常处理格式
try：
    程序块
except Exception as 异常名称:
    异常处理模块
```
```
for i in range(0,10):
    try:
        print(i)
        if(i==4):
            print(k)
    except Exception as err :
        print(err)
```

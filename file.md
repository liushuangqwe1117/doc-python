## python文件操作
---
### 打开文件
open(文件地址,操作形式)
```
w:写入
r:读取
b:二进制
a:追加
```
```
fh=open("C:/Users/LS/Desktop/任务列表","r",encoding="utf-8")
data=fh.read() #一次读取所有文件内容
fh.close() #关闭文件
print(data)
```
```
fh=open("C:/Users/LS/Desktop/任务列表","r",encoding="utf-8")
while True:
    line=fh.readline() #一行一行的读取
    if(len(line)==0):
        break
    print(line)
fh.close() #关闭文件
```

### 写入文件
```
fh=open("C:/Users/LS/Desktop/任务列表2","w",encoding="utf-8") #覆盖写入
fh.write("开始学python")
fh.close() #关闭文件
fh=open("C:/Users/LS/Desktop/任务列表2","a",encoding="utf-8") #追加写入
fh.write("\n用python写爬虫")
fh.close() #关闭文件
```

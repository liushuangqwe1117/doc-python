## 用户代理池
> 用户代理池就是将不同的用户代理组建成为一个池子，供随后使用

---

### 浏览器代理池

```
#浏览器代理池
import urllib.request
import re
import random

uapools=[
    "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36",
    "Mozilla/5.0 (Windows NT 6.3; WOW64; Trident/7.0; rv:11.0) like Gecko"
]

def ua(uapools):
    thisua=random.choice(uapools)
    print(thisua)
    headers=("User-Agent",thisua)
    opener=urllib.request.build_opener()
    opener.addheaders=[headers]
    #将opener安装为全局
    urllib.request.install_opener(opener)

pat='<div class="content">.*?<span>(.*?)</span>.*?</div>'
for i in range(0,5):
    ua(uapools)
    url="https://www.qiushibaike.com/8hr/page/" + str(i) + "/"
    data=urllib.request.urlopen(url).read().decode("utf-8","ignore")
    #S : 让.匹配包括换行符
    rst=re.compile(pat,re.S).findall(data)
    for j in range(0,len(rst)):
        print(rst[j])
```


### IP代理
> IP代理：网络爬虫使用代理IP去爬取网站

```
网络资源：
    西刺代理(免费)：http://www.xicidaili.com/nn
    大象代理(收费)：http://daxiangdaili.com/
```

### IP代理构建的第一种方案(适合代理ip稳定的情况)
```
#IP代理构建的第一种方案(适合代理ip稳定的情况)
import random
import urllib.request
ippools=[
    "110.73.28.177:8123",
    "112.82.237.191:8118",
    "180.121.128.49:808"
    ]

def ip(ippools):
    thisip=random.choice(ippools)
    print(thisip)
    proxy=urllib.request.ProxyHandler({"http":thisip})
    opener=urllib.request.build_opener(proxy,urllib.request.HTTPHandler)
    #将opener安装为全局
    urllib.request.install_opener(opener)

url="http://www.baidu.com"
for i in range(0,len(ippools)):
    try:
        ip(ippools)
        data=urllib.request.urlopen(url).read()
        print(len(data))
        fh=open("C:/Users/LS/Desktop/ip_baidu" + str(i) + ".html","wb")
        fh.write(data)
        fh.close()
    except Exception as err:
        print(err)
```

### IP代理构建的第二种方案(接口调用，适合代理ip不稳定的情况)
```
#IP代理构建的第二种方案(接口调用，适合代理ip不稳定的情况)
import urllib.request

def ip():
    thisip=urllib.request.urlopen("http://tvp.daxiangdaili.com/ip/?tid=559126871522487&num=1")
    print(thisip)
    proxy=urllib.request.ProxyHandler({"http":thisip})
    opener=urllib.request.build_opener(proxy,urllib.request.HTTPHandler)
    #将opener安装为全局
    urllib.request.install_opener(opener)

url="http://www.baidu.com"
for i in range(0,5):
    try:
        ip()
        data=urllib.request.urlopen(url).read()
        print(len(data))
        fh=open("C:/Users/LS/Desktop/ip_baidu" + str(i) + ".html","wb")
        fh.write(data)
        fh.close()
    except Exception as err:
        print(err)
```


### 淘宝商品图片爬虫实战
```
#淘宝商品图片爬虫
'''
请求URL规律
https://s.taobao.com/search?q=关键词&s=(页码-1)*44

图片地址规律：
"pic_url":"//g-search1.alicdn.com/img/bao/uploaded/i4/imgextra/i2/12683027/TB2_Jb6lMLD8KJjSszeXXaGRpXa_!!2-saturn_solar.png"
正则
"pic_url":"(.*?)"

'''

import urllib.request
import re
import random

keyname="连衣裙"
key=urllib.request.quote(keyname)


uapools=[
    "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36",
    "Mozilla/5.0 (Windows NT 6.3; WOW64; Trident/7.0; rv:11.0) like Gecko"
]

def ua(uapools):
    thisua=random.choice(uapools)
    print(thisua)
    headers=("User-Agent",thisua)
    opener=urllib.request.build_opener()
    opener.addheaders=[headers]
    #将opener安装为全局
    urllib.request.install_opener(opener)

for i in range(1,2):
    url="https://s.taobao.com/search?q=" + key + "&s=" + str((i-1)*44)
    ua(uapools)
    data=urllib.request.urlopen(url).read().decode("utf-8","ignore")
    #图片地址正则
    picPat='"pic_url":"//(.*?)"'
    imgList=re.compile(picPat).findall(data);
    for j in range(0,len(imgList)):
        thisImg=imgList[j]
        thisImgUrl="http://" + thisImg
        localFile="C:/Users/LS/Desktop/html/" + str(i) + str(j) + ".jpg"
        urllib.request.urlretrieve(thisImgUrl,filename=localFile)
```


### 同时使用用户代理池与IP代理池的方法
```
def ua_ip(myurl):
    import random
    uapools=[
        "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.79 Safari/537.36 Edge/14.14393",
        "Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.22 Safari/537.36 SE 2.X MetaSr 1.0",
        "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Maxthon 2.0)",
        ]
    import urllib.request
    def api():
        print("这一次调用了接口")
        thisall=urllib.request.urlopen("http://tvp.daxiangdaili.com/ip/?tid=559126871522487&num=10&foreign=only&filter=on")
        ippools=[]
        for item in thisall:
            ippools.append(item.decode("utf-8","ignore"))
        return ippools
    def ip(ippools,time,uapools):
        thisua=random.choice(uapools)
        print(thisua)
        headers=("User-Agent",thisua)
        thisip=ippools[time]
        print("当前用的IP是："+ippools[time])
        proxy=urllib.request.ProxyHandler({"http":thisip})
        opener=urllib.request.build_opener(proxy,urllib.request.HTTPHandler)
        opener.addheaders=[headers]
        urllib.request.install_opener(opener)

    x=0
    for i in range(0,35):
        try:
            if(x%10==0):
                time=x%10
                ippools=api()
                ip(ippools,time,uapools)
            else:
                time=x%10
                ip(ippools,time,uapools)
            url=myurl
            data1=urllib.request.urlopen(url).read()
            data=data1.decode("utf-8","ignore")
            x+=1
            break
        except Exception as err:
            print(err)
            x+=1
    return data
#data=ua_ip("http://www.baidu.com")
```

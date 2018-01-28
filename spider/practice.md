## 爬虫实战
---

### 准备工作
1. 将之前写的uaip模块放到python安装目录的Lib目录下

```
#如何同时使用用户代理池和IP代理池
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
        #临时加上这个配置
        thisip="127.0.0.1:8888"
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
            print(len(data))
            #fh=open("D:\\我的教学\\Python\\韬云教育-腾讯-Python爬虫\\rst\\ip_baidu_"+str(i)+".html","wb")
            #fh.write(data1)
            #fh.close()
            x+=1
            break
        except Exception as err:
            print(err)
            x+=1
    return data
#data=ua_ip("http://www.baidu.com")
```

2. 安装fiddler
3. 实现Fiddler对HTTPS的代理
参考：http://blog.csdn.net/weiwei_pig/article/details/54647680

### 微信爬虫

```
from uaip import *
import urllib.request
import re
key="Python"
for i in range(0,10):
    key=urllib.request.quote(key)
    thispageurl="http://weixin.sogou.com/weixin?oq=&query="+key+"&type=2&page="+str(i+1)+"&ie=utf8"
    thispagedata=ua_ip(thispageurl)
    print(len(thispagedata))
    pat1='<div class="txt-box">.*?href="(.*?)"'
    rst1=re.compile(pat1,re.S).findall(thispagedata)
    if(len(rst1)==0):
        print("这一页没有爬成功")
        continue
    for j in range(0,len(rst1)):
        thisurl=rst1[j]
        pat2='amp;'
        thisurl=thisurl.replace(pat2,"")
        print(thisurl)
        thisdata=ua_ip(thisurl)
        print("这篇文章爬取成功，长度为：" +str(len(thisdata)))
        fh=open("C:\\Users\\LS\\Desktop\\html\\\\"+str(i)+str(j)+".html","w",encoding="utf-8")
        fh.write(thisdata)
        fh.close()
```


### 腾讯视频评论爬虫（单页评论爬虫）:获取深度解读评论内容
```
import urllib.request
import re
#https://video.coral.qq.com/filmreviewr/c/upcomment/[视频id]?commentid=[评论id]&reqnum=[每次提取的评论的个数]
vid="j6cgzhtkuonf6te"
cid="6233603654052033588"
num="20"
#构造当前评论网址
url="https://video.coral.qq.com/filmreviewr/c/upcomment/"+vid+"?commentid="+cid+"&reqnum="+num
headers={"User-Agent":"Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.22 Safari/537.36 SE 2.X MetaSr 1.0",
        "Content-Type":"application/javascript",
         }
opener=urllib.request.build_opener()
headall=[]
for key,value in headers.items():
    item=(key,value)
    headall.append(item)
opener.addheaders=headall
urllib.request.install_opener(opener)
#爬取当前评论页面
data=urllib.request.urlopen(url).read().decode("utf-8")
titlepat='"title":"(.*?)"'
commentpat='"content":"(.*?)"'
titleall=re.compile(titlepat,re.S).findall(data)
commentall=re.compile(commentpat,re.S).findall(data)
for i in range(0,len(titleall)):
    try:
        print("评论标题是:"+eval('u"'+titleall[i]+'"'))
        print("评论内容是:"+eval('u"'+commentall[i]+'"'))
        print("------")
    except Exception as err:
        print(err)
```


### 腾讯视频评论爬虫（自动切换下一页评论的爬虫）:获取深度解读评论内容

```
import urllib.request
import re
#https://video.coral.qq.com/filmreviewr/c/upcomment/[视频id]?commentid=[评论id]&reqnum=[每次提取的评论的个数]
vid="j6cgzhtkuonf6te"
cid="6233603654052033588"
num="3"
headers={"User-Agent":"Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.22 Safari/537.36 SE 2.X MetaSr 1.0",
        "Content-Type":"application/javascript",
         }
opener=urllib.request.build_opener()
headall=[]
for key,value in headers.items():
    item=(key,value)
    headall.append(item)
opener.addheaders=headall
urllib.request.install_opener(opener)
for j in range(0,100):
    #爬取当前评论页面
    print("第"+str(j)+"页")
    thisurl="https://video.coral.qq.com/filmreviewr/c/upcomment/"+vid+"?commentid="+cid+"&reqnum="+num
    data=urllib.request.urlopen(thisurl).read().decode("utf-8")
    titlepat='"title":"(.*?)","abstract":"'
    commentpat='"content":"(.*?)"'
    titleall=re.compile(titlepat,re.S).findall(data)
    commentall=re.compile(commentpat,re.S).findall(data)
    lastpat='"last":"(.*?)"'
    cids = re.compile(lastpat,re.S).findall(data);
    if(len(cids) == 0):
        break;

    cid=cids[0]
    for i in range(0,len(titleall)):
        try:
            print("评论标题是:"+eval('u"'+titleall[i]+'"'))
            print("评论内容是:"+eval('u"'+commentall[i]+'"'))
            print("------")
        except Exception as err:
            print(err)

```

### 获取影视短评内容

```
import urllib.request
import re
#https://coral.qq.com/article/1743283224/comment?commentid=6237632351690994016&reqnum=20
vid="1743283224"
cid="6237632351690994016"
num="20"
headers={"User-Agent":"Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.22 Safari/537.36 SE 2.X MetaSr 1.0",
        "Content-Type":"application/javascript",
         }
opener=urllib.request.build_opener()
headall=[]
for key,value in headers.items():
    item=(key,value)
    headall.append(item)
opener.addheaders=headall
urllib.request.install_opener(opener)
for j in range(0,100):
    #爬取当前评论页面
    print("第"+str(j)+"页")
    thisurl="https://coral.qq.com/article/"+vid+"/comment?commentid="+cid+"&reqnum="+num
    data=urllib.request.urlopen(thisurl).read().decode("utf-8")
    #titlepat='"title":"(.*?)","abstract":"'
    commentpat='"content":"(.*?)"'
    #titleall=re.compile(titlepat,re.S).findall(data)
    commentall=re.compile(commentpat,re.S).findall(data)
    lastpat='"last":"(.*?)"'
    cid=re.compile(lastpat,re.S).findall(data)[0]
    for i in range(0,len(commentall)):
        try:
            print("评论内容是:"+eval('u"'+commentall[i]+'"'))
            print("------")
        except Exception as err:
            print(err)

```

## python小课堂32 - 初识原生爬虫（二）

### 前言

跑上来继续完成前面爬虫系列！上章介绍了本次爬虫案例的需求，本节完成上次 TODO LIST 的后半部分代码编写以及介绍。本篇为代码讲解，没有耐心的童鞋看大概会非常枯燥吧！

回顾上篇关联性文章如下：



[python小课堂31 - 初识原生爬虫](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659374&idx=1&sn=d2252c900a04ccccc78d87e6aeac063c&chksm=8c97d2d7bbe05bc18561ca6e3ac3270bf425a970b1b0683ee53a96ddc01ae1f25be819b9c84c&scene=21#wechat_redirect)



PS：本期爬虫案例并**不是最完善**的爬虫，仅为了将爬虫的原理基础介绍清楚。要清楚，爬虫具有时效性，由于现在各大网站都有相关的反爬机制，所以也许现在写的爬虫代码此时适用，但过些时日就可能失效了，这点需要注意。**本章仅供学习参考，请在遵守网络法律前提下进行相关操作。**


### 爬虫代码架构

有了需求以后，第一件事要干的就是搭出代码的整体架构，借此机会，我们可以将面向对象章节介绍的知识点串联到本章来使用，若需回顾可以点击如下查看：

[python小课堂18 - 面向对象篇（一）](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659087&idx=1&sn=2d65a5e2efc4f848d7242e6619e30211&chksm=8c97d1f6bbe058e0a90f58bd16f72e0392d14bf2621455547577ab1a89e0fa73a9f9c3537455&scene=21#wechat_redirect)

[python小课堂19 - 面向对象篇（二）](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659101&idx=1&sn=5d8b202ca7fb139ef72284bd90a7c38f&chksm=8c97d1e4bbe058f2963a2b14e2022f0c8e103b0e3696467967731a16be6654cebf56834106b0&scene=21#wechat_redirect)

[python小课堂21 - 面向对象(三)](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659128&idx=1&sn=f15496cd61c29e51ee3662af1884fe31&chksm=8c97d1c1bbe058d7a7a4891cf9c318f6dc397939cfd231023bd1b3e85daeeec853fa93c9db43&scene=21#wechat_redirect)

[python小课堂22 - 面向对象(四)](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659140&idx=1&sn=d0e851bae9d3a4afc762bd96525ee3ef&chksm=8c97d13dbbe0582b4dbf9ef8de12c13db1cdf8b4a9eaed49ca464a313ccf679ddd948c17e707&scene=21#wechat_redirect)



经需求设计，已知步骤有：

1. 模拟请求网页，拿到返回的网页源代码

2. 解析返回的源代码，对想要的信息进行节点的提取

3. 有上两步骤，最终运行代码


具体架构如下：

```python
class SpiderPandas(object):
    """ 类：原生爬虫 - 爬取 熊猫王者荣耀 直播

    目标：直播标题、主播网名、热度

    """

    def __crawl_html(self):
        """ 请求网页源码,私有方法 """
        pass

    def __analysis_node(self):
        """ 分析网页返回的节点,私有方法 """
        pass

    def run(self):
        """ 运行方法 """
        pass
```

设计一个爬虫类，其中模拟请求和解析网页节点的方法设置为私有方法，类的内部使用即可，类外部需要调用的是公开的 run 运行方法。

### 模拟请求

所谓的原生爬虫，直接使用 python 自带的库完成对网页进行模拟请求，而此处的自带库就是 urllib 了！简单的介绍一下，模拟请求网页只需要使用到 urllib 下的 request 方法即可，名如起义，就是请求的意思。本处不会过多介绍其使用方法，重点是一步步的思路，具体可以去官方文档网站查看：



https://docs.python.org/3/library/urllib.html



有了使用方法后，我们来尝试写一下代码，变成如下：


```python
from urllib import request
class SpiderPandas(object):
    """ 类：原生爬虫 - 爬取 熊猫王者荣耀 直播

    目标：直播标题、主播网名、热度

    """

    # 请求网页的url
    url = 'https://www.panda.tv/cate/kingglory'

    def __crawl_html(self):
        """ 请求网页源码,私有方法 """
        r = request.urlopen(SpiderPandas.url)
        html_content = r.read()
        print(type(html_content))
        print(html_content)

if __name__ == '__main__':
    spiderPandas = SpiderPandas()
    spiderPandas.run()
```

首先先把 request 导入，然后定义类变量 url ，对其发出模拟请求，调用 request 的 urlopen 方法，传入 url 即可。使用 r 变量接受，再次调用 r 的read 方法即可得到网页源代码内容。关于

```python
if __name__ == '__main__':
```

的用法，大家可以自行网上查阅资料，通俗的解释就是可以将其看做入口函数，代码会先从此处进入执行。

可以看下上述代码的最终结果：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQw6Wu3iajiagVng8Lszcogdo9FNvXw7nK02NW8nY9uBCG0KQxOenR8QTuvFKYNp1cBcDT3ckPTIaQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


返回结果是字节类型的，将之打印输出，可以看到后续中文是字节码，所以还需要将之转化为字符串才可以。如下：


```python
from urllib import request
class SpiderPandas(object):
    """ 类：原生爬虫 - 爬取 熊猫王者荣耀 直播

    目标：直播标题、主播网名、热度

    """

    # 请求网页的url
    url = 'https://www.panda.tv/cate/kingglory'

    def __crawl_html(self):
        """ 请求网页源码,私有方法 """
        r = request.urlopen(SpiderPandas.url)
        html_content = r.read()
        html_content = str(html_content,encoding='utf-8')
        print(type(html_content))
        print(html_content)

if __name__ == '__main__':
    spiderPandas = SpiderPandas()
    spiderPandas.run()
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQw6Wu3iajiagVng8LszcogdczIOc1N63HbZ5InoRicusdKFapc9NTTA15lrqibpXOoiaibdfkibAzyD4Bw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


有了以上代码，模拟网页请求并且获取到其源代码便完成了。如果在 pycharm 不好观察节点信息，可以将之复制到在线网页格式化html的网页工具中，先格式化一下，变成漂亮的代码后再复制到文本中查看即可。



### 分析 html 信息节点


再来回顾分析一下我们要爬取的信息节点，打开 F12 ，通过观察可以发现，需要的信息都在这一个大的 div 标签下，这样一来，就非常省事儿了！


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQw6Wu3iajiagVng8Lszcogdqop2bOxRVcyBsKRMYjrcdDxWYageXDVRkaAojNxpoVGY1cBNktatNQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

粘出来格式化下，看得更清楚：

```python
<div class="video-info"> 
   <span class="video-title" title="五排开车">五排开车</span> 
   <span class="video-nickname" title="简单点丶无双"> <i class="icon-hostlevel icon-hostlevel-10" data-level="10"></i> 简单点丶无双 </span> 
   <span class="video-number"><i class="ricon ricon-eye"></i>5921</span> 
   <span class="video-station-info"> <i class="ricon ricon-fleet"></i> <i class="video-station-num">3人</i> </span> 
  </div>
```

用思维导图画出来，其一是整体流程，其二是具体分析：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQw6Wu3iajiagVng8Lszcogd64Y1x2LomAHTzwvwQzrybl0IhQzic337pPYj11HOmgDPQbSIzkJRYbg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQw6Wu3iajiagVng8LszcogdczNibaJhL4A5wQSVnZDRAoJVibVXBHS6ia1icEGLP4Z4V6TezEASy3Dptw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

还记得很早之前的正则表达式就说过，如果会用正则的话，处理文本信息是非常容易并且省力的！正则相关内容回顾：

[python小课堂23 - 正则表达式(一)](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659173&idx=1&sn=47e1d13da88c0c105b048dd386641077&chksm=8c97d11cbbe0580abbef1819f8d17129929545a602113ec855e257c506d0d6be03aeb5fa44bd&scene=21#wechat_redirect)


[python小课堂24 - 正则表达式(二)](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659187&idx=1&sn=5c0271d94fc98a7da7f20426c870e4ed&chksm=8c97d10abbe0581cf574653a577eed6db2c2c5d13bbdadbb5f1233871937401aa64c899caca2&scene=21#wechat_redirect)


**1. 正则匹配根节点 video - info**


按照思维导图的步骤2进行细分，先把根节点整段内容匹配出来，代码如下：

```python
import re
from urllib import request


class SpiderPandas(object):
    """ 类：原生爬虫 - 爬取 熊猫王者荣耀 直播

    目标：直播标题、主播网名、热度

    """

    # 请求网页的url
    url = 'https://www.panda.tv/cate/kingglory'
    root_node_pattern = r'<div class="video-info">[\s\S]*?</div>'

    def __crawl_html(self):
        """ 请求网页源码,私有方法 """
        r = request.urlopen(SpiderPandas.url)
        html_content = r.read()
        html_content = str(html_content, encoding='utf-8')
        return html_content

    def __analysis_node(self, html):
        """ 分析网页返回的节点,私有方法 """
        video_info_lists = re.findall(SpiderPandas.root_node_pattern, html)
        print(video_info_lists)


    def run(self):
        """ 运行方法 """
        html = self.__crawl_html()
        self.__analysis_node(html)


if __name__ == '__main__':
    spiderPandas = SpiderPandas()
    spiderPandas.run()
```

说下思路，请求网页的源码私有方法，可以对其 return ，使得解析节点的私有方法调用。重要的是写出匹配 video-info 的根节点正则表达式，也就是 **root_node_pattern** 。使用 re.findall 进行全局匹配，结果如下：


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQw6Wu3iajiagVng8Lszcogd2WUfWAoALpCRP2jlRboELlaRuOKb89vbjM7FRMSj7OJBAmx80UhUvg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


列表呈现的各节点信息。但是这样会发现一个问题，匹配到的内容是包含边界原字符(也就是div class = "video-inof....")的。所以可以改变正则匹配，使用分组即可去除！

```python
root_node_pattern = r'<div class="video-info">([\s\S]*?)</div>'
```

**2. 正则匹配根节点下的细节信息**

```python
# 房间名称正则
title_node_pattern = r'<span class="video-title" title="([\s\S]*?)">'
# 主播称号正则
nickname_node_pattern = r'<span class="video-nickname" title="([\s\S]*?)">'
# 房间热度正则
number_node_pattern = r'ricon-eye"></i>([\s\S]*?)</span>'
```

```python
def __analysis_node(self, html):
    """ 分析网页返回的节点,私有方法 """
    video_info_lists = re.findall(SpiderPandas.root_node_pattern, html)
    for video_info in video_info_lists:
        title = re.findall(SpiderPandas.title_node_pattern, video_info)[0]
        nickname = re.findall(SpiderPandas.nickname_node_pattern, video_info)[0]
        number = re.findall(SpiderPandas.number_node_pattern, video_info)[0]
        print(f'房间名称:{title},主播名称:{nickname},房间热度:{number} \n')
```

类似根节点的处理方式一样，找规律，正则具体内容一样，在私有的分析节点方法中直接 for 循环拿出每个大 div 来，在对每个 video-info 下的三类进行正则匹配，最后输出打印：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQw6Wu3iajiagVng8Lszcogd02c2O6bE9QfddBv90SGUCoxb7iaP7g3ic41sf9ZMXrxGZdRShlbc7OOA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


### 总结

可以看到，上面的所有思路已经将小爬虫最主要的功能实现了，但是对于有些细节实现并不完美，后续还会有一章讲解哪些地方应该进行优化，哪些地方是代码的缺陷。

 


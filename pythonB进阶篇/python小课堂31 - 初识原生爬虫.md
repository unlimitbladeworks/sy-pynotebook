## python小课堂31 - 初识原生爬虫

### 前言

在上一期介绍了爬虫之前必会浏览器的开发者工具，忘记的童鞋可以在回顾一下：

[python小课堂30 - 爬虫之前必会的浏览器开发者工具.](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659358&idx=1&sn=e8af5138490d5e2aa0b91e4fc7c88e49&chksm=8c97d2e7bbe05bf1a983f110ad339280ddcb34cb70187f30fa2f6aa6fa516a2b02b223d88512&scene=21#wechat_redirect)

本篇文章将以实战来介绍一期 “**原生**” 爬虫，这里的原生是指使用 python 自带的**请求库**来完成爬虫，不借用第三方库（如 requests....贼好用！谁用谁知道...）。同时需要注意的是本次案例不使用任何爬虫框架去完成，大部分知识依赖于前面介绍的基础知识，少部分知识需要后续介绍学习。

PS：本期爬虫案例并**不是最完善**的爬虫，仅为了将爬虫的原理基础介绍清楚。要清楚，爬虫具有时效性，由于现在各大网站都有相关的反爬机制，所以也许现在写的爬虫代码此时适用，但过些时日就可能失效了，这点需要注意。**本章仅供学习参考，请在遵守网络法律前提下进行相关操作**。


### 什么是爬虫？

> 网络爬虫（又被称为网页蜘蛛，网络机器人，在FOAF社区中间，更经常的称为网页追逐者），是一种按照一定的规则，自动地抓取万维网信息的程序或者脚本。             -- 百度百科

引用了下百度百科对爬虫的定义，接下来用笔者理解的大白话来说下：在咱们现在生活的这个时代，多数信息的传递都是以浏览器作媒介进行传播的，比如你要查寻一部电影，你首先得打开浏览器，然后打开百度（或谷歌或其他搜索引擎）的主页，在搜索框输入XXXX，回车后就会跳转到相应的网页，而这些所谓的搜索引擎，如百度，其本身就是一个**大爬虫**。


![](https://mmbiz.qpic.cn/mmbiz_jpg/E4ianOkSOYIaFwvslwIVzHpBoehrib5xqFDSGzxQUiaRHG97cQgr1jh06orezNWeqL10cib3NnP4XNHMFQDsykkyqA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

互联网就像一张蜘蛛网，你可以想象成每个网页就是粘在蜘蛛网上被包裹住的食物，在这张蜘蛛网上，不同网页组成了许多食物，食物的种类过于繁多，作为人类的你，想要从中挑选最美味，最可口的食物很是麻烦，于是创造出来一个可以行进于蜘蛛网上的“蜘蛛”，通过给蜘蛛下达规则性的命令，让蜘蛛来在这张网上帮你搜寻你想要的“食物”。


上面所讲的小故事，人类泛指开发者，蜘蛛泛指爬虫，而食物则泛指网页，或者说是信息。



最后一句话总结一下：爬虫，即在网络上，根据你所定义的规则流程，通过程序化将你想要的，有用的信息获取下来，这个程序称之为爬虫。

### 王者荣耀直播

这里就用笔者近期玩的游戏来做一次有趣的分享吧，王者荣耀。



众所周知，近几年随着物质生活的提高，相应精神物质也随之上升，越来越多的游戏被大家所认知，比如风靡一时的 dota2、 LOL等，近两年移动端的火热，例如吃鸡、王者荣耀等。。。随着游戏本身“社会地位”的上升，相应的越来越多人选择做起了直播，观众们可以第一视角观看直播的犀利操作，从中学习相关操作，提升自己的操作意识。



那这里呢，笔者就以王者荣耀的直播为例（因为在王者方面，笔者也算是上过王者的男人）废话不多说，下面进入正题。

### 明确信息目标


首先，写爬虫的第一步就是要明确自己的信息，你要从网络中获取怎样的信息？它们有怎样的特征呢？所以不急，**先确定你要爬取（或者说是获取）的内容。**



打开熊猫 tv 直播间，让我们来分析一下：



https://www.panda.tv/，浏览器输入后，进入熊猫直播间，首页长这样：


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaFwvslwIVzHpBoehrib5xqF1VMia0RyxJ0XQtXW7LGzcTWRyj2xarqqU7HTVSjJQke8nJu2GjNiaDrQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


但从首页上看去，除了中间有视频播放器以外，没有什么笔者想要的信息。但是可以看到首页旁边，有个分类按钮，点过去看下：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaFwvslwIVzHpBoehrib5xqFglWMiaYBicLReTeMseGVMiazbEqAzeZPmFFDSVODv3wwPHCLNfKgSFH3Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


可以看到，游戏的种类繁多，我们可以搜索下想要的王者荣耀，继续点进去看下：



![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaFwvslwIVzHpBoehrib5xqFjiaAZ7Q50eib0PiaZhT9mvXicJJq6sPG3sibAxHAYcM50yHWczWqb6UcMeQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

当前所有与王者荣耀直播的相关主播，随便找一个，比如下面这个：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaFwvslwIVzHpBoehrib5xqFgFQqS1WDUBvqWPcjkaHcCxziacd2BiaC93wNlOicctibgLib4uNnnhQOZlg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

上图可知，有主播自己起的直播标题，还有主播的网名，以及当前的热度（小眼睛应该就是热度，小汽车好像是当前观看的人数）。嗯，笔者目标很明确，就是想抓取当前热度最高的主播，学习一波大佬的操作！

**明确抓取目标：直播标题、主播网名、热度（小眼睛）。**

### 分析网页结构

目标明确以后，来使用浏览器开发者工具分析下对应数据的网页结构，打开F12，分析如下：

**直播标题：**

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaFwvslwIVzHpBoehrib5xqFPrGheTevZib8xianK4uXVia4VkyZMWIVTI5RbPW0UhibFJ6EickfhCmV8lw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**主播网名：**

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaFwvslwIVzHpBoehrib5xqF8rEYa1BrhtlbpvJ8jU0ymNPhQEJae4xBDeokIfhx18wCDTNXIVribYg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**热度（小眼睛图标）：**

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaFwvslwIVzHpBoehrib5xqFuUjm52zcHljxzMxuwdBLxB1ibo941dRfhyd02hc1vMnADcibqZ0lic5Mg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 总结

好了，以上就是本篇对于熊猫直播网页结构的分析。



总结一下爬虫前需要准备的：



**1. 明确目的，知道自己的需求是什么，想要什么样的数据。**

**2. 找到数据对应的网页，比如笔者这里想找王者直播。**

**3. 根据目的，分析出网页数据对应的 HTML 结构标签代码。**



前三步是本章介绍的主要内容，消化一下！下面的步骤是实现的思路，放在下一篇文章去写吧.....



#### TODO LIST （待做的....）

模拟 Http 请求，使用 Python 原生包对服务器发起请求，获取到服务器返回给我们的 HTML 代码。



通过返回的 HTML 代码，使用正则表达式等手段提取出我们想要的数据信息即可！（当然这里有些网站是肯定会遇到坑，现在没有哪个网站会让你轻轻松松获取信息的，比如斗鱼直播的数据...毕竟都 9102 年了！）



以上便是一个简单的小小只爬虫原理概念性的介绍了！下篇文章，尽请期待....
 


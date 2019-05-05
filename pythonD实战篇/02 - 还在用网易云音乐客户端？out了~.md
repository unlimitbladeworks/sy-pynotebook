## 还在用网易云音乐客户端？out了~


### 前言

网易云音乐随着互联网时代的来临，优秀的以“大数据”而闻名。自2016年以后，越来越多人接受了这款优秀的音乐网站 or app，因良好的用户体验感而出名，比如歌单这个功能，只有你想不到的，没有用户共享、上传歌单做不到的！什么张雨生合集呀，什么动漫名曲。。。等



对于歌单这项功能来说，应该是许多网易云用户最喜爱的功能之一，毕竟整合了许多符合自己口味的歌曲在一起，省时又省力。但也同时面临着一个问题，即下载！



假如你的电脑上装了网易云音乐的客户端，那么还好说，比如下面这样，你可以一键下载：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaJDXbIjqrBuDnfywib4wXVGHwwW1NoQyWdqKeE9BSL5Pibl1P9JAIDeibIKJbia2LQILG1eWuIZoBzuw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


当然，也不排除有些朋友不喜欢这么麻烦，还要装个客户端。。。比如我，能不装电脑上的软件，绝对不会装！所以浏览器听歌成了首选，局限性就是如果没有网，那么浏览器这条路就走不通了！



所以今天，咱们就用**爬虫**的方式来实现一下，如何用 Python 下载歌单下的所有歌曲！顺便了解下爬虫下载音乐的原理机制。也许下载网易云音乐的文章满大街都是，但具体实现思路，笔者觉得应该一人一个样，不妨耐心的看下去，说不好有意外收获！



**PS：本文目的是抱以学习心态而分享，禁止用于非法以及商业途径，如有风险，一切后果自己承担！**


### 成果演示

依然是先看成果，有了成果，才能勾起你的兴趣，看了成果还提不起兴趣的，那确实就是没兴趣了，也不用在往下看了！走着客官，上图~

![](https://mmbiz.qpic.cn/mmbiz_gif/E4ianOkSOYIaJDXbIjqrBuDnfywib4wXVG2PfDjGbph4jia2ibxW1Z3wJCJ9x7KkVywV3tdMSBDJ5XaUrAeKnyC0Hw/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaJDXbIjqrBuDnfywib4wXVGibt8be7Yuhg1xRVwuTteqPJQ2lNe7XSOcar9Wy3t1NFDibRcYpmsWC0g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


### 爬取以及设计思路

**1. 找下载歌曲的外链(对外链接,简称外链)地址**

既然主要功能是下载，那么肯定是需要找到对应下载音乐的地址的，如果单从网易云主页分析，还要破解 js 加密什么的，实在麻烦，不妨换一种思路！多多利用搜索引擎，经查询，发现网易云提供了一个对外下载歌曲的地址，只需要知道歌曲id，即可使用地址加id形式打开网页进行播放，地址如下：

```python
# 只需要将歌曲 id 传给此网页，直接打开即可播放！
http://music.163.com/song/media/outer/url?id=xxxxx.mp3
```

来试试，"金鱼邓紫棋"的这首歌，翻唱龙卷风，id=28427775：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaJDXbIjqrBuDnfywib4wXVGcMaVOXpTNdiac3Y1EeVlRDybGibicrVxWSOTo81dtsrl9FyjncKE9lyxA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


把id替换到上面给出的外链中，打开后，网址自动跳转，将url加密了，同时自动播放：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaJDXbIjqrBuDnfywib4wXVGQg9iabamQKbIuicwoulTxGBEJfndA2icAEAasBk9KGiakadZ14GgnRbm1Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


**2. 分析歌单下各歌曲关键信息**


有了下载地址后一切都变得简单了，只需要做的是，获取你喜爱的歌单地址，然后将此歌单下所有歌曲id进行爬取！还记得爬取的步骤吗？



首先要明确自己想要的信息，而笔者这里想要的信息就三个：**歌单名称、歌曲名称、歌曲id。**



那么接下来就对网页分析下相应的节点。



歌单名称，看不清楚手机可以点开放大看，以下图片均可：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaJDXbIjqrBuDnfywib4wXVGrY6iaXIOLOV24WNrFvib3zBwI5rpB8aE9Yn0YwnVTBjUVZzawwLbkkWQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


歌曲名称：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaJDXbIjqrBuDnfywib4wXVG88Yic9lVNFYC8nFM8DyUYX3HGr0iav1yde98AyicXj7XncL4Kic18jgrvg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

歌曲id：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaJDXbIjqrBuDnfywib4wXVGjrnqYWc67exKRU4zY2kIJF96UB0icibc2kowfoY4HgASJGPiaicoIxZyyg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


**3. 爬取歌单下所有歌曲的id，同时传入外链地址，进行下载**


有了以上分析后，只需要验证下，我们用 Python 模拟请求，访问此网页时，返回的信息与我们F12分析后的结果是否一致。是否真的存在F12看到的信息节点呢？

网页地址：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcNKD8Y4iaLkewcYib65bUC2sZ3N9MuiaVlbgjiaWkjibgw7qC1zcKHUOJNyA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcNKD8Y4iaLkewcYib65bUC2sZ3N9MuiaVlbgjiaWkjibgw7qC1zcKHUOJNyA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

此处使用 requests 库模拟发送请求，得到返回的数据，代码是这样的：

```python
import requests
headers = {
            'user-agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko)\
            Chrome/69.0.3497.100 Safari/537.36'
        }
url = "https://music.163.com/#/playlist?id=2722916074"
r = requests.get(url=url,headers=headers)
print(r.text)
```

用上面这段代码，你请求后返回的内容，会惊奇的发现，怎么找也找不到与F12看到的相似节点内容！为什么呢？猜测是因为网易云做了一层地址上的反爬机制，隐藏了真正的歌单网页。



打开F12，再来找下请求：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcD5JSBrfc8VVSjgXJU3RmlcUQF8VaQFBArn8x22uVziajFNwskDQiaYQA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

经查找，确实隐藏了真实地址，现在浏览器上看到的 url 多了一个#，所以当我们请求图中 3 的地址时，便是返回的与F12看到的节点信息一致。

### 思考与动手

本篇文章，大致的思路已经带大家梳理清楚了，接下来就是动手了！笔者本次不打算将自己写的代码放出来，大家对学习爬虫感兴趣的，不妨自己动手写下程序试试。



思路有了，剩下的就是编程实战了！算是给大家留个小作业，有时间有兴趣的，可以评论区留言提问。写完的同学，可以自己动手验证下，是否能将音乐下载到本地，此次案例是一个不错的练手小项目！



下一期，笔者会写一篇讲解自己是如何设计代码的，顺便在把代码开源出来，敬请期待！

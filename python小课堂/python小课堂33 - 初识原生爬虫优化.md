## python小课堂33 - 初识原生爬虫优化

### 前言

上周写的爬虫代码分析思路，没多少人看丫....果然还是代码的讲解比较枯燥无聊吧....没看的可以回顾一下啦：

[python小课堂32 - 初识原生爬虫（二）](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659395&idx=1&sn=1125b5ffab398b59189dfa5f9608427a&chksm=8c97d23abbe05b2c7d24c63e857488fd0c37e2372cdd709e2658f6fc95a28f246aa6e68e8f36&scene=21#wechat_redirect)

本篇文章写完会将代码放在github上，想要地址源码链接的小伙伴，可以关注公众号后，后台回复：**爬虫33** 获得源码地址。

PS：本期爬虫案例并**不是最完善**的爬虫，仅为了将爬虫的原理基础介绍清楚。要清楚，爬虫具有时效性，由于现在各大网站都有相关的反爬机制，所以也许现在写的爬虫代码此时适用，但过些时日就可能失效了，这点需要注意。**本章仅供学习参考，请在遵守网络法律前提下进行相关操作。**


### 优化的几点

不幸的是，据说 2019-03-18 熊猫tv就要倒闭了，写上这篇文章也算是对其一个纪念吧，截图留念（今日2019-03-11）。

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIapQmHpWukSOtvNNwmlW3jVmMRMUh6VDwVV4PFkic9hVjAqtaQmNAaK1rJmAVCgrtt99n4kZPrEOSQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

看了上次文章的小伙伴，一定知道基础的信息我们已经可以获取到了，获取的过程中非常轻松，对方网站并没有设置反爬虫的机制。



即使这样，在其他也有不足，来看下结果图：


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQw6Wu3iajiagVng8Lszcogd02c2O6bE9QfddBv90SGUCoxb7iaP7g3ic41sf9ZMXrxGZdRShlbc7OOA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

优化：

有的主播房间热度，后面是带有“万”字的，同时，有些数字后面爬取下来是带有空格的，控制台看到的不太清晰（自己动手的时候肯定会遇到），我们可以用之前学过的知识，对此数据进行相关的清洗，并且对其来个热度排序，分析出最高的热度。

### 枯燥的代码


为了不那么枯燥，笔者直对部分代码讲解思路，具体代码自行观看吧！

**数据清洗部分：**

```python
def __refine(self, list_hot):
    """ 数据清洗, 去空格等操作, 回顾 map 和 lambda 表达式 """
    l_hot = lambda hot: {'nickname': hot['nickname'][0].strip(),
                         'number': hot['number'][0].strip()
                         }

    return map(l_hot, list_hot)
```

使用了 lambda 和 map ，列表中的字典进行了去空格处理，python字符串自带的内置函数strip()，可以完美的将空格去掉！

**数据排序部分：**

```python
def __sort(self, list_hot):
    """ sorted 函数排序房间热度 """
    list_hot = sorted(list_hot, key=self.__sort_seed)
    return list_hot

def __sort_seed(self, hot):
    """ sorted 函数用到的关键词种子 """
    return hot['number']
```

排序部分特意解释下：调用sorted()内置函数，可以对列表中的内容进行排序，但是由于列表中放的是字典类型，所以需要传入 key 作为排序的依据，依据是什么呢？



就是 __sort_seed 方法，而此方法直接将字典中的热度返回作为sorted的排序依据。一般称之为**种子函数**。简单理解就是一个因子！

**数据展示部分：**

```python
def __show(self, list_hot):
    """ 单独对控制台打印展示 """
    for hot in list_hot:
        print(f"{hot['nickname']} ------------ {hot['number']}")
```

运行看下与上篇文章不一样的结果：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIapQmHpWukSOtvNNwmlW3jVSjSmnU46MEMkQ1k7F3f1qvibMuMVshr56IbWd3XChW6mI53xvF9P1Hg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

很明显，展示的结果并不是顺序排列的！但是有规律可言，可以发现，它是根据热度的第一个数字进行了升序排列，继续修改一下：

```python
def __sort(self, list_hot):
    """ sorted 函数排序房间热度 """
    list_hot = sorted(list_hot, key=self.__sort_seed, reverse=True)
    return list_hot

def __sort_seed(self, hot):
    """ sorted 函数用到的关键词种子,对 '万' 进行处理排序 """
    r = re.findall(r'\d*', hot['number'])
    number = float(r[0])
    if '万' in hot['number']:
        number *= 10000
    return number
```

在 __sort 函数中，加了一个 reverse 参数，其可以使结果变为降序。

在种子函数中，需要对匹配到的热度数字进行数据清洗，用正则匹配到数字，并且将数字转为浮点型，如果包含了中文“万”字，则对数字进行一个乘法操作，并将 number 返回。这样一来，最终排序时依赖的就是**浮点型的数字**了。


美化一下打印输出，可以看到如下，已经是排序好的了：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIapQmHpWukSOtvNNwmlW3jVGaTSnX57bVquHd4bgAuBJpiaY5PchNdhYick6h12o8Y6esLgLlibJXwNw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


PS: 若有忘记的童鞋，可以回顾下之前的相关知识点文章：

[python小课堂28 - 进阶必修之匿名函数与高阶函数](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659294&idx=1&sn=cdf311c32639e1b9c0c022fd38dcb8c9&chksm=8c97d2a7bbe05bb1de292ac9d4439bd07d0c77e43a3273b74e19a9aaee5cd5c5ed41a0db396c&scene=21#wechat_redirect)


### 案例中的严重缺点

从本章的代码来看，确实是串联起了之前所学过的各种小知识点，看上去用到了面向对象等思想，实则从爬虫架构的整体性，扩展性考虑，其实非常糟糕。为什么这么说呢？假如你换一个直播网站，例如斗鱼直播，此案例的代码所有相关点都需要修改，并没有什么相关复用性可言。代码架构最好的方式就是抽象，将所有共有的特征以一种形式抽象出来，也就是将不变的代码抽出来写出相应方法，变量作为入参去设计。

### 反爬虫机制

本篇的网站采集并没有涉及到反爬虫的相关机制，对于现在的各大网站来说，反爬虫机制是非常常见的。这里随便说几个常见的：



1. http 请求头相关信息。模拟发送请求，一般常见的网页服务端会对你的请求头进行第一步校验，对于 user-agent 校验， 此处推荐一个好用的 python 库，fake-useragent。 



相关库的安装链接：https://pypi.org/project/fake-useragent/



2. 电脑网络ip限制。爬虫采集时，若你同一ip访问请求过于频繁，服务端采取的措施一般是暂时封掉你的ip，不让你对其进行相关访问，常用解决思路，加大采集信息网站的相应时间，使用ip动态代理池，免费的可以自行去网上搜索，然后将其爬取下来自己使用，例如常见的西刺：



https://www.xicidaili.com/nn/。



3. 登陆验证。例如知乎，你想爬取里面的内容，首先需要进行登录验证，才能访问知乎里面的内容。知乎这个网站是一个高流量的地方，所以反爬机制经常变更，对于登陆时，表单相关信息进行了加密处理，对于这种情况，只能看网上各种大神的反 js 解密思路了，效率低点的可以无脑采用 selenium 等自动化测试框架进行抓取...效率堪忧。



4. 动态数据加载。例如淘宝网，通过普通的请求返回的源码，有些数据并得不到你想要的数据，因为网站利用了 js 动态请求到后台，后台返回信息到前台页面，浏览器进行动态渲染补充到网页上相应位置的。故此类一般是使用抓包工具或者浏览器自带的F12找到相应的后台请求地址，对其进行调用访问，获取到有用的信息并解析。实在不行还有万能的 selenium ，现在的 selenium 也支持了无头机制，同样效率是个问题....



以上，是笔者认为最常见的几种反爬机制，若遇到其它的，欢迎大家留言补充！

### 总结

到这里，原生爬虫篇就到此结束了，通过三篇文章，来总结下爬虫的大体流程：



**1. 明确需求，你想要的信息**

**2. 找到对应的网页，并且利用开发者工具查看网页的相应元素信息**

**3. 根据 python 的请求库（urllib、requests..等）模拟请求网页，获取网页源代码并对其进行数据的解析与提取。**

**4. 提取后，对数据进行相应的清洗，保证数据的准确性。**

**5. 对数据进行相关业务理解，并对其可视化，根据你的思维分析出想要的信息结论。**



在此说下由于熊猫TV马上就要GG了，所以本篇文章后续也许跑不通了，但是其中的细节思路还是可以借鉴的，重要的还是思想！



说句实话，本章爬虫从业务层次没有任何的实际意义，因为你为了看一个直播没必要这么大费周折，还需要先获取下信息热度，再去看吗？有这时间，你自己都够玩一把的时间了！



所以，本系列爬虫篇目的在于，带你了解什么是爬虫，对一个爬虫来说，重要的东西是哪些方面，编程中遇到的问题点，有哪些是可以进行优化的。我们获取到信息后，**又能从中分析出什么有用的信息来，这才是最关键的**！





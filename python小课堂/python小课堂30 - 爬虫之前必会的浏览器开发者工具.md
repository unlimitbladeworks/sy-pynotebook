## python小课堂30 - 爬虫之前必会的浏览器开发者工具

### 前言

本篇要介绍的是开始学习爬虫之前必会的技能 - 浏览器自带的开发者工具，学会了浏览器开发者工具，才能更好的分析出网页相应的内容结构，以及如何使用开发者工具来找出网站中信息交互的请求接口地址。



PS：请求接口地址，小白可以理解为一个网页的地址。此地址是服务器（服务器可以看做配置高点的电脑）专门返回数据用的请求地址，比如我们在浏览器上输入一个地址，回车以后能看到浏览器上返回相应的网页，请求接口地址与之类似，只不过一般返回的都是格式化的数据信息，如 JSON。不懂 JSON 的详见：[python小课堂25 - 你真的了解JSON嘛？](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659204&idx=1&sn=ab145e9567b94ba4994491bf22282ab1&chksm=8c97d17dbbe0586b2aed15b6059850da300906845ba168af8088411ceb0e7ba9cd813e0a2eef&scene=21#wechat_redirect)


### 浏览器的选择

浏览器的选择，特意来说下对于分析爬虫元素的浏览器，笔者常用的3个，分别为：谷歌、火狐、360极速浏览器。



对于浏览器的选择，基本上只要除了微软的 IE 浏览器以外，其余浏览器都可以使用，因为 IE 自带的浏览器开发工具不太好用。这里推荐**谷歌浏览器**。但是作为讲解，笔者这里使用的是360极速浏览器，因为360的浏览器是双核的，既可以用 IE 内核，也可以用谷歌内核，在工作中**兼容性较好**，支持一些只有 IE 能访问的网页。可以放心的是下面讲解的截图虽然是360的开发者工具，但是与谷歌浏览器基本一样，安心观看啦。。。



PS：会了谷歌浏览器的开发者工具，其余浏览器同理。

### 浏览器的开发者工具准备

首先，打开浏览器随意进入一个网页，如百度，按下**F12**后可以看到下图所示：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZWayJjIlQOOdUXictiayA88d6vwibuW3mqqjMMLicd6wxO4DeNvtpyMnlsBzsPPxqVRn0razJ3wvdSvw/640)

也许你看到的框框和笔者的不一样，现在看到的框是默认吸附于浏览器的，笔者更习惯将开发者工具作为单独的一个页面呈现。笔者选择第一个按钮，可以调节如下：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZWayJjIlQOOdUXictiayA88dgoiayolpEHcbqB4Cvq6icFNiaI6e0CK8UO7ZWnftLK8Wgd6qGPfb1N2dw/640)

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZWayJjIlQOOdUXictiayA88dT08rs2I8nlWnwthkZsVvQeMzgkZM5qIIjq7OE9H4fQD9ckMK0RWib4A/640)


### 浏览器开发者工具详讲

调整后，可以看到浏览器上面一排按钮，这里只为了爬虫介绍最常用的前四个按钮，**元素（Elements）**、控制台（Console）、源代码（Sources），**网络（Network）**：


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZWayJjIlQOOdUXictiayA88dZSPqsvvjkuvqTqqicvJV5wB6yg3S0bMZf4NvJZuR1TFULFS4L7nJRNA/640)

标粗的文字（元素、网络）是学爬虫前提必须掌握的选项卡，其余两个了解即可，以下按照掌握程度的优先级进行介绍。

**1. 元素（Elements）**

查看元素代码结构：点击如下图的箭头（或用者用快捷键Ctrl+Shift+C）进入选择元素模式，然后从页面中选择需要查看的元素，然后可以在开发者工具元素（Elements）一栏中定位到该元素源代码的具体位置 。

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZWayJjIlQOOdUXictiayA88djpK3iby6DOq15VnnE6XRh250GOia02J3u3O0G4hSWNREXEYqnQBibDQ1Q/640)

举个栗子，比如想看百度热搜对应的 html 代码，只需要点击此箭头，选择你想查看的文本，鼠标左键点击后，方可在 Elements 中看到对应的 html 代码，如下：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZWayJjIlQOOdUXictiayA88d1LD22zsImicHgibJfRhDqHibQ7gGfaBibZpH34cyj4EW1TB2n6uzfzLAsA/640)

根据文字找出对应代码块，是学习爬虫之前分析的必要阶段，当然这里交小白一个好玩的操作。我们可以对其页面内容进行修改，选中对应页面元素，双击即可修改文字，比如改为下面的：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZWayJjIlQOOdUXictiayA88dwSlv0vqkCibtoP2icTrCCSkTZ1gc1pJibqFqoJKtkWEb7qG2fscmklFug/640)

当然，这里仅限于你不刷新的情况，一旦刷新了页面，其实又回到原来的热点新闻文字了，因为静态页面我们是可以用此方式修改的，若刷新页面，相当于重新请求了服务器一次，所以又变回原来的文字信息了。

**2. 网络（Network）**

点到 Network 选项卡，查看下面图片可以看到最常用的几个功能：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbDutbpHKrxarErdgUkbTuOe5zQ8RCw03q5WNH03xFAZEmLPVoNsZN2wsI3HOIQe4XOZqZq9R37aw/640)

第二行的按钮可以根据网页资源进行网页监控的过滤：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbDutbpHKrxarErdgUkbTuOdGKBgxR7dmibBJqUnn3nPfo081jzMGCnjjT4eniafKUtcvZIufu14I2w/640)

比如选择XHR时，就是所谓的异步请求，比如我们常用的百度翻译，有时候不需要你点击翻译按钮，左侧写完英文后，右侧可以自动翻译出结果，就是因为使用了异步调用的请求方式，如下图：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbDutbpHKrxarErdgUkbTuOicfSic6nBh5rQ1G6ylGLfS6joNfbYpgSibl87CDp7GHtJJAVVNb2GPssw/640)

对于爬虫来说，分析请求服务器的接口异常重要，就拿百度翻译为例，我们可以依次点击这四个请求依次查看其请求内容，直接以 v2tranapi 网页请求为例，先来看  Headers ：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbDutbpHKrxarErdgUkbTuODaIPNEbEavMez2z4ICaQ8defwVryUR7srVdzicxJw8iaumX1qZcCDXWw/640)

其次是 Preview ：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbDutbpHKrxarErdgUkbTuOhzelOd5MQXMMc7yYsjziaGC0gw2bnfcicKjw3HRFyG5W0Iicj0O3T53Og/640)

Response ：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbDutbpHKrxarErdgUkbTuOu3ZAISQ79nlJzGZvibG2bcpiaFibGeKziaHJ0wwdz8OWF8cUStoQaQng4A/640)

还有 Cookies ， timing ，此处详细介绍了，自行了解即可。爬虫必须掌握的就是对网页的分析，而分析网页的元素以及请求接口是学习爬虫之前必要的知识。

PS：多说一句，对于 Cookies 的相关信息，不要随意公布在网上给人看...！Cookies 涉及账号密码，会有安全问题，如果后续有机会，单独开一篇来讲下。

**3. 控制台（Console）**

控制台，类似 Pycharm 中的控制台，编写程序都需要用到控制台，目的是为了便于调试，点击如下，可以看到百度设置的招聘小彩蛋（各大厂都有...）：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbDutbpHKrxarErdgUkbTuOpdOXEqfeEyuylyE0RP6c2XRsKuEGUw7IrU8glTccStbjoGjiaSgEFaQ/640)

了解即可，前端开发人员用到的较多，这里不多介绍了，有需要自己可以搜索相关知识....

**4. 源代码（Source）**

在源代码（Source）页面可以查看到当前网页的所有源文件,如下图：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbDutbpHKrxarErdgUkbTuOz3ria4Zds0Q55I9iaL7pBx4B8ysLNAZicTISI14MLeygAxjLflr9suhJg/640)

在编写前端页面时，可以通过此项进行代码的调试，了解即可。

### 总结

本篇粗略的介绍了一下学习爬虫之前必须要掌握的技能，有些地方没有写的非常详细，笔者认为，F12 必会的就是 **网页元素的选择** 与 **网络中分析接口** ，这两个是**重点**。



至于了解的知识点，大家可以自行百度，网上有许多优秀详细的文章，比笔者这里介绍的要详细得多，本篇目的只有一个，认准学习的目标，突出重点去学习。再次强调，浏览器开发者工具 F12 熟练掌握 **网页元素** 和 **网络分析**，后续学习爬虫才会懂得原理。


---

有想学习交流Python的同学，欢迎关注公号：migezatan(咪哥杂谈)。



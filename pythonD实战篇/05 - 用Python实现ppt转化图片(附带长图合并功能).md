## 用Python实现ppt转化图片(附带长图合并功能)


### 前言

笔者前一阵在学习数据相关的东西，从初学开始，一直在参加社区中的**图表小挑战**，此项活动是社区出题人给出一定官方数据，参加小挑战的人员可以对数据进行可视化，从而挖掘出有趣的信息。



而这个可视化的过程中，用到的可视化工具叫 Tableau ，大家有兴趣可以去查看下，能做出非常美丽的图，之前一直分享在朋友圈里，有些朋友也看到了。



在参与比赛的过程中，笔者遇到一个头疼的点，每次做成的图表拷到ppt中，要想可观的将ppt中的多个图叠在一起生成一张长图，或者单独生成图片，是万万不能实现的！因为。。。WPS自带的功能，很脑残的印上了水印！！就是为了**收取会员费用**。微软的PPT要自己安装插件！



经过百般查找，一些在线网站是支持的，但是要不是遇到了图片限定大小，要不遇到了带水印的！



于是，ε=(´ο｀*)))唉，还是自己动手，丰衣足食一下吧！有了这个想法，用 Python 实现下这个功能！估计也有不少人有此需求吧。。



**在明确需求，确认下目标，其一，可以实现 ppt 每页都生成对应图片。其二，支持将图片进行长图合并。**

### 效果演示

先来看下我的 ppt ，一共三页：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbVnP36lhViaJuibibnId3sSFnhj0xMbj5gNcgEg9TTTl4AiaqJPTFXibzvHBvibg8EPDX3MRfrcOhZ3VsA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


演示效果：

![](https://mmbiz.qpic.cn/mmbiz_gif/E4ianOkSOYIbVnP36lhViaJuibibnId3sSFn9iaMtqiabUvXJFzo3Ioro7VDIAIkPPKHBfFU44jkVJYaibBTfoaFqLuBQ/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

### 核心代码讲解

1. ppt 转 png 方法，利用 win32com 来操作 ppt。这个库的安装在这篇文章介绍过了，感兴趣的可以看下，[用 Python 教你制作查找电脑上隐藏文件的小工具](http://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659560&idx=1&sn=420a1ba051f335ef09639dd613ac0158&chksm=8c97d391bbe05a87db3e6df957785efe9818260d0d1eaea53cdc30d875d0847672a1661aa61a&scene=21#wechat_redirect)：

```python

def ppt2png(ppt_path, long_sign: str):
    """
    ppt 转 png 方法
    :param ppt_path: ppt 文件的绝对路径
    :param long_sign: 是否需要转为生成长图的标识
    :return:
    """
    if os.path.exists(ppt_path):
        output_path = output_file(ppt_path)  # 判断文件是否存在

        ppt_app = win32com.client.Dispatch('PowerPoint.Application')
        ppt = ppt_app.Presentations.Open(ppt_path)  # 打开 ppt
        ppt.SaveAs(output_path, 17)  # 17数字是转为 ppt 转为图片
        ppt_app.Quit()  # 关闭资源，退出

        if 'Y' == long_sign.upper():
            generate_long_image(output_path)  # 合并生成长图

    else:
        raise Exception('请检查文件是否存在！\n')
```

2. 多个单图合并，生成长图，使用了 PIL。

```python
PIL：Python Imaging Library，已经是Python平台事实上的图像处理标准库了。
PIL功能非常强大，但API却非常简单易用。
由于PIL仅支持到Python 2.7，加上年久失修，于是一群志愿者在PIL的基础上创建了兼容的版本，名字叫Pillow，
支持最新Python 3.x，又加入了许多新特性，因此，我们可以直接安装使用Pillow。

廖雪峰官方站
```

在使用 PIL 之前，需要先安装 pillow 。（中文，枕头的意思）

```python
$ pip install pillow
```


```python

def generate_long_image(output_path):
    picture_path = output_path[:output_path.rfind('.')]
    last_dir = os.path.dirname(picture_path)  # 上一级文件目录

    # 获取单个图片
    ims = [Image.open(os.path.join(picture_path, fn)) for fn in os.listdir(picture_path) if fn.endswith('.png')]
    width, height = ims[0].size  # 取第一个图片尺寸
    long_canvas = Image.new(ims[0].mode, (width, height * len(ims)))  # 创建同宽，n高的白图片

    # 拼接图片
    for i, image in enumerate(ims):
        long_canvas.paste(image, box=(0, i * height))

    long_canvas.save(os.path.join(last_dir, 'long-image.png'))  # 保存长图
```

代码没什么可讲的，注释写的贼清楚啦！自行观看即可！

### 结语

在自己"造轮子"之前，其实笔者是查阅了相关资料的，github 上有两个脚本，但是不符合笔者的需求，所以还是又重新造了一遍。。。



本项目可以当做入门，实用的练手小项目，自己写外加调试大概用了一个多小时，即可完成。



老规矩，有想要源码的同学，后台回复**图片转化**， 即可获得。



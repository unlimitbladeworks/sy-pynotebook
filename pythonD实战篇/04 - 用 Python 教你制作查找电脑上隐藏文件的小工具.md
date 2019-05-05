## 用 Python 教你制作查找电脑上隐藏文件的小工具


### 前言

从本篇文章开始，要分享给大家的是一些好玩、有用的东西了，偏向于实战，主要是为了帮大家慢慢建立编程思维，都是使用 Python 来实现的。



昨天晚上跟一个读者聊了许多，他初学的疑惑是看书能看懂，但是自己一上手，依然写不出来代码。



笔者这里对于有这样疑问的初学者给出的建议是，多动手，多练！写代码入门的注重点就是多多练习，真的没有别的快捷方法，光看是没用的，相信每个入门的程序员都是这么一步步过来的....除非你真的是有编程天赋的人，也就是所谓的记忆超群....过目不忘的那种！关于初学者多多练习这一点，不想在啰嗦了....



今天给大家分享的主题是：如何用 Python 实现一个查找电脑文件中隐藏文件的小工具，目的说过了，**简单、实用、好玩，帮大家训练出编程思维。**



下面进入正文。

### 小项目演示成果

在看之前，先要了解 windows 下隐藏文件如何配置：

![](https://mmbiz.qpic.cn/mmbiz_gif/E4ianOkSOYIYFNO21VhEReZCbjiaumJ1J6bXQZibibK9EvicqdDJEAo9PSEf7n94Bjh5Dxp7S1USw0zibcT2sozBbJuw/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)


用电脑干过坏事的小朋友们都知道，隐藏文件的重要性！于是笔者创建了许多许多目录以及自建了几个文件：

![](https://mmbiz.qpic.cn/mmbiz_gif/E4ianOkSOYIYFNO21VhEReZCbjiaumJ1J6k3g1h0vmZp0DxsjSQKXoKgszrXetefvFsbZUsTEBYic5EeSSCBoLJZQ/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)



接下来，有了隐藏文件以后，来看下用 Python 写的小程序，最终达到一个什么样的效果：

![](https://mmbiz.qpic.cn/mmbiz_gif/E4ianOkSOYIYFNO21VhEReZCbjiaumJ1J6FNH3rZibGZQnNyugzdAGS5zxlIkoMibHa1DVFomkdnaQCj4cahnicUVTw/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)


![](https://mmbiz.qpic.cn/mmbiz_gif/E4ianOkSOYIYFNO21VhEReZCbjiaumJ1J6lOpE9D2fTHGEA2ed8D7XClVwoibSrD969ia8ogzZGkgwZpp5bicjzS6NA/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)


![](https://mmbiz.qpic.cn/mmbiz_gif/E4ianOkSOYIYFNO21VhEReZCbjiaumJ1J6kH2ugnKjA2cAa4gYJtPtHkDEUbBU3OfuGDcibq1yGbVh3WuvCJsiaJIw/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)


![](https://mmbiz.qpic.cn/mmbiz_gif/E4ianOkSOYIYFNO21VhEReZCbjiaumJ1J6N89nicZqUuYK0qT9kWCGp80LJcz1PlU1DofVI374NiboJNN0ebXibiabicg/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)


emmm.....大致呢，就两个按钮，一个文本框，你输入地址路径后，然后点击执行，会弹出提示框，是否执行，点是，就会开始扫描你电脑路径下的隐藏文件了！如果没有隐藏文件，只会输出一句，搜索完毕！最终将路径显示在最下面的只读文本框里，可以进行下拉，同时可以对路径进行复制。

### 代码讲解

**1.环境**

首先说下涉及到的 Python 第三方库。涉及到一个pywin32，使用此库可以使 Python 程序方便调用 Windows 的东西。

```python
pip install pywin32
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYFNO21VhEReZCbjiaumJ1J6o108DGpPGQdm1KZ0cuiatKhSMkZCibH89UgNQCCPjs9wvh4QUYiamXzXg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


剩下用到的库都是 Python 内置自带的，所以省事儿！用到的有：

```python

import os  # 对接操作系统的
import win32file  # 安装好 pywin32 后即可 ，操作windows的
import win32con  # 安装好 pywin32 后即可 ，操作windows的
import platform  # 判断电脑系统是什么系统
import tkinter as tk  # 图形化界面的库
```

**2.核心代码**


核心代码一，判断文件是否为隐藏文件：
```python

def is_hidden_file(self, file_path):
    """ 判断 windows 系统下，文件是否为隐藏文件,是则返回 True """
    if 'Windows' in platform.system():
        file_attr = win32file.GetFileAttributes(file_path)
        if file_attr & win32con.FILE_ATTRIBUTE_HIDDEN:
            return True
        return False
    return False
```

判断 windows 文件是否是隐藏文件，先判断电脑系统是否是 Windows ，若不是直接返回 False。



然后用 win32file、win32con 模块进行运算，结果返回非0说明是文件是隐藏类型。



运算的原理则是下图，手机可以点开放大看：


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYFNO21VhEReZCbjiaumJ1J6ibgejPEPaQCHN8elxec39MPeH8P6rsOz2DY3N868FqIrVD3fxfZdt1Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



核心代码二，递归遍历：

```python

def iter_files(self, root_dir):
    """ 遍历文件夹根目录 """
    for root, dirs, files in os.walk(root_dir):
        for file in files:
            file_name = os.path.join(root, file)
            if self.is_hidden_file(file_name):
                self.listbox.insert(tk.END, file_name)  # 将路径填充到 listbox 控件上去
        for dirname in dirs:
            # 递归调用自身,只改变目录名称
            self.iter_files(dirname)
```

使用 os.walk() 可以获得路径的文件夹，以及文件。对多个文件files进行遍历，拿到单个文件进行判断是否为隐藏文件，调用核心代码一；拿到多个文件夹，循环得到单个文件夹，若是文件夹，调用自身即可，这一过程就叫递归。



递归可以理解为无限调用自己，举个栗子，盗梦空间大家看过吧，其中男主比较会玩，电影中涉及到了一层梦境，二层梦境，三层梦境，四层梦境。


四层梦境建立在三层上，三层在二层上，二层在一层上。这其实就是一个递归的过程，一层可以看做最外层，而四层则是最内层，当符合一定条件时，内层梦境则会打破，回到上一层梦境，以此类推。。。



回到咱们的代码中，递归目录时就像盗梦空间一样，只要是目录，则调用自身，直到最底层没有目录，是文件时，则进行文件的处理操作，操作完，返回到上一层目录，以此类推。。。



核心代码就这么两段儿，非常短！~而关于界面的代码就不介绍了，主要就是自己看 tkinter 官方文档，复制粘贴即可，很容易理解。

### 总结

要说这个小项目的实际意义在哪里呢？前面说过了，主要是帮助大家提升自己的编程思维，而对于 Windows 系统的电脑来说，确实是个很 “hack” 的小工具，比如你可以用这个工具专门去快速的获取别人电脑的隐私资料，只有隐私资料，才会被设置成隐藏！至于这个隐私程度，你懂的！~ 具体的隐私文件是什么内容还取决于人嘛~



这个小工具，尚且还不完善，比如系统方面，仅仅支持 Windows 系统，不兼容 Linux 或是 Mac OS 系统，但是当一个练手的小项目足矣！



小工具源码老规矩，放到 github 上了，感兴趣的同学后台回复**找你**，即可获得源码地址。




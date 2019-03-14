## python小课堂17 - 30行代码破解加密ZIP文件

### 前言
今天来点实战干货，想必之前的小课堂中一直在讲基础也会显得非常枯燥，有了前面的相关知识，即可以实现本章内容。若有不懂得的地方，请回顾python小课堂1-16。

在多数人眼中一直觉得黑客很神秘，实际上当初我学python入门时正是因为那会在学安全相关的东西，机缘巧合得以在360和爱春秋联合组织的网课中学到了不少安全相关的知识。很早以前，python就被公认为黑客届的编程语言之一，自身有着强大的第三方库（也就是包和模块的统称）来使用，并且语言上手度非常容易。废话不多说，今天就来演示下如何手写一段python程序来实现暴力破解压缩文件的密码！重点在于编程的思路！

****声明****：本章内容仅供学习记录使用，请勿用于商业以及非法用途！

### 暴力破解的实现思路

利用python内置模块zipfile来实现破解文件，zipfile模块有一种函数，其可以实现将压缩文件路径传入，通过函数返回值去调用提取文件的方法，若文件是加密的且密码传入的不正确，程序则会发生异常(也就是程序报错)。通过这样的思想，我们可以通过读取一个字典文件(字典文件就是包含各种弱密码的一个txt文本文件)，用for循环读取此文件来实现循环尝试。但是python单线程跑比较大的字典文本会非常耗时，所以此程序采用多线程来实现调用。

PS：线程是计算机中的专有概念，举个例子来说吧，比如咱们平时用到的360杀毒软件，它整体作为一个软件被大家使用，而这样的一个独立软件可以称之为进程，当我们使用360杀毒时，在它正在运行杀毒的过程中，我们还可以用它对电脑进行卸载软件，或者清理垃圾等操作，这样在同一时刻，可以干很多事情，就利用到了多线程。一个进程软件下可以同时干好多事情，而线程就是可以干好多事情的“人”。多线程使得计算机程序的运行效率大大提高，减少了我们平时使用时候的耗时。

### 破解密码效果演示

<font color = gree> 1. 自己建立一个加密的zip文件，密码自主设定。

我们将一个文本文件进行加密，将其压缩成zip文件。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181216181616588.gif)


<font color = gree> 2. 打开命令行，执行py脚本。

我这里命令行用的是git bash shell，这是一种windows下的类linux命令行，非常好用，兼容所有linux命令，装了git的同学用了都说好！！~

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181216181701987.gif)

可以看到有个进度条，进度条前面走的数字就是每个行密码都去开一个线程，字典一共200W行，在读取到2W多行时将密码破解出来，接下来手动停止程序即可。


<font color =gree>3. 关于zip加密若不正确

这里要说下，正常情况下，一个加密的zip文件，即使你输入错误的密码也是能用压缩文件打开的，只不过相应的文本文件是被加密的。所以，通过手动方式去解压加密zip文件，即使是错误密码也可以提取到原文本文件，只不过是乱码罢了，如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181216181729583.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

###  代码的实现讲解

<font color =gree>1. 命令行函数代码
```python
# 第一行通过调用optparse的函数创建一个parser的实例化对象
parser = optparse.OptionParser('\n  %prog -z <zipfile> -d <dictionary>')
# 第二行添加一个参数，在命令行上输入-z xxxx 可将命令行上的zip路径作为字符串传入到变量zname中
parser.add_option('-z', dest='zname', type='string', help='specify zip file')
# 第三行添加一个参数，在命令行上输入-d xxxx 可将命令行上的字典文件作为字符串传入到变量dname中
parser.add_option('-d', dest='dname', type='string', help='specify dictionary file')
# 第四行进行解析，得到相关参数，得到options。
options, args = parser.parse_args()
# 第五行，通过zname和dname判断是否传入的参数为空
if options.zname and options.dname:
    zip_name = options.zname
    dict_name = options.dname
else:
    print(parser.usage)
    exit(0)
```

<font color =gree>2. 多线程函数代码
```python
# 通过try-except来抓取运行程序时的异常，若报错，说明传入的文件不存在
try:
    # 调用zipfile模块的实例对象方法，将zip路径传入
    zip_file = zipfile.ZipFile(zip_name)
    # 打开字典文件，用python自带的with关键词来打开，可以交由python自主关闭文件的资源
    with open(dict_name, 'r', encoding='utf-8') as f:
        # 读取每一行，并且将密码后的\n 清空，也就是清空换行符
        for line in tqdm(f.readlines()):
            password = line.strip('\n')
            # 对每个密码开启线程去处理，调用extract_file函数，传入的参数为元组(zip_file, password)
            thread = Thread(target=extract_file, args=(zip_file, password))
            # 调用线程开始的方法
            thread.start()
except Exception as e:
    print(f'发生异常！请检查文件是否存在！异常信息为：{e}')
```

假设我输入了错误的文件名称，可以看到报错！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181216181836508.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

<font color =gree> 3. 调用zipfile模块的核心代码

这里的核心代码便是多线程调用时触发的函数。

```python
def extract_file(zip_file, password):
    """ 提取压缩文件，通过密码不断尝试 """
    try:
        zip_file.extractall(pwd=bytes(password,'utf-8'))
        print(f'\n  发现密码，正确密码为：{password}')
    except:
        pass
```

### 代码中额外的知识点

<font color=gree>1. 安装python第三方库(python的强大之处，就是很多好用的第三方库，人为封装写好的包和模块，直接拿来用即可！)


为了我们方便读取文件是看到相关进度，所以这里额外安装了第三方库tqdm，一个非常好用的进度条库。tqdm在阿拉伯语中表示“progress”，而在西班牙语中则是“I love you so much”的缩写。


介绍一个python第三方库的官方网站：https://pypi.org/

这个网站有各个模块官方的安装命令以及文档，比如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181216181933855.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

在之前的小课堂中，如果你配置好python的环境变量，打开命令行是可以直接进行安装的，只需执行命令```pip install modal name```即可,如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181216181947875.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

因为我已经安装过了，所以会这样提示。若没安装过，可以看到有下载的进度条，最后安装完会显示success。



<font color =gree>2.  optparse、zipfile、tqdm模块的简介

optarse：这是一个python自带的库，通过上面介绍的代码可以和linux命令似的，带参数执行。举个例子，如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181216182011278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

zipfile： python自带的库，可以对zip文件进行解压缩，本章实现的重点模块，需要注意的是，在用extractall时，传入的字符串密码进行字节编码的转化。```zip_file.extractall(pwd=bytes(password,'utf-8'))```

关于解压出来的文件名字会有乱码的情况，请看文章：
https://www.cnblogs.com/limengjie0104/archive/2018/06/17/9192449.html


tqdm：需要安装的第三方库，在可以循环迭代的对象上使用即可。如：
```for line in tqdm(f.readlines()):```

### 爆破字典的项目

爆破字典的开源项目，其中收录了不少相关的密码，可以star 或者 fork到自己的仓库记录使用。地址如下：
https://github.com/rootphantomer/Blasting_dictionary



本篇文章的完整代码地址如下：
https://github.com/unlimitbladeworks/python-tools/blob/master/hack/zip/zip_hack.py
至此完！

<hr/>

有想学python的同学，欢迎关注公号：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181216182145450.png)
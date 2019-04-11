## python小课堂39 - 用 with 优雅的读写文件
### 前言

本篇来介绍一下 Python 中的关键词 with 的小技巧。但是在了解 with 之前，需要先了解一下如何使用 Python 对文件进行读写操作。



在了解基本的文件读写操作后，在使用 with 对其进行优雅的操作。写出符合 Pythonic 的代码。

### 对文件的读写操作

**1. 读文件**

> 在 Python 中，有一个函数 open ，就像英语中描述的一样，具有打开的意思，先来看下函数详情：
> 
> open(name[, mode[, buffering]]) 
> 
> 
> 
> name : 一个包含了你要访问的文件名称的字符串值。  
> 
> 
> 
> mode : mode 决定了打开文件的模式：只读，写入，追加等。所有可取值见如下的完全列表。这个参数是非强制的，默认文件访问模式为只读(r)。 
> 
> 
> 
> buffering : 如果 buffering 的值被设为 0，就不会有寄存。如果 buffering 的值取 1，访问文件时会寄存行。如果将 buffering 的值设为大于 1 的整数，表明了这就是的寄存区的缓冲大小。如果取负值，寄存区的缓冲大小则为系统默认。
> 
> 菜鸟教程

首先，在 py 文件的同目录下创建一个1.txt的文本，对其进行读取：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbKd73dw4GKJMrJxzv7E6iaiaeUlZVdnJXKYADrWZOTNvYkhXTTr5uqfRIbXRmTXAjMmbc9IfN2ggIQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


只需要，两行代码，即可操作文件：

```python
f = open('./1.txt', 'r', encoding='utf-8') # 获取文件对象
print(f.read())  # 读取文件内容
f.close()  # 释放资源
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbKd73dw4GKJMrJxzv7E6iaia8xbJzZmf5xwsCRRUgZ2VYow17FB6UjbGf2r4LkHq8ibWegbJpIaz85A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

解释下代码，通过 open 函数获得到一个文件对象，其中第一个参数传入文件路径，第二个参数使用 ‘r’ (read) 模式，第三个参数是使用utf-8 编码进行文件读取。读取完成后，需要关闭资源。



**注意**：如果你指定的文件路径不存在，则会报错 ```IOError``` 错误，可自行尝试。


**2. 写文件**

写文件，只需要改变模式参数即可，其余参数不需要改变，代码如下：

```python

f = open('./1.txt', 'w', encoding='utf-8')  # 写文件
f.write('abdc')  # 具体什么内容写到文件
f.close()  # 关闭资源
```

写完后的结果：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbKd73dw4GKJMrJxzv7E6iaialgzprOzDpIoa3VL7qEEyarCVkkq6IHXibbmMgdsa7yKIfX7rVyQjwSA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


写完后，可以发现，新内容将原来的中文覆盖掉了。所以若想在源文件后追加，可以将 'w'(write) 改为 'a'(append) 即可。



关于具体模式参数，可以自行查阅菜鸟教程，或者通过 Pycharm 按住 Ctrl 点击鼠标左键，看查 open() 函数中的源码注释来使用，故不作详细介绍了：
![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbKd73dw4GKJMrJxzv7E6iaia4Tn9QrOMNHp5vIIU8AoYypkZorBhicLfKd0xMn6V7JEKjJZAxx2Cw2Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**3. 读写文件异常处理**
关于操作资源类的代码，需要注意的是必须要对资源进行释放，比如读写文件，在使用完毕后必须关闭，因为文件对象会占用操作系统的资源，并且操作系统同一时间能打开的文件数量也是有限的，所以你会看到上述代码中，需要用 f.close() 进行关闭。



对于读写文件来说，非常容易发生 ```IOError``` 这样的异常，改进下代码，正常写法：

```python
try: 
    f = open('./1.txt', 'r', encoding='utf-8')
    print(f.read())
except Exception as e:
    raise e      # 抛出异常
finally:
    if f:
        print('file close')
        f.close()
```

使用 try - except - finally 语句来捕获异常，若有异常进行抛出，无论是否有异常，最终将文件对象进行关闭。



可以自行制造一个异常来检验下，最终是否会走入 finally 中：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbKd73dw4GKJMrJxzv7E6iaiad3PB6riatYfPHFMsDukuJFcYlTu7e2yYpJicibctvYQpuEDSelJLYPenA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


手动制造一个 1/0 的错误，可以看到，即使程序发生了异常，最后的代码也会走入。

### 使用 with 优雅的操作文件

以上正常的写法，大家有没有觉得有一种冗余的感觉，并且每次这么写会非常麻烦，一点也不符合 Python 的简洁特点。人生苦短，我用 Python，这句话不是白说的！所以 Python 提供了一个 with 关键词可以自行管理资源，比如在程序结束后，自动关闭文件资源。

代码写法：

```python

with open('./1.txt', 'r', encoding='utf-8') as f:
    print(f.read())
    
# 控制台输出
>>> abdc
```

仅仅两行代码，实现了 try - except - finally 的方法， 使用 with 对文件对象进行 as 别名处理，具体逻辑中，操作 f 即可，最终 with 会帮我们调用资源关闭的方法。

### with 背后的工作原理

with 背后的工作原理，要涉及到两个 Python 的魔术方法(Magic method)了，__enter__() 和 __exit__()。在 Python 中，任何对象实现了这两个魔术方法，都可以被称作上下文管理器。而正是这样的管理器，来使用 with 关键词实现代码中的简洁编写。



下面来看个例子，我们可以手写一个类似文件对象的类，封装 open 函数：

```python
class MyOpen:

    def __init__(self, filename, mode, encoding):
        """ 对象初始化,传入路径,模式,编码 """
        self.filename = filename
        self.mode = mode
        self.encoding = encoding

    def __enter__(self):
        """ 准备工作 """
        print('----- Connect File -----')
        self.f = open(self.filename, self.mode)
        return self.f

    def __exit__(self, exc_type, exc_val, exc_tb):
        """ 退出工作 """
        print('----- Release File ------')
        self.f.close()

with MyOpen('./1.txt', 'r', encoding='utf-8') as f:
    print(f.read())
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbKd73dw4GKJMrJxzv7E6iaiaBOiaygHiatSFfHiaDWew4k0oN8o9JaiaeSF06MsictCxMN1ebcMrS2870tA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


使用 with 关键词创建自己的类时，相当于在 enter 函数中，封装了 open 函数方法，将 open 函数实例化对象进行返回，便是 as 得到的实例对象 f，然后调用 f 文件对象的 read 方法，最终程序结束，文件资源被释放。



假设，在 enter 返回时，我们不返回文件对象 f ，而返回的是 self ，也就是 MyOpen 的实例对象，那么结果会怎么样呢？



![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbKd73dw4GKJMrJxzv7E6iaiaBsUcFJLQo0O7drKECEW4H4fzTWiaKmtIH4fyQpeFjPm9XVG2BFcb02Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


看到了，因为 MyOpen 类根本没有 read 的方法，所以此时， as f代表的含义是 MyOpen 的实例对象，意味着 **enter 的返回决定着 with ... as ... 生成什么样的实例对象。**

改一下的结果：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbKd73dw4GKJMrJxzv7E6iaiabic2dKEaFibQbEr4Mm7w2DGfhqMgEibvg2NbicBzxKIicia20Rsiaa2gzWTMw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

再多思考一下，如果发生异常会是怎样的呢？依然是手动制造一个异常，1/0 即可，同时在 exit 中还有三个参数，分别打印看下结果：

```python

class MyOpen:

    def __init__(self, filename, mode, encoding):
        """ 对象初始化,传入路径,模式,编码 """
        self.filename = filename
        self.mode = mode
        self.encoding = encoding

    def __enter__(self):
        """ 准备工作 """
        print('----- Connect File -----')
        self.f = open(self.filename, self.mode)
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        """ 退出工作 """
        print('----- Release File ------')
        self.f.close()
        print(f'exc_type:{exc_type}')
        print(f'exc_val:{exc_val}')
        print(f'exc_tb:{exc_tb}')


with MyOpen('./1.txt', 'r', encoding='utf-8') as myOpen:
    1 / 0
    print(myOpen.f.read())
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbKd73dw4GKJMrJxzv7E6iaiax5EPggWpkWRHzacd4Cnicm2DicXtic6EAfNdzx54P16QTBMrgmDdxjyIw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


先来看，即使发生了异常，我们的资源还是被成功释放了，符合了 with 关键字发生异常时会自动关闭的机制。



其次，打印出的 exit 函数中的三个参数，分别是 异常类型、异常值信息，还有 traceback (异常堆栈)。但是若不发生异常，这三个参数则都是 None ，可以自行尝试把异常抹去后，看看打印结果。



额外说的一点，关于 exit 函数的返回值，决定着是否向外抛出异常，什么意思呢？来看下面代码示例：



```python
class MyOpen:

    def __init__(self, filename, mode, encoding):
        """ 对象初始化,传入路径,模式,编码 """
        self.filename = filename
        self.mode = mode
        self.encoding = encoding

    def __enter__(self):
        """ 准备工作 """
        print('----- Connect File -----')
        self.f = open(self.filename, self.mode)
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        """ 退出工作 """
        print('----- Release File ------')
        self.f.close()
        return True


try:
    with MyOpen('./1.txt', 'r', encoding='utf-8') as myOpen:
        1 / 0
        print(myOpen.f.read())
except Exception as e:
    print(e)
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbKd73dw4GKJMrJxzv7E6iaiaCjWSNNjRqGlNLkxUqyibDlbianKlXAI7nyS0tp6QaLicnoplyoVd0PsgQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


通过手动制造一个错误，使 exit 返回 True，可以看到，在 with 处捕获异常，没有打印出异常。说明 **exit 的返回值控制着 with 语句发生异常时，是否抛出异常。默认 exit 返回值是 None，而 None 在 Python 中的值就是 False。所以默认情况下，有异常时，控制台会抛出异常提示。**

### 总结

在对文件进行操作时，使用 with 这种 pythonic 的方式来代替 try - except - finally，省时经济又实惠，而 with 背后的工作原理则是 Python 上下文管理器的 2 个魔术方法上的实现。在我们日常写操作资源类时，为了达到优雅的方式，不妨用上下文管理器的来实现自定义类，最终使其达到 pythonic 风格！


## python小课堂29 - 进阶必修之装饰器

### 前言

装饰器(Decorators)是 Python 的一个重要部分，通俗的说：它们是修改其他函数的功能的函数，使用装饰器有助于让代码更简短，也更 Pythonic（Python范儿）。大多数初学者不知道在哪儿使用它们，跟随笔者的步伐来看下装饰器如何使用吧！



PS：装饰器和闭包一样，并不是说少了装饰器对于Python编写代码来说就不能完成相应的需求功能了，装饰器是在编程中的设计模式中抽象出来的一个重要思想，许多框架都使用到了装饰器。

### 装饰器的定义

在这里，笔者首先不会直接给出装饰器的定义，因为它本身的含义就很抽象，并不像上一次介绍的高阶函数，了解入参和结果就能使用了。依然遵循老规矩，采用 **场景** + **示例**  的模式一步步推导出装饰器的定义来。



**场景1**：假设现在有一个函数，这个函数里面什么也不干，仅仅是让它休眠2秒，现在的需求是，如何才能不修改原有函数的基础上，直接对原来的函数增加一个打印耗时的功能呢？（实际上这是写出良好代码的设计原则，之前有提到过，开闭原则，对修改是封闭的，对拓展是开放的，非专业人员混个眼熟啦~）思考尝试想一下或者写一下试试，再看下面的程序：

```python

import time


def sleep_func():
    time.sleep(2)


def time_spend_func(func):
    before = time.time()
    print(f"开始执行前时间:{before}")
    func()
    after = time.time()
    print(f'开始执行后时间:{after}')
    print(f'耗时时间：{int(after - before)}s')


time_spend_func(sleep_func)
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7p2cmzlDa1lViaYLXcmBicFSHUpskrMjqjic0vicYys3Rf6zZmq3ibibiaMVCZg/640)

**推导步骤1**：

讲解一下上面的程序，使用 Python 自带的 time 模块，我们可以调用 sleep 方法让程序休眠，参数是以秒为单位，可以自行 Ctrl 点进去看下官方注释。

在场景设定下，不修改原来的代码，想看原来的函数一共耗时多少，所以可以新增一个专门计算耗时的函数，姑且称之为 time_spend_func 。在其里面使用 time.time() 方法可以得到当前时间的时间戳形式。（时间戳 timestamp ，一个能表示一份数据在某个特定时间之前已经存在的、 完整的、 可验证的数据,通常是一个字符序列，唯一地标识某一刻的时间。）

可以看到最后调用新增程序时，笔者将原有函数以参数的形式传入了计算耗时的函数中（这点在闭包时已经介绍过了，详见 [小课堂26-进阶必修之闭包](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659222&idx=1&sn=65fdcccb09cef1d2b441a6810b1cdf32&chksm=8c97d16fbbe05879798d95303b8608aa6b1ef17b31c702c8bb39768d2b4335732731759fe08b&scene=21#wechat_redirect) ）。传入原有函数的目的，是为了在新增函数中调用原有函数的逻辑，也就是睡上 2s。

最终耗时的具体时间，通过时间戳的数字进行减法得到的是 float 型，将之转为数字整型即可显示最终耗时结果。

这样的实现方法是没有对原有函数进行修改的，虽然确实符合场景设定，但是它本身是存在缺点的！大家可以想一下，新增函数所实现的功能确实属于新增功能，但这个功能原应该“依赖”于原有函数，这句话怎么理解呢？**消耗时间这个动作是属于原有函数本身的，而现在的新增函数是在调用原有函数的前后强制新增了一段记录时间的代码**。


如果还不能理解，来看下上面的写法和下面的写法有什么不同吗？

```python
def sleep_func():
    time.sleep(2)


before = time.time()
print(f"开始执行前时间:{before}")
sleep_func()
after = time.time()
print(f'开始执行后时间:{after}')
print(f'耗时时间：{int(after - before)}s')
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7pG5kwP9ib3zib1eVWVMqLyPdB7DNXf6a5KElD8768xek5w8Hax0Ut93ZQ/640)

无非就是取消了函数的写法，强制在调用原函数的前后加上了时间的逻辑！



好好体会一下，明白了以后，我们可以通过**装饰器**来解决这一缺点，使新增功能原本就属于原有函数，继续看推导2。



推导步骤2：



接下来看下 Python 中的装饰器如何书写呢？

```python
def decorators(func):
    def wrapper():
        before = time.time()
        print(f"开始执行前时间:{before}")
        func()
        after = time.time()
        print(f'开始执行后时间:{after}')
        print(f'耗时时间：{int(after - before)}s')
    return wrapper

def sleep_func():
    time.sleep(2)

f = decorators(sleep_func)
f()
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7pkXd0j6ajRFqQjJuMT16g5ke6xIlfISO4icIgibBePKBhKMux3lDWeT2g/640)

先仔细看一下代码，decorator 是装饰器的意思，wrapper 是包装的意思。看完代码的同学，乍一看结构是不是与之前提到的闭包结构非常相似！只是少了一个所谓的“环境变量”....



解释一下这段代码，定义一个外层函数 decorator 装饰器，内层函数定义一个 wrapper 的包装函数，其中外层函数接受外界传入的函数作为参数，并且在内部函数 wrapper 中进行调用，而其余的打印耗时的逻辑依然没有修改。



这么一看，肯定有人会有疑问，这样的写法意义在哪里？最终调用还是和推导1一样，调用装饰器函数，并且将具体的休眠函数作为参数传入，最后还多出一步f的调用。没错，如果你想到了这里，恭喜你，说明走心了！这样的写法确实不是最完美的，笔者写到这里仅仅是**定义了一个装饰器**而已，但是并没有使之起到**装饰**的作用，下面继续看推导3。


**推导步骤3**：



有了前两步的推导，第三步就是要介绍一下Python的语法糖了！

> 语法糖(syntactic sugar)是指编程语言中可以更容易的表达一个操作的语法，它可以使程序员更加容易去使用这门语言：操作可以变得更加清晰、方便，或者更加符合程序员的编程习惯。

在Python中，通过 @ 符号来表示装饰器！而 @ 则是Python的语法糖之一，具体用法如下，终极装饰器的示例：

```python
def decorators(func):
    def wrapper():
        before = time.time()
        print(f"开始执行前时间:{before}")
        func()
        after = time.time()
        print(f'开始执行后时间:{after}')
        print(f'耗时时间：{int(after - before)}s')

    return wrapper

@decorators
def sleep_func():
    time.sleep(2)

sleep_func()
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7pXCckFGKIo8kcUFGxLqUxxp3ibjXXnp9xibyAZkJBpMsVEhiaECREnopMg/640)

解释一下代码，在推导2的基础上，只需要将 @装饰器函数的名称 加在原有函数的“头上”，便可完成所谓的装饰器装饰，最终调用原有函数即可执行。看到这样的写法，知道为什么叫装饰器了吧~因为是装饰在原有函数的“头上”来做装饰物的呀！[罒ω罒]......



了解Java的人可能见过这样的写法，这种写法在Java中被叫做注解。但是意义却与Python中的装饰器截然不同。



推导了三个步骤，最终带出了装饰器的定义，大家有没有看出来最终装饰器的好处呢？下面来说明一下：



**1. 使用类似闭包的方式来定义装饰器，通过 @ + 装饰器名称 来装饰已有函数。**



**2. 装饰器的好处，符合了开闭原则，不用修改原有代码，只需新增。**



**3. 终极装饰器的写法，不会改变原有函数的调用，原来怎么调用，加上装饰器后依然可以使用原来的方法调用，此处指 sleep_func() 的调用。**



**4. 装饰器还起到了代码复用的作用，因为一个装饰器是可以修饰多个函数的。**


### 装饰器多参数

在上面提到了装饰器还有代码复用的作用，来看下具体示例就会明白为什么这么说了，场景如下：

在推导1~3的场景下，假设我们的 sleep_func 函数休眠时间是由外界传入的，而非固定值，如何修改下推导3中的装饰器呢？

```python
@decorators
def sleep_func(seconds):
    time.sleep(seconds)
    print(f'休眠函数休眠时间：{seconds}')
```

修改休眠函数，如上，然后直接调用，来看下结果：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7pFvGz8OE8YIiaYicIxTzm91gG0BNnYA6riaribnhFfNfUUwLkiazn4PBRlow/640)

可以看到，报错啦，错误信息大概意思是 wrapper() 必须给定一个参数，因为我们调用的函数传入了一个参数3秒，所以在装饰器中的内层函数需与之同步，修改为如下代码：

```python
def decorators(func):
    def wrapper(seconds):
        before = time.time()
        print(f"开始执行前时间:{before}")
        func(seconds)
        after = time.time()
        print(f'开始执行后时间:{after}')
        print(f'耗时时间：{int(after - before)}s')

    return wrapper

@decorators
def sleep_func(seconds):
    time.sleep(seconds)
    print(f'休眠函数休眠时间：{seconds}')

sleep_func(3)
```

在 wrapper 函数以及内部调用的 func 两处同步加入 seconds 形参，再次调用:

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7pCV6awiatHEtwFdLj5iaAVqre9lYuibjG7oJumric7GGhTSiaibbs8QYXaib6w/640)

但是这样的写法太死板了，一点也不灵活，假如在 sleep_func 函数中，业务逻辑变了，其中有多个参数传递，那装饰器中岂不是也要修改无数次了？而且每对应一个函数，不同参数个数就需要新建一个装饰器，何谈代码的复用？！

所以，多参数的情况依然可以进行完善，使之达到一个通用的状态。这里要普及一个Python小知识点了，知道这两个小知识点后对后续写出灵活性代码非常有用！


### *args 和 **kwargs 的妙用

举两个小例子，一看便了解Python中这两个写法的用途了！

**1. \*args 用法**

```python
def print_words(*args):
    print(type(args))
    for word in args:
        print(word)

print_words(1, '呵呵', True, 1.02333)
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7prLOFkrMKrvMZv1IU6iahhRLxicP7pKRbMWibEUwrbD2XOmAOiaeckvrZNw/640)

在定义函数时，可以使用 **\*args** 作为形参，代表着可以接受无穷多个参数，以上面为例，可以看到在定义得打印函数中，调用时传入了各种类型的参数，最终通过 for 循环遍历打印，可见  **\*args** 本身类型是一个 **tuple** 类型。需要注意的是，这里的写法 **\*** 是必须的，**args** 作为形参名称，可修改。


**2. \*\*kwargs 用法**

```python
def print_words(**kwargs):
    print(type(kwargs))
    print(kwargs)

print_words(a=1, e='呵呵', f=True, b=1.02333)
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7pRGOV6EpZz2ra3IK9KKTtoRlHlgRLYcaDEblvC5m9Gwuia0xk8TrK0PQ/640)

**kwargs，之前的基础篇讲过关键词参数，详见：[python小课堂16-函数篇](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659045&idx=1&sn=462606dd90fce0b8422708bc6e6cd04a&chksm=8c97d19cbbe0588ac689253df0544df65f3bc2be9741164dd80320dd0553010e8a608d0b8cb5&scene=21#wechat_redirect)。

而此种写法作为形参传入，最终实参调用时，传入到函数内部解析之后其实就是字典形式，关键词作为字典的key，值则作为 value。


**3. \*args 和 \*\*kwargs 混合使用**

```python
def print_words(*args, **kwargs):
    print(type(args))
    print(args)
    print(type(kwargs))
    print(kwargs)

print_words(1, 23, 4, '----分割线----', a=1, e='呵呵', f=True, b=1.02333)
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7pjtZyHXE4E82mqhBRpHTibKia5IBGreNH464AemdMe86CVMgEk8wWTfYg/640)

混合使用，效果更佳！这样定义函数的形参非常灵活，可以看到许多第三方库的底层都是利用了这样的写法。。思路拉回到正题，认识到这种写法的好处，将之用到我们的装饰器中去。

### 装饰器最终灵活版

用到我们的装饰器中去。示例代码如下：

```python
def decorators(func):
    def wrapper(*args, **kwargs):
        before = time.time()
        print(f"开始执行前时间:{before}")
        func(*args, **kwargs)
        after = time.time()
        print(f'开始执行后时间:{after}')
        print(f'耗时时间：{int(after - before)}s')

    return wrapper

@decorators
def sleep_func(seconds, a, b, **kwargs):
    time.sleep(seconds)
    print(f'休眠函数休眠时间：{seconds}')
    print(a, b)
    print(kwargs)

sleep_func(3, '我是a', '我是b', c='我是{"c":"c"}', d='我是{"d":"d"}')
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7pXviaUIJZYQX6M0oDOYpqE3QW49sIibaib1EVMDavQfziao3KOzDbZFgGeA/640)

注意标记红框的位置，在调用 func 时，传入的都是带星号的形参，只有使用时才将星号去掉！不要记混啦，建议多多练习！写到这里，最终完美版的装饰器也就诞生了，整篇下来通过一步步的推导将装饰器梳理了一遍！在说最后一句，什么叫做可以复用的装饰器，在上面的基础上在多加一个新的函数，使用相同的装饰器：


```python
@decorators
def sleep_func_new(words):
    print(words)
    time.sleep(1)


sleep_func_new('调用了sleep_func_new')
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7pbcm31R5GTdcNCY2cqtnY46y3W42403PwE0kZrzE80O66Y36QKkV4bw/640)

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZyosnSL6snoSTfFM22Pt7pibHnJibiahaXOMzmCGWeD9IyHq1bL2zQ8ES4VkVjFHf1NhC97VWv5xsZA/640)


### 总结

感觉一写技术文章，不知不觉就超长了.....又是一篇非常详细，非常长的文章，目测上千字啦，学到这里，关于Python的基础与进阶基本上告离段落了，大家看了笔者的文章有木有成长一些呢？从开文到现在，无论是从文字功底还是文字的排版，对于笔者而言都有不少进步，通过各大平台推广，每天公众号的后台人数也在一点点增加，只要有读者看，就是继续写下去的最大动力！



接下来的文章跟实战挂钩了，将之前所有知识点串联在一起最好的方式就是通过实战去训练，而学习Python最有趣的就是关于爬虫的知识了！下一章通过爬虫带你快速入门，串联所有学过的知识以及网络信息采集的开篇！敬请期待....


 








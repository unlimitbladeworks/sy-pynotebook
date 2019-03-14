## python小课堂28 - 进阶必修之匿名函数与高阶函数


### 前言

嗨！大家好哇，一星期没见了，后台收到朋友的留言以为我停更了....哇哈哈哈时间永远留不住，在春节期间，拥有这么多空闲时间的你，有木有好好充电呢？让我们继续回归python小课堂之路，本章为进阶篇，介绍的是匿名函数与高阶函数。


### 匿名函数之 lambda 表达式

见名知意，所谓的匿名函数就是没有名字的函数。我们平时所写的函数都是带有名字和参数的，并且有返回值，而匿名函数的写法却非常简洁，对于初学者而言，代码的阅读性可能会较差一些，但是多加实践，看习惯了之后就能明白所谓的lambda表达式是什么意思了！接下来还是用示例说话，场景是这样的：有个函数，传入两个参数a和b，在函数内部将他们做差，并将结果返回。

**示例1 - 普通函数：**

```python
def sub(a, b):
    return a - b

result = sub(1, 2)
print(result)

>>> -1
```

**示例2 - 匿名函数：**

```python
sub = lambda a, b: a - b
result = sub(1, 2)
print(result)
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3TL8hjicBslkf0iacvKpT84djlrlVRg3Ve6dgPjd3ffRLQsiaEicsRIATE9Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

解释一下上面的案例，使用 python 中的 lambda 关键词来定义匿名函数，参数在冒号前面，表达式在冒号后面，将整个 lambda 表达式赋予一个变量sub，通过调用sub传入参数得到结果result，与普通函数得到一致的结果。

匿名函数的写法，通过关键词 lambda 来表示匿名，基于数学中的λ演算得名。lambda表达式完整的写法公式如下：

```python
lambda parameter_list : expression
```

什么意思呢？通过 lambda 后面跟上传入的参数，加上冒号，以及冒号后面的表达式组成了匿名函数，注意：**冒号后面一定要是表达式！**


表达式意味着，如果我们写成赋值语句或者for循环语句等非表达式语句，那么 lambda 表达式则会报错！如下：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3T0Qbdoh3sar8FCnKiafiabE41hIcujkqVGGeCBib5lWEeJAoIJ0qfdtMTQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


所以由此引出了匿名函数 lambda 中常用的**三元表达式**。


**示例3 - Python的三元表达式：**

假设现在有两个变量，a = 1，b = 2，请使用一行代码来判断 a 小于 b ，若 a 小于 b 为真，则将 a 的值返回。

```python
a = 1
b = 2
result = a if a < b else b
print(result)
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3T9iaNqkHfHdKH9HQRRYbOWrQdyJBn383XNHz86DumOV2dyFFuicDwX0Cw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

result 这一行就是所谓的 Python 中的三元表达式，用中文描述一下就是：

```python
条件为真时返回的结果 if 条件判断 else 条件为假时返回的结果
```

### 高阶函数

高阶函数，Python中自带了一些高阶特性的函数，在某些特定场景下非常实用，这里举几个常用的，当然也会结合具体场景去说，毕竟要结合使用不能滥用！

**1. map 函数**

map 函数，map中文意思是地图的意思，但是在程序中代表映射的意思。高中学过的映射，不知大家是否还记得！跟那个意思差不多。。。



场景如下：现在有一个 list_a ，它其中的包含着 1~6 的数字，请将此集合中的数字都乘以 2 ，最终得到的结果组成一个新的 list_b。

```python
list_a = [1, 2, 3, 4, 5, 6]
xxxxx
得到 list_b 
```

不使用 map ，你会怎么做呢？思考一下，然后再看下面的答案：

```python
list_a = [1, 2, 3, 4, 5, 6]
list_b = []

def double_fun(a):
    return 2 * a

for a in list_a:
    list_b.append(double_fun(a))

print(list_b)
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3TkicgGicTrO81DDwJobMT4gNwLWPeiaG3q5uAbEt7BgNup9B6SbMibhC6WA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

通过 for 循环取出 list 每个值，在对其调用乘2的函数，最后将结果进行拼接，得到 list_b 。

使用 map 函数之前，先了解下 map 函数语法：

> map(function, iterable, ...)

> map() 会根据提供的函数对指定序列做映射。
> 第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表。

```python
list_a = [1, 2, 3, 4, 5, 6]

def double_fun(a):
    return 2 * a

result = map(double_fun, list_a)
print(result)
print(type(result))
print(list(result))
```
![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3TzwXd3JquV33eqfh6oWAFRWdNz00gzjkhWwGpW8ZrDibIuVAm5ydcYUQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，素质三连print！得到的结果，map返回的结果是一个 map 对象，而它本身的类型就是 map，将其转化为 list，可以得到与不用 map 函数时的一样结果！



实际上，如果会活学活用的话，还可以将上述代码进行缩减，用我们刚学过的 lambda 表达式来完成！

```python
list_a = [1, 2, 3, 4, 5, 6]


# def double_fun(a):
#     return 2 * a

result = map(lambda a: 2 * a, list_a)
print(list(result))
```

将普通函数注释掉，使用匿名函数来完成，实际上就3行代码即可完成，如下：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3TONFnvYsmd3ibAqJKVYkhHE0PNwrDibuQ8gEO7I26wicGs6uzkr3G2aBibg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

如果有多个参数作为匿名函数的入参如何写呢？

可以使用 pycharm 自带的源码查看功能，查看 map 函数的定义，按住 Ctrl 点击 map 即可：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3TJl7TdwFxgmU0VktPIpN2FF4pHqicKicCe9Jlf8eF2GJy92Vicetnb5NmA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

map 第一个参数传入函数名称，第二个传入的是一个可以迭代的对象，例如list，而用红框标出来的其中包括了一个 * 号，在Python中参数前面跟一个星号代表多个形参的意思。所以我们可以写法如下，当有两个相同 list 时，多次传入 map 函数中即可：

```python
list_a = [1, 2, 3, 4, 5, 6]
list_b = [1, 2, 3, 4, 5, 6]
result = map(lambda a, b: 2 * a + 2 * b, list_a, list_b)
print(list(result))
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3TWHT8rqibXCbbJJLTiagkAJ7x3JFkOXK2Yl8hK02icNvruD2NtEhatmE6g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

现在是相同的个数的 list ，如果要是不同个数内容的 list 会如何？做个实验，将 list_b 的个数改为 10 个观察下：

```python
list_a = [1, 2, 3, 4, 5, 6]
list_b = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
result = map(lambda a, b: 2 * a + 2 * b, list_a, list_b)
print(list(result))
```

![](https://img-blog.csdnimg.cn/20190220130434504.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到，即使两个不同内容的list进行map计算，最终结果也会根据内容少的list得到最终结果，也就是只进行前6位的计算。

**2. reduce 函数**

reduce 函数不能直接进行引用，在 Python3 中，reduce() 函数已经被从全局命名空间里移除了，它现在被放置在 functools 模块里，如果想要使用它，则需要通过引入 functools 模块来调用 reduce() 函数，还是先来看下 reduce 函数的语法使用：

> reduce(function, iterable[, initializer])

> function -- 函数，有两个参数
> 
> iterable -- 可迭代对象
> 
> initializer -- 可选，初始参数
>
> 函数将一个数据集合（链表，元组等）中的所有数据进行下列操作：用传给 reduce 中的函数 function（有两个参数）先对集合中的第 1、2 个元素进行操作，得到的结果再与第三个数据用 function 函数运算，最后得到一个结果。

老规矩，点进去看源码，其中有官方的文档注释：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3Te2PK9N1N4fgpmY9IetibtMeczGdtJWxckIhd2Xdib3ZePWSG0XwD3qVw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

咱们就用它注释中的例子来实践一下，作为 reduce 的第一个函数，入参必须是两个参数，否则会报错，例如下面：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3TpbicEJOWic9wy0pAeGKIto54r3F8ILPibRiaLrDIZDNiboh6ibOHX9DX6H7Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

改成官方例子：

```python
from functools import reduce

result = reduce(lambda x, y: x + y, [1, 2, 3, 4, 5])
print(result)
print(type(result))
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3T1qyjibLxld6TiabY4ia9LibhtmELsbNjqk6uMEurp4pjYgqFzSBrI9mWXQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

素质二连，print出结果，可以看到这次与 map 函数不同，返回的结果是一个计算后的整数 15 ！这个 reduce 函数是怎么算出来的呢？仔细看过注释的同学一定知道怎么来的了，实际上就是这样来的：

```python
 reduce(lambda x, y: x+y, [1, 2, 3, 4, 5])  --->  ((((1+2)+3)+4)+5)
```

**第一次计算时，x = 1，y = 2，于是将 1 + 2 = 3 的结果作为下一次调用时入参的x，而第二次计算时的 y 则是列表中的数字3 ......以此类推。**

(1+2) --> ((1+2)+3) --> ....  --> ((((1+2)+3)+4)+5)


reduce 函数是一个**连续计算**的函数！

再来看下 reduce 函数的第三个参数，初始化第一个入参值：

```python
from functools import reduce

result = reduce(lambda x, y: x + y, [1, 2, 3, 4, 5], 10)
print(result)
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3TF6iaiaEEYibMBuUTlMolcUpQd87KkzBKs34eL39aH6icWyHSmqXGGrXcfw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**这个计算的顺序则是第一次 x = 10，y = 1，将 x+y 的值 11 赋予第二次计算的 x 作为入参，第二次计算时的 y = 2，第二次计算结果等于 11 + 2 = 13 .... 以此类推。**

(10+1) --> (10+1)+2) --> ((10+1)+2)+3) .... --> ((((10+1)+2)+3)+4)+5)


**3. filter 函数**

filter 函数，这个英文单词的中文含义是过滤的意思。依然是看下官方语法：

> filter(function, iterable)

> function -- 判断函数。
>
> iterable -- 可迭代对象。

> filter() 函数用于过滤序列，过滤掉不符合条件的元素，返回由符合条件元素组成的新列表。
> 该接收两个参数，第一个为函数，第二个为序列，序列的每个元素作为参数传递给函数进行判，然后返回 True 或 False，最后将返回 True 的元素放到新列表中。

示例，请将下面的 list 中为小写字母的字符串提取出来，生成一个新的列表：

```python
list_word = ['a', 'A', 'B', 'c', 'D', 'E', 'f']
```

思考一下再看答案哟：

```python
list_word = ['a', 'A', 'B', 'c', 'D', 'E', 'f']
result = filter(lambda word: word if word.islower() else False, list_word)
print(result)
print(list(result))

>>> <filter object at 0x000001D82D743080>
>>> ['a', 'c', 'f']
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3T5ggNw82j2icdBIkTx9siboBpiaRicg0u4qmvicp2WjXoFuMdJJP2TH4ibvow/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

结果如上图，通过字符串的自带函数，islower() 可以判断字符串是否是小写字母，若是小写字母则返回一个 True ，可以看到笔者的 lambda 表达式用了一个三元表达式的写法，来过滤掉了原列表的大写字母，是不是很简洁呢！毕竟人生苦短，我用Python啊！

### map - reduce 扩展知识

map / reduce 实际上是大数据中的一个编程模型，其中 map 代表映射的意思，reduce 代表归约的意思，而这个模型主要是用来进行并行计算的！可以用一张图来看生动的看下 hadoop （Hadoop是一个由Apache基金会所开发的分布式系统基础架构。）中的 map / reduce：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbQkuia171SSJrecxic5zFia3TWNhxnFiciaawmQRYegUpLEVb3G5ZDcgwdbw4CDJicpGKAicEKIXQtZxLJA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

做三明治，用到了各种蔬菜，首先我们先将每个蔬菜切碎，通过map 映射成碎片，在使用 reduce 进行并行计算使之合体！

### 总结

说一些学习上的技巧，对于一个新的函数，首先学习看它的语法，第一时间可以去找官方文档看，比如点进去看它的官方注释，如果英文看不懂的话呢，可以去菜鸟教程上搜下，上面也是有不少官方文档的定义，都是中文教程。写到现在，大部分Python小课堂上的小实例都是非常简单的，入门与进阶通俗易懂，但是不要小瞧这些小 demo ，如果你真的把它们都弄明白了，就像前期种下一颗种子一样，稳定根基之后必将作为长成参天大树的必要前提！



有想一同探讨Python的同学，欢迎关注公号:migezatan.(咪哥杂谈)






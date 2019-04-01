## python小课堂36 - 你可知对象也有真假之分？

### 前言

前天写了一篇[《零基础如何入门Python》](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659480&idx=1&sn=0f9209bb6bd986d46986310d4d9c6ff8&chksm=8c97d261bbe05b77e02cf6a17a68524d6c5ed0aed4659af69b56d670e40c74e851347fbeeaf8&token=322910151&lang=zh_CN#rd)，感兴趣的读者可以看一下。学习多数靠自律，毕竟在编程领域，勤真的能补拙。。。



今天这篇标题有人可能会疑惑，大概看不明白是什么意思吧....来解释一下，Python 中一切万物皆为对象，而几乎所有的对象都是和 Python 中 True 和 False 有着对应关系的。下面就来看下怎么回事！~



PS：本章会带你一步步有逻辑性的进行推理，耐心观看！

### Python各种对象的真与假

在[《小课堂Python35》](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659473&idx=1&sn=d8ef7b4bbbf98490cf614d37f8b08a90&chksm=8c97d268bbe05b7e97781e445c4127218f2176c98723b003781500ef7ec598a63476198f6840&token=322910151&lang=zh_CN#rd)中，提到了一个 None的关键词，在 Python 中代表空的意思。在初期的时候，介绍过 bool() 的用法，它是 Python 的内置函数，使用它可以判断对象的结果是 True 还是 False。如下：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYtOibOjufw0qM7CravH8NUfSWWW8Mjic4hJONksWIJQX1y4bP8ev1xB2h40glrTmGkCzw8PICmX0yQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

结果显示：None 的布尔类型为 False。



为了提起回忆，再来几个，分别字符串、数字、列表的空与不空。



除了数字型特殊，不难观察到，只有0才是False，剩下的数字都是True。而字符串和列表，但凡是空值，则是False。


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYtOibOjufw0qM7CravH8NUfhpaldjoIfAy0k4azfd3jU5DRAU1Sj90HbB6ZnvgkzkuetNpyTxaBUw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


由以上观察结果，得出一个**结论1：但凡是一个空值的对象（不包括数字），那么它的布尔类型一定是False。**


上面的结论是否真的正确？看到这里思考质疑一下，真的是对的吗？



反驳上面的结论示例如下：



如果由我们来自定义一个空壳对象，并且将对象进行实例化，判断实例化后的布尔值，你觉得会得到怎样的结果呢？



业务场景：

手写一个名为 TestBool 的类,当然这个类里什么也不写，目的就是为了让它看起来是空的，然后对这个类进行实例化，最后打印实例化的布尔值。可以思考下，动手实验后再看笔者答案。

```python

class TestBool(object):
    pass

test = TestBool()
if test:
    print('Wow,test is True!')

print(f'验证是否真的是真:{bool(test)}')
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYtOibOjufw0qM7CravH8NUfK90cxIgJUSxIL40nesGMdMQuA1Siaz8OFvaB3pYAZ1KlIpnYrpibia27A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


**结论2：由我们自身定义的一个空对象，将它实例化，得到的结果却是 True，反驳了上面的结论！虽然看上去为空对象，但若是使用type()查看下就知道，它的类型并不是 None，而是自己定义的类型，可以理解为对象已经存在，所以它依然会走进 if 的分支中去。**



**多说一句，对象存在的理解。**

> 举个例子，有对夫妻要生孩子。
> 
> 如果已经生下来了，取名字叫“小明”，“小明”目前是真实存在这个世上，那就是实例化出来的 test 。
> 
> 实例化出来的就已经是实体了，这个实体会占用内存的，并且是一个对象的形式存在。


### 对象真假值背后的原理

既然对象根据不同的应用场景会出现“真假”，那么它背后的原理究竟是什么呢？是什么左右了它的布尔值呢？



将自定义对象中添加一个内置方法 __len__(self)，并返回0。



PS：内置方法之前在面向对象中简单的介绍过，[python小课堂19 - 面向对象篇（二）。](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659101&idx=1&sn=5d8b202ca7fb139ef72284bd90a7c38f&chksm=8c97d1e4bbe058f2963a2b14e2022f0c8e103b0e3696467967731a16be6654cebf56834106b0&scene=21#wechat_redirect)

```python
class TestBool(object):
    def __len__(self):
        return 0

test = TestBool()
if test:
    print('Wow,test is True!')
else:
    print('False.....!!')

print(f'验证是否真的是真:{bool(test)}')
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYtOibOjufw0qM7CravH8NUfIT30LQXfKBiawkc21R9KVA3MusRbHb1Yyibv2sNQGWYfMYkHNvuFqT9A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


神奇的事情发生了，自定义对象，通过内置方法 __len__ 改变了自身的布尔类型，只因为返回了0，这便是其中的原理！



好奇宝宝1号总会多试探下，若不返回0，我返回其他数字行吗？行啊没问题，代码如下：

```python

class TestBool(object):
    def __len__(self):
        return 10
        
test = TestBool()

if test:
    print('Wow,test is True!')
else:
    print('False.....!!')

print(f'验证是否真的是真:{bool(test)}')
print(f'长度:{len(test)}')
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYtOibOjufw0qM7CravH8NUfbMgiarddbxl28qAhozUZygrxTpxmFIbmYchO92O0sficeCxNA9ZChv9A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


可以看到，改为10后，不光对象的布尔类型又回到了True，而且笔者还将它的长度打印出来！勤于思考的同学一定会想到，内置方法__len__ 和 len() 单词语法长这么像，一定会关联！



**没错，内置方法__len__ 决定着对象的 len() 长度，而同时 __len__ 的返回值也控制着一个对象的真与假！返回0就是假，其余数字都是真！**



好奇宝宝2号也想多试探下，不返回数字行吗？返回个空列表，空字符是不是可以影响对象的布尔类型为 False？


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYtOibOjufw0qM7CravH8NUfibmreQLwlrtMeJfbnooCmqQISO0sTDHDgESzRxT0o0hwudaT6NzuicoQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

好奇宝宝2失败，对于 __len__ 来说只能返回整形数字，那么话又说回来了，其实还可以直接返回 True 或者 False，因为他们对应着数字呀：

![](https://mmbiz.qpic.cn/mmbiz_jpg/E4ianOkSOYIYtOibOjufw0qM7CravH8NUfCTzeGjz81c2kqDRBmXMF8h4vvDVUr2RZ66CTbQLX8A9jZA1SP4IUMg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


所以可以尝试，当返回 False 时的结果：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYtOibOjufw0qM7CravH8NUfopSjazibFwzibjMQhwS0LN2EwJLRJXks6ZkSjAEmvBX8DiclEkVsXE3BQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

需要注意一点，对象中若是没有定义内置函数 __len__ ，直接调用 len() 是会报错的，也就是说 len() 的内置原理其实就是对象的内置方法 __len__ ，如下图：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYtOibOjufw0qM7CravH8NUfO14d4TyAGexeCGe3OLBzaq29Ml4icrFHiargicwWDbjiaCEMdOhfAlERpg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**结论3：结论1和结论2都不是最终的答案，在 Python 中，若是自定义对象，需要看对象中的 __len__ 返回结果，才能判断一个对象的布尔类型。**

那么问题又来了！我们都知道有个 bool() 的方法可以看一个对象的布尔值，好奇宝宝3号会不会好奇，其实它的内置原理是有个叫 __bool__ 的内置函数在起着作用呢？



没错，好奇宝宝3号想的太TM对了....代码如下：

```python

class TestBool(object):

    def __bool__(self):
        print('__bool__ is execute')
        return True

    def __len__(self):
        print('__len__ is execute')
        return 0

test = TestBool()
if test:
    print('Wow,test is True!')
else:
    print('False.....!!')

print(f'验证是否真的是真:{bool(test)}')
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYtOibOjufw0qM7CravH8NUfNH9RwqRzjQouMOfLn2V33Z4mUAOuXq0d4uUTuicmsX9ymBIxLPD0pdQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


当 __len__ 和 __bool__ 同时存在时，可以看到上面代码结果，__bool__ 起着效果，因为它返回的是 True，而 __len__ 返回的是0，按理应该返回 False，然而它并没有生效。

意味着，**__bool__ 和 __len__ 同时存在，判断对象的布尔值时，“正宫”是 __bool__，__len__ 会失效！__bool__ 返回的类型只能是布尔类型，即 True 或者 False，有兴趣的可以自行尝试。**





**终极结论： 通过结论 1~3，得出一个终极 boss 结论。对于Python的普通类型来说，空值是 False的；对于自定义对象来说，先看内置方法 __bool__的返回结果，若有则以此为准，若无则以 __len__ 返回的结果为准。若既没有 __bool__ ，也没有 __len__ 方法，默认布尔值结果返回为 True。**


### 总结

本篇文章从0到1，以有序的逻辑推理了一遍，相信看到最后的你一定会有所收获，因为在正常的编程中，很多情况下是对 对象 是否为空的 if 判断，若基础概念模糊，会导致一些想象不到的 bug 产生！关于结论，记住最后的终极结论即可。


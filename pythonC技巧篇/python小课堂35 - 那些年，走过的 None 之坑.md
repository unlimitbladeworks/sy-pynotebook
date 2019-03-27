## python小课堂35 - 那些年，走过的 None 之坑

### 前言

今天的主角是 Python 中的 None，那些年，我们一起走过的 None 之坑。



说到 None ，与之对应的中文，第一个想到的就是空。在任何程序中，总会有着空伴你左右，下面就来聊一聊 Python 中的空！

### Python 中的 None

一提到 None，是不是有人会想到我们平时的空字符串，空列表。又或者是 0 ， False 这样的值？在写 if 判断时，我们想要判断一个字符串是不是空，你会不会这样写：

```python
a = ''
if a is None:
    print('a 字符串 is None 返回结果是 True')
```

猜一猜输出结果会打印吗？



如果你觉得会打印输出的同学，怕是要打脸了.....请务必好好看下今天这篇 None 的技巧文章！因为在 Python 中 None 并不等于以上说的这些！



不等于的前提下，是从 Python 的 id值（内存地址），类型，值 三点出发考虑的，让我们场景带入看看....

### 场景带入与代码实现

动手实践是最好的证明方法，写一段代码来验证下！



需求场景很简单，有个空字符串a，有个空列表b，还有个等于0的c，最后再来一个等于 False 的d。



先来验证值相等不相等，不知道大家还记不记得如何判断值相不相等呢？之前在 Python 小课堂基础章节介绍过，使用 == 即可判断值是否相等，返回的结果是个 bool 类型的结果，True 说明值相等，False 说明值不相等。



再来使用 is 验证内存地址，类型，值是否一致。



忘了的回顾文章：[python小课堂12 - 运算符篇](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451658877&idx=1&sn=0efcf8a346661fd56553deede8bab878&chksm=8c97d0c4bbe059d2240343bb89b55d358cace18ccc1716486022334677a0ac60c57970f6ccf4&scene=21#wechat_redirect)



具体场景代码如下：

```python

a = ''
b = []
c = 0
d = False

# 值是否相等
print(a == None)
print(b == None)
print(c == None)
print(d == None)

# id值(内存地址)是否相等
print(a is None)
print(b is None)
print(c is None)
print(d is None)
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIb1rTDG3liaLdmibqGB3GVaWY64vmDTxrpHEkNLhR1JAmNick1hyf7icdpgq5pnOjbo7kI1tBaAmqj8dA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


打印结果全部都是 False，说明**不论是上面试的哪种空类型，都不等于 None，不论使用 == 或者 is 来进行判断。**

### None与各种空值不等的原因

要说 None 与上述各种空值不等的原因，其实也很简单。大家是否还记得一句话，在 Python 中，一切万物皆为对象！这意味着，None 自身就是个对象，曾经在小课堂的对象篇介绍过，对象可以理解为类型。

具体回顾文章：[python小课堂18 - 面向对象篇（一）](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659087&idx=1&sn=2d65a5e2efc4f848d7242e6619e30211&chksm=8c97d1f6bbe058e0a90f58bd16f72e0392d14bf2621455547577ab1a89e0fa73a9f9c3537455&scene=21#wechat_redirect)

使用 type() 内置函数，可以看到一个对象的类型是什么。

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIb1rTDG3liaLdmibqGB3GVaWYBFVdxPCMbaqfR7JRfQib5VZl8dlsibEtsiape2xkdaMyRN6mS9rRVpVHg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

打印结果为 NoneType ，这边是 None 关键字的类型了。所以**使用 is 判断 空字符串，空列表等 与 None 是否相等，单从类型上来说，返回结果就是 False 了！**


### 在 if 判断中，None 踩过的坑

来，请大家看一个深坑，下面这段代码从逻辑思维上来讲是有些绕的，不过笔者已经将正确的逻辑用中文的形式写在了 print 打印结果中，思考一下，看看会打印出什么呢？



坑一，a变量以函数进行返回 None ：

```python

def function_a():
    return None


a = function_a()

# not + 变量 进行判空， if not ，
if not a:
    print('if not a , 返回结果是 True! 中文意思是如果 a 是空值！')
else:
    print('if not a , 返回结果是 False! 中文意思是如果 a 是不空值！')

# 变量 is None 进行判空
if a is None:
    print('if a is None 返回结果是 True! 中文意思是如果 a 是空值！')
else:
    print('if a is None 返回结果是 False! 中文意思是如果 a 是不空值！')
```

坑二，变量 a 直接赋值空字符串：

```python

a = ''
# not + 变量 进行判空， if not ，
if not a:
    print('if not a , 返回结果是 True! 中文意思是如果 a 是空值！')
else:
    print('if not a , 返回结果是 False! 中文意思是如果 a 是不空值！')

# 变量 is None 进行判空
if a is None:
    print('if a is None 返回结果是 True! 中文意思是如果 a 是空值！')
else:
    print('if a is None 返回结果是 False! 中文意思是如果 a 是不空值！')
```

上面这两段代码，希望大家可以在留言区进行自己的看法输出，欢迎留言，如果你真的看懂了本文的介绍，相信这两段代码很容易得出答案！



PS：多说一句，输出是一个动脑子的过程，单单是看文章，不一定是真的看明白了，好多人关注了系列文章，相信都是想去主动学习的读者，学习如何牢固，输入->思考->输出。

### Pythonic 写法式判空

提倡 Pythonic ，说白了就是简洁性的 Python 代码。判空其实很容易，如下：

```python

a = ''
if a:
    print('a 是有值的！非空')
else:
    print('a 是空值！')
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIb1rTDG3liaLdmibqGB3GVaWYMWn7DZvNUUGEqrdHR0NCVPdLQr1QAhlffOZIUFibWicCdicISeSLiarXvA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**结论： 在 Python 中，多数以 "if 变量:" 形式进行判空操作！**

```python
if 变量:
```





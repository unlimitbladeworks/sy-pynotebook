## python小课堂16 - 函数篇
## 前言

函数篇 ------ 说起函数，大家高中应该都学过类似的概念，函数指一个量随着另一个量的变化而变化，而在编程中，函数的概念则不尽相同。举个例子，比如打过dota的同学都知道，在dota中通过shift可以对英雄进行预操作，也就是当英雄还没到某一地方时，我们可以通过shift键来设定好相应的路径以及施法，来完成对英雄的提前操作，这样起到的作用就是将操作模板化。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20181213123925995.gif)



而相应的，在程序中，函数就是为了将代码进行模板化管理，它可以实现一些特定功能的小方法或是小程序。而在python小课堂之前的介绍中，其实就已经介绍过不少python自带的函数了，比如print()、max()、ord()等。。

## 定义函数

通常在python中，我们可以类似下面的写法去定义一个函数：

```python
def print_hello(words):
  print('hello ' + words)
  
print_hello('world!')

>>> hello world!
```

def作为python中的关键标识字，全拼define 定义的意思，后面的print_hello作为函数的名称，小括号里面可以传入不同的参数，以便外面调用时将参数传入。想后面的print_hello('world!')就是将'world!' 传入到print_hello中。

### 函数的参数

**1. 形参和实参**

其中print_hello(words): words代表的是函数的形参，形式上的参数。

其中print_hello('world!')： 'world!'代表的是函数的实参，即实际的参数。

**2. 必须参数和关键字参数**


想象一个实际场景，当我们在计算减法算数的时候，需要你手写一个函数，传入x,y并且将最终相加的结果打印出来。


```python

def sub(x, y):
    sub = x - y
    print(sub)
sub(2,1)

>>> 1
```

调用add函数时，传入的1,2称之为必须参数，也就是实参，传入时是有顺序的，所以我们最终结果得到的是1，但是如果我们把sub(2,1)改成了sub(1,2)最终得到的结果就是-1，有没有一种方法依然可以得到1呢？此时使用关键字参数即可实现。忽略实际参数传入时的顺序，写法如下：


```python
def sub(x, y):
    sub = x - y
    print(sub)
sub(y = 1,x = 2)

>>> 1
```

可以看到，在传入实参时，我们可以指定对应的函数形参值，进行传入对应的值，来达到无序传入。关键字参数在一些源码中是经常被用到的！


**3. 默认参数**

场景更新一下！比如现在需要我们求一个半径默认为1的圆形面积，半径可以通过外界因素进行改变，请设计出对应的函数。代码如下：

```python
def circle_area(r = 1):
    area = 3.14 * r
    print(area)
circle_area()

>>> 3.14
```

默认参数就是在形参处写好一个默认值，若调用时没有传入值，则变量会取默认值。再来看下如果传入值会发生什么？

```python
def circle_area(r = 1):
    area = 3.14 * r
    print(area)
circle_area(10)

>>> 31.400000000000002
```

可以看到外面调用10时，将形参r=1覆盖掉了，最终算出来的结果以r=10为准。

### 函数的返回值

函数的返回值：通过return关键词来进行返回，当我们调用函数时，可以将函数的处理结果返回到调用处，来看一个加法的函数例子：

```python
def add(x, y):
    sum = x + y
    return sum

result = add(1, 3)
print(result)

>>> 4
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018121312421964.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

如果什么add函数不写return值呢？来看下结果：



![在这里插入图片描述](https://img-blog.csdnimg.cn/20181213124228993.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


上面的例子可以看到，python函数默认return值为None，而#代表的是注释，在代码中起到的作用是解释当前代码的意思，是写给人看的，并不执行。同样的#只能注释一行，要想注释多行可以使用 ''' 你的代码 '''，"""  你的代码 """  ,也就是所谓的三双引号和三单引号。如下：



```python
'''
def add(x, y):
    sum = x + y
    return sum
'''
"""
result = add(1, 3)
print(result)
"""
```

return关键词在函数中也代表这停止的意思，也就说在函数中如果遇到return，那么return后面的代码不会进行执行。如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181213124253919.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### python的序列解包

在python的函数中，返回值是可以有多个值的，比如现在有一个场景，让你去超市买水果，然后你花钱买到了苹果和香蕉。我用简单的函数代码来演示下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181213124308774.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


```python
def buy(money):
    if money > 10:
        fruit_a = 'banana'
        fruit_b = 'apple'
        return fruit_a, fruit_b

fruit = buy(20)
print(type(fruit))
print(f'通过元组索引得到的值：{fruit[0]}, {fruit[1]}')
banana, apple = buy(20)
print(f'通过解包得到的值:{banana}, {apple}')

>>> <class 'tuple'>
>>> 通过元组索引得到的值：banana, apple
>>> 通过解包得到的值:banana,apple
```

可以看到，如果我们去超市买水果，身上带了大于10块钱的钱，那么我就可以同时买到苹果和香蕉，同时函数将两个值一起返回，得到的是元组，在调用时解析时，可以直接对元组进行解包操作，直接定义对应变量的名称即可！推荐用解包形式去得到函数多个返回值，因为逻辑非常清晰！

### 你不知道的python小知识点

**1.python的系统递归参数**

现在有一个场景，请你实现打印一句话hello！并且在函数内部调用自己本身。代码实现如下：

```python
def print_hello(words):
  print(words)
  print_hello('hello')
print_hello('world!')
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181213124347471.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到报错了！错误中文大概意思是递归错误，超过最大递归深度。最大深度就是屏幕上的993次。

> Tips：
> 递归 ---> 递归的意思就是函数本身自己调用自己。比如上面的例子中，在print_hello函数中又调用了自己，所以python就会一直执行下去，但是python自身有检测递归函数的机制，所以如果你写了一个死循环这样的递归，它会直接进行最大次数的尝试并且报错。常见的错误：在程序中若写了一个死循环递归方法，最终报错的信息则是：MemoryError: stack overflow，也就是常说的栈内存溢出。

拓展知识：

在上一节中，我曾经说过一个python自带的包，叫做sys。通过sys可以来设定递归函数的最大深度。请看下面的代码：

```python
import sys
sys.setrecursionlimit(1000)

def print_hello(words):
  print(words)
  print_hello('hello')

print_hello('world!')
```

**2. python的链式赋值**
在python中，是支持链式赋值的，什么是链式呢？就是类似将元素串起来形成一个链子一样。如下：


```python
a = b = c = 1
print(a, b, c)

>>> 1 1 1
```

**3. "序列解包"赋值**

道理和上面讲过的序列解包差不多：
```python
a, b, c = 1, 2, 3
print(a, b, c)

>>> 1 2 3
```

至此完！
<hr />

有想学python的同学，欢迎关注公号：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181213124617194.png)
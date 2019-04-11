## python小课堂38 - 关于 *args,**kwargs 的作用

### 前言

有时在看在大神写的程序中，会看见 **\*args,\*\*kwargs** 这样的写法，那么你知道，这样写法的含义是什么吗？

本篇用最简短的小示例来介绍下它们的用法，以及这样写的好处。

### *args 用法

```*args：``` 可以理解为多个无名参数，也有人叫可变位置参数的。

**示例1**，定义一个打印的函数，传入任意参数即可：

```python
def print_func(*args):
    print(type(args))
    print(args)

print_func(1, 2, '呵呵哒', [])
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaExGyZcVjia9qK4Fp8OjIe75icTdicibmeKcZKDnkP9XXaazmZyDooKbicx9LPVAib14Nvs9jeG6icr5gUg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

打印 args 的类型是一个元组。直接对此变量打印输出，可以看到虽然我们以正常的多个参数传入，但是用到 args 时，将外界参数以元组形式呈现出来。

**示例2** ，在打印函数中的参数处，新增 x 和 y 变量。

```python

def print_func(x, y, *args):
    print(type(x))
    print(x)
    print(y)
    print(type(args))
    print(args)

print_func(1, 2, '呵呵哒', [])
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaExGyZcVjia9qK4Fp8OjIe7QCWzRN9d5DIxD6nPKE9z2B8g150z80Mz9sl4Cxr6aR9s8m80suCD4g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


若在函数参数定义处，有多个实体变量，它会按照顺序一一将传入的参数对应上，就像上面的例子，1传入对应就是x，2传入就是y，其余的参数对应 ```*args 。```

**示例3**，若要是将 *args 放在参数最前面，颠倒顺序会如何？


```python

def print_func(*args, x, y):
    print(type(x))
    print(x)
    print(y)
    print(type(args))
    print(args)

print_func(1, 2, '呵呵哒', [])
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaExGyZcVjia9qK4Fp8OjIe7IqcGpnlbib9Ric5EMLRaqBYfPjEUDmU1SLmRbzTHhtVXsbIFibwcGHYbg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，报错了，错误信息，提示找不到关键词参数 x，y。

所以若 ```*args``` 不是在最后，则需要在参数传入时，明确定义 ```*args``` 后面的变量参数名，如下：
```python

def print_func(*args, x, y):
    print(type(x))
    print(x)
    print(y)
    print(type(args))
    print(args)

print_func(1, 2, '呵呵哒', [], x='x', y='y')
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaExGyZcVjia9qK4Fp8OjIe7h9FPVrXqVee2JtuDenFMc6PpVIMwPklXFbw4FXq9tBumU7zJ0r8kZQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

上面分别介绍了：

1. (x,y,*args) 顺序

2. (*args,x,y) 顺序



其实还有第三种顺序，就是放在中间，至于结果怎样？可以自行尝试，留个小小的悬念，多多动手才能学到东西，哈哈哈。

### **kwargs 用法


```**kwargs：``` 多个关键词参数。

**示例1：**

```python

def print_func(**kwargs):
    print(type(kwargs))
    print(kwargs)

print_func(1, 2, '呵呵哒', [])
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaExGyZcVjia9qK4Fp8OjIe7bz9S7WPoJcCme7UKKICo4tHvIXDbsTdCT2pLE2TOqZSO0djPjQiaGWA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

直接报错了，大致意思是需要给出四个参数！



改下调用函数时的入参：

```python

def print_func(**kwargs):
    print(type(kwargs))
    print(kwargs)

print_func(a=1, b=2, c='呵呵哒', d=[])
```
![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaExGyZcVjia9qK4Fp8OjIe7ALps6QiaubuwvmkLVHHJU5PB5WibAoGFIOXwWSj82xwU5dZOkdibXYPxA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

入参时，多添加了关键词。可以看到打印时，kwargs本身是字典类型，将传入的参数以字典形式呈现出来。

### 组合使用

```arg,*args,**kwargs``` ,三者是可以组合使用的，但是组合使用需要遵循一定的语法规则，即顺序为王。



需要按照： 

```arg,*args,**kwargs ``` 作为函数参数的顺序。

```python
def print_func(x, *args, **kwargs):
    print(x)
    print(args)
    print(kwargs)

print_func(1, 2, 3, 4, y=1, a=2, b=3, c=4)
```
![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaExGyZcVjia9qK4Fp8OjIe7hKOBHic6JrMagTDa3lapZsygUsEzD5MMjVliagTygASVV6yPZ5QxuKjA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


可以看到按照顺序，依次进行解析打印。若不按照顺序，可自行尝试，会报错的哟！

### 优点

首先说明一点用 ```*args 和 **kwargs```  只是为了方便并没有强制使用它们。使用这两个得好处就是使得代码非常灵活。



当你不确定你的函数里将要传递多少参数时你可以用```*args``` ，就像上面的示例中一样，它可以传递任意数量的参数。```**kwargs``` 允许你使用没有事先定义的参数名。

### 你不知道的小知识点

当**调用函数**时你也可以用```*```和```**```语法.例如:

```python
def print_func(a, b, c):
    print(f'a = {a}, b = {b}, c = {c}')

animal_list = ['pig', 'dog', 'cat']
print_func(*animal_list)
```
![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaExGyZcVjia9qK4Fp8OjIe7qktPjt7s9sZJqsMQI3RM9hksDjZqdjajZqjNwzAhcSCWCqkd8hIhpw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


正如结果显示，它可以传递列表(或者元组)的每一项并把它们解包。

注意：入参时必须与它们在函数里的参数个数相吻合，所以你可以在函数调用时用*。



同理，**也是相似的：

```python

def print_func(a, b, c):
    print(f'a : {a}, b : {b}, c : {c}')

animal_dict = {'a': 'pig', 'b': 'dog', 'c': 'cat'}
print_func(**animal_dict)
```
![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaExGyZcVjia9qK4Fp8OjIe7TxO20T2cq1GO5iaX1E2J31elZg25Wl2y9Nu9LIxiay6weZ4Hj0x4FPfg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

需要注意：定义的 animal_dict 中，key 必须等于调用函数中的变量关键词，否则会报错！

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaExGyZcVjia9qK4Fp8OjIe7TGnPQLFK7wS7XI0LKibaOaSibCHB2jCcknG2icicjPADqiaGZTWyGeReeYw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 总结

本想着，介绍此篇应该会很短的内容，没想到写着写着又这么多了，总之相信下次再看见 ```* 和 **``` 的你，应该不会有逃避心理了！


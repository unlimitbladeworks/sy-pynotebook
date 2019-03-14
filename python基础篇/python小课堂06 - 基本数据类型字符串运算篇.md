## python小课堂06 - 基本数据类型字符串运算篇
###    字符串的运算

就题目而言，字符串的运算？乍一看！这是什么鬼？所谓的运算，数学定义的含义就是将数字之间进行各种算法，例如加减乘除。那么字符串运算呢？同理：就是将字符串进行所谓的“加减乘除！

当然如果在字符串中获取相关对应的字符，也算是对其运算的一种方式。

例如:
```python
"Hello World!  I 'm coming!"
```
此字符串我想获取当中的'W'字符，如何获取呢？(具体操作看下面中的实践！)

以上的这种行为操作都算是对字符串的运算，下面来看下具体实践吧！


###    动手实践字符串的运算

打开idle，让我们实践一下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181108125400888.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

如上图实验所示，通过乘法可以实现对单一字符串的重叠复制，而通过加法可以将两个字符串进行拼接。

如何获取字符串中某一字符呢？请看下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181108125413835.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到通过在字符串后面跟上中括号的而形式来对内容进行截取！上面的例子都是正数的下标，那么如果要是负数的下标是否可以呢？

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181108125429865.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以通过负数来进行相应的倒数截取字符串！负下标的目的是什么呢？如果你字符串中内容很多，比如有1W个字符，那让你取倒数第二个，你不得一直数下去了。。！所以python创出了负数下标的表达方式。

###    字符串额外小知识

说到字符串，回想下在上一章，我曾经说过的转义字符，那么实际上python有一个转义字符的小知识点！

场景如下：

现在让你用print()在idle中打印出 
```python
'你好 ！
我是你的老铁！
'
```
想必你会知道这样去写:

```python
print('你好！ \n 我是你的老铁！')
```

如果此时，我就想让结果显示出```'你好！ \n 我是你的老铁！' ```呢？

在python中有着一个 r 或者 R 的写法，可以将原始转义字符不进行转义输出！r代表的含义是：raw，中文是未加工的的意思！也就是原始的意思。

写法：

```python
print(r'你好！ \n 我是你的老铁！')
print(R'你好！ \n 我是你的老铁！')
```
我们通过idle试一下，将代码输入看下结果：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181108125605962.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到上面输出将原有的转义字符直接打印出来了！

### 小结

```字符串运算```在日常的编码中也是用到非常频繁的，尤其是+号来对字符串进行拼接！而相应的，切片对字符串的截取也是必要掌握的小技能，在处理数据时，会经常用到切片的概念！

当你看到```r```加在''字符串前面，则代表的是```原始字符串(raw str)```，其中包含的转义字符将失去转义自身的含义！

欢迎想学python的同学关注公号哟，一起学习共同进步：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181108125829238.jpg)
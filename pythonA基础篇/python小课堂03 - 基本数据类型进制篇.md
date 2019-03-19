## python小课堂03 - 基本数据类型进制篇
###     什么是进制？

>来自百度:
进制也就是进位计数制，是人为定义的带进位的计数方法（有不带进位的计数方法，比如原始的结绳计数法，唱票时常用的“正”字计数法，以及类似的tally mark计数）。 对于任何一种进制---X进制，就表示每一位置上的数运算时都是逢X进一位。 十进制是逢十进一，十六进制是逢十六进一，二进制就是逢二进一，以此类推，x进制就是逢x进位。

通俗的讲，所为的进制就是一种计数时表示的方法，多少进制，就是当满足此进制时就向高位进一位，比如我们生活中常用的十进制，11 + 9 = 20,个位数1 + 9 = 10，所以此时向高一位进1，最后得出的结果就是20。举个更简单的例子，生活中我们经常以60秒作为1分钟来计数，这也可以理解为一种进制（“60进制”）。

> Tips(小常识):
二进制： 0 和 1 表示.

> 八进制：0，1，2，3 ，4，5，6，7

> 十六进制：0,1,2,3....9，A,B,C,D,E,F
(十六进制从10到15分别用A-F来表示)

### 动手实践各种进制

有了上节课的IDLE基础，这次来看下在python中，对应的进制数是如何表达的呢？



找到python中的idle，前期练手通过这个工具比较便捷，可以右键发送到桌面，下次找就不用费劲了！（后续不在介绍了！）

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIarypl3bSrumybnibYAeg7Z6d4Ktp12KeicibKR0wjFVHHEItOLnf1e0722jBpMsiajMJZnBcJiauwzn4g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


先来看下在python中，如何表达二进制，八进制，十六进制以及我们常用的十进制，如下图所示：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZcgX4n68P9MS9qo8zmEDickEutaKib6eiaZgOSnEa2uqjCmicmSmFZj5icp3zxbIicFLMA3Suf6JRcGsibw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


0b:binary(二进制) 所以小写b

0o:octal(八进制) 所以小写o

0x:Hexadecimal(十六进制) 所以小写x

由上图可以看到结果：

```python
>>> 0b1
1
>>> 0b10
2
>>> 0b100
4
>>> 0b1000
8
>>> 0o1
1
>>> 0o10
8
>>> 0o100
64
>>> 0o1000
512
>>> 0x1
1
>>> 0x10
16
>>> 0x100
256
>>> 0x1000
4096
>>> 
```

如何计算出上图的结果呢？

二进制计算：
```python
0b1 : 1*2^0 = 1

0b10 : 1*2^1 + 0*2^0 = 2 + 0 = 2

0b100 : 1*2^2 + 0*2^1 + 0*2^0 = 4 + 0 + 0 = 4

0b1000 : 1*2^3 + 0*2^2 + 0*2^1 + 0*2^0 = 8 + 0 + 0 + 0 = 8
```

这也是学过计算机专业同学嘴中经常说到的“8421”！等同于二进制的1111。

八进制计算：

```python
0o1 : 1*8^0 = 1

0o10 : 1*8^1 + 0*8^0 = 8 + 0 = 8

0o100 : 1*8^2 + 0*8^1 + 0*8^0 = 64 + 0 + 0 = 64
```

......后续以此类推！

十六进制不列举了，一个道理！

忘了说了！常规的十进制，实际在python中正常输入即可，就像上一章所讲的整数类型，所表示的都是十进制的数字！

### 进制之间的转换


进制之间的转换，便于我们在不同场景下有着不同的进制表示，就像生活中的时间，时间很短的情况下，咱们可以用秒作为单位来衡量，一旦时间很长，则用分钟，或者小时来计量了，此时需要将秒转换为分钟或者小时，与进制是一个道理的！

下面来看下python中如何将上述的进制之间做转换。

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZcgX4n68P9MS9qo8zmEDickAvjZFSzQric3ZugSG3Idsw5QeKKvpKbIypDqskBcu86HNWkpL0Jhs2g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

bin(): 将括号中的数值转为二进制

int():将括号中的数值转为十进制

oct():将括号中的数值转为八进制

hex():将括号中的数值转为十六进制

以上四个函数方法类似于上章讲到的type()，大家可以先理解这是一种写法即可。在python中这样的语法非常简单，就如同写英语一样，就是一句话！

### 小结

在我们实际的编程过程中，进制可能会接触的非常少，但是依然会用到，再此算是做一个基础的总结吧。

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIZcgX4n68P9MS9qo8zmEDickSibe4Wq2x8tILbeGvA6hYGpK8geA7YuKU5C1od8CNibJtMjYkApaLXrg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

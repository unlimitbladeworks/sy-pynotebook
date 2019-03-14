## python小课堂04 - 基本数据类型布尔篇
###  什么是布尔类型？
布尔类型：```英文boolean。```

举个栗子，比如今天是愚人节！你发工资了，于是你兴高采烈的去与同事探讨一番，同事偷偷的告诉你，他涨工资了！然后你表示很开心，但是你意识到今天是愚人节了，于是你充满疑问的心态去问他，真的涨工资了吗？！他回答你：真的！(此处的真便是布尔类型的一种)。夜幕降临，当你打开手机查看工资详细的时候发现工资并没有涨！原来同事说的都是假话！！！(此处的假便是布尔类型的另一种)。

在真实世界中的真假，映射到计算机中，即布尔类型。所以在python中，boolean 的值有两种，一种为```真(英文:True，T要大写！)```,一种为```假(英文:False,F大写！)。```


### 动手实践布尔类型

打开idle，让我们实践一下布尔类型：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181106205925815.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到上图，在python中通过type()查看True或者False得到的类型是bool(而在其他语言中，布尔类型一般关键词用boolean来表示)。

### 布尔类型在python中隶属于数字

如下图所示，我们可以将布尔值转为数字来观察，发现将True转为数字后就是1，False转为数字后就是0.

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181106205954374.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

```python
>>> int(True)
1
>>> int(False)
0
>>> bool(1)
True
>>> bool(0)
False
>>> bool(2)
True
>>> bool(1.111111)
True
>>> bool(0b01)
True
>>> bool('abc')
True
>>> bool('')
False
>>> bool([1,2,3])
True
>>> bool([])
False
>>> 
```

### 小结
布尔类型在编程中是非常常用的，在写一些逻辑判断的过程中，需要用布尔类型来判断程序是否应该进行怎样的逻辑运行，就像日常生活中，如果你坐上了公交车(此时为真)，那么你就得刷卡交钱！(符合布尔型为真后做的事情)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181106210037963.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)
 


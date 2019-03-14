## python小课堂02 - 基本数据类型数字篇
### 什么是基础数据类型 ？

在我们的日常生活中，当我们去菜市场买菜交钱的时候，会出现用**数字**作为计量单位来衡量一个物品值多少钱，而此时交钱的数字有零有整，比如一斤普通鸡蛋的价钱是1元钱整，我们将1元钱称之为**整数**；一斤普通鸭蛋的价钱是1.7元，我们将之称之为小数。

上面的例子对应到我们的Python编程语言中也是一样的，在Python中，最基础的数据类型有数字(number)，数字又分为整数(**int**)和小数(专业点来说:浮点数,**英文float**)。

结论来了:数字中的整数(int)，小数(float)就是python众多基础数据类型中的两员。

> Tips(小常识): 
在其他的编程语言中，浮点数还会细分：单精度(float)，双精度(double)，双精度的小数位准确率是高于单精度的！而在Python语言中，不会区分单双精度，只有一种类型，即float！
对于整数来说，其他语言还会有short，long这样的数据类型，对于python而言，整数类型只有一个，就是int！

### 动手实践int、float

编程，光理解概念是不够用的，必须动手实践一下才能出真理！

还记得上一篇安装环境我在最后说过的一个python自带工具IDLE，今天我们就用这个工具来亲自动手实践一下！

> Tips(小常识): 
IDLE:IDLE 是一个纯 Python 下自带的简洁的集成开发环境(IDE)。用通俗的话来讲，大家可以将其理解为一个高级点的计算器，我们通过键盘向这个窗口进行输入，而IDLE通过我们输入的东西进行计算，最后通过窗口将结果进行输出。

找到python中的idle，前期练手通过这个工具比较便捷，可以右键发送到桌面，下次找就不用费劲了！

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIarypl3bSrumybnibYAeg7Z6d4Ktp12KeicibKR0wjFVHHEItOLnf1e0722jBpMsiajMJZnBcJiauwzn4g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

让我们在IDLE上随意输入几个数字看看：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIarypl3bSrumybnibYAeg7Z6GQXwIYQ1KSGFDYPW6qGSfSwkFfcEY3Wx5sOwytDlFibeCPNqDyTl9bA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

接下来试下计算器的效果：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIarypl3bSrumybnibYAeg7Z6HaXfGrkTocm0ic5NYSt43IOhHU5iceA2zEXhgRWbA5NpEQiarMUUa5Szw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


别忘了今天的主旨！我们学习的是python的基础数据数字篇！所以如何来查看python的数字到底是什么类型的呢？这里引入一个python自带的函数 --- type()

至于什么是函数,在后续的文章中会有介绍，这里大家暂时理解为python中的一个写法就行，我通过这样的写法就可以知道我在IDLE中输入的数字属于什么类型。看下图：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIarypl3bSrumybnibYAeg7Z6bNibhib0rKzianG1ZKWnpI2UGzpdYVyantttr1lENNJX8mGpRBZImNBRg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


数字1  ---> int ，数字1.23333333  ---> float。以上就是基础类型的数字篇。

### 思考

留下一个小问题给大家，如果当我输入的是 99/10 的时候，此时的类型是什么呢？当我输入的 99 // 10的时候，又是什么呢？

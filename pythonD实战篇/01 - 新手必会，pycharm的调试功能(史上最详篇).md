## 新手必会，pycharm的调试功能(史上最详篇)
### 前言

Debug调试，是一项学习编程人员的重要技能。只有当你学会 debug 了以后，才可以正确的知道程序的走向流程是如何的，今天就来给大家介绍一下 pycharm 中的 debug 功能！

### debug的前世

在正式讲解之前，先来了解下 debug 这个词的由来，就像我们初学Python 时，先要了解下它历史的由来。

> 1937年，美国青年霍华德·艾肯找到IBM公司为其投资200万美元研制计算机，第一台成品艾肯把它取名为：马克1号（mark1），又叫“自动序列受控计算机”，从这时起IBM公司由生产制表机，肉铺磅秤，咖啡研磨机等乱七八糟玩意儿行业，正式跨进“计算机”领地。
> 
> 
> 
> 
> 
> 为马克1号编制程序的是哈佛的一位女数学家葛丽斯·莫雷·霍波，有一天，她在调试程序时出现故障，拆开继电器后，发现有只飞蛾被夹扁在触点中间，从而“卡”住了机器的运行。于是，霍波诙谐的把程序故障统称为“臭虫（BUG）”，把排除程序故障叫DEBUG，而这奇怪的“称呼”，后来成为计算机领域的专业行话。从而debug意为排除程序故障的意思。
> 
> 百度百科


看了上面的小故事，debug 一词的由来，是由 bug 词得来的，bug 是臭虫的意思，debug 就是解决臭虫。



在如今的互联网时代，多少你肯定听说过 bug 这个词，比如什么什么软件又出 bug 了！说的就是软件在使用的过程中，程序出现了一些错误。故称之为 bug。



**而 debug 则是通过工具来对代码进行调试，一步步找出程序中出现 bug 的位置，也就是程序中具体错误代码的位置。**就像故事中所说，debug过程就是在解决虫子一样。。

### pycharm 中的 debug 模式

来步入今天的正题。

首先，还是用示例说话，我们书写一段简短的代码，来帮我们完成今天要讲的内容。

```python
def sum_demo(x, y):
    for _ in range(2):
        x += 1
        y += 1
        result = x + y
    return result

if __name__ == '__main__':
    result = sum_demo(1, 1)
    print(result)
```

肉眼识别下，猜猜结果是多少呢？初学者可能没见过 for 循环中的下划线，在 Python 中是占位符的意思，因为单纯的循环两次而已，并不用到它的循环结果。最终 result 会输出 6 。

在 pycharm 中，如何开启 debug 调试，一共有三种进入的方法，如下（下图均可点开放大观看）：

方法一：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcovic6R1r6aYqleelicIVg1FNu6bglAZQfbvSBDOP7vOufKZ5B54eDS8w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


方法二：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcYAQMDwibNwzKhD8D66ic2hduseTibYsXzK9o2uyG9iaO7aIpdJTichhj23w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


方法三：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPckGf2JKym4Mnic2XHQpfW4k0pZf6l1pa4Y7RreKUaYQbfx0icJDKiaibCkw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


还有一种方法，就是 pycharm 导航栏处，有个run，点开以后即可看到 debug ，这里就不截图演示了。



单纯的进入 debug 模式，你会发现，与正常的 run 去运行程序没有差异。差异就是 pycharm 的控制台部分，从 run 跑到了 debug 显示。

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPc4n4WWVSa4zs7SL6a19NHzNtuMASzQl31WgiciaoV1leygWHZL8dsTnPw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

接下来要讲的，才是 debug 中的重中之重，即断点调试！

### debug 的断点调试



断点调试，英文 breakpoint。用大白话来解释下，断点调试其实就是在程序自动运行的过程中，你在代码某一处打上了断点，当程序跑到你设置的断点位置处，则会中断下来，此时你可以看到之前运行过的所有程序变量。



来继续刚才的演示，pycharm 中如何设置断点。



点击前：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcgmXXAHJqaicNfFttzKGJCwXZ7mb4po54YHaAFqTRQPvTDBFwic14ib5HQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

点击后，皮一下，每行代码都设置上断点：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPc0EEWsZq5GVWblzVic6pjWQ8uE24HjuMbvvvicnwkXzPhCkejEcF9YsOw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

设置完断点后，开启 debug 调试模式运行下，看到结果：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcSvNPjEU2gV9icxicTLVaZwLmOLb2ItpUd4Cqf76tf3P7uPkVllkiaSEOQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


看到了这么多新摆设，是不是有点怕了！不怕，咱们先来从控制台每个按钮讲起：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcXibwV8SUyvoNhDMBPkQjL62mRr79WhiaOLnQ55f6iapLtiby5ibacEawwnw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


如果要是忘记中文意思的话，没有关系，鼠标指到按钮处，悬浮一会儿，会有英文提示的。继续再来说横排按钮：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcichm62DoAialVLvU1tTNmaehicQicVdtZpYAbv31hM16zL2ttIHzOL3LmQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


其中，横排最重要，经常用到的按钮，来解释一下，自己鼠标悬浮去看英文即可：



step over（F8快捷键）：在单步执行时，在函数内遇到子函数时不会进入子函数内单步执行，而是将子函数整个执行完再停止，也就是把子函数整个作为一步。在不存在子函数的情况下是和step into效果一样的。简单的说就是，**程序代码越过子函数，但子函数会执行，且不进入。**



step into（F7快捷键）：在单步执行时，遇到子函数就进入并且继续单步执行，有的会跳到源代码里面去执行。



step into my code（Alt+Shift+F7快捷键）：在单步执行时，遇到子函数就进入并且继续单步执行，不会进入到源码中。



step out（Shift+F8快捷键）：假如进入了一个函数体中，你看了两行代码，不想看了，跳出当前函数体内，返回到调用此函数的地方，即使用此功能即可。



Resume program(F9快捷键)：继续恢复程序，直接运行到下一断点处。


以上四个功能，就是最常用的功能，一般操作步骤就是，**设置好断点，debug运行，然后 F8 单步调试，遇到想进入的函数 F7 进去，想出来在 shift + F8，跳过不想看的地方，直接设置下一个断点，然后 F9 过去。**


### 示例演示

上面的基础概念明白了以后，直接用图片示例演示下：

**1.设置初步断点**

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPc8BaFJBBYibFeYkB9zTN9DzRqAqNIiaFt0YUrNUbth8ibRb7f834Y2bMFw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


**2.F7 进入函数**


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcLiacelZ3sTOibIoIFBy2AhgG2A2oM0eOYDeN5phONag5UYGT8YqNUKSw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


**3.F8 单步调试，往下执行代码**


![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcA5XwdN4CicGF5HnPJ1uzaIYPmUb8NLLJT9icibTO8EVTM98avKF1yVLXQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

继续 F8 单步调试，往下执行代码：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcaBMpXia72pyHXPqqBibYwOF3OhNUO4flolJYl8XCtTcHyKRVQXc7F9xA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

继续 F8 单步调试：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcfNwONIBlQ4uBAyNM92XLckMAL2pMRzz9RVBceKT9iawVphMNf8POOtA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

继续 F8 单步调试：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcQV4UYPP9zJibibfKw3PRK81hagu8ed59C3MUuvYas3RZ97Mibk4NOzevg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcGbfQiciaPp2ftcmqdrb5SJ1XziayxUvbp8Y1yPYxKeOibsvUAtN4iavtaYQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**4.看够了循环，想直接看最终 result 加完的结果，结果处打断点，直接 F9**

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcwuhMsdNuC2CIjiaZqQMj5C8vMwMfZ1uBYagqFvI8O8CjicSrZ97w6sXg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIas5LYE1TDJqqrnaQnmWcPcvNCdFJsicWPa7mWQ8qC5c1C8bAjbMScdicL58ibiaWl7JU3DuxRUkLcIZw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


以上就是断点调试的全过程。看完之后，理解了吗~是不是顿时明白了断点调试的重要性，使用断点可以快速帮助我们理解程序中的各处逻辑！

### 结语

看到这里，基本的调试，相信你认真看完的话，已经可以上手使用了！但是要拓展的点还有很多，比如 pycharm 为什么在工程性的程序中颇受欢迎，因为它实在是太强大了。。。还有一些拓展功能，大家可以去慕课网上搜下**IntelliJ IDEA神器使用技巧** ,老师讲的非常详细，涉及到许多技巧，idea和pycharm是一家公司出的，所以使用上的技巧也是一样的，可以融会贯通。



慕课网课程具体地址（免费课程）：



https://www.imooc.com/learn/924



为什么在 Python 小课堂中，没有提前介绍这么重要的技巧，其实是有所顾虑的，前期学习中，笔者认为更多地精力应该放在学习本身上，而非工具上，就算没有debug，如果借助 Python 中的 print() 函数依然可以达到想要的结果，最笨的方法不就是一步步的 print 打印出你想要的结果吗！然而笨方法往往使人印象深刻呢！



希望本篇文章可以帮到正在初学的你，写程序的过程中，断点调试真的很重要！！欢迎点赞，评论，留言，收藏，转发哦！工具类教学最适合分享了！~


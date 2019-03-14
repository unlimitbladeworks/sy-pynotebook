##  python小课堂00


### 01 THE FIRST 编程、编程语言?



首先，在正题了解Python开始之前，让我们先来聊聊什么是编程吧！编程 - 中国文字拆分开来，就是编写程序的意思,英文 Programing。举个例子，假如老板给了我一个任务，要求是每天都要记录天气，并且最后以报表的形式报告给他！于是我按照他说的做了，每天早上9:00，打开浏览器，百度查看今天的天气,将当天的天气数据记在excel中。日复一日，终于有一天我厌倦了这样繁琐，重复的操作！开始自己想法让电脑自己来完成这一系列，在网络的搜索过程中，我得知了计算机是通过编程语言来实现操作的，比如我点击鼠标这个动作，对应着计算机背后的一条指令。那么如果我按照平时手动的操作去让计算机来帮我实现，这一系列过程(电脑自己打开浏览器,电脑自己查百度,电脑自己记录数据)就是编程！

在上面的例子中提到了编程语言，什么又是编程语言呢？通俗的讲，就是人与计算机交流的语言，你跟计算机说什么，它就得干什么!而现代社会，编程语言层出不穷,比如师祖老大哥C语言(贴近硬件的语言...),然后它的小弟C++(大型软件,例如游戏引擎...),灵感来源于咖啡的Java(web时代的王者...),还有文章的主角 --- Python(人工智能时代的"弄潮儿"...),等等等等，还有很多语言就不一一列举了！





### 02 THE SECOND Why Python?

Why Python？为什么要学Python？废话不多说，先来看2张图！

漫画一：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181104162700177.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)
上图片右下角是python(被我的水印挡住了!)





图二(自己总结的思维导图)：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181104162711593.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

所以，为什么选python？我想两张图足以表达我想说的了...当然python届最著名的的一句话莫过于：
```python
 Life is Simple,I Use Python!
       人生苦短,我用Python!
```

作为编程语言来讲，Python所具有的特色就是简洁！其自身语法读起来，就像读英文故事一样(当然代码本身的风格具备pythonic①)

这也是为什么我一直想使用Python的原因，因为简洁，所以贴近生活，非常容易解决身边的难点！



注：①pythonic:很·python！就像说英语一样的关键词语法!例如 in,代表的是包不包含....



### 03 THE THIRD Python一行代码


```python
        Python 之禅
Simple is better than complex.
        简洁胜于复杂
```

说了这么多,来实际看下Python的代码魅力,所谓一行代码可以作出哪些事情来？



一行代码：
```python
print('\n'.join([''.join([('AndyLove'[(x-y)%8]if((x*0.05)**2+(y*0.1)**2-1)**3-(x*0.05)**2*(y*0.1)**3<=0 else' ')for x in range(-30,30)])for y in range(15,-15,-1)]))
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181104162825207.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)




一行代码：
```python
print('\n'.join([' '.join(['%s*%s=%-2s' % (y, x, x * y) for y in range(1, x + 1)]) for x in range(1, 10)]))
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181104162835107.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)



其实还有很多类似这样的代码....简洁而强大!



### 04 THE LAST 结语

emmm....本期的python小课堂00篇到这里就结束了,接下来的文章要开始干货了,尽量每周更新一篇吧！真的是人生苦短，我用Python呀！(绿了....捂脸逃...) 哦!对了，祝大家十一快乐..


想学习python的朋友，欢迎关注我的公众号：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181104163828973.png)

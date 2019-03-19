## python小课堂05 - 基本数据类型字符串篇(重要)

### 什么是字符串？

> 题西林壁         作者：苏轼
> 横看成岭侧成峰，远近高低各不同。
> 不识庐山真面目，只缘身在此山中。

如上面的诗词一样，将其映射到我们计算机程序中，显然不是前几张介绍的数据类型，那么今天就来说下编程中最常用的数据类型 --- 字符串类型(英文```str```)。


如何在python中表示字符串类型呢？
```python
有三种表示的方法： '横'，"看"，"""成玲""" ，'''侧成峰'''

注意:以上分别是单引号;双引号;三双引号;三单引号。(全部为输入法英文状态下！)
```

> Tips:
> 引号在程序中出现要成对出现！并且引号一定要在英文输入法状态下！


### 动手实践字符串类型

打开idle，让我们实践一下字符串类型：



![在这里插入图片描述](https://img-blog.csdnimg.cn/20181107192701963.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到，当我们使用中文的单引号和双引号时，python会报错！(不仅是单双引号必须是英文状态，因为编程语言是国外发明的，所以输入法也必须跟国外```一致```，必须使用```英文```！)同时，可以看到被单引号，双引号括起来的内容类型，是```str```，即```字符串```类型。



大家思考一个问题！单单是字符串的写法就有三种，为什么python创始人要设计出三种写法呢？必然是各有各的好处的！请看下面的写法：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181107192739240.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)
图中蓝色字体已经阐述出单引号和双引号设计之处的用心了！不在多做阐述。



### 字符串中涉及到的转义字符写法
还有没有除了利用单双引号不同写法，来完成本身语义的表示呢？必然是有的，这里引出一个概念，转义字符，请看下图：



![在这里插入图片描述](https://img-blog.csdnimg.cn/20181107192800674.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

通过 \ 加上字符串中想表达的引号，构成了转义字符的写法，可以看到程序也正常输出了！```但是```不推荐这种写法，看上去很```复杂```，并且容易```出错```，如果可以用单双引号解决，还是使用上文涉及到的方法来书写，这样才比较pythonic(开篇介绍过此词，可以查看00篇)！

> Tips:
>转义字符(弄明白转义即可！)： 
> \n   换行
>  \ '    单引号
> \t    横向制表符
>\r    回车
>\n和\r 是有区别的

### 字符串的三引号表示含义



除了单双引号，上面还说到过三引号也是可以表示字符串的！那么它的使用场景是什么呢？来看下面的例子：



![在这里插入图片描述](https://img-blog.csdnimg.cn/20181107192959402.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

           所以问题来了，我现在想输入两个hello world后就进行换行，如何操作呢？请看下图：


 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20181107193018526.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

```python
>>> '''
hello world
hello world
hello world
'''
'\nhello world\nhello world\nhello world\n'
>>> 
>>> 
>>> """ hello world
hello world
hello world """
' hello world\nhello world\nhello world '
>>> 

```

   可以看到一个问题，此处python已经将我们的回车转成\n 显示出来(此处实际上是IDLE的一个特色，了解即可)！字符串实际上有些特殊字符是我们```肉眼看不到的```，但不代表```不存在于字符串```当中！例如```\n```，代表```回车```。。。

反向思维思考一下？如果我们在字符串中手动写上\n，此时IDLE会输出什么呢？来看一下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181107193132296.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到上图，\n并没有我们想象的那样换行输出！



普及一个常识，在写程序中，换行还有一个更加简便的方法！来看下图：

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20181107193150430.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### 小结      
```字符串```是编程中最```常用```到的数据类型，因此熟练掌握是非常重要的！本期小课堂介绍的内容非常多，也是字符串的重要性所在！回顾一下，字符串在python中的表达方式，各种写法的区别，以及转义字符的含义！
### 思考

思考问题：为什么\n并没有我们想象的那样换行输出！？？

 







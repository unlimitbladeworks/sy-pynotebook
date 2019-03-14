## python小课堂08 - 基本数据类型元组篇
###    python中的元组   

python中的元组，也是作为基础数据类型之一，英文: ```tuple```。

Python的元组与小课堂上一章所介绍的列表类似，不同之处在于元组的元素```不能修改```。元组使用小括号()来表示，列表使用方括号[]来表示。

###    动手实践元组类型

下面看下idle中的写法：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181111210736827.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到上述操作，基本和列表一致！(此处不过多介绍，基础类型列表篇已经介绍！)那么问题来了？既然和列表操作一致，那么为什么python中还会有元组这样的类型呢？(想必你也有这样的疑问吧。。如果没有，你就是没有思考！！~)

此处留一悬念！后续的小课堂中会讲到！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181111210752642.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到，通过type()来查看()相关类型是tuple类型的数据类型！



###    元组你不知道的小知识点

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181111210820667.gif)

来谈谈你不知道的元组！请看下面的小例子：
```python
>>> type((1))

>>> type(('Hello'))
```

大家认为这两个type会输出什么呢？

emmm。。来看下！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181111210854311.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

有木有很神奇！明明我创建的是元组类型啊！！~

有没有小伙伴知道这是为什么呢？欢迎留言区留言探讨呀！
### 小结
关于元组(tuple)的基础操作，与列表(list)，字符串(str)非常相似！聪明的你学会了吗！本节小课堂到此结束了，下期内容会将最近的知识点总结一下，敬请期待！

有想学python的朋友，欢迎关注公号哟：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181111210949311.png)
## python小课堂09 - 基本数据类型序列总结篇
###  回顾基础数据类型   

在小课堂之前的章节中，介绍python的基础类型包含了**int、float、bool、str、list、tuple**。那么这些基础类型里有没有相似之处呢？必然是有的，今天就来做一下总结。


###   python的序列概念
还得在小课堂07中所说到的组的概念吗？实际上在python中专业术语称之为```序列```。之前的案例中，```str、list、tuple```这三类的操作都有着相似的共同性，所以，这三种就是今天要总结的重点，也就是序列！

序列共有操作：

①获取单一元素：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181115223012503.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)
通过[n]下标的形式来获取前面基础类型中内容的某一元素。

②截取多个元素：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181115223032267.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)
通过前面介绍的切片特性，[x:y]的方式对原有内容进行截取，```注意```：切片的括号包含左侧，不包含右侧。

③ + 和 * ：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181115223048875.png)


④ in 关键词用法：

此处引出一个新的python语法关键词：```in，中文意思 ---> 包含，在```

可以通过in来判断一个元素是否在序列中！而得到的类型是True/False ，也就是布尔类型。可以看下面的例子：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181115223125474.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

相反的如果不包含呢？只需要加一个not就行了！是不是很```python```！如下：

```python
>>> 'a' in 'abcdefg'
True
>>> 'a' not in 'abcdefg'
False
```
⑤序列的python方法：
```python
len()：将返回()内容中的长度

max()：将返回()内容中最大的值

min()：将返回()内容中最小的值
```

len():
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181115223212414.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

max():
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181115223225442.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

min()同理max()不举例子啦，大家自己尝试即可！



###    字符背后你不知道的知识点

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181115223450652.gif)

> Tips:
> 每个字符背后实际上对应的ascll码。
> ASCII（American Standard Code for Information Interchange，美国信息交换标准代码）是基于拉丁字母的一套电脑编码系统，主要用于显示现代英语和其他西欧语言。
通过python自带的一个方法可以查看。
```python
ord()    此方法可以查看对应字母的ascll码！
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181115223326630.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### 小结
今天的python小课堂主要介绍了序列的总结(```str、list、tuple```三剑客)，所谓的```序列```二字，重要的是```序```这个字，也就是说这三种基础类型的内容元素都是有序的，每位都可以通过自带的下标索引(索引，index，可以理解为现实生活中字典的目录栏，有了```索引查找```你想要的信息会一目了然，非常快！)来获取不同位置的值，正因为它们是有序的！

### 个人心声



python的基础类型介绍到现在基本要接近尾声了，虽然这些基础的python语法很枯燥，但是打好基础是非常有必要的，在未来的编程道路上，有良好的基础才可以减少代码的bug，就像盖房子一样，地基不稳，hhhh，小心楼塌啊！！


有想学python的朋友，欢迎关注公号哟：
![咪哥杂谈](https://img-blog.csdnimg.cn/20181111210949311.png)









## python小课堂10 - 基本数据类型终篇集合和字典


### 基础类型集合 

python中集合的概念就像我们高中数学学过的集合概念相似，集合英文：```set```。下面来看下集合的写法：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181120123748423.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

重点，说下集合的特色：

```python
>>> {1,2,3,4,5,6} - {3,4}
{1, 2, 5, 6}
>>> 
>>> {1,2,3,4,5,6} & {3,4}
{3, 4}
>>> 
>>> {1,2,3,4,5,6} | {3,4}
{1, 2, 3, 4, 5, 6}
```

特性：

```python
-  :   通过减号，可以将后者集合的元素从前者集合剔除。

&  :   通过单与符号，可以将两个集合之间通过元素组合成新的集合。

|  :   通过竖线符号，可以将两个集合做并集处理，相同元素去除。
```

创建一个空的集合操作：

```python
set()
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181120123943204.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

> Tips:
> 集合，作为python中的基础数据结构，与上一章节介绍的序列从概念上来有些特性是相反的。其一：集合中是不能存在重复元素的！可以试下{1，1，2，3}这样在idle中查看输出结果是什么！其二：集合中的元素是无序的。

关于集合记住2个特性以及三个操作即可。



###    基础类型字典


python的基础类型----字典，英文：```dict```。

在实际生活中，实际上对应的就是我们的字典。看下图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181120124023920.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

当我们使用字典时查找一个陌生的字，需要先对拼音首字母进行检索，再通过其下面的具体拼音定位到具体页数。

在python中亦是如此，dict的写法如下：


```python
{'a':1,'ai':1,'an':2}
上面就是图片中字典对应的拼音加页数。
通过{x : y}这样的形式来表示字典!其中x、y是python的基础类型！
在python中我们经常把x、y称之为 key - value，中文键值对。
```
<font color = red>**注意：dict中的key位置是不可变的基础类型，value位置可以是任意基础类型，后续小课堂中会说到不可变性。**

在idle中实验一下：

实验一：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181120124111863.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

实验二：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181120124124548.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

对于dict字典的操作，实际上多多注意key-value即可，日常通过key去访问value的场景比较多，应用dict的场景多为物体之间起到了映射关系，就像拼音字典的索引目录一样！

### 基础类型终篇的总结
一图胜过千言万语！接下来看下思维导图的总结：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181120124146467.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

点开食用，效果更佳哟！

### 个人心声

到这里，基本上基础数据类型算是总结完了，通过一个星期的日日更新，总结了一遍所有python的基础类型，以及涉及到的知识点，int，float，bool，str，list，tuple，dict。通过这种总结自己对基础数据类型又更深了一步了解，不管有没有人看，hhhh，收获最大的还是自己呀！


 


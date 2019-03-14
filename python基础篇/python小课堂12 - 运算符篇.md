## python小课堂12 - 运算符篇


### 前言 
继续回归python小课堂！这几天状态有点不佳，本章小课堂只想上图，不想说话！看图吧.....

1.算数运算符：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114005805.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

没什么好说的，前面基本介绍的滚瓜烂熟了。

2.赋值运算符：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114020612.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

没什么好说的，直接看下面代码吧！

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018112511403051.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

其余的同理，记住一点，赋值运算最终是要达到赋值的效果，也就是将计算后的结果赋值于左侧变量。上例即a。

3.赋值运算符：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114044986.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

没什么好说的！比出来的结果是布尔类型，前面小课堂已经介绍过了！注意，能比较的不一定是数字，字符串也可以进行比较，元组、列表都是可以进行比较的，不信的话自己测试下！

4.赋值运算符：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114100136.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

这个需要说下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114109610.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

结论：is代表身份运算符，不仅仅判断的是值，还判断了变量的内存地址是否一致，只有两者都一致的时候，结果才会返回True，缺一条件返回即为False。而 == 只进行值的判断，is not 就是与is最终结果相反。

5.逻辑运算符：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114123396.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)
具体重点看下图！

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018112511414699.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

6.成员运算符

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114157616.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

具体重点看下图！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114205933.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


7.位运算符

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114217292.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

位运算符都是对二进制数字进行操作的！继续看图：

按位与运算：
```python
>>> a = 2      
>>> b = 3  
>>> a & b  
2
```
解析：

将a，b转成2进制进行计算，数列操作，个位上0&1=0，十位上1&1= 1。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018112511425136.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


按位或运算：

```pyhton
>>> a = 2      
>>> b = 3  
>>> a | b  
3
```

解析：

将a，b转成2进制进行计算，数列操作，个位上0|1=1，十位上1|1= 1。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114323617.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

其余的都是一个道理！

###   额外知识点

如何判断一个变量的类型？

之前小课堂中介绍到过一个type()，例如下面：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114342176.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

上面的方法虽然可以对变量的类型进行判断，但python中官方推荐的方法是下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114351938.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

> Tips：
> 提前引出对象的三个特征：id、value、type。

###   总结思维导图



点开食用，效果更佳:

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018112511441992.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


有想学python的同学，欢迎关注公号：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125114453423.png)


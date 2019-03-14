## python小课堂13 - 流程控制语法篇


### 前言

ε=(´ο｀*)))唉，上篇文章写的软文，即使分享了朋友圈。。。发现阅读量也不是那么大呀，对比了下隔壁的那位老大哥，人家分享朋友圈就70+的阅读量。。。还是鸡汤文！算了，我还是踏踏实实写我的技术吧~今天继续python小课堂的知识分享。今天要介绍的是python中的程序控制关键词，也就是条件，以及python的包、模块的概念。

### 条件控制、循环控制

在步入正题之前，先来阐述一个概念 --- 表达式(运算符 和 操作数所构成的)。

它长什么样子呢？如下：

```python
a = 1 + 2 + 3
a = [1,2,3,4]
a > b
```

而现在写的代码，就是用类似上面的表达式所构成的，我们可以通过条件控制，循环控制来使代码形成具有逻辑的体系。

打开IDEL，按下**Ctrl + n**打开文本编辑器，后续设计到代码块的格局。或者点击idle的File --- > New File 也是一样的。

##### 1.条件控制  (if ，if  else， if elif)

之前一直说过的，计算机世界中实际上映射了现实生活中的例子！在现实生活中，举个例子：如果我当年好好学习，那么我现在早就是大神了！这样的话语就是条件控制，当然现实世界并不存在如果，说多了如果都是侥幸心理罢了。

if代表的就是如果。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129122749846.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

需要注意的是：Python 不想其他语言通过{}来控制代码的作用域，在之前的小课堂就说过，写代码时通过4空格来控制！


如果条件为真，就走条件里的内容，否则就走其它的条件里的内容，else就是其它的意思。

if - else:

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129122805471.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

if - elif：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129122815315.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

给个经常用到的小例子吧，不要小瞧if - else！我们生活中的各种账号登录，可以来写一个小程序看看：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129122823582.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

要说明的是，我上面的截图中，有一点是不符合python官方规范的！赋值的前两步骤，是两个恒定不变的字符串，这样的东西在编程中称之为**常量**！常量正规写法**应该大写**！所以下面我修改了....


代码本文版：


```python
CORRECT_USER = 'sssyyy'
CORRECT_PASSWORD = '123456'

username = input('请输入登录的用户名:\n')
password = input('请输入登录的密码:\n')

if CORRECT_USER == username and CORRECT_PASSWORD == password :
    print('登陆成功了！')
else :
    print('用户名或者密码错误！')
```

通过上面的小程序，将前几章的小知识串联起来了一部分。通过if来判断是否登录成功，有变量的赋值操作，还有 and 、== 操作符，以及input()这样的python自带方法。

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129122905538.png)
所以当我们输入1的时候，实际上进去的是字符串类型，这也是为什么我小程序中是将字符串赋值给了变量。

 ##### 2. 循环控制   (while  ，for ...  in ，continue，break)

循环控制：依然是以现实生活中举例子吧，有些朋友们一定听说过暴力破解，在登录某些网站时，通过不断对其密码的排列组合进行登录，也就是所谓的穷举。每登录一次，换一次密码组合尝试，最终达到对比出正确的密码进行登录。而这种思想，就是在循环控制下实现的。

while中文含义是在…期间。

while:

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018112912292733.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


如何跳出呢？继续写个小例子来演示，现在有个场景，每次将变量a加2，如果当a大于10，则结束while循环。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129122936595.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

>Tips：
>```python
>a = 1
>print(f'当前的值为 {a}')
>f'{变量名字}'  ----->  这样的语法是python3.6 以上的新特性，支持直接将字符串进行格式化。而不需要自己手动在后面累加。


while - else：



![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129123033951.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


for ，为了的意思，for关键词在之前有介绍过，我们可以通过for来遍历序列（str、list、tuple）、字典(dict)、集合(set)这样的类型。。

for：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129123047324.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

> Tips：
> print()第二个参数添加end，就是每次追加''，而print默认追加\n换行符
> print('',end = '')

来介绍一个python中比较屌的内置方法 --- > range()。

range()经常与for套用在一起使用，比如现在需要循环10次，每次循环打印出数字！如何去写：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129123114328.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

如果每次递增2个数字，再去打印呢？



![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129123122987.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

如果我想倒过来打印呢？



![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129123133376.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

> Tips:
> range(a,b,c)  --->  a，起始的数值 ； b，结束的数值； c，步长，类似之前介绍的切片特性的步长机制！

### 循环控制的跳出

在上面的while中，我介绍了通过一种“活”条件来实现跳出，那么有没有方法直接可以跳出循环控制呢！一定是有的，就是python中的关键词:**break,continue**

break：中文意思打破，中断！是不是很通俗易懂，再循环中加上break字眼，即可中断程序。

场景：数字a初始值为1，在while循环中，每次循环加1，当a = 10时，中断程序，并且输出中断程序。(初学者可以自己去idle中尝试动手！)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129123206659.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


continue：中文有继续的意思，所以在使用循环时符合当前条件，continue后面的代码都**不执行**，跳过后进行继续下一次循环。

场景：数字a初始值为1，在for循环中，每次将a累加1，一共循环20次并打印输出结果，在循环第10次的时候，跳过累加，打印出当前a的值。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129123219286.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### 总结

到现在python的流程控制也讲完了。基本上到这里如果有思路，爱动手的同学，已经可以自己开始编程了。无论学习哪种语言，重要的还是编程的思想！有了思想，无非就是需要熟悉熟悉语法罢了。来看看到现在为止，点亮了多少小图标了！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129123241531.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

有想学python的同学，欢迎关注公号：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181129123327529.png)
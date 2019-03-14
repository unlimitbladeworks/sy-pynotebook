## python小课堂26 - 进阶必修之闭包（一）

### 前言
时光飞逝，直至今日，2019年的第一个月都要过完了！从2018年10月份决心开始写python小知识，已经过了3个月了，写到现在基本上占总进度的一半了吧！


从本章起，开始进行python进阶篇的知识分享，python小课堂0-25皆为基础知识，其中有两篇是结合基础讲解实战，分别是暴力破解和图片定位，链接如下:

[python小课堂20 - 5分钟教你用图片定位具体地址！](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659112&idx=1&sn=93c28fc18e1af2c84666fbf9b9a01218&chksm=8c97d1d1bbe058c7b00d4a7065507617caeea02ffc640c2d0318914a008432bb37f3f47e1f64&scene=21#wechat_redirect)

[python小课堂17 - 30行代码破解加密ZIP文件](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659077&idx=1&sn=232d05d83a95d9a8e1a2827d1c11934f&chksm=8c97d1fcbbe058ea9442195b4b7c500dc26670b31bde1690202076de523897f4cad00986b412&scene=21#wechat_redirect)



相信学到现在，这两篇实战的原理以及代码你一定可以看懂了！好了，废话不多说了，进入今天的正题吧，python进阶篇-闭包！


### 再谈函数

讲真的，闭包从概念是非常难讲明白的一个词。所以，先来搞清楚函数在Python里是怎样的存在，深入了解了函数的概念，会为学习闭包打下基础。闭包与函数有着密不可分的关系。



通常，在一般的编程语言中，函数只是一段可执行的逻辑代码，并不是所谓的对象。比如在Java中，如下代码，打印输出一句话：

```java
/**
* 函数描述：说一句话
* public : 共有方法
* void   ：没有返回类型
* @param words 参数，传入的话语
*/
public static void say(String words) {
    System.out.println(words);
}
public static void main(String[] args) {
    say("你好");
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190129122911835.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

像Java这种有明确类型定义声明的语言，如果没有设置返回类型，在调用函数时，则不能用任何变量去接受，否则编译时就会报错。（只是作对比的例子，非专业人员忽略即可）。



再来看下Python中呢，若我们像打印一句话，也需要定义一个函数，然后调用即可，同时，我们可以通过任何变量来将此函数进行赋值操作，如下：
```python
# 打印一句话
def say(words):
    print(words)


say('你好')
a = say
print(type(a))
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190129122930504.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

结果显示，在Python中，是可以用**函数不加小括号**的形式将其赋值给任何变量，并且其自身也可以作为**函数的参数进行传递**，不仅如此，函数也可以用此种方式将其自身作为**返回结果进行返回**，通过上面的代码可以看到，say赋值给变量a，打印a的类型，得到**class function**，说明它是一个**类**。之前的小课堂中提及过，在Python中**一切皆为对象**，函数也不例外！



可能有人会说，你在Java中不是这么写的啊，你也像在Python中那样调用试下，看看结果呗，于是有了下面的图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190129123029687.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到，当在Java中写say不加小括号时，编译器已经报错了，提示找不到say的标识符（会Java的人都知道这么写是没有意义的）。这也是Java与Python作为编程语言的不同之处，一个为编译型语言，一个为解释型语言。



正因为Python有了这么一个特性，所以才会很好地支持接下来要介绍的闭包！

### 什么是闭包？
在解释概念之前，先来看个自带场景的小例子吧！不知道大家还记不记得小学（是小学还是初中来着，忘记了...默认小学吧！）学过的一个数学公式，如何去求圆的面积？记忆好的一定记得：S=π*r^2r为圆的半径，π为3.1415926.....



现在的场景是，需要定义一个求圆形面积的函数，同时，在这个函数的外部还要包裹着一层求圆形面积之前提前做准备的外层函数，这外层函数的目的是你可以在真正求圆形面积前演算一些内容（假设大家都是刚学这个公式的小学生哟！），写法分解成以下步骤：

#### 1. 定义两个函数，并且在调用内部计算圆形面积的函数
```python
def circular_area_pre():
    def circular_area():
        print('This is circular_area function!')
```
其中 circular_area_pre 是计算圆形面积前的准备函数，circular_area 是计算圆形面积的函数。此时若想在外面直接调用 circular_area 如何做呢？（不要感到这种写法奇怪，Python中是可以进行**函数嵌套**的！）尝试下自己手动调用！如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190129123224405.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

当尝试在外层直接进行调用时，可以看到，已经报错了！如何正确调用呢？在上面的标题「再谈函数」中说过，函数可以通过“对象”的写法将其自身作为结果进行返回！（忘记的往上翻翻，找找看！）所以改下写法如下：

```python
def circular_area_pre():
    def circular_area():
        print('This is circular_area function!')

    return circular_area()

c = circular_area_pre()
c()
```

通过调用外层的计算准备函数 circular_area_pre ，函数返回接受到的内部计算圆形面积函数 circular_area 作为变量c，以函数的形式调用变量c（也就是在c后面加上小括号进行函数调用），执行即可！而此时的变量c实际上是一个函数（这点在后面的步骤中会进行**验证**，先记住。）！执行一下，咦？？？发现报错了，因为多了个小括号：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190129123256631.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

去掉后成功，所以一定要注意小括号的问题！！如下图 :

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019012912330585.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

#### 2. 在第一步的基础上，将其补充完整，套入公式

```python
def circular_area_pre():
    """ 省略了一些演算步骤的代码,毕竟假设嘛 """
    pai = 3.14

    def circular_area(r):
        s = pai * r ** 2
        return s

    return circular_area

c = circular_area_pre()
print(c(10))
```
解释下这段代码的含义，将pai（π）定义为3.14，放在作为计算圆形面积之前的函数 circular_area_pre 中，而求面积的公式则写在 circular_area 函数中，将面积变量s作为内部函数返回，同时，最外层的 circular_area_pre 函数返回 circular_area 函数作为结果。想要计算出圆形的面积，在外层就需要先调用 circular_area_pre 准备函数，在调用其返回结果变量c，打印 c(10)，可以看到如下图结果：

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019012912333338.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

打印结果输出的是314.0，实际上就是将10传入到了 circular_area 函数中，而其中的**pai引用**的是在 circular_area_pre **局部**里定义的pai，值为3.14 。验证下步骤1说的，看下变量c的类型，以及直接打印c会出现什么样子的结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190129123354971.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

现在可以看到，其实变量c就是一个类，而它的类型是**function**. 

#### 3. 关于 pai 的定义位置


抛开外层的准备函数，假设现在只有计算圆形的函数，假设阿基米德突然复活了，把这个pai推算成了其它数字！姑且定义为10吧，如下：

```python
pai = 3.14

def circular_area(r):
    s = pai * r ** 2
    return s
pai = 10
print(circular_area(10))
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/201901291234224.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

输出结果为1000，记住这个值，咱们继续往下看！

#### 4. 如果此时在外部修改了pai的值，打印结果如何？

回到双层函数的示例来，在 circular_area 函数中，pai是没有被定义的，所以它会向上一层寻找，于是找到了 circular_area_pre 函数中定义的pai，所以计算的时候值就会取为3.14，假设现在依然在最外层函数的外面修改pai的值，继续改为10，那么代码的结果会是如何呢？

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190129123439662.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

来看下：

```python
def circular_area_pre():
    """ 省略了一些演算步骤的代码,毕竟假设嘛 """
    pai = 3.14

    def circular_area(r):
        s = pai * r ** 2
        return s

    return circular_area


pai = 10
c = circular_area_pre()
print(c(10))
```

在调用准备函数之前，将pai修改为10！猜猜看，结果会打印出什么呢？（先不要看结果，自己思考一下！）结果如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190129123458619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

没错，你没有看错，依然是314.0，这个结果与没加入pai = 10 的代码得到的结果是一样的！为什么不是1000呢？？？请继续往后看！

#### 5. 闭包的概念

啰里啰嗦的举例了这么多，到底跟今天要说的闭包有什么关系呢！各位看官，莫急，下面就是重头戏了，只要你耐心的把上面的示例都看懂，保证你看完接下来的这段概念性文字一目了之！



在上面的函数 circular_area 与 pai = 3.14 形成了闭包！通俗的说就是把内部函数 circular_area 与 pai = 3.14 这个环境变量包含在了一起，做了一个封闭，所以外界想要去改变 pai 这个变量是改变不了的！



需要注意的是，所谓的环境变量，一定要定义在**内部函数的外部，就像 pai 一样**，且不能是**全局变量**！



**闭包的概念：闭包 = 函数 + 环境变量！**

#### 6. Python函数作用域

Python变量的作用域一共有4种，分别是：

- L （Local） 局部作用域

- E （Enclosing） 闭包函数外的函数中

- G （Global） 全局作用域

- B （Built-in） 内建作用域

以 L –> E –> G –>B 的规则查找，即：在局部找不到，便会去局部外的局部找（例如闭包），再找不到就会去全局找，再者去内建中找。



通过这段作用域的概念，可以得知，为什么在求面积的函数外部去修改pai的值，最终取到的还是原来的3.14，Python的变量查询是一个“由内到外”的过程，一旦找到，则取最内部的变量进行使用。

### 如何查看一个函数是否闭包
闭包是可以通过python内置函数检测出来的，如下：


```python
def circular_area_pre():
    """ 省略了一些演算步骤的代码,毕竟假设嘛 """
    pai = 3.14

    def circular_area(r):
        s = pai * r ** 2
        return s

    return circular_area

pai = 10
c = circular_area_pre()
print(c.__closure__)
print(c.__closure__[0].cell_contents)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019012912383161.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

通过调用 __closure__ 内置方法可以查看到两个内存地址，结果返回cell就是闭包，None 则不是闭包，可以看出来其实这是一个元组类型，使用[0].cell_contents可以得到闭合数值，也就**闭包**所需要的**环境变量**。

小题，请你判断下面这段代码属于闭包吗？如下：
```python
def circular_area_pre():
    """ 省略了一些演算步骤的代码,毕竟假设嘛 """

    def circular_area(r):
        pai = 3.14
        s = pai * r ** 2
        return s

    return circular_area


c = circular_area_pre()
print(c.__closure__)
print(c.__closure__[0].cell_contents)
```

答案：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190129123922384.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

只把pai 进行了换位，导致现在的写法并不是闭包，调用Python内置方法来查看，得到的是None，没获取到闭包时产生的cell！

### 总结

说真的，本章的闭包要想讲明白真的挺难得，这篇文章大概是花了一星期的时间去写的，基本上基础的概念介绍的差不多了，但是要想懂闭包，还是得看懂示例才行，记住**闭包就是函数和环境变量封闭组成的！外界想改环境变量？没门！**



后续还有一篇闭包二，会讲述闭包的使用场景，究竟什么时候使用闭包才是合适的。敬请期待.....



至此完！ 
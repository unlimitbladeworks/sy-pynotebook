## python小课堂22 - 面向对象(四)
### 前言
本节介绍面向对象的“继承”特性，这将是面向对象篇最后的基础部分，随后我会画出一个思维导图来总结下这一个月以来面向对象设计到的知识点。



面向对象的三大特征分别为：**封装、继承、多态。** 封装实际上就是上次讲的私有化，但是封装是一种思想，它所涉及的东西非常广，后续在慢慢补充，忘记的可以看下上次的总结。[python小课堂21 - 面向对象(三)](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659128&idx=1&sn=f15496cd61c29e51ee3662af1884fe31&chksm=8c97d1c1bbe058d7a7a4891cf9c318f6dc397939cfd231023bd1b3e85daeeec853fa93c9db43&scene=21#wechat_redirect)



而多态打算作为后续的进阶知识点来介绍。所以基础部分到继承就会将面向对象作为一个完结。废话不多说了，进入正题吧。


### 继承

何谓继承？在现实世界，比如爸爸到了一定年龄终归要留下一笔财富，而此时的财富一般就由儿子来继承。这样一来原来属于爸爸的钱，儿子在继承这笔财富之后，便有了使用权。所以这里儿子是**子类**，爸爸是**父类**。



而映射到计算机中也是一个道理，可以想象之前的python面向对象的章节中，我一直以女朋友作为例子来进行讲解，这里女朋友再往上抽象一层得到的是什么呢？女朋友可以归为人类这一范畴。所以我们可以说女朋友继承了人的基本特性，人都有名字，性别，年龄的属性，来看下女朋友的类是如何继承人的类去实现的：

父类（人类）：
```python
class Human(object):
    """人的初始化方法,传入名称和年龄"""
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def say(self):
        print(f'人的名字:{self.name}')
        print(f'人的年龄:{self.age}')

    def eat(self):
        print('This \'s Human eat method!')
```

可以看到，上面的代码中将女票的姓名与年龄提到了人的初始化方法中，再来看下女票类的代码：

```python
from toobject.python22 import Human

class GirlFriend(Human):
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age, weight):
        self.weight = weight

    # 行为，说出自己的特征
    def eat(self):
        print('Here \'s girlFriend eat method')


girlFriend = GirlFriend('女儿国公主', 18, 90)
girlFriend.say()
```

可以看到```GirlFriend(Human):```通过这样的形式来实现所谓的继承，调用时，我们可以直接调用父类的say()方法，来看下能否直接调用。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190111190655139.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


报错了，可以看到英文大致意思是说女朋友这个类并没有name的属性！为什么呢？可以思考下，我们通过子类直接调用父类的方法，然后报错信息出现在了父类的代码上。

实际上因为我们在调用女朋友类的时候，没有将name、age属性向父类进行传递，所以在父类中的name、age属性是空的，所以会在打印时发生报错！

### 继承调用父类

原因既然知道了，那么一切都好说了，我们现在只需要在女朋友初始方法中调用人的初始方法，并将name、age参数传递到后面，即可实现调用父类的say()方法，来看下代码：

```python
from toobject.python22 import Human

class GirlFriend(Human):
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age, weight):
        Human.__init__(self, name, age)
        self.weight = weight

    # 行为，说出自己的特征
    def eat(self):
        print('Here \'s girlFriend eat method')


girlFriend = GirlFriend('女儿国公主', 18, 90)
girlFriend.say()
print(girlFriend.age)
print(girlFriend.name)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190111190737399.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

通过```Human.__init__(self, name, age)```将外面的参数传入到父类中，成功调用了父类的方法以及属性，也就是人中的姓名和年龄，以及说话的方法。


### 继承中的super关键词



上面的写法大家可以想一想有没有什么问题呢？虽然确实可以通过用父类的类名来直接调用__init__方法进行初始化，而这种特性在之前的面向对象小课堂中也讲过，直接用类.方法是python这门语言的一种特性！忘记的话可以回顾：[python小课堂19 - 面向对象篇（二）](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659101&idx=1&sn=5d8b202ca7fb139ef72284bd90a7c38f&chksm=8c97d1e4bbe058f2963a2b14e2022f0c8e103b0e3696467967731a16be6654cebf56834106b0&scene=21#wechat_redirect)

假设后续我们要修改女朋友所继承的父类，不让她继承人类了，原本女儿国国王就是妖怪的化身！所以让她继承妖怪类好了....~那么此时我们就需要改两个地方了，如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190111191105444.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

要知道一点，写程序其实有一个本质，就是如果有改动的地方，尽量让自己写出的代码在原有的基础上进行最少的修改！这点也就是设计模式常说的**开闭原则**（听不懂的话忽略即可，有好奇心的宝宝可以去查查看咯...）



所以为了遵循以上的原则，我们将原有程序进行改装，就要用到标题4所说的**super**关键字了！super：超级的意思，因为有些语言中父类也叫超类，所以估计才会用super来作为调用父类的关键词吧，个人猜测.....接下来看下如何进行调用呢？

```python
from toobject.python22 import Human

from toobject.python22 import Human

class GirlFriend(Human):
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age, weight):
        super(GirlFriend, self).__init__(name, age)
        self.weight = weight

    # 行为，说出自己的特征
    def eat(self):
        print('Here \'s girlFriend eat method')


girlFriend = GirlFriend('女儿国公主', 18, 90)
girlFriend.say()
print(girlFriend.age)
print(girlFriend.name)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190111191148586.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

通过 ```super(GirlFriend, self).__init__(name, age) ```的调用方式，将子类以及self传入到super里，在调用父类的构造方法将参数传入即可！



仔细思考下，这样一来，我们如果改变了继承类，将女朋友的父类改为妖怪....那么只需要在class声明的小括号后修改就能达到目的了，同时实现了代码的最小改动！

### 继承中的重写

心细的同学在上面的子父类中发现了一个相同点，没错，就是它们都共同有一个名为eat()的方法函数。如果我此时用实例对象去调用eat()，你们猜会打印输出什么？

```python
from toobject.python22 import Human

class GirlFriend(Human):
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age, weight):
        super(GirlFriend, self).__init__(name, age)
        self.weight = weight

    # 吃
    def eat(self):
        print('Here \'s girlFriend eat method')


girlFriend = GirlFriend('女儿国公主', 18, 90)
girlFriend.eat()

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190111191231895.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

输出了子类eat()方法中的调用，说明了子类把父类的eat()覆盖掉了，说专业点就是传说中的重写！  那么问题来了，**为什么会有重写呢？重写的好处是什么呢？**



**必然是扩展性与复用性**！大家可以想想，女朋友继承了人类的特征，会吃！所以到具体类中，让“吃”具体化，女票有着一套自己吃东西的体系！



若既想保留人类的吃方法，又要凸显女朋友吃法的个性，那该如何是好呢？这点就利用了super关键字去解决了.....！

```python
from toobject.python22 import Human

class GirlFriend(Human):
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age, weight):
        super(GirlFriend, self).__init__(name, age)
        self.weight = weight

    # 吃
    def eat(self):
        super(GirlFriend,self).eat()
        print('Here \'s girlFriend eat method')


girlFriend = GirlFriend('女儿国公主', 18, 90)
girlFriend.eat()
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190111191305780.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到都输出了.....

### 总结

总结一下，python的继承跟别的语言不太一样，比如Java类的继承，只能单继承，而Python不一样，Python自身可以多继承，也就是继承多个类，这点放到后面讲，因为是进阶的知识点。



到这里，我就将面向对象所有的基础点讲完了.....来用思维导图做个总结吧！基础归基础，后续还有面向对象的进阶部分，敬请期待......思维导图如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190111191329159.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

至此完！

有想交流沟通python相关知识的同学，欢迎关注公号：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190111191401843.png)
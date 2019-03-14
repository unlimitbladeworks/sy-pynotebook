## python小课堂19 - 面向对象篇（二）
### 前言
哈喽呀Everybody，又到了更新干货的时间了，继续python小课堂的回归之路，面向对象篇的第二章，面向对象的涉及的东西实在是太多了，所以打算拆开三次写吧，后面还有一次面向对象篇，但是打算写完这篇之后用面向对象的设计思想来一波实战篇教学，依然是和安全相关的，敬请期待.....

### 实例对象中的self

回顾下上一章中，学习了定义一个对象（类）的方法，并且这个类中有自己的类变量以及实力变量，还有自己对应的方法以及构造方法。在实例方法中有个特殊的关键词需要默认传入 -- self 。来看下引用上节的例子。

```python
class GirlFriend():
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self,name,age):
        self.name = name
        self.age = age

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')

girlFriend = GirlFriend('人类女孩',18)   # 实例化
girlFriend.say_feature()
```
实际上，**self**这个关键字并不一定非得叫**self**，如果学过java的同学一定知道this这个关键词，特指在一个类中实例对象生成后的本身，而python中的self与其一致，我们可以将self修改成this来看下程序会不会正常运行。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224125025754.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到上图，改成this后依然成功运行，所以**self**只是python中的一个官方写法，具体你要定义成什么样子的默认第一个参数，随你喜好，但是推荐默认self就好啦。


### 实例对象中的变量机制(__dict__)


通过**__dict__**  可以查看实例对象的属性。什么意思呢？来看下：

```python
class GirlFriend():
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')

girlFriend = GirlFriend('人类女孩', 18)  # 实例化
print(girlFriend.__dict__)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224125059168.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到结果，将实例化后的对象中的变量成员以字典的形式打印出来，name和age是实例变量，而人类女孩和18便是我通过创建对象时传入的参数。

### 实例方法访问变量

实例方法：见名知意，即类中定义的方法，需要实例化对象后才能调用的方法称之为实例方法。比如在上面的GirlFriend类中的say_feature()，就叫实例方法。那么问题来了，实例方法可以直接访问实例变量，这是大家都可以想到的，比如在say_feature()中通过self.name调用了实例变量name。那实例方法中如何访问类的变量呢？在上面的代码中，**类变量**就是total_nums，也就是你迄今为止交过女朋友的总数量。
先来个<font color = red>**错误**</font>的例子：

```python
class GirlFriend():
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age):
        self.name = name
        self.age = age
        print(f'访问类变量total_nums:{total_nums}')

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')


girlFriend = GirlFriend('人类女孩', 18)  # 实例化
print(girlFriend.__dict__)

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224125148155.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

看到控制台报错，输出没有定义total_nums，说明这种方式在实例方法中直接访问类变量是**错误**的。

<font color = gree>**正确**</font>的例子1：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224125224264.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

实际上在上一节的python小课堂的末尾处，提到过如何在类外访问类变量，直接通过类.变量即可访问，在实例对象内部也可以通过这种方式进行访问。

<font color = gree>**正确**</font>的例子2：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224125243565.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

```python

# 通过 self.__class__ 调用类变量也可以进行调用

self.__class__.total_nums   
```

类变量还有个特性，就是实例化对象将其共有，这种场景也许在以后的编程中会遇到，我这里依然以女朋友举例，每个实例变量是你每个不同女票的名字和年龄，而假设你每次交一个女票，这个交女朋友的总数total_nums就会增加1。

来看下代码示例：

```python
class GirlFriend():
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age):
        self.name = name
        self.age = age
        self.__class__.total_nums += 1
        print(f'迄今为止交到的女朋友个数total_nums:{self.__class__.total_nums}')

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')

girlFriend = GirlFriend('人类女孩1', 18)  # 实例化
girlFriend2 = GirlFriend('人类女孩2', 23)  # 实例化
girlFriend3 = GirlFriend('人类女孩3', 20)  # 实例化

````

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224125309851.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


看到结果，每次实例化一个女盆友，总数都会增加一次使用场景自行细细品味一番吧......



再多说一句，方法和变量之间的关系：变量其实就是我们日常所说的数据，而方法就是如何去处理数据，也就是将变量读取后进行相关处理。这层处理关系就是方法和变量的关系！

### 类方法

在本章开篇处介绍了实例方法，那么类方法则是不需要进行实例化对象，可以直接通过类.方法进行调用。来看下面的例子：

```python
class GirlFriend():
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')

    # 类方法
    @classmethod
    def make_girlfriend_count(cls):
        cls.total_nums += 1
        print(f'迄今为止交到的女朋友个数total_nums:{cls.total_nums}')

GirlFriend.make_girlfriend_count()
GirlFriend.make_girlfriend_count()
girlFriend = GirlFriend('人类女孩1', 18)  # 实例化
girlFriend.make_girlfriend_count()
```

通过在方法上面加上<font color =red> **@classmethod**</font>，这样来定义类方法，这个写法可以先了解下，后序会讲到python的装饰器，就知道这种写法的意义了。classmethod，中文翻译就是类方法的意思，在方法的默认参数中，需要默认给出一个<font color =red>**cls**</font>作为参数，这里类似实例方法中的self字段，他们都是形式上的默认参数，名字可以改变，不一定必须叫cls，python默认会给出cls，而cls是class的简写，<font color =red>也指代的是自己本身。</font>



将交到女朋友的个数作为类方法来演示下最终的运行结果：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224125451633.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

调用类方法时，只需要通过类名称直接调用即可。当然python也支持先实例化在调用类方法，也不会报错，可以看到上图中最后一次 调用，但是绝不推荐这样用，因为没有意义！

### 静态方法

静态方法：定义时，不需要像类方法和实例方法默认传入参数，在方法上面声明一个叫@staticmethod的装饰器，staticmethod，中文翻译静态方法。来看下写法：
```python

class GirlFriend():
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')

    # 类方法
    @classmethod
    def make_girlfriend_count(cls):
        cls.total_nums += 1
        print(f'迄今为止交到的女朋友个数total_nums:{cls.total_nums}')

    @staticmethod
    def study_language(language,score):
        print(f'我在学习{language},熟练分数:{score}')

GirlFriend.study_language('中文',90)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018122412551867.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

**注：**在静态方法和类方法中，是无法直接用self.xxx引用实例变量的。可自行尝试！



类方法和静态方法的区别：在调用时，都可以通过类名直接进行调用。但是一般不推荐使用静态方法，因为类方法同样可以实现，并且可以通过默认参数cls直接引用类中的类变量使用。

### 总结

以上就是python面向对象的第二部分，后面我会画一个思维导图来整理下学到的相关知识，其实图一画出来，逻辑就非常清晰了。回顾下本章内容，介绍了self的应用，类方法的应用，实例方法的应用以及相互之间访问的关系。文章略长，还望耐心观看....切忌浮躁（也是说给自己的！）

至此完！
<hr/>

有想学python的同学，欢迎关注公号：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224125601588.png)
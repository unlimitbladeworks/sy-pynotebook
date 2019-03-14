## python小课堂18 - 面向对象篇（一）

### 前言

又到周末了！时间过得好快啊...依稀记得公众号刚开时，有个大学同学跟我说，介绍的太详细了，什么时候才能介绍到面向对象的章节啊！结果时间飞逝，2018年12月1日，距离开号正式写文章的时间（2018年9月21号）已经过去2个多月了...

好了废话不多说..依然继续回归python小课堂知识分享，这次开始了重头戏，就是编程届的重要思想 --- 面向对象(没错，它是一种编程的思想)。时常在编程届，经常听到有人说找不到女朋友怎么办？对于程序员来说，so easy啊，直接new 一个“对象”出来就行了！而在python中，对象的概念也是非常重要的，因为在python中有着万物即对象的概念，所有东西都可以看做是对象！今天就来演示下，如何用代码创建出一个女朋友来！~（屌丝！！捂脸跑...）

### 面向对象编程

什么是面向对象编程呢？之前的小课堂中，我一直在强调一个概念，就是计算机中的代码就是现实世界的映射，而对象也不例外。举个例子来说，比如现实世界的车，奔驰，宝马，玛莎拉蒂，阿斯顿·马丁，这些品牌所造出来的车，都属于汽车这一类型，而所谓的汽车这一类型映射到编程世界就是对象。再举个栗子，前言说到的女朋友，也可以看做一个类型，对应到代码中也可以是一个对象。。所以类型，我们一般在编程中简称类， 类 = 面向对象。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181220122503971.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### 定义一个女朋友(创建对象)

自己用代码创建一个女朋友吧！你的女朋友，你当然知道她的姓名，年龄，身高，生日等等，这里所说的都是描述女朋友的特征，对应到python代码中可以理解为女票就是一个对象，而特征即为这个对象的特有属性。

**类**，在Python中用**class**作为关键词表示。下面来看下代码演示：
```python

class GirlFriend():
    name = '女儿国国王'      # 姓名
    age =  300              # 年龄
    height = '177'          # 身高
    birthday = '1718-12-01' # 出生

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')
        print(f'我的身高:{self.height}')
        print(f'我的生日:{self.birthday}')

girlFriend = GirlFriend()   # 实例化
girlFriend.say_feature()  # 调用对象的方法
```

> 最终输出：
>\>>>我的姓名:女儿国国王
>\>>>我的年龄:300
>\>>>我的身高:177
>\>>>我的生日:1718-12-01

① 可以看到上述代码段中，class 后面定义了类的名字女朋友，一般定义对象时，命名符合首字母大写，后面每个单词首字母大写，编程中称之为驼峰命名法。例如girlfriend，你就要写成GirlFriend。名字定义完后面跟上小括号，需要注意的是小括号中只能传入另一种对象，而非类似函数的形参。后续会讲到**继承**，到时候就懂了。

② 在类中，我定义了一些女朋友的特征，并且给了她一个行为，她可以自己说出自己的特征。这个行为和我们定义的函数一样，也是通过```def```定义，在类中，我们可以将之成为方法，方法和函数的写法一样，但是概念上稍有差异。方法是从设计层面定义得，而函数是从执行过程中设计的，了解即可。然而调用自身的属性时，必须要在方法中传入形参```self```，只有通过self.xxx才可以调用变量(name,age....)，也就是特征。否则可以自行尝试，直接调用变量名称会报错。

③ 如何调用，让女朋友自己说话？girlFriend = GirlFriend() 通过这样的写法，将对象进行实例化，然后可以通过赋予的变量加以.来调用她内部的方法。可以看到上段代码最后一行就是调用方式。


思考一个问题，当我们有一个女朋友时，此时创建多个实例对象会怎么样呢？他们会属于一个对象吗？来看下：

```python
girlFriend = GirlFriend()   # 实例化
girlFriend1 = GirlFriend()
girlFriend2 = GirlFriend()
```

还记得python中自带的id()函数吗，可以通过此函数来查看对应的内存地址，结果如下：

```python
print(id(girlFriend))
print(id(girlFriend1))
print(id(girlFriend2))

>>> 1361650701648
>>> 1361650701760
>>> 1361650631512
```

显而易见！虽然公用的是一个女票作为类来进行实例化，但是到具体的对象时，她们之间的内存地址却不尽相同。

### 女朋友的初始化行为(构造函数)

什么叫女朋友的初始化行为呢？还是用上面的例子来举例说明，女儿国国王，初始的设定就是为了娶到唐僧，然后嘿嘿嘿........吃掉。来看下代码：

```python
class GirlFriend():
    name = '女儿国国王'      # 姓名
    age =  300              # 年龄
    height = '177'          # 身高
    birthday = '1718-12-01' # 出生

    def __init__(self):
        print('我要先把唐僧娶了，嘿嘿嘿....然后在吃了！')

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')
        print(f'我的身高:{self.height}')
        print(f'我的生日:{self.birthday}')
        
# 实例化时，会输出我要先把唐僧娶了，嘿嘿嘿....然后在吃了！
girlFriend = GirlFriend()   

>>> 我要先把唐僧娶了，嘿嘿嘿....然后在吃了！
```

可以看到我在女朋友的类中新增了一个 def __init__(self) 方法，此方法见名知意，init是初始的意思，也就是常说的构造方法。什么意思呢？每当我们实例化对象时，默认会调用此方法，一般用于类调用时候的初始操作，比如女儿国国王的初始任务就是对唐僧下手！



需要注意的几点如下：

①  __init__方法可以手动调用，但是没有必要。

```python
girlFriend = GirlFriend()   # 实例化
girlFriend.__init__()       # 可以通过调用此方法看下

>>> 我要先把唐僧娶了，嘿嘿嘿....然后在吃了！
>>> 我要先把唐僧娶了，嘿嘿嘿....然后在吃了！
```

② __init__()的默认返回值:None

```python
girlFriend = GirlFriend()   # 实例化
print(girlFriend.__init__())
print(type(girlFriend.__init__()))

>>> 我要先把唐僧娶了，嘿嘿嘿....然后在吃了！
>>> None
>>> <class 'NoneType'>
```

③ 尝试给init添加返回值，报错，可以看到只能返回None，不能返回其他类型。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181220122808702.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

<hr/>
对于女儿国国王为女朋友的例子，如果我作为她背后的黑幕，每次都想让她的初始任务听命于我呢，也就是所谓的每次实例化时，再将具体的任务分配给她，如何做到？于是有了下面的代码：


```python
class GirlFriend():
    name = '女儿国国王'      # 姓名
    age =  300              # 年龄
    height = '177'          # 身高
    birthday = '1718-12-01' # 出生

    def __init__(self,task_name):
        print(task_name)

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')
        print(f'我的身高:{self.height}')
        print(f'我的生日:{self.birthday}')

girlFriend = GirlFriend('我要先把唐僧娶了，嘿嘿嘿....')   # 实例化
girlFriend1 = GirlFriend('然后在吃了！')   # 实例化

>>> 我要先把唐僧娶了，嘿嘿嘿....
>>> 然后在吃了！
```

通过构造方法的传参，可以实现我们对一个对象实例化时进行可控的参数传入。但是需要注意，如果在构造方法处定义了参数，那么实例化对象时一定要传入对应的数量参数，否则会报错缺少参数的错误，如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181220122919322.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


### 类变量与实例变量的对比

什么是类变量？什么是实例变量呢？还是回归到“女儿国国王”女朋友的例子上：

```python
class GirlFriend():
    name = '女儿国国王'      # 姓名
    age =  300              # 年龄
    height = '177'          # 身高
    birthday = '1718-12-01' # 出生

    # 初始化构造方法
    def __init__(self,name,age):
        self.name = name
        self.age = age

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')
        print(f'我的身高:{self.height}')
        print(f'我的生日:{self.birthday}')

girlFriend = GirlFriend('人类女孩',18)   # 实例化
girlFriend.say_feature()
print(f'类变量姓名:{GirlFriend.name}')
print(f'类变量年龄:{GirlFriend.age}')

>>> 我的姓名:人类女孩
>>> 我的年龄:18
>>> 我的身高:177
>>> 我的生日:1718-12-01
>>> 类变量姓名:女儿国国王
>>> 类变量年龄:300
```

所谓的类变量就是指上述代码中没有定义在方法中的变量，而直接暴露在类中定义的变量，例如height = '177'。实例变量是指定义在类方法中的变量，例如构造方法中我们传入的name和age。通常使用self.xx = xx将外界参数绑定到实例变量中。可以看到上面代码中的结果，通过实例化传入的变量，最终调用打印说话时，以实例变量为准，而非类变量。

> Tips：
实际上，目前这个女朋友的例子中的类变量写的并没有实际意义，只是为了演示而演示，从设计的角度出发，类变量怎么可能选择姓名和名称这种不固定的值呢？可以思考下，既然是类的变量，那应该是一个种类所具体有的特征，而非具体到某一特征，比如姓名，一个人可能一生会谈好几次恋爱，每次女朋友的名字都是会变得，那你能把名字作为所有女朋友这一类共同特征吗！肯定是不行的，所以类变量定义时应该是选取共同特征时的变量去定义，我这里只是举例而已。


### 总结
类最基本的作用：封装，类就像一个模板，说白了就是代码共用的一套写法，而类就是现实世界的抽象！什么是抽象！！！抽象在编程世界中就是将所有有共同性的东西抽出来封装成一个模板！而实例化后的对象才是具体的实现。（编程思想，非专业人员了解即可。）


至此完！

<hr>

有想学python的同学，欢迎关注公号：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181220123046502.png)
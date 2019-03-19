## python小课堂21 - 面向对象(三)

### 前言

昨天分享了一篇面试最常见的知识点，可以消化消化，今天这篇文章实际上是我昨天晚上加点写的，为的是与之前的面向对象篇连上，要不后面时间越拖越久，知识的连贯性就断开了，所以趁热打铁，定时推送一篇吧。



PS：可以在通勤（上下班，估计有人不知道通勤是啥意思，这里解释下）的路上充分利用碎片时间来学习！

### 面向对象的可见性

这里可以先回顾一下之前的示例代码，还记得之前女朋友的例子嘛，忘记的话回顾看下哟！

[python小课堂18 - 面向对象篇（一）](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659087&idx=1&sn=2d65a5e2efc4f848d7242e6619e30211&chksm=8c97d1f6bbe058e0a90f58bd16f72e0392d14bf2621455547577ab1a89e0fa73a9f9c3537455&token=2088543086&lang=zh_CN#rd)、[python小课堂19 - 面向对象篇（二）](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659101&idx=1&sn=5d8b202ca7fb139ef72284bd90a7c38f&chksm=8c97d1e4bbe058f2963a2b14e2022f0c8e103b0e3696467967731a16be6654cebf56834106b0&token=2088543086&lang=zh_CN#rd)

#### 1. 成员变量以及方法的公开性

所谓的公开性，就是谁都可以访问的属性，比如下面的代码，在之前的小课堂代码基础上给女朋友这个类中多添加一个体重的属性！

```python
class GirlFriend():
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age, weight):
        self.name = name
        self.age = age
        self.weight = weight

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')


girlFriend = GirlFriend('女儿国公主', 18, 90)
girlFriend.say_feature()
print(f'女朋友的体重:{girlFriend.weight}斤')

结果输出：
>>> 我的姓名:女儿国公主
>>> 我的年龄:18
>>> 女朋友的体重:90斤
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108123951412.png)90斤是不是非常轻了，这算是苗条了吧！

然而....公开性的意义就是我是老大，我说了算，我完全可以修改对象初始化时女票的体重，我要给她修改成一个大胖纸。。。来看下：

```python
class GirlFriend():
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age, weight):
        self.name = name
        self.age = age
        self.weight = weight

    # 行为，说出自己的特征
    def say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')


girlFriend = GirlFriend('女儿国公主', 18, 90)
girlFriend.weight = 300
print(f'女朋友的体重:{girlFriend.weight}斤')

结果输出：
>>> 女朋友的体重:300斤
```

O(∩_∩)O哈哈~，变成胖纸了呢！这就是所谓的对象公开性，我们可以通过实例化后的引用来直接访问对象的变量，方法。甚至可以修改变量的值！

#### 2. 方法的私有性

现实世界处处皆有平衡性，有阴即有阳，有公开即有私有！大家都知道，女生的体重一直是比较隐私的数据了，不可能让我们这么随意的修改，所以呢，我们将其置为私有变量，外部就无法将其修改了，同样的对象中的方法也是一个道理！先来看下对象的私有方法，我们将与女生体重无关的```say_feature```变为私有方法，只需要在它前面加上__即可：

```python
class GirlFriend():
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age, weight):
        self.name = name
        self.age = age
        self.__weight = weight

    # 行为，说出自己的特征
    def __say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')


girlFriend = GirlFriend('女儿国公主', 18, 90)
girlFriend.say_feature()
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108124121902.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到报错了，说找不到这个```say_feature```属性，因为已经将其前面加上了双下划线，那我就改下代码，试试访问```__say_feature```呢？

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108124139395.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

依然可以看到报错，因为python的内置将方法前面带有双下划判定为私有方法，有人可能回想之前说过的__init__，前面也带有双下划线，为毛没有被认定为私有方法呢？因为凡是__xx__这样构造的样式，都是python的内置函数，细微之差就是人家还有后面的双划线！

#### 3. 成员变量的私有性



为什么我把成员变量的私有性单独提出来了一个小点，因为变量的私有性还与方法有点那么不一样！如下，将weight变量前面加上```__weight```：

```python
class GirlFriend():
    # 交过的女朋友个数
    total_nums = 0

    # 初始化构造方法
    def __init__(self, name, age, weight):
        self.name = name
        self.age = age
        self.__weight = weight

    # 行为，说出自己的特征
    def __say_feature(self):
        print(f'我的姓名:{self.name}')
        print(f'我的年龄:{self.age}')


girlFriend = GirlFriend('女儿国公主', 18, 90)
print(f'女朋友的体重:{girlFriend.weight}斤')

```

结果，可以看到实例调用的体重已经报错了：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108124215386.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

在来试试通过下划线的形式修改并且访问呢？毕竟已经将实例变量weight重名为了__weight:

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108124225589.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

神奇的发现，居然可以修改，并且还可以访问，不是已经改为私有变量了嘛。。。其实这就要跟下面的讲到的python特性有关了，请继续往下看.....

### 关于私有化的进阶话题

python是一种动态语言，所谓的动态语言，这里来举个例子，比如咱们在python中创建变量时，是无需声明变量明确的类型的，而可以直接用```a = 1 ```来将整型的数字1赋值给变量a。在其它的语言中，比如Java，是需要在a的前面声明变量类型的，例如 ```int a = 1;```这样的写法。而在python的面向对象特性中，正因为这种动态化影响了私有化的理解，这么说可能不太明白，还是下面用刚才的示例来解释下，只需要将上述代码修改一下顺序，将打印的结果与修改的代码顺序互换，即可得到答案：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108124255817.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)



发现报错了！实际上，由于python的动态性，将 ```girlFriend.__weight = 300```这行代码动态赋值给了girlFriend这个实例名为```__weight```的新属性，还记得上一节提到的```__dict__```吗？来验证看下女票这个实例对象究竟有哪些属性：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108124320529.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


**注意**到后两个参数，实际上我们第一次赋给女票体重的90斤，在python实例对象中叫```_GirlFriend__weight```，而```__weight```赋值的300斤则是新增的属性罢了！

相信热于思考的同学绝对会再去尝试，是不是如果访问```_GirlFriend__weight```，并且修改它，就可以实际修改了所谓的私有变量呢？如果你是这么想的，恭喜你，想的一点也没有错！可以看到下面的实验：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108124348759.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

**结论**：python实际上是没有所谓真正的私有变量，只要你想访问，就一定可以访问到，只要你想修改，那么一定可以修改，就是这么神奇！python对于私有变量实际上耍了一个小聪明，就是将__xxx的变量修改了名字，表面上不让你访问到而已罢了！~

### 总结

本篇介绍了python面向对象的成员的可见性，对于对象的私有化来说，可以屏蔽那些外界想主动修改的变量或者方法的操作，禁止他们访问与修改。



回顾下前面的两章面向对象，主要讲了面向对象的类变量、实例变量；类的实例方法、类方法、静态方法和构造函数。本章介绍了类的成员可见性。写到这里，不知不觉已经这么多了，后面看来还得在延长至少一章介绍面向对象的三大特性！敬请期待....

至此完！ 


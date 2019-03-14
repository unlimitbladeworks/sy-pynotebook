## python小课堂27 - 进阶必修之闭包（二）

### 前言
马上就要放假了！本周原本应该比较轻松，但是并不是这样啊....心情由晴天转为阴天....周末完成的文章，定时更新！闭包系列二。忘记之前的闭包一，可以点击下面的链接进行回顾。

[python小课堂26 - 进阶必修之闭包（一）](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659222&idx=1&sn=65fdcccb09cef1d2b441a6810b1cdf32&chksm=8c97d16fbbe05879798d95303b8608aa6b1ef17b31c702c8bb39768d2b4335732731759fe08b&scene=21#wechat_redirect)

这里还是多说一句，闭包在编写代码的过程中并不是必不可少的，某些场景下使用闭包，对编程的代码在架构上会起到精简代码的作用，但是绝不是说少了闭包就无法实现功能了！就像类和对象一样，没有对象和类就不能写代码了吗？？我们依然可以用普通的函数去实现某些功能！

### 举个栗子看闭包

![在这里插入图片描述](https://img-blog.csdnimg.cn/201902011449127.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

西游记的故事大家都有所听说，唐玄奘西天一去，取经之路长达十万八千里，而悟空一跟头就能翻到地方，却依然一路护送唐僧，其实这是有原由的：如来佛祖在取经任务前就跟这取经小团队说了，你们要想取到这真经，就得踏踏实实，一步一脚印，还要过这九九八十一难。而中途经过了：



长安(今陕西西安)——秦州(今甘肃天水)——兰州——凉州(今甘肃武威)——瓜州(今甘肃安西县东南)——玉门关——伊吾(今新疆哈密)——高昌(今新疆吐鲁番)——阿耆尼国(今新疆焉耆)——屈支国(今新疆库车)——跋逯迦国(今新疆阿克苏)——凌山(今天山穆苏尔岭)——大清池(今吉尔吉斯斯坦伊塞克湖)——素叶城(即碎叶城，今吉尔吉斯斯坦托克马克西南)——昭武九姓七国(都在今乌兹别克斯坦境内)——铁门(乌兹别克斯坦南部兹嘎拉山口)——今阿富汗北境——大雪山(今兴都库什山)——今阿富汗贝格拉姆——巴基斯坦白沙瓦城——印度



这么一写出来，唐僧走了这么远的吗！233333333333....回归正题，唐僧师父是从东土大唐而来，东土大唐的长安作为整个西游的起点，其中每过之地的总行进距离应该是在上一个地点的距离进行累加。比如在长安时，起始的西游距离是0，当经历过一难之后，走到了秦州，行进距离增加到100里，再过一劫，到了兰州，秦州到兰州的距离是200里，此时行进距离是在100里的基础上加200里，到兰州时，总行进了300里，后续以此类推....**每到一个国度，使用中途经过的距离与上次进行累加，请打印输出每次途径国度的总行进距离（各国度到长安的距离）。**

接下来，请你用程序来实现一下。

### 非闭包实现栗子

首先来看下，非闭包实现的例子，在开题之时就说过，闭包并不是必不可少的东西，即使没有闭包，功能依然可以实现。依然是有逻辑的讲下最终代码的实现，步骤如下：



#### 1. 定义walk函数，将每次的间隔距离传入到其中，每次进行相加看结果

```python
ChangAn_distance = 0

def walk(midway_distance):
    total_distance = ChangAn_distance + midway_distance
    return total_distance

print(f'从长安到秦州的总距离{walk(100)}')
print(f'从长安到兰州的总距离：{walk(200)}')
print(f'从长安到凉州的总距离{walk(300)}')
```

讲解：定义初始变量 - 长安街的距离，再定义一个walk走路的函数，将每次中途的距离传入此函数中，在其中计算每次相加的距离，将结果返回，如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190201145006469.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

这样写的最终结果，只是打印出了每次中间的距离，比如100，就是长安到泰州的距离，200里是泰州到兰州的距离，而不应该是长安到兰州的总距离。所以这样写是不对的，继续看步骤2。

#### 2. 将计算的总距离赋值给初始值ChangAn_distance

```python
ChangAn_distance = 0

def walk(midway_distance):
    total_distance = ChangAn_distance + midway_distance
    ChangAn_distance = total_distance
    return ChangAn_distance

print(f'从长安到秦州的总距离{walk(100)}')
print(f'从长安到兰州的总距离：{walk(200)}')
print(f'从长安到凉州的总距离{walk(300)}')
```

讲解：将计算的总距离赋值给初始距离，这样一来每次 ChangAn_distance 就会进行累加，最终将其返回就是总距离了。看第一个print执行时，调用了walk函数传入100，total_distance 算出来得100，ChangAn_distance 接下来被赋值为100，其自身从0变为了100；到第二个print时，此时的 ChangAn_distance 已经变为了100，所以在第二个print时候调用的walk函数，里面的 total_distance 算出来得就是 100 + 200 = 300，以此类推.....

乍一看这段思维逻辑是没有任何问题的，但是若是执行时，就会像下图一样报错：

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019020114503946.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

错误信息是：本地变量 ChangAn_distance 在引用之前没有被定义。有人可能会想到上节中说到的，函数内部找不到变量，会向外层寻找，外层不是已经初始化了吗？怎么还会报错呢！实际上是因为此行代码受到了赋值变量的影响，也就是16行写到的代码，可以看步骤1中，若将16行代码抹掉，是不会报错的。在Python中，16行代码的左侧变量 ChangAn_distance ，解释器一旦发现它在左侧，说明在局部的函数中就认为是对其进行初始化了，但是在walk函数中并没有对其进行初始化，所以报错了。

#### 3. 将 ChangAn_distance 设为全局变量即可

```python
ChangAn_distance = 0

def walk(midway_distance):
    global ChangAn_distance
    total_distance = ChangAn_distance + midway_distance
    ChangAn_distance = total_distance
    return ChangAn_distance

print(f'从长安到秦州的总距离{walk(100)}')
print(f'从长安到兰州的总距离：{walk(200)}')
print(f'从长安到凉州的总距离{walk(300)}')
```

通过global关键词，可以将变量定义为全局的变量，此时在进行调用就不会出现步骤2中的错误了，如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190201145103947.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

这个答案正是程序的正确答案！唐僧感到欣慰啊........



### 闭包实现栗子

前面又铺垫了这么多，现在让我们来用闭包实现一下唐僧取经的例子！依然是分为几个步骤，如下：

#### 1. 定义闭包函数，外层函数假设是骑马，内层函数是走路

西天取经之路，大部分时间唐僧是骑马行进的，这样一来，马可以作为一个代步工具来使用，当没有马的时候，只好自己走路咯。所以定义外层函数为骑马，内层函数为走路：

```python
ChangAn_distance = 0

def ride_horse(init_distance):
    def walk(midway_distance):
        total_distance = init_distance + midway_distance
        init_distance = total_distance
        return init_distance

    return walk

w = ride_horse(ChangAn_distance)
print(f'从长安到秦州的总距离{w(100)}')
print(f'从长安到兰州的总距离：{w(200)}')
print(f'从长安到凉州的总距离{w(300)}')
```

通过白龙马这层代步工具，我们可以在起始的时候，将起始距离（ChangAn_distance）传入到骑马函数（ride_horse）里，使用闭包的特性，在调用外层函数时，将内层的walk函数返回从而得到w，调用w将中途距离（100，200，300）传入，最后输出打印！walk函数中的计算逻辑是和非闭包一样的，看懂了非闭包后，看这个也是一样的，于是运行如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190201145138388.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

#### 2. 使用 nonlocal 关键词告知python变量非本地变量

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190201145156298.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

只需使用 nonlocal 定义变量，方可告知Python此变量并不是本地变量即可。

有人可能会有疑问，这写法是闭包吗？结合上节课说到的，不是要有个环境变量与内部函数组成封闭在一起使用吗！想到这里的同学，说明动脑思考了哟！没错，在这个例子中，作为**环境变量**而言的其实是外部函数（ride_horse）中的形参，也就是init_distance！来验证下呗：

```python
ChangAn_distance = 0

def ride_horse(init_distance):
    def walk(midway_distance):
        nonlocal init_distance
        total_distance = init_distance + midway_distance
        init_distance = total_distance
        return init_distance

    return walk

w = ride_horse(ChangAn_distance)
print(f'从长安到秦州的总距离{w(100)}')
print(w.__closure__)
print(w.__closure__[0].cell_contents)
print(f'从长安到兰州的总距离：{w(200)}')
print(w.__closure__)
print(w.__closure__[0].cell_contents)
print(f'从长安到凉州的总距离{w(300)}')
print(w.__closure__)
print(w.__closure__[0].cell_contents)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190201145223138.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

关于闭包与非闭包的区别，一张图醒目：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190201145238436.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

闭包之后是不会对全局变量的值进行修改的！而非闭包内部计算时影响了外部全局的变量！

### 关于闭包的面试题

来看一到比较基础的，跟闭包相关的面试题：

```python
def f1():
    a = 100

    def f2():
        a = 200
        print(a)

    print(a)
    f2()
    print(a)

f1()
```

思考一下，最终会输出什么呢？如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190201145309174.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

想一休哥一样思考吧.......不解释原因了！论动手实践的重要性！

### 总结

终于写完了闭包，写完之后的感想就一个，真TMD难写！！！自己说过的话，哭着也要完成。总之大家要是想明白闭包是个怎么样的概念以及其自身是怎么样的一个存在，还是自己动手多多实践下，实践出真理啊！闭包算是比较难的一个概念了，因为其本身就是很抽象的存在！反正笔者是逼着自己完成的闭包篇，中途是真的想放弃，不太想写了.....坚挺之后，收获最大的还是自己！对这种“函数式编程”有了更深一步了解....



立个flag，2月底之前完成所有Python小课堂！！！！！！



有想交流python的同学，欢迎关注公号：migezatan(咪哥杂谈).
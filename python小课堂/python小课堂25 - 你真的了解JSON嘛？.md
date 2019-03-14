## python小课堂25 - 你真的了解JSON嘛？
### 前言

原谅我标题党了一波，哈哈哈哈！其实今天这篇文章算是题外番了，为什么这么说呢？因为JSON这个词，在当今的web环境下，作为一种最常使用的数据格式来进行各处的交互，本想着不打算介绍JSON的，但是因为后续的爬虫章节肯定会涉及到这个知识点，早就说过，此系列文章是为了让小白也能入门……所以还是单独提出来写一篇文章来讲解下。


### JSON的概念
JSON，全拼JavaScript Object Notation, 中文是JavaScript 对象表示法的意思，它是一种**轻量级的数据交换格式**。来！划重点……轻量级的！数据交换格式！概念上来说，这两点是最重要的，也是最应该记住的。

PS: JavaScript是前端的一种脚本语言，比如我们浏览器的一些按钮交互动作，都是由JS来实现的。


### JSON与XML的比较


再普及一个新的名词知识点XML，早期传递数据，是用XML来进行传递的。等到后来JSON出来以后，越来越多的人开始使用JSON在网络上进行数据的传递了，当然是因为JSON比XML有更多的优点，才会被人们接受哇！⊙∀⊙！来看下面的两个观点:

> 什么是 XML?
> · XML 指可扩展标记语言（EXtensible Markup Language）
> · XML 是一种标记语言，很类似 HTML
> · XML 的设计宗旨是传输数据，而非显示数据

> 什么是JSON？
> · JSON 是轻量级的文本数据交换格式
> · JSON 独立于语言 *
> · JSON 具有自我描述性，更易理解

说了这么多，分别来看下二者长什么样子吧！以下截图来源介来于网址：

http://www.w3school.com.cn，有兴趣的可以去看下官方的讲述。



图1，XML：

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019012212372924.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

学过HTML的同学看上去是不是非常熟悉，XML也是采用闭合标签的形式来标记数据。



图2，JSON：

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019012212373956.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


而JSON呢？实则就是一串字符串，是不是看起来非常像Python的数据类型dict，也就是字典呢！

### Python中JSON的用法


了解到上述所有概念后就好说多了，JSON在每种语言中都有着不同的数据类型相互对应，比如在Python中，当我们把一个普通的JSON字符串解析完成后，得到的就是dict类型。口说无凭，来直接看下面的示例吧！



示例1：场景来咯，假设你的女朋友！被我用JSON字符串来描述她的特征了，那么现在需要将此JSON串，在python中将她的体重读取到，改如何做呢？



首先import一个叫做json的内置库，python一向秉承着简洁，通过名字就知道这个库是做什么的啦！而json有个方法，可以将JSON数据格式直接转化为python内置的数据类型，调用loads方法来进行转化。下面就来看下具体代码：

```python
import json

girlfriend_json1 = "{name : 女儿国公主 , age : 10000, weight : 200kg}"
girlfriend_json2 = "{'name' : '女儿国公主' , 'age' : 10000, 'weight' : '200kg'}"
girlfriend_json3 = '{"name" : "女儿国公主" , "age" : 10000, "weight" : "200kg"}'

girlfriend_dict = json.loads(girlfriend_json1)
girlfriend_dict = json.loads(girlfriend_json2)
girlfriend_dict = json.loads(girlfriend_json3)
print(type(girlfriend_dict))
print(girlfriend_dict)
```

可以看到代码中，在设定JSON字符串时，以女朋友的特性来作为JSON字符串的“key”，对应的值来作为JSON字符串的"value"。那么问题来了，你认为girlfriend_json1 ~ 3 哪个才是正确的写法呢？（先不要看下面的解释哟，独立思考下！）



解释：

① girlfriend_json1 ，大体格式是没有错的，正如python中的dict一样，JSON字符串也是有类似key-value这种形式组成的数据格式。但是，假设如果我们解析正常了，此时的name肯定是一个没有经过定义的变量，这样的存在在程序中是不被允许的，所以肯定会报错！如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190122123815567.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

② girlfriend_json2 ，有了1的解释，那么我们可以得出一个结论，JSON中未定义的变量是不能直接命名的，所以必须用引号来修饰，也就是说要定义成字符串的形式来写，于是呢有了2的写法，继续来运行下看看能否成功呢？

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190122123826486.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

这是为什么呢?已经用单引号括起来了，还是报错，实际上虽然在python中定义字符串是可以用**单双引号**来修饰，但是请务必记住，JSON本身规定如此，在JSON自身中必须由**双引号**去定义才算是属性字符串。所以呢，所以呢，继续看下面的3吧！



③ girlfriend_json3 ，此种写法在1,2上层层优化，得出的双引号定义属性，而对于数字来说，是不需要被双引号括起来进行修饰的，这点可以注意下，如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190122123856160.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

经过不断地调整，因为JSON本身需要用双引号来定义所谓的变量，所以在python中定一个JSON字符串，最外层就要用单引号来修饰，通过loads转化成功后，可以看到转成的数据类型是python中的dict类型！这里就非常容易可以将女票的体重读取出出来了！只需要利用**dict['key']**操作即可。



示例2：场景再次变更，假设还是你的女朋友！一个前任，一个现任，需要作对比！依然是用JSON字符串来描述她们的特征，最终还是要在python中将她们的体重读取到，改如何做呢？而这个JSON字符串该如何定义呢？（思考思考....）

```python
import json

girlfriend_json = '[{"name" : "前任女儿国公主" , "age" : 10000, "weight" : "200kg"},' \
                  '{"name" : "现任嫦娥小姐姐" , "age" : 18, "weight" : "50kg"}]'

girlfriend_list = json.loads(girlfriend_json)
print(type(girlfriend_list))
print(girlfriend_list)
print(f"前任的体重：{girlfriend_list[0]['weight']}")
print(f"现任的体重：{girlfriend_list[1]['weight']}")
```

在定义前任后，通过\ 对字符串的定义进行了换行操作，要不实在是太长了！可以看到，通过[]将两个JSON组合到了一起，但是依然是字符串形式，运行下代码，输出看下结果：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190122123930622.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到，经过类似python中list的去定义JSON，在解析后，得到的python基础数据类型就是list，而不是在示例一种解析得到的dict类型！



这也是为什么我又再次举例了示例2的原因，JSON自身是有着所谓不同的“数据基础类型”，而每一种都可以对应到不同语言中去！（包括你可以进行布尔值的尝试）这就要涉及到另一个知识点了，序列化与反序列化。

| JSON | Python | Java |
| ---- | --------- | ----|
| object(JSON整串)| dict | Map |
| array | list | List |
| string | str | String |
| number | int | int |
| number | float | float |
| true | True | true |
| false | False | false |
| null | None | null |

### python的序列化与反序列化

#### 序列化

先来看下序列化是什么意思？实例如下：



示例：场景再次降临，假设你的女朋友！前任和现任(捂脸逃，跟女朋友杠上了！汪汪汪……).....这次不定义在JSON上了，我们将其定义在python的基础数据类型list中....

```python
import json

girlfriend_list = [{'name': '女儿国公主', 'age': 10000, 'weight': '200kg'},
                   {'name': '嫦娥小姐姐', 'age': 18, 'weight': '50kg'}
                   ]

# ensure_ascii = False,此参数加上，中文才不会被转为unicode编码
girlfriend_json = json.dumps(girlfriend_list,ensure_ascii=False)
girlfriend_json2 = json.dumps(girlfriend_list)
print(girlfriend_json)
print(girlfriend_json2)
print(type(girlfriend_json))
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190122124039492.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

代码中，通过**json.dumps**方法，将定义好的python基础类型list转为本章男猪脚JSON形式，打印输出你可以看到，它其实就是一段字符串。



需要注意的是:如果你的内容里包含了中文字符，在dumps方法里传入第二个参数，将ascii码选项设置为False即可成功显示原有中文，否则默认为True,中文会被转为unicode进行输出。此处所说可以点击上图查看到结果的输出案例。



以上说了这么多，实际上我们将程序内存中的基础数据类型转为JSON的这一过程，就称之为**序列化。**



序列化的目的:序列化之后，就可以把序列化后的内容写入磁盘，或者通过网络传输到别的机器上，也就是所谓的数据落地(落地，写入数据库中或者电脑磁盘上)与数据调用传输。

#### 反序列化
反序列化就是将序列化的过程反过来，实际上并不难以理解，在上面我们将JSON转化为Python内置数据基础类型的这个过程，其实就是称之为**反序列化**。当然这里不限定与JSON转为Python的内置数据类型，类似的，比如XML转为Python数据类型的过程也可以称之为反序列化。从硬件的思维角度解释来说，就是将硬盘、网络上的数据转化为语言本身内存的数据基础类型来供程序使用。

### 关于JSON额外的一些话题



在网络系统的交互中，像这种数据格式进行交互来说是必不可少的，比如我们日常生活中经常会用浏览器访问网页，拿淘宝举例，它上面的物品价格数字有可能每天都会发生变化，而这些数据就是通过后端系统使用JSON这种数据格式将数据传到页面上，最终由浏览器动态渲染而成，你才能看到每种商品都有不同的价钱。



在不同的语言系统中，JSON也可以作为跨语言的统一数据格式来规定其他语言，从而实现跨语言的系统交互。数据格式呢，类似于中间代理，你要是想跨语言系统进行交互，那你就得遵循我定义的规范(这里的规范就是指JSON数据格式)。


如下图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190122124127531.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

好了，以上就是本章介绍的番外篇JSON啦.

至此完！


有想交流沟通python相关知识的同学，欢迎关注公号：
migezatan.(咪哥杂谈)
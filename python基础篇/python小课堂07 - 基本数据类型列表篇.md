## python小课堂07 - 基本数据类型列表篇
### python中组的概念？

在前面的小课堂中，我每介绍一个新的数据类型的概念，都会去用一个现实世界的实例来引导出新的概念，这次依然是这样，因为计算机中的一些概念就是通过现实世界的例子而映射进去的！本节课堂要说的是python中组的概念，什么是“组”？

生活中“组”的概念非常常见，我大四之前一直是一个游戏迷，就用游戏来举例说明下“组”的概念吧！

事例一：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181109125756899.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

女生们最爱玩的开心消消乐。。。手动来回滑来交换位置，一旦满足横竖行相同的三个元素，则会被消除。而这三个元素，其实就是一个“组”。


事例二：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181109125839912.gif)

英雄联盟中亚索的技能，一共四个技能QWER，加上闪现治疗DF，一共6个技能，此时这六个技能为```一组```！如果英雄就一个技能呢。。八成这游戏也没啥意思吧.

###   python基础类型-列表(list)

```列表(list)```便是上面“组”的一种。在python中，list的写法跟上节介绍的切片写法有点像，[]。

下面看下idle中的写法：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181109125926476.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

###   列表的操作方法

下面说下列表的各种操作方式，事例就拿亚索来说吧，假如亚索有四个技能，我们将他的四个技能用字符串来表示，并且放入列表中：

```pythn
['斩钢闪','风之障壁','踏前斩','狂风绝息斩']
```

一、获取"技能"列表中的某一技能！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181109130003600.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

二、给列表"技能栏"中加减乘除操作！

emmm....我们来加一下闪现和点燃技能吧：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20181109130015162.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### 小结

```列表(list)```的概念本节小课堂先引出了基本概念，实际上对于list而言，还有别的一些操作，后续会慢慢介绍，不着急！通过实验我们可以看到，list中可以放入不同的数据类型，并且可以通过加法将两个已有的list进行相加，从而得到想要的大list！


原文地址：https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451658779&idx=1&sn=0bfc5344b0c15c2e483948db549d5b94&chksm=8c97d0a2bbe059b431971dd8a477aca4b19b2ed8d8b431dad0084a153b43f3dc5cdda5f33648&token=1167262384&lang=zh_CN#rd

有想学python的朋友，欢迎关注公号哟：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181109130141538.jpg)
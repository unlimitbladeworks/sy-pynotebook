## python小课堂14 - 代码编辑器PyCharm篇

### 前言

古人云：工欲善其事必先利其器！写代码也一样，虽然好多人都说，初学者不推荐使用很高大上，智能，自动化的编辑器，但是我想说：“强大的，智能的东西为什么就不推荐新手用呢？！！”我自学java的时候，也直接用的是eclipse写代码，而非网上好多人说的用什么txt文本编辑。用txt文本写代码的初衷是熟悉语法，自己对着相关文档巧罢了，效率极低，还容易出错，很容易对新手造成学不下去的恐惧与困扰，所以我推荐初学代码，该用智能的，就用智能的！至于熟不熟悉代码，敲多了自然就熟悉了！步入正题，今天推荐的编辑器就是 --------> PyCharm(自带代码提示，检查语法，以及调试功能的编辑器)。此款也是JetBrains公司出的，在2016年的时候，这家公司掀起了新时代代码编辑器的热潮，他家出的编辑器都超级好用的伐！！！堪称智能的一B。。。。下面就来介绍下PyCharm的安装与配置，方面后续介绍函数和模块的概念。

### 安装PyCharm

1.给出官网链接：http://www.jetbrains.com/pycharm/

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141001179.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

2.点击专业版的进行下载！功能多，教你如何破解它！永久免费。。。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141011162.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

3.点击完稍等片刻，我家网是50M的光纤，但是下载速度并不乐观呀，估计是外国服务器的原因。。。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141020752.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

借着等待下载的时间，普及一个网络小常识吧！平时我们说到的50M的网速，100M的网速，实际上网速的单位是 bit/s，也就是一秒走了多少bit。50M bit/s，在网络中数据流的单位是一秒内传输了50M的bit。然后1byte=8bit，1MB=1024KB，1KB = 1024 Byte ，你想算出1s中最大的下载速度，单位按照流量来算的话就是50除以8，得到6.25MB/s(理论值)。实际上公式是： 50 *1024 *1024/8 ，单位是 byte，换算回去的话就是直接用50/8即可。

4.安装PyCharm，windows大多都是无脑一步又一步进行安装即可，说下需要注意的点。

① 点击next
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141038145.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

② 选择对应安装路径

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141047350.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

③ 出现选项卡

第一项是创建桌面快捷方式，32位或者64位。

第二个是对以.py为后缀的文件是否关联pycharm，勾上就是默认通过pycharm打开.py文件。

第三个是会自动下载安装JetBrains版的jre环境。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141059357.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

推荐勾选方式：

64位，.py勾不勾看心情，最后一项一定要勾，因为pycharm基于java实现，需要jre环境才能运行。我这里勾选如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141118373.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

④ 勾完一路next ，install 即可，进入下面界面，等待下载和安装：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141131963.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

⑤ 安装完毕后，打开桌面上的快捷方式。选择第二个，OK即可。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141140399.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

右侧滚动条，拖到最底下，然后accept。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018120114115030.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

问你是否需要数据共享，看你心情，随意选。我选的不发送，Don't send.

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141159499.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

Pycharm默认主题是黑色，写python代码黑色很炫酷，默认即可，点击右下角Next：Featured Plugins。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141209854.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

一些可选的插件，安装与否都可以，后续也可以自己安装，右下角Start using Pycharm。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141223147.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### 破解PyCharm专业版

重头戏来了！！可以看到当点完上述设置后，进入下图，开始找你要序列号版权之类的信息了！！！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141254926.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

我们到这里先点击Exit，退出PyCharm.......

① 进入此网站 ：http://idea.lanyus.com/  ，下载破解补丁，不到1MB。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141308926.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

② 将补丁放到pycharm的bin目录下。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141318619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

③ 编辑这两个文件的内容：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141326925.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

原本显示应该是pycharm.exe.vmoptions和pycharm64.exe.vmoptions，因为我用记事本打开了，所以改变了图标显示。

打开pycharm.exe.vmoptions，尾行追加：

-javaagent:C:\Program Files\JetBrains\PyCharm 2018.2.4\bin\JetbrainsCrack-3.1-release-enc.jar

**一定要改成你自己对应的破解补丁路径！**


![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141345917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

pycharm64.exe.vmoptions同上。



![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141354439.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

④ 打开http://idea.lanyus.com/，点击获取注册码：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141403192.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

⑤ 打开你的pycharm，选择Activation code，粘贴④中注册码，点击Activate

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141411675.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

⑥ 激活成功，2100年，虽然网站上说激活码会失效，到时候大家看看使用吧，若没失效，切忌别自己更新pycharm版本，继续用就好了，若失效了，在安装本篇文章来一遍即可。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141420471.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### PyCharm配置python环境

① 创建新项目

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141432270.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

② 选择Pure Python，纯python脚本，Location修改脚本放置路径，点Create.

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141441349.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

③ 去掉在启动开启提示，都是一些pycharm的小技巧，有兴趣可以看看。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141449772.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

④ 配置主题，以及相关设置。

早期我选择了默认的黑色版，不知道为什么是白色背景，现在来配置下。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141502169.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

点击File ----> Settings。 打开设置的快捷键是Ctrl + Alt + S。

现在是IntelJ IDEA设置，默认白色，我们将其选成Darcula，就非常有python气氛了，点击OK。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141512150.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141517661.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

设置下字体，搜索Font，在Editor下，我目前用的是Consola，字体大小18。看着比较顺眼，适合编程。。。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141525681.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

⑤ 创建一个python文件，右键PycharmProject目录即可。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141533168.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141538672.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

⑥ 配置python环境对应的解释器

python环境之前的小课堂有讲过如何安装，现在是需要将python与pycharm进行关联，这样pycharm才可以直接调用python来运行代码。

打开设置，左上方搜索interpreter(解释器的意思)，右侧选择你本地对应之前安装的python，最后别忘了点OK。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141548980.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

⑦ 书写一个Hello World，并且运行！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141600676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

⑧ 看到控制台输出：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141610770.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

终于写完了........这怕是史上最详细的Pycharm安装教程了吧！！！

有想学python的同学，欢迎关注公号：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181201141649859.png)
## python小课堂15 - 史上最详细的包和模块import讲解篇
### 前言

在大量的代码设计中，我们不可能将所有代码都写在一个.py文件，所以有了**包、模块**，而为了代码可以重复利用(复用性)，就有了**类、函数**的概念。类和函数在下次介绍。

### python中的包


python中的包，对应到计算机中，可以理解为文件夹，但是文件加下必须有一个名为__init__.py的文件，若没有此文件，python则会认为其只是一个普通的文件夹。

打开pycharm，创建一个包，如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210123807417.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210123815786.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### python中的模块


python中的模块就非常好理解了，实际上，之前所有的.py文件，我们都可以称之为一个模块。单独的一个py文件就是一个模块。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210123829279.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


![在这里插入图片描述](https://img-blog.csdnimg.cn/2018121012383667.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

test1和test2不同区别就是test2是和package这个包是同级目录，而test1是属于package包的。

再来看下总的概念：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210123848575.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### 包和模块的引入
**1.<font color = gree>模块处于同级目录</font>（<font color = red>并且不在包下 </font>）**

当我们想在一个模块中使用另一个模块中的变量时，如何操作呢？test2、test3处于同一级目录。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124000740.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


我想在test3中引入test2的变量，test2.py中有个变量a = 2。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2018121012401058.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124020703.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124026701.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

如上所示,只需要在当前模块，用import语句，即可导入模块，具体使用的时候需要用模块的名字.变量。

**import 后面必须是模块的名称！ ------> import modul name**

还有一种写法如下图pycharm中：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124046820.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

如上所示,只需要在当前模块，     **from 模块名字 import  变量**     

2.**<font color = gree>模块处于同级目录</font>（<font color =red>在同一包下</font>）**

来看下，test1，test4都属于package包下的模块。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124146679.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

test1.py中有着字符串a = 'I am success!'
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124156272.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

在test4.py中引用test1.py中的a，如何引用呢？

可以看到如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124206523.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

```python
关键语法：import 包名.模块名 as 别名
```

<font color =red>但是！！！！！！！如果我们脱离pycharm，找到本机相应的python目录，通过cmd来运行下，看下效果如何：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124239555.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124245133.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以清晰的看到上图，通过命令行模式执行就会报错！错误显示模块没有被找到：没有模块叫'package'。这是为什么呢？在pycharm中通过右键run as运行test4，可以看到控制台成功输出，而本地调用命令行的形式就报错了！



打开pycharm的setting，搜索 python console，右侧其中有一项，add content roots to pythonpath，默认pycharm是勾选上此项的。此项的意思是将内容的根路径加到python的环境变量路径下。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124259646.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到上图下面代码块里写着一堆代码，正是这段代码，我们才可以在pycharm中正确运行。



我们可以在test1.py里来看下sys.path，顺便打印看下结果。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2018121012431271.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

pycharm控制台输出：



```python
['F:\\pycharm\\python14\\package', 'F:\\pycharm\\python14', 
'D:\\python3.6\\python36.zip', 
'D:\\python3.6\\DLLs', 'D:\\python3.6\\lib', 'D:\\python3.6', 
'C:\\Users\\sy\\AppData\\Roaming\\Python\\Python36\\site-packages', 
'D:\\python3.6\\lib\\site-packages', 
'D:\\python3.6\\lib\\site-packages\\win32', 
'D:\\python3.6\\lib\\site-packages\\win32\\lib',
'D:\\python3.6\\lib\\site-packages\\Pythonwin']
```
实际通过命令行输出，应该没有'F:\\pycharm\\python14' 这一项，因为这一项是pycharm中setting自动加上的！

实际控制台输出：

```python
['F:\\pycharm\\python14\\package',
'D:\\python3.6\\python36.zip', 
'D:\\python3.6\\DLLs', 'D:\\python3.6\\lib', 'D:\\python3.6', 
'C:\\Users\\sy\\AppData\\Roaming\\Python\\Python36\\site-packages', 
'D:\\python3.6\\lib\\site-packages', 
'D:\\python3.6\\lib\\site-packages\\win32', 
'D:\\python3.6\\lib\\site-packages\\win32\\lib',
'D:\\python3.6\\lib\\site-packages\\Pythonwin']
```

sys.path是一个list。默然情况下python导入文件或者模块的话，他会先在sys.path里找模块的路径。如果没有的话，程序就会报错。可以看到，sys路径下有package的包名，而没有test4.py中引用test1.py模块。



而pycharm能够成功运行，正是因为它已经帮我们把项目的根路径添加到了python的环境变量中。所以我们仿照其类似写法也可以完成！



解决方案：

这里不得不说几个重要的python自带模块了，如下：

① 

```__file__   : python模块自身的名称```
pycharm打印下__file__:

可以看到pycharm会将模块的绝对路径输出到控制台上。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018121012441778.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

在用命令行执行下看看：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124428327.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

python额外小知识：可以看到上图有一个__pycache__的文件夹，这个文件夹在pycharm的目录中，我们是看不到的，那么此文件夹的意义何在呢？点进去看下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124438969.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

> Python程序运行时不需要编译成二进制代码，而直接从源码运行程序，简单来说是，Python解释器将源码转换为字节码，然后再由解释器来执行这些字节码。而解释器的具体工作： 
> 1、完成模块的加载和链接。
> 2、将源代码编译为PyCodeObject对象(即字节码)，写入内存中，供CPU读取。
> 3、从内存中读取并执行，结束后将PyCodeObject写回硬盘当中，也就是复制到.pyc或.pyo文件中，以保存当前目录下所有脚本的字节码文件。
> 4、若再次执行该脚本，它先检查【本地是否有上述字节码文件】和【该字节码文件的修改时间是否在其源文件之后】，是就直接执行，否则重复上述步骤。
> 第一次执行代码的时候，Python解释器已经把编译的字节码放在__pycache__文件夹中，这样以后再次运行的话，如果被调用的模块未发生改变，那就直接跳过编译这一步，直接去__pycache__文件夹中去运行相关的 *.pyc 文件，大大缩短了项目运行前的准备时间。
> CSDN来源：
> https://blog.csdn.net/index20001/article/details/73501375


继续回归正题：

②
```python
import sys,os   ：  sys ，os模块是python系统自带模块

os模块： operate system 操作系统的意思，一般可以通过调用此模块来对系统进行相关操作

sys 模块： system 系统的意思，通过此模块来实现对python自定义包和模块的导入
```
有了以上两个知识点，我们可以对test4.py进行如下操作：
```python
import sys,os

print(__file__)
print(os.path.abspath(__file__))
print(os.path.dirname(os.path.abspath(__file__)))
print(os.path.dirname(os.path.dirname(os.path.abspath(__file__))))
```
因为pycharm会对__file__进行路径补充，所以我们用命令行来执行test4.py：



![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124554768.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到上图结果：
```python
__file__             模块名字
test4.py           
os.path.abspath(__file__)     模块名字的绝对路径
F:\pycharm\python14\package\test4.py
os.path.dirname(os.path.abspath(__file__))    模块的包名绝对路径
F:\pycharm\python14\package

os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
F:\pycharm\python14                           项目本身的绝对路径
```
通过最后一步，我们可以将项目本身的路径直接拼入python的sys下
```python
base_path = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
sys.path.append(base_path)
```
验证究竟有没有加到我们的python环境变量中，最终代码为：
```python
import sys, os

print(sys.path)
print(__file__)
print(os.path.abspath(__file__))
print(os.path.dirname(os.path.abspath(__file__)))
print(os.path.dirname(os.path.dirname(os.path.abspath(__file__))))
base_path = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
sys.path.append(base_path)
print(sys.path)
```

通过命令行执行来看下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124648899.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

有了以上的所有操作步骤，我们可以完美的将test1.py的a变量引入test4.py中了！来看下命令执行：
```python

import sys, os
base_path = os.path.dirname(os.path.dirname(
                            os.path.abspath(__file__)))
sys.path.append(base_path)
----------------  sys拼接 一定要在自定义包引入之前定义   ----------------------------------
import package.test1 as test1       注意import的顺序。
print(test1.a)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124708623.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

成功！

写到这里涉及的知识点就已经这么多了。。。继续写。。。

**3.<font color = gree>包处于同级目录</font>（<font color =red>包和包同级，包1下的模块引入包2下的模块变量</font >）**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124753365.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到，通过from test3 import c，pycharm中是正常输出的，控制台是报错的！原因实际和“**2.模块处于同级目录（在同一包下）**”的解释是一样的，只需要在引入自定义包之前，将我们项目的根路径加到python的系统变量中即可。

**4.<font color = gree>模块处于不同级目录</font>（<font color =red>包和模块同级，模块引入包下模块的变量</font>）**
![在这里插入图片描述](https://img-blog.csdnimg.cn/2018121012483582.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124841333.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210124850552.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

若属于3的情况，可以看到，不需要对python系统进行sys.append，可以正常使用import 或者 from 语句进行导入。



**5.<font color = gree>模块处于不同级目录</font>（<font color =red>包和模块同级，包下模块引入与包模块同级的变量</font>）**


test3.py 中有：
```c = 123455666```
在packeage下的test1.py调用：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2018121012495237.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

可以看到，通过from test3 import c，pycharm中是正常输出的，控制台是报错的！原因实际和“2.模块处于同级目录（在同一包下）”的解释是一样的，只需要在引入自定义包之前，将我们项目的根路径加到python的系统变量中即可。

```python
import sys, os
base_path = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
sys.path.append(base_path)
from test3 import c
print(c)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210125012291.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### 模块之前的相对引入
什么叫相对引入呢？相对路径大家可能听说过，相对引入和相对路径是一个道理的，比如 .代表的是当前目录，..代表的是上级目录,此处的写法就是相对路径，相对于某个文件来说，即相对！



实际上，在**2.模块处于同级目录（在同一包下）中**，还有一种相对引入的写法，但是对于test4.py引入test1.py来说，不能直接运行test4.py，否则会报错。来看下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210125051768.png)

test1.py中有个a字符串：
```python
test1.py
a = 'I am success !'
```
test4.py中，我用from .test1 import a来引入test1.py的变量a，注意，包下同级目录，我使用的是.test1  ！！！！

```python
test4.py

from .test1 import a
b = a + 'I am test4.py import .test1'
```
如果此时我直接将test4.py运行，并且打印b，就会报错！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210125131313.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)
```python
ModuleNotFoundError: No module named '__main__.test1'; '__main__' is not 
a package
```
如果此时，我通过test2.py间接行调用test4.py中的b
```python
from package.test4 import b
print(b)
```
无论是pycharm还是命令行，都是有成功运行的：



![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210125222499.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

也就是说python对于相对引入来说，主动引入的函数不能作为主体去运行！



### pycharm中可能会遇到的import报错



有人可能会遇到，当一个新项目导入到pycharm中，python代码的import有可能会报错，可以将项目设置为根路径，这样import错误即可消失，操作如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210125243291.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

### 包和模块自身的额外小知识点
1. 关于包下的 __init__.py

init,中文意思是初始化的意思，而__init__.py实际上就是作为包名来配合的，当我们调用一个包时，第一步python就会去调用__init__.py模块，所以，经常我们可以将包下的__init__.py中放入一些需要初始化的操作。

举个例子：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210125258811.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

```python
__init__.py:
init_a = 'I am __init__.py'
print(init_a)
```
在package包下定义了初始化的字符串。
而test2.py调用package下的test1.py中的a变量时：
```python
test2.py:
from package.test1 import a
print(a)
test1.py:
a = 'I am success !'
```
可以看到下图运行结果,先输出了初始化模块中的字符串:

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210125334835.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

2. 关于模块中的限定变量写法

依然是test2.py引入test1.py的变量：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210125353559.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

```python

test2.py:
from package.test1 import a,b,c
print(a)
print(b)
print(c)
test1.py:
__all__ = ['a','b']
a = 'I am success !'
b = 'I am fail !'
c = 'I am fuc***  you!!! !'
```
在test2中引入test1通过import单独引入三个变量，运行结果：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210125409237.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


若将import 后面改成* ，则会限制变量。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210125426159.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

而此处所说，就是因为在test1.py中有着__all__ = []  ,这样的写法可以限定住import * 的限制，test4.py import *时，则会被限制住骂人的语句！

### import 模块的万金油方法

上面说了这么多种情况，如果你实在是记不住，那么请记住一点，万金油的import方式，就是在你所有模块的入口模块处，以下面代码为例，将你项目本身的绝对路径拼入到python 的系统path下，**<font color =red>这样自定义的包一定不会出错！！！**

```python
import sys, os
base_path = os.path.dirname(os.path.dirname(
                            os.path.abspath(__file__)))
sys.path.append(base_path)
```
有想学python的同学，欢迎关注公号：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20181210125552148.png)
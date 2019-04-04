## python小课堂37 - 你并没有真正的理解 if __name__ 的作用


### 前言

在 Python 中，我们经常会看到

```python 
if __name__ == '__main__':
```

那么你真的理解此写法的作用吗？今天我们就来聊一聊它真正的含义。



笔者最喜欢的就是用示例讲明白一个问题，这次也不例外，依然是看例子来说话！

### 示例说话

举个例子来说： 


有一个物体质量 m=10,g=9.8 (重力参数)，求它的重力。 
公式：G=m*g 
所以创建一个 param.py 的文件，其中代码如下：

```python

# 重力参数
g = 9.8
def main():
    print("g:", g)

main()

>>> 控制台会打印出 -->  g : 9.8。
```

在创建一个 sum.py 的文件求 G ，代码如下：

```python

# 在这里我们将上面文件定义的param中的g作为重力参数引入到其中
from param import g

# 计算重力的函数
def calc_G(m):
    G = m * g
    return G

def main():
    print("G：", calc_G(10))

main()
```

结果如下：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYwdaG2pMb1R2O3Awv8UFR2pkUhJVNbgU5XKQekaotmKIicdf2FkRBibwJfyKSweuDvTVfLFHCmial8A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

结果可以看到，在 param.py 文件中的 main 函数也被执行了，而实际上我们并不希望它被执行，只是想 G 被打印出来即可。

此时 ```if __name__ == '__main__' ``` 便派上了用场。我们将 param.py 中稍作修改：

```python

# 重力参数
g = 9.8

def main():
    print("g:", g)

if __name__ == '__main__':
    main()
```

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYwdaG2pMb1R2O3Awv8UFR267WwrYIA9ceHesGFBwmziaMwOWsS38ibTqd5a9Wx5V06B63sQibicFPh7w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

加上后，Pycharm 中多了一个绿色小按钮，点击后：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYwdaG2pMb1R2O3Awv8UFR2GpdcRFXHS7oGm0QAYcEc5gwCzyNBToLsYG5rZrSl0DRO4UtKFdabZQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，在 param.py 中加上这么一句话，起到了一个入口函数的作用，也就是说对于 param.py 来说，程序入口是从这里开始的。同时不影响它自身的 g 打印输出，那么来看下求 G 中的程序。

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYwdaG2pMb1R2O3Awv8UFR29qw0AoNPh0JjibpvPFDUH0ylZvPyBscL4TnL6uHgVO2rDzj0ehycSUg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

求重力 G 的程序中，我们是没有改变任何代码的，可以看到结果已经变了。

### 结论

``` if __name__ == '__main__' ``` 相当于 Python 模拟的程序入口。Python 本身并没有规定这么写，这只是一种编码习惯。由于模块之间相互引用，不同模块可能都有这样的定义，而入口程序只能有一个。到底哪个入口程序被选中，这取决于 __name__ 的值。



__name__ 是内置变量，用于表示当前模块的名字。



所以，

``` if __name__ == '__main__'  ```

我们简单的理解就是： 如果本模块是被直接运行的，则代码块被运行，如果本模块是被导入到其它模块中去，则处于 __name__ 中的代码不被运行。

### 官方文档

查阅官方文档可以看到相应的解释：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYwdaG2pMb1R2O3Awv8UFR2cJg0GzNuErYic5qdEDPTfP3DnHJKicW7f9wngvdsZbFhE8t39hfySicCg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


什么？看不懂，来个中文的！~

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYwdaG2pMb1R2O3Awv8UFR2TEAQQRgibBfgFRZ1hmlRiczhibadpSw9DDkySFibZDPVUWDlDKVLhnfXcA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


> https://docs.python.org/3/library/__main__.html?highlight=__name__
> 
> 原文链接


### 关于 Flask 中的拓展知识

学过 Flask 的同学，可以看下此知识点，没有学过的也可以了解一下，万一后续用到了呢，有可能面试中会问到的一个小知识点。



在 Flask 框架中，我们通常使用下面的代码来进行项目的启动：

```python
from flask import Flask
app = Flask(__name__)

# Flask quickly start
@app.route('/')
def hello_world():
    return 'Hello World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0',port=81)
```

上面的代码是官方给出来的一段最快启动的小 demo。不难发现，在官方定义的代码中，入口函数把 app.run() 放在了``` if __name__ == '__main__' ```里。



但是有没有想过为什么要放在里面呢？



正常开发情况下调用 app.run() 启动，使用的 web 服务器是 Flask 自带的一个简单内置服务器。



对于生产环境而言，启动一个 Flask 项目是不能直接通过 Python 去运行的，因为还面临着很多问题，比如并发性不好，无法监控项目各指标等。。。



所以在正式的生产环境中，我们是不会使用 Flask 自带的服务器的，而是通过 nginx + uwsgi 来部署项目。 nginx 作为前置服务器，用来接收浏览器发来的请求，接着会把请求转发给 uwsgi ，uwsgi 会以配置文件的形式加载我们写好的项目，而加载入口则是本地开发环境下的 app.run() 方法所在的入口模块。就像下图：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIYwdaG2pMb1R2O3Awv8UFR2r8o66kuHufPCQhhtebGC8jbyib7skSXF3Sxj24CP1Y8p8icB5cTbRqsA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


于是，在生产环境下， app.run() 所在的模块相对于 uwsgi 来说便不是入口文件了，它是需要被导入到 uwsgi 中的一个普通模块。使用``` if __name__ == '__main__' ``` 的用途就是，不让 app.run()进行启动。也就是**禁止所谓 Flask 自带的服务器启动。**



这块儿算是一点小小的拓展，关于拓展知识，若是哪里有疑问，欢迎沟通交流呐！


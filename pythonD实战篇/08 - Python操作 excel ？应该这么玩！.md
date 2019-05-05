## Python操作 excel ？应该这么玩！

### 前言

当今社会，工具越来越具有高效率性，然而避免不了的是，即使是工具，也有着重复的操作。



今天给大家简单的介绍下，如何使用 Python ~~来便捷的操作 execel~~。不对，现在满大街都是教你如何玩 Excel ，太简单了，今天教你，如何用 Python 操作 Excel 简单的画出股票走势。



实际上，涉及到 excel 的第三方库有许多，所以在国内外也经常会有人问，"python excel 库哪家强？" 中国山东找飞翔！~

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbg54iardrbiaEgSM1ia4uiasxFic5oicBRb7HAltVbZF5PxyLJf1VyBib56lmFZ4RVLFsfaJMTR0CSWVkqw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

上面介绍的是 5 个可以操作 excel 的库。而在数据分析领域，还有一个可以高效处理 excel 数据的库，即 pandas。由于 pandas 涉及到许多专业的名词，具体学习只能自行体会的对照文档去学习，就不介绍了，本篇文章会用到它提供好的股票方法。

在查询的过程中看到一个这样的问答：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbg54iardrbiaEgSM1ia4uiasxFic7HH78aDUibCIuIYltv2VsLCJtp4fxLvrC7EuH11MesaEibr4iadEwiaPQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

而在 xlsxwriter 中可以非常好的结合 pandas 库进行使用。（pandas 操作 Excel 时可以将 xlsxwriter 作为引擎。）

### 环境准备

开始之前，你需要做的事情：



1. 创建一个虚拟环境 （可选）

2. 安装好

```python
pip install pandas
pip install pandas_datareader
pip install xlsxwriter
pip install fix_yahoo_finance
```

pandas：一个数据分析必用的库，大数据量清洗数据必备神器。

pandas-datareader：获取股票数据源的库。

xlsxwriter：操作 excel 的库，在本文中作为引擎。

fix_yahoo_finance：解决雅虎数据源问题。



多说一句，来看下 pandas-datareader 官网介绍：

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIbg54iardrbiaEgSM1ia4uiasxF5iaFEn1Jicng4o9f7sQibOiaJtuRjkw5wgibnycEWG0msQ3icB1USocYFH6Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


早期，获取股票数据源的方法是集成在 pandas 里的，但 0.19.0 之后不再支持 pandas.io.data 方法了，后续使用必须用此库来进行替换。

### 股票 Excel 成果展示

运行代码后，可以在当前目录得到一个 Excel，打开你可以看到 Excel 中的股票数据，以及用代码画出的折线图。

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaRMCHHHUFdCa2y0rtlJicPbvwHdYD6Hic9lfia0icGFZPs47y2s01iadjuPN6ZgVnXyc139UZJO8ia0CfA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

通过 pandas-datareader 获取的两只美股，一个是百度，一个是阿里巴巴。



y轴是当天收盘价，x轴是时间。



昨天特意请教了下懂金融的同学相关专业知识。



市值=股票数量*股价,如果要对比，应该看两家公司的财报、营收、净利润、PE值、PB值等等。。。



总之因素很多，从业务角度来考虑，对比这两只股票是没有实际意义的。所以，抽出这两只股票只是为了做演示而已。

### 代码思路讲解

实现思路其实很简单，分为以下几步：



1. 使用 pandas_datareader 获取股票数据,条件是时间，需要注意的是，调用雅虎数据源之前，使用 fix_yahoo_finance 修复，否则直接获取数据会报错。

```python

import fix_yahoo_finance as yf

yf.pdr_override()

def get_stock(self):
    start = datetime.datetime(2009, 8, 5)
    end = datetime.datetime(2019, 4, 30)
    all_data = {}
    stock_list = ['BABA', 'BIDU']
    for ticker in stock_list:
        all_data[ticker] = pdr.get_data_yahoo(ticker, start, end)
```

2. 将 xlsxwriter 作为 Excel 引擎，用 pandas 来创建 Excel 需要用到的工作表与 sheet 页。

```python
def write_excel(self):
    # 利用 xlsxwriter 作为引擎，用 pandas 创建一个 excel
    writer = pd.ExcelWriter('pandas_chart_stock.xlsx', engine='xlsxwriter')
    self.df.to_excel(writer, sheet_name=self.sheet_name)

    # 使用 xlsxwriter 引擎后，初始化 excel 的工作表和sheet页
    workbook = writer.book
    worksheet = writer.sheets[self.sheet_name]
```

3. 依据数据填充图表，设置一些图表的属性。代码就不贴了，因为全是官方设置，官方文档有很好的解释。

### 总结

![](https://mmbiz.qpic.cn/mmbiz_png/E4ianOkSOYIaRMCHHHUFdCa2y0rtlJicPbWqjzias9wnPAsR1608eIBvODsr0wHy8DzCwbngXDNIpyywWVL3ibgtpw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

对于如何详细的操作 xlsxwriter ，笔者就不介绍了。。因为网上的案例非常多，而如果自己写的话，对照着官方文档复制粘贴就可以满足日常要求了。。。



而获取雅虎的股票信息，背后原理其实类似爬虫机制，只不过人家帮忙写好了，对使用者而言提供了一个方法罢了！



如需本章源代码地址，可以后台回复 **股票走势** ，即可获得。

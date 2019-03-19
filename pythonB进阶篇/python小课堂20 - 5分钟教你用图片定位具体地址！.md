## python小课堂20 - 5分钟教你用图片定位具体地址！
### 前言

今天像上次一样来点实战干货，有了面向对象以及之前所介绍的知识，即可以实现本章内容。为了复习下面向对象的使用方法，特意写了一篇实战，若有不懂得的地方，请回顾python小课堂1-19。



在我们的日常生活中，经常离不开照相，尤其是在中国这么网络发达的国家，出去旅个游或者晒个娃都会通过互联网的形式将照片发到朋友圈留个纪念。那么今天的主题就是5分钟教会你用python如何通过图片来定位到图片拥有者的地理信息！由于本章内容涉及到个人隐私问题，所以请遵守以下声明。



**声明**：本章内容仅供学习记录使用，请勿用于商业以及非法用途！


### 图片定位的实现思路

在正式讲解思路之前，先来补充一个知识点，描述数据的数据信息，我们称之为元数据！简单地举个栗子来说：比如，有一条学生信息记录，其中包括字段姓名（name）、年龄（age）、性别（male）、班级（class）等，那么name、age、male、class就是元数据。通过它们的描述，一条关于学生信息的数据记录就产生。

相对的，图片信息也是存在元数据的，网上官方称之为exif(exchange image file format)，中文意思是交换图像文件格式。**要注意的是**有些图片是没有元数据的，比如压缩过的图片，元数据被破坏，无法探测，所以图片一定要是原图。如果你想用微信朋友圈，微博的图片来测试这次的代码，怕是没有希望了，因为都是被压缩过的图片。后续会提供一些额外思路，通过图片来定位物理信息在网络安全中还是非常有用途的。

这次用到的是python第三方库**exifread**，通过此库可以直接对图片进行元数据的读取。读取后其中有4项是关于GPS的经纬度坐标，将其清洗转化为gps在线网页(http://www.gpsspg.com/maps.htm)查询的经纬度格式。


### 定位的演示效果以及讲解
这里以我前一阵去顺义为例吧，途中路过孙河附近，当时觉得天气还不错，借着太阳错位发出的光给路灯随手拍了一张，图片如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181227122811225.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)


上面这张图片原图，接下来我把它放到一个文件夹下，通过命令行调用python脚本来得到它的经纬度位置。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181227122849651.gif)


随后将得到的经纬度复制到在线查看的网页上：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20181227122904678.gif)


**讲解**>：其实明白了背后的原理，实现起来并不困难，来看下下面的图，是我在手机上查看图片的详情信息得到的：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181227122931525.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3M3NDA1NTY0NzI=,size_16,color_FFFFFF,t_70)

原理就是通过python获取照片的这类信息！一般手机照相功能默认是开启定位显示的，所以当你手机开着网时，相机会基于网络对你所在的位置进行定位，然后写入到照片的属性中去，也就是上文所说的元数据！



### 代码的实现讲解

**1. 整体代码：**

放出整体代码是为了复习上一章节所讲到的类，也就是面向对象的概念。

```python
# -*- coding: utf-8 -*-
"""
@author: sy

@file: meta_picture.py

@time: 2018年12月08日21:32:49

@desc: 读取图片,解析其中的元数据小脚本
       在线GPS定位网站:http://www.gpsspg.com/maps.htm

"""
import os
import exifread


class MetaPicture(object):
    # 类变量,图片文件夹的绝对路径
    picture_paths = os.path.join(os.path.dirname(os.path.abspath(__file__)), 'picture')

    def read_picture(self):
        """ 读取图片,并调用自身提取元数据方法 """
        pictures = os.listdir(self.__class__.picture_paths)
        for picture in pictures:
            picture_path = os.path.join(self.picture_paths, picture)
            self.get_picture_exif(picture_path)

    def get_picture_exif(self, picture_name):
        """ 提取图片元数据 """
        img_file = open(picture_name, 'rb')
        picture_info = exifread.process_file(img_file)
        if picture_info:
            for tag, value in picture_info.items():
                print(f'{tag}:{value}')
            print('*' * 150)
            GPSLatitude = picture_info['GPS GPSLatitude']  # 纬度数
            GPSLatitudeRef = picture_info['GPS GPSLatitudeRef']  # N,S 南北纬
            GPSLongitude = picture_info['GPS GPSLongitude']  # 经度数
            GPSLongitudeRef = picture_info['GPS GPSLongitudeRef']  # E,W 东西经
            GPSDate = picture_info['EXIF DateTimeOriginal']  # 拍摄时间
            if GPSLatitude and GPSLongitude and GPSDate:
                print(f'纬度:{GPSLatitudeRef}{GPSLatitude}\n精度:{GPSLongitudeRef}{GPSLongitude}\n拍摄时间:{GPSDate}\n')
                latitude = self.deal_data_format(GPSLatitude)
                longitude = self.deal_data_format(GPSLongitude)
                print(f'处理后的经纬度:【{GPSLatitudeRef}{latitude},{GPSLongitudeRef}{longitude}】')
        else:
            print('请检查提取的图片是否为原图,若为原图,则说明无相关元数据！')

    def deal_data_format(self, data):
        """ 处理数据,清洗格式生成对应内容 """
        data_list_tmp = str(data).replace('[', '').replace(']', '').split(',')
        data_list = [data.strip() for data in data_list_tmp]
        data_tmp = data_list[-1].split('/')
        data_list[-1] = str(int(data_tmp[0]) / int(data_tmp[1]))
        # 为了适配gps定位网站的规格输出,将列表做成度分时的状态
        data_list.insert(1,'°')
        data_list.insert(3,'′′')
        data_str = ''.join(data_list)
        return data_str


def main():
    metaPicture = MetaPicture()
    metaPicture.read_picture()

main()
```

**2. 读取图片，获取元数据：**

整体代码有兴趣可以看下，核心代码利用了python第三方库**exifread**，可以通过pip install exifread来进行安装(不详细介绍了，zip爆破章节讲过pip命令)。

利用python自带的open对图片进行读取，将二进制流传入第三方库的方法中进行处理，可以得到图片信息的字典，可以看上面的gif演示中，有许多属性，而我们关心的只是gps，所以可以取出gps相关value进行处理打印。


```python
def get_picture_exif(self, picture_name):
        """ 提取图片元数据 """
        img_file = open(picture_name, 'rb')
        picture_info = exifread.process_file(img_file)
        if picture_info:
            for tag, value in picture_info.items():
                print(f'{tag}:{value}')
            print('*' * 150)
            GPSLatitude = picture_info['GPS GPSLatitude']  # 纬度数
            GPSLatitudeRef = picture_info['GPS GPSLatitudeRef']  # N,S 南北纬
            GPSLongitude = picture_info['GPS GPSLongitude']  # 经度数
            GPSLongitudeRef = picture_info['GPS GPSLongitudeRef']  # E,W 东西经
            GPSDate = picture_info['EXIF DateTimeOriginal']  # 拍摄时间
            if GPSLatitude and GPSLongitude and GPSDate:
                print(f'纬度:{GPSLatitudeRef}{GPSLatitude}\n精度:{GPSLongitudeRef}{GPSLongitude}\n拍摄时间:{GPSDate}\n')
                latitude = self.deal_data_format(GPSLatitude)
                longitude = self.deal_data_format(GPSLongitude)
                print(f'处理后的经纬度:【{GPSLatitudeRef}{latitude},{GPSLongitudeRef}{longitude}】')
        else:
            print('请检查提取的图片是否为原图,若为原图,则说明无相关元数据！')
```

**3. 清洗gps元数据：**

由于exifread库取出的数据并不符合gps在线网站的经纬度定位样式，所以特意数据清理一番，将原有数据改为在线网站所需的格式即可。在线网站需要的格式为：【N40°2′′19.356,E116°31′′36.7031】，花括号逗号前面是纬度，后面是经度。


```python
def deal_data_format(self, data):
        """ 处理数据,清洗格式生成对应内容 """
        data_list_tmp = str(data).replace('[', '').replace(']', '').split(',')
        data_list = [data.strip() for data in data_list_tmp]
        data_tmp = data_list[-1].split('/')
        data_list[-1] = str(int(data_tmp[0]) / int(data_tmp[1]))
        # 为了适配gps定位网站的规格输出,将列表做成度分时的状态
        data_list.insert(1,'°')
        data_list.insert(3,'′′')
        data_str = ''.join(data_list)
        return data_str
```


### 代码中的知识点复习与额外知识点

**1. 获取图片文件夹的绝对路径**

在[《python小课堂15 - 史上最详细的包和模块import讲解篇》](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659012&idx=1&sn=f8eac7ca55f51a22a9cbb6e382e7aa9b&chksm=8c97d1bdbbe058abc84f7c3629414ad17bc14f244d86e735c498d17cab60a96e6c05afd08178&scene=21#wechat_redirect)，曾经介绍过这样的用法，不熟悉的可以去看下，不做多与讲解了。

```python
# 类变量,图片文件夹的绝对路径
picture_paths = os.path.join(os.path.dirname(os.path.abspath(__file__)), 'picture')
```

**2. 类变量以及实例变量的引用**
上一章节讲过的面向对象中讲过，不熟悉请看[《python小课堂19 - 面向对象篇（二）》](https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451659101&idx=1&sn=5d8b202ca7fb139ef72284bd90a7c38f&chksm=8c97d1e4bbe058f2963a2b14e2022f0c8e103b0e3696467967731a16be6654cebf56834106b0&scene=21#wechat_redirect)。


```python
 def read_picture(self):
        """ 读取图片,并调用自身提取元数据方法 """
        pictures = os.listdir(self.__class__.picture_paths)
        for picture in pictures:
            picture_path = os.path.join(self.picture_paths, picture)
            self.get_picture_exif(picture_path)
```

**3. list内容转为str类型**

将list中的每个元素，进行无符号拼接，最终成为字符串，如果想让每个元素以逗号进行拼接，将**''.join**改为**','.join**即可。

```python
data_str = ''.join(data_list)
```

### 拓展思维使用场景
如果意识到元数据的重要性，其实玩出的花样非常多，这也是网络安全中取证调查的常用手法。举两个使用场景，就意识到其实这个手法很有效。



1. 假设一个士兵把他的一些带有元数据的照片放在他的博客或者web网站上，那么敌军就可以下载照片，并且在很短的时间内掌握这名士兵的活动轨迹。



2. 如果你想定位你女朋友的具体位置，只需要让她发你微信一张刚拍好的**原图**照片即可！前提是她手机相机打开了“保存照片的地理位置（明白人都懂....不多说了！:imp:）

### 隐私的安全性

所以呢，通过本章了解到，其实我们日常生活中的照片包含的隐私信息量是非常有利的，为了个人的隐私安全，一般不要轻易在各大网站上或者微信上上传原图（毕竟现在手机都联网，没人会在意相机是否开启了保留地理位置），否则你的地理信息位置很轻易的就会暴露给一个懂元数据的人哟！

### 代码的开源地址

附上github开源地址：



https://github.com/unlimitbladeworks/python-tools/tree/master/hack/meta



以上就是本章所有内容了！至此完！ 
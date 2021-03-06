# 行为识别（时间序列）特征提取代码

多种传感器可以用于行为识别，如最常用的加速度计、陀螺仪、蓝牙与WiFi等。针对蓝牙与WiFi的特征提取，要根据具体的问题情况来进行。通常来说，**加速度和陀螺仪**的数据是最常用的。因此，我们就以这两种信号为例，提供针对它们的特征提取代码。

加速度和陀螺仪都是典型的时间序列信号，在行为识别中，通常我们都会提取一些统计信息（又称为**时域**）和频率信息（又称为**频域**）。两部分合起来，就可以用于行为识别了。从经验出发，能够识别人体常见的大多数运动行为。

**也可以用本代码进行一些时间序列的特征提取，用法是一样的**

关于时域和频域具体特征的计算方法请见我在知乎的这个回答：https://www.zhihu.com/question/41068341/answer/89926233

### 推荐使用

[一个简洁明了的时间序列处理(分窗、特征提取、分类)库：Seglearn](https://dmbee.github.io/seglearn/index.html)

用这个库会比用我们下面提供的自己写的方便！

### Python版本

- - -

Python版本比较通用，也比较好扩展。目前刚放到pypi下，可能 用pip直接安装。该目录下的`feature_extraction`文件夹是核心的文件夹。

内核提取方法针对Python2和Python3一样通用。`test.py`文件是按照Python3格式写的，无伤大雅。

#### 需求：

pip install numpy

#### 调用方式（直接拷贝）：

1. 拷贝`feature_extraction`文件夹到你的目录（通常是你的特征提取代码目录）下；
2. 在同一层目标下，首先导入引用：

`from feature_extraction import feature_core`

然后有两种调用方式：

(1) 有窗口：`feature_core.sequence_feature(a, 5, 4)`，表示对a这个数组按照窗口大小为5,步长为4进行特征提取

(2) 无窗口：`feature_core.sequence_feature(a, 0, 4)`，表示直接对a这个数组进行特征提取，它本身就是一个窗口。

#### 返回：
一个2D的numpy.array

#### 调用方式（pip）：

`pip install tsfeature`
`import tsfeature.feature_core`


#### 扩展：

目前提取了19维特征，可以直接扩展`feature_time.py`和`feature_fft.py`文件中的函数，加上自己在时域和频域上的特征提取方案。

附本代码中提取到的19维特征：

（1）时域：均值，方差，标准差，最大值，最小值，过零点个数，最大值与最小值之差，众数

（2）频域：直流分量，图形的均值、方差、标准差、斜度、峭度，幅度的均值、方差、标准差、斜度、峭度

- - -

### Matlab版本

- - -

Matlab版本的特征提取代码见它目录像下的readme。在Matlab版本R2014a及以上均通用。不过建议还是用python，更好用一些。

- - -

### 结果评价

行为识别是一个分类问题，评价效果的好坏通常不只看精度，还要看准确率、召回率、F1、特异性等。我们提供一个计算所有结果的函数：[Evaluate.m](https://github.com/jindongwang/activityrecognition/tree/master/code/Evaluate.m)。
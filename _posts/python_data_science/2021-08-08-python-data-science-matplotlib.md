---
layout: post
title: "Python Data Science: Matplotlib, Seaborn"
subtitle: 'How to use Matplotlib and Seaborn to draw plots and graphs'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Science
  - Matplotlib
  - Seaborn
  - Data Visualisation
---

### Matplotlib

Python的绘图库 - `Matplotlib`

将数据预处理和清洗后，会将数据按照横纵坐标进行绘图，利用人工来检查数据情况

#### Install Matplotlib

Open terminal to install matplotlib:

`pip install matplotlib`

#### Draw curves

`import matplotlib` 库的 `pyplot` 模块

**1.Draw a simple curve 绘制一个简单曲线:**

[More detail in blog](shttps://blog.csdn.net/whereismatrix/article/details/78195783)

```vim
import matplotlib
matplotlib.use('TkAgg')
import matplotlib.pyplot as plt

# draw a simple curve
plt.plot([1, 3, 5], [4, 8, 10])
plt.show()

```

graph input:


**2.Draw a custom curve 绘制一条 `numpy` 计算过的自定义曲线**

绘制一条 `numpy` 计算过的自定义曲线, 区间是从正 `pi` 到负 `pi` 之间选择100个点

```vim
# 横坐标是x
# x轴的定义是 -3.14 ~ 3.14, 中间间隔100个元素
# y轴是sin(x)

import matplotlib
matplotlib.use('TkAgg')
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-np.pi, np.pi, 100)
plt.plot(x, np.sin(x))
plt.show()

>>>

```

**3.Draw multiple curves**

绘制多条曲线:
- `figure(1， dpi=50 )` - 创建一个图表, 精度为50
- 绘制图形的详细精度，精度越高，生成的图片体积就越大
- 如果使用默认的“样式”可以不用`plt.figure`，如果使用自定义的“样式”需要显式的指定

```vim
# 定义域为： -2pi ~ 2pi
x = np.linspace(-np.pi * 2, np.pi * 2, 100)

# create a graph
plt.figure(1, dpi=50)

# draw four lines
for i in range(1, 5):
    plt.plot(x, np.sin(x / i))
plt.show()

```

#### Types of Matplotlib graphs

[Matplotlib Official Website:](https://matplotlib.org/stable/tutorials/index.html)

**1.hist() - draw histogram**

绘制直方图:`plt.hist()`

```vim
import matplotlib
matplotlib.use('TkAgg')
import matplotlib.pyplot as plt

plt.figure(1, dpi=50)
data = [1, 1, 1 , 2, 2, 2, 3, 3, 4, 5, 5, 6, 4]
plt.hist(data)
plt.show()

```

**2.scatter() - draw scatter**

绘制散点图: `plt.scatter()`

```vim
# scattered graph 散点图

x = np.arange(1, 10)
y = x
fig = plt.figure()

# draw the graph
# c='r' means red color
# marker means turning shape into round

plt.scatter(x, y, c = 'r', marker= 'o')
plt.show()
```

**Use `pandas` to read data and use `matplotlib` to draw graph**

用pandas读取数据然后用matplotlib来绘制图形:

`ir.plot(kind='scatter', x='120', y='4')`

```vim
# coding=utf-8
import matplotlib
matplotlib.use('TkAgg')
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

ir = pd.read_csv('iris')
print(ir.head())

# based on the first two columns to draw a scattered graph
ir.plot(kind='scatter', x='120', y='4')

# no meaning but to show pandas.plot() method in pyCharm
plt.show()

>>>
   120    4  setosa  versicolor  virginica
0  6.4  2.8     5.6         2.2          2
1  5.0  2.3     3.3         1.0          1
2  4.9  2.5     4.5         1.7          2
3  4.9  3.1     1.5         0.1          0
4  5.7  3.8     1.7         0.3          0
```

### Seaborn

`Seaborn` - 更漂亮的图形库:

#### Import seaborn

Open terminal: 

`pip install seaborn`

#### Draw scatter using seaborn

`jointplot()` - 用seaborn绘制散点图
- x轴是120这一列
- y轴是4这一列

```vim
# coding=utf-8
import matplotlib
matplotlib.use('TkAgg')
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
import warnings
warnings.filterwarnings('ignore')

ir = pd.read_csv('iris')
# set style
sns.set(style='white', color_codes=True)

# set drawing format as scattered graph
sns.jointplot(x='120', y='4', data=ir, size=5)

# use distplot() to draw the line
sns.distplot(ir['120'])
plt.show()

```

#### Draw colorful graph using seaborn

**Coloring based on categories - 根据分类进行颜色划分:**
- `FacetGrid` means 一般绘图函数
- `hue` 彩色显示分类0/1/2
- `plt.scatter` 绘制散点图
- `add_legend()` 显示分类的描述信息

```vim
ir = pd.read_csv('iris')
sns.set(style='white', color_codes=True)

# FacetGrid means 一般绘图函数
# hue 彩色显示分类0/1/2
# plt.scatter 绘制散点图
# add_legend() 显示分类的描述信息

sns.FacetGrid(ir, hue='virginica', size=5).map(plt.scatter, '120', '4').add_legend()
plt.show()

```


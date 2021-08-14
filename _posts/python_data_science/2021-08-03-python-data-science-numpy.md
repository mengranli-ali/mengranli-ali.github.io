---
layout: post
title: "Python Data Science: NumPy"
subtitle: ''
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Science
  - NumPy
---

## NumPy

**NumPy** is a Python library used for working with arrays. It is the core library for scientific computing in Python. 

It provides a high-performance multidimensional array object, and tools for working with these arrays.

**NumPy** stands for Numerical Python.

**NumPy is faster than Lists** - NumPy arrays **are stored at one continuous place** in memory unlike lists, so processes can access and manipulate them very efficiently. It aims to provide an array object that is up to 50x faster than traditional Python lists.

**NumPy** library 库 - 进行数据预处理, 用于高性能科学计算和数据分析，是常用的高级数据分析库的基础包。

**Why using `Numpy` not `list` ?**
- 这是因为列表 `list` 的元素在系统内存中是分散存储的，而 NumPy 数组存储在一个均匀连续的内存块中。这样数组计算遍历所有的元素，不像列表 list 还需要对内存地址进行查找，从而节省了计算资源。
- Python 的列表 `list` 其实就是 `array` 数组。这样如果我要保存一个简单的数组`[0,1,2]`，就需要有 3 个指针和 3 个整数的对象，这样对于 Python 来说是非常不经济的，浪费了内存和计算时间。
- `NumPy` 中的矩阵计算可以采用**多线程的方式**，充分利用多核 CPU 计算资源，大大提升了计算效率.


Example:

```vim
import numpy as np

arr1 = np.array([2,3,4])
print(arr1)
print(arr1.dtype)

>>>[2 3 4]
>>>int64
```

### Install NumPy

use terminal and input `pip3 install numpy`

```vim
$ pip3 install numpy
```


### NumPy array & data type

NumPy的数组与数据类型

`array` 列表已经过 NumPy 的封装, 所以在计算效率上更高:

`Integer` - 整数int65:

```vim
import numpy as np

arr1 = np.array([2,3,4])
print(arr1)
print (arr1.dtype)

>>>
[2 3 4]
int64
```


`float` 浮点数/小数 float64:

```vim
import numpy as np

arr2 = np.array([1.2, 2.3, 3.4])
print(arr2.dtype)

>>>
[1.2 2.3 3.4]
float64
```

`array + array` 列表array累加：

```vim
import numpy as np

arr1 = np.array([2,3,4])
arr2 = np.array([1.2, 2.3, 3.4])

print(arr1 + arr2)

>>>
[3.2 5.3 7.4]
```

### NumPy Matrix Calculation

NumPy的数组与标量的计算:

**数组 * 标量10**

```vim
import numpy as np

arr1 = np.array([2,3,4])
arr2 = np.array([1.2, 2.3, 3.4])

print(arr2 * 10)

>>>
[12. 23. 34.]

```

**NumPy矩阵库 `Matrix`** 

`NumPy` 中包含了一个矩阵库 `numpy.matlib`，该模块中的函数返回的是一个矩阵，而不是 `ndarray` 对象。

一个 `m x n` 的矩阵是一个由 `m` 行（row） `n` 列（column）元素排列成的矩形阵列。

矩阵里的元素可以是数字、符号或数学式。

以下是一个由 6 个数字元素构成的 2 行 3 列的矩阵：

```vim
[[1,9,13]
 [2,3,10]
 [5,7,19]]
```

**NumPy two-dimensional array** 二维数组 - 矩阵

Example: 嵌套列表- 通过 numpy 将嵌套列表转换为二维矩阵 a:

```vim
import numpy as np

data = [[1,2,3], [4,5,6]]
arr3 = np.array(data)

print(arr3)
print(arr3.dtype)

>>>
[[1 2 3]
 [4 5 6]]
>>>int64
```

1.Define one-dimensional Matrix = 0 定义全为0的矩阵 

定义一维矩阵:

```vim
import numpy as np

print(np.zeros(10))

>>>
[0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
```

2.Define n-dimensional Matrix with value of 0

定义多维矩阵 - 3行5列的为 0 矩阵：

支持类型为Union, 所以应该包含在枚举中

```vim
import numpy as np

print(np.zeros((3,5)))

>>>
[[0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0.]]
```

3.Define n-dimensional Matrix with value of 1

定义多维矩阵 - 4行6列的为 1 矩阵:

```vim
import numpy as np

print (np.ones((4,6)))

>>>
[[1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1.]]
```

4.Set Matrix as null value

定义三维矩阵为空值 - 矩阵设置为空值并不安全, 所以系统随机填充任意值

```vim
import numpy as np

print(np.empty((2,3,2)))

>>>
[[[-1.72723371e-077  2.00389337e+000]
  [ 3.45845952e-323  0.00000000e+000]
  [ 0.00000000e+000  0.00000000e+000]]

 [[ 0.00000000e+000  0.00000000e+000]
  [ 0.00000000e+000  0.00000000e+000]
  [ 0.00000000e+000  0.00000000e+000]]]
```

### NumPy Slicing and Indexing

NumPy的索引和切片

**1.Slicing array 对数组进行切片**

```vim
import numpy as np

arr4 = np.arange(10)

print(arr4)
print(arr4[5])
print(arr4[5:8])

>>>
[0 1 2 3 4 5 6 7 8 9]
5
[5 6 7]
```

**2.Editing array 对数组进行内容修改**

```vim
import numpy as np

arr4 = np.arange(10)
arr4[5:8] = 10

print(arr4)
print(arr4[5])
print(arr4[5:8])

>>>
[ 0  1  2  3  4 10 10 10  8  9]
10
[10 10 10]
```

**3.Copy array but not editing original elements**

对数组切片进行复制, 再对复制的数组进行修改, 而原数组仍旧不变：

```vim
import numpy as np

arr4 = np.arange(10)
arr4[5:8] = 10

print(arr4)
arr_slice = arr4[5:8].copy()
arr_slice[:] = 15

print(arr_slice)
print(arr4)

>>>
[ 0  1  2  3  4 10 10 10  8  9]
[15 15 15]
[ 0  1  2  3  4 10 10 10  8  9]
```

## Two Objects in NumPy 

**Two key objects in  `NumPy`：**
- `ndarray`（N-dimensional array object）解决了多维数组问题。
- `ufunc`（universal function object）则是解决对数组进行处理的函数。

### `ndarray` 对象

`ndarray` 实际上是多维数组的含义。

在 `NumPy` 数组中，维数称为秩（`rank`），一维数组的秩为 1，二维数组的秩为 2，以此类推。

在 `NumPy` 中，每一个线性的数组称为一个轴（`axes`），其实秩就是描述轴的数量。

Example:
- `.shape` 属性获得数组的大小
- `.dtype` 获得元素的属性
- 对数组里的数值进行修改的话，直接赋值即可。下标是从 0 开始计的，所以如果你想对 b 数组，九宫格里的中间元素进行修改的话，下标应该是`[1,1]`。

```vim
import numpy as np
a = np.array([1, 2, 3])
b = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
b[1,1]=10

print a.shape
print b.shape
print a.dtype
print b

>>>
(3L,)
(3L, 3L)
int32
[[ 1  2  3]
 [ 4 10  6]
 [ 7  8  9]]
```

**Structured Array：**

**If calculating names, ages, subject grades of students in a class:**

如果你想统计一个班级里面学生的姓名、年龄，以及语文、英语、数学成绩：

通过 struct 定义结构类型，结构中的字段占据连续的内存空间，每个结构体占用的内存大小都相同

首先在 `NumPy` 中是用 `dtype` 定义的结构类型，然后在定义数组的时候，用 array 中指定了结构数组的类型 `dtype=persontype`，这样可以自由地使用自定义的 `persontype` 。

比如想知道每个人的语文成绩，就可以用 `chineses = peoples[:][‘chinese’]`。

```vim
import numpy as np

persontype = np.dtype({
    'names':['name', 'age', 'chinese', 'math', 'english'],
    'formats':['S32','i', 'i', 'i', 'f']})

peoples = np.array([("ZhangFei",32,75,100, 90),("GuanYu",24,85,96,88.5),
       ("ZhaoYun",28,85,92,96.5),("HuangZhong",29,65,85,100)],
    dtype=persontype)
    
ages = peoples[:]['age']
chineses = peoples[:]['chinese']
maths = peoples[:]['math']
englishs = peoples[:]['english']

print np.mean(ages)
print np.mean(chineses)
print np.mean(maths)
print np.mean(englishs)

>>>
28.25
77.5
93.25
93.75
```

### `ufunc` 运算

`ufunc` 是 `universal function` 的缩写，它能对数组中每个元素进行函数操作。`NumPy` 中很多 `ufunc` 函数计算速度非常快，因为都是采用 C 语言实现的。

**1.Create continuous array 连续数组的创建**

`np.arange` 和 `np.linspace` 起到的作用是一样的，都是创建等差数组。

这两个数组的结果 `x1,x2` 都是`[1 3 5 7 9]`。结果相同，但是你能看出来创建的方式是不同的。
- `arange()` 类似内置函数 `range()`，通过指定初始值、终值、步长来创建等差数列的一维数组，默认是不包括终值的。
- `linspace` 是 `linear space` 的缩写，代表线性等分向量的含义。`linspace()` 通过指定初始值、终值、元素个数来创建等差数列的一维数组，默认是包括终值的。

```vim
import numpy as np

x1 = np.arange(1,11,2)
x2 = np.linspace(1,9,5)

print(x1)
print(x2)
>>>
[1 3 5 7 9]
[1 3 5 7 9]
```

**2.Basic Calculations 算数运算** 

通过 NumPy 可以自由地创建等差数组, 也可以进行加、减、乘、除、求 n 次方和取余数。

在取余函数里，你既可以用 `np.remainder(x1, x2)`，也可以用 `np.mod(x1, x2)`，结果是一样的。

```vim
x1 = np.arange(1,11,2)
x2 = np.linspace(1,9,5)

print np.add(x1, x2)
print np.subtract(x1, x2)
print np.multiply(x1, x2)
print np.divide(x1, x2)
print np.power(x1, x2)
print np.remainder(x1, x2)

>>>
[ 2.  6. 10. 14. 18.]
[0. 0. 0. 0. 0.]
[ 1.  9. 25. 49. 81.]
[1. 1. 1. 1. 1.]
[1.00000000e+00 2.70000000e+01 3.12500000e+03 8.23543000e+05
 3.87420489e+08]
[0. 0. 0. 0. 0.]
```

**3.Statistical Func in Numpy 统计函数**

How to use statistical func in Numpy:
- To have a clear understanding of data, we need to use descriptive statistics 描述性统计分析
- For example, Maximum/Minimum/Mean of data, 比如了解这些数据中的最大值、最小值、平均值，是否符合正态分布，方差、标准差多少等等。

**amax(),amin()**

计数组 / 矩阵中的最大值函数 amax()，最小值函数 amin()
- amin() 用于计算数组中的元素沿指定轴的最小值。
- 对于一个二维数组 a，amin(a) 指的是数组中全部元素的最小值
- **amin(a,0) 是延着 axis=0 轴的最小值**，axis=0 轴是把元素看成了`[1,4,7], [2,5,8], [3,6,9]`三个元素，所以最小值为`[1,2,3]`。
- amin(a,1) 是延着 axis=1 轴的最小值，axis=1 轴是把元素看成了`[1,2,3], [4,5,6], [7,8,9]`三个元素，所以最小值为`[1,4,7]`。
- 同理 amax() 是计算数组中元素沿指定轴的最大值。
- axis=0 means 纵列
- axis=1 means 横行

```vim
import numpy as np
a = np.array([[1,2,3], [4,5,6], [7,8,9]])

print np.amin(a)
print np.amin(a,0)
print np.amin(a,1)
print np.amax(a)
print np.amax(a,0)
print np.amax(a,1)

>>>
1
[1 2 3]
[1 4 7]
9
[7 8 9]
[3 6 9]
```

**ptp()**

计最大值与最小值之差 ptp()
- np.ptp(a) 可以统计数组中最大值与最小值的差，即 9-1=8
- ptp(a,0) 统计的是沿着 axis=0 轴的最大值与最小值之差，即 7-1=6（当然 8-2=6,9-3=6，第三行减去第一行的 ptp 差均为 6
- ptp(a,1) 统计的是沿着 axis=1 轴的最大值与最小值之差，即 3-1=2（当然 6-4=2, 9-7=2，即第三列与第一列的 ptp 差均为 2


```vim
import numpy as np
a = np.array([[1,2,3], [4,5,6], [7,8,9]])

print np.ptp(a)
print np.ptp(a,0)
print np.ptp(a,1)

>>>
8
[6 6 6]
[2 2 2]
```

**percentile()**

统计数组的百分位数 - percentile() 代表着第 p 个百分位数：
- 这里 p 的取值范围是 0-100，如果 p=0，那么就是求最小值
- 如果 p=50 就是求平均值，如果 p=100 就是求最大值。
- 同样也可以在 axis=0 和 axis=1 两个轴上的 p% 的百分位数。

```vim
import numpy as np
a = np.array([[1,2,3], [4,5,6], [7,8,9]])

print np.percentile(a, 50)
print np.percentile(a, 50, axis=0)
print np.percentile(a, 50, axis=1)

>>>
5.0
[4. 5. 6.]
[2. 5. 8.]
```

**median(), mean()**

统计数组中的中位数, 平均数

```vim
import numpy as np
a = np.array([[1,2,3], [4,5,6], [7,8,9]])

# median
print np.median(a)
print np.median(a, axis=0)
print np.median(a, axis=1)

# mean
print np.mean(a)
print np.mean(a, axis=0)
print np.mean(a, axis=1)

>>>
5.0
[4. 5. 6.]
[2. 5. 8.]
5.0
[4. 5. 6.]
[2. 5. 8.]
```

**average()**

统计数组中的加权平均值:
- `average()` 函数可以求加权平均
- 加权平均的意思就是每个元素可以设置个权重，默认情况下每个元素的权重是相同的
- 所以 `np.average(a)=(1+2+3+4)/4=2.5`

指定权重数组：
- 你也可以指定权重数组 `wts=[1,2,3,4]`
- 这样加权平均 `np.average(a,weights=wts)=(1*1+2*2+3*3+4*4)/(1+2+3+4)=3.0`

```vim
import numpy as np
a = np.array([1,2,3,4])
wts = np.array([1,2,3,4])

print np.average(a)
print np.average(a,weights=wts)

>>>
2.5
3.0
```

**std(), var()**

统计数组中的标准差,方差:
- 方差的计算是指每个数值与平均值之差的平方求和的平均值
- 即 `mean((x - x.mean())** 2)`

标准差是方差的算术平方根:
- 在数学意义上，代表的是一组数据离平均值的分散程度。
- 所以 `np.var(a)=1.25`, `np.std(a)=1.118033988749895`

```vim
import numpy as np
a = np.array([1,2,3,4])

print np.std(a)
print np.var(a)

>>>
1.118033988749895
1.25
```

### NumPy Sorting

使用 `sort` 函数: `sort(a, axis=-1, kind=‘quicksort’, order=None)`，默认情况下使用的是快速排序。

在 `kind` 里，可以指定 `quicksort`、`mergesort`、`heapsort` 分别表示快速排序、合并排序、堆排序。

同样 `axis` 默认是 `-1`，即沿着数组的最后一个轴进行排序，也可以取不同的 `axis` 轴，或者 `axis=None` 代表采用扁平化的方式作为一个向量进行排序。

另外 `order` 字段，对于结构化的数组可以指定按照某个字段进行排序。

#### Axis

Axis就是数组层级，在Numpy中，dimensions指代的是数组的维数。
- axis=0 是跨行（纵向）
- axis=1 是跨列（横向）

这个array的维数只有2，即axis轴有两个，分别是axis=0和axis=1

如下图所示，该二维数组的第0维(axis=0)有三个元素，即axis=0轴的长度length为3

第1维(axis=1)也有三个元素，即axis=1轴的长度length为3。

正是因为axis=0、axis=1的长度都为3，矩阵横着竖着都有3个数，所以该矩阵在线性代数是3维的(rank秩为3)。

```vim
array([[1, 2, 3],
       [2, 3, 4],
       [3, 4, 9]])
```

```vim
import numpy as np
a = np.array([[4,3,2],[2,4,1]])

print np.sort(a)
print np.sort(a, axis=None)
print np.sort(a, axis=0)  
print np.sort(a, axis=1) 

>>>
[[2 3 4]
 [1 2 4]]
[1 2 2 3 4 4]
[[2 3 1]
 [4 4 2]]
[[2 3 4]
 [1 2 4]]
```

```vim
import numpy as np
a = np.array([1, 2, 3])
b = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
b[1, 1] = 10
b[0, 1] = 11
b[1, 0] = 12
b[1, 2] = 99

print(a.shape)
print(b.shape)
print(a.dtype)
print(b)

>>>
(3,)
(3, 3)
int64
[[ 1 11  3]
 [12 10 99]
 [ 7  8  9]]
```

**How to use Axis?**

Example: 4 people scored the preference of 3 fruits, with total score of 10 points. 

例如现在我们收集了四个同学对苹果、榴莲、西瓜这三种水果的喜爱程度进行打分的数据（总分为10），每个同学都有三个特征：

```vim
item = np.array([[1,4,8],[2,3,5],[2,5,1],[1,10,7]])

array([[1, 4, 8],
       [2, 3, 5],
       [2, 5, 1],
       [1, 10, 7]])
```

每一行包含了同一个人的三个特征，如果我们想看看哪个同学最喜欢吃水果，那就可以用：

`item.sum(axis = 1)`

可以大概看出来同学4最喜欢吃水果:

`array([13, 10,  8, 18])`

哪种水果最受欢迎：

`item.sum(axis = 0)`

可以看出基本是榴莲最受欢迎:
`
array([ 6, 22, 21])`



#### Practice

**Example: Using NumPy to calculate Mean, Median, Max, Min, Variance, Std Deviation**

```vim
import numpy as np
a = np.array([[4,3,2],[2,4,1]])

print(np.sort(a))
print(np.sort(a, axis=None))
print(np.sort(a, axis=0))
print(np.sort(a, axis=1))

print("\npart 6 作业\n")

persontype = np.dtype({
    'names':['name', 'chinese','english','math' ],
    'formats':['S32', 'i', 'i', 'i']})
peoples = np.array([("ZhangFei",66,65,30),("GuanYu",95,85,98),
       ("ZhaoYun",93,92,96),("HuangZhong",90,88,77),
       ("DianWei",80,90,90)],dtype=persontype)
       
#指定的竖列
name = peoples[:]['name']
chinese = peoples[:]['chinese']
english = peoples[:]['english']
math = peoples[:]['math']

#定义函数用于显示每一排的内容
def show(name,cj):
    print('{} | {} | {} | {} | {} | {} '
          .format(name,np.mean(cj),np.min(cj),np.max(cj),np.var(cj),np.std(cj)))

print("科目 | 平均成绩 | 最小成绩 | 最大成绩 | 方差 | 标准差")
show("语文", chinese)
show("英语", english)
show("数学", math)

print("排名:")

#用sorted函数进行排序
ranking = sorted(peoples,key=lambda x:x[1]+x[2]+x[3], reverse=True)
print(ranking)

```


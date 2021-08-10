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

### NumPy

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

#### Install NumPy

use terminal and input `pip3 install numpy`

```vim
$ pip3 install numpy
```


#### NumPy array & data type

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

#### NumPy Matrix Calculation

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

#### NumPy Slicing and Indexing

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

### Two Objects in NumPy 

**Two key objects in  `NumPy`：**
- `ndarray`（N-dimensional array object）解决了多维数组问题。
- `ufunc`（universal function object）则是解决对数组进行处理的函数。

#### `ndarray` 对象

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

#### `ufunc` 运算

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









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


















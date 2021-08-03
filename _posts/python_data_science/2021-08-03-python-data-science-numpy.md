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
print(arr1 + arr2)

>>>
[3.2 5.3 7.4]
```










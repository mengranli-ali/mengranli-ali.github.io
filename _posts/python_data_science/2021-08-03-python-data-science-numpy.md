---
layout: post
title: "Python Data Science: NumPy"
subtitle: ''
author: "Mengran"
header-style: text
tags:
  - Python
  - Tensorflow
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





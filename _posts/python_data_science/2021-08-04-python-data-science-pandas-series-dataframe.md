---
layout: post
title: "Python Data Science: Pandas and Series"
subtitle: ''
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Science
  - Series
  - Pandas
---


**Pandas 可以说是基于 `NumPy` 构建的含有更高级数据结构和分析能力的工具包**

**在数据分析工作中，Pandas 的使用频率是很高的:**
- 一方面是因为 Pandas 提供的基础数据结构 DataFrame 与 json 的契合度很高，转换起来就很方便。
- 另一方面，如果我们日常的数据清理工作不是很复杂的话，你通常用几句 Pandas 代码就可以对数据进行规整。
- Pandas 可以说是基于 NumPy 构建的含有更高级数据结构和分析能力的工具包。

`Series` 和 `DataFrame` 这两个核心数据结构，他们分别代表着一维的序列和二维的表结构。


### Pandas

**数据结构: `Series` 和 `DataFrame`**

基于这两种数据结构，`Pandas` 可以对数据进行导入、清洗、处理、统计和输出。

`Pandas` 用于数据预处理和数据清洗

`Pandas` 会自动对齐显示, 灵活处理缺失数据, 比如用平均值来填充。

**Install Pandas**

`pip install pandas`

**Import Pandas**

```vim
from pandas import Series, DataFrame
import pandas as pd

```

### Series

**用`Pandas`定义一维数组 - `Series`**

`Series` is `Pandas` one-dimensional array; 它对`Numpy`的`array`进行封装

**Series 是个定长的字典序列。**
- 说是定长是因为在存储的时候，相当于两个 `ndarray`，这也是和字典结构最大的不同。
- 因为在字典的结构里，元素的个数是不固定的。`Series` 有两个基本属性：`index` 和 `values`。
- 在 `Series` 结构中，`index` 默认是 `0,1,2,……` 递增的整数序列，当然我们也可以自己来指定索引，比如 `index=[‘a’, ‘b’, ‘c’, ‘d’]`。


```vim
from pandas import Series, DataFrame
import pandas as pd

obj = Series([4,5,8,-1])

print(obj)

>>>
0    4
1    5
2    8
3   -1
```

```vim
import pandas as pd
from pandas import Series, DataFrame

x1 = Series([1,2,3,4])
x2 = Series(data=[1,2,3,4], index=['a', 'b', 'c', 'd'])

print x1
print x2

>>>
0    1
1    2
2    3
3    4
dtype: int64
a    1
b    2
c    3
d    4
dtype: int64
```

这个例子中，x1 中的 index 采用的是默认值，x2 中 index 进行了指定。

我们也可以采用字典的方式来创建 Series，比如：

```vim
d = {'a':1, 'b':2, 'c':3, 'd':4}
x3 = Series(d)

print x3 

>>>

```

**Indexing Series 单独对Series进行索引取值**

start=0 索引从0开始, 在第4处索引停止, 每个值的长度为1:

```vim
from pandas import Series, DataFrame
import pandas as pd

obj = Series([4,5,8,-1])
print(obj.index)
print(obj.values)

>>>
dtype: int64
RangeIndex(start=0, stop=4, step=1)
[ 4  5  8 -1]
```

**`Dictionary` 字典是通过哈希hash运算**

字典是通过哈希表（`hash table`）方式实现的存储， 存储的时候先取字典的`key`，使用哈希函数计算`key`对应的哈希函数值。

如果地址没有被占用就存入这个元素，如果占用就找下一个地址，如果还被占用就继续找下一个地址。

简单字符会经过哈希运算成复杂字符，通过 `key` 可以得到同样的哈希值，将 a b c映射成比较复杂的字符。

如果字符相同，就会进行覆盖，因此字典中的key不能重复。

**_Q: 哪些可以作为字典中的key?_**

`int float string tuple`

**_Q: 哪些不可以作为字典中的key?_**

`['a']
{'b'}`

_**Q: pandas的索引可以相同，那如何唯一确定一个元素呢？**_

重复索引可以算得上`pandas`的一个大坑了，但是软件支持，那么就需要人为去控制。

最常见的解决方法是使用`reindex()`生成新的索引，替代旧的重复的索引，或使用`reset_index()`重置索引。


### Series Basics

**Series的基本操作:**

**1. Series index 手动操作`Series`的索引`index`**

```vim
from pandas import Series, DataFrame
import pandas as pd

obj2 = Series([4,5,6,-9], index=['a', 'c', 'e', 'g'])

print(obj2)

>>>
a    4
c    5
e    6
g   -9
dtype: int64

```

**2.Adding value to Series 对索引赋值**

```vim
from pandas import Series, DataFrame
import pandas as pd

obj2 = Series([4,5,6,-9], index=['a', 'c', 'e', 'g'])
print(obj2)
obj2['c'] = 6
print(obj2)

>>>
a    4
c    6
e    6
g   -9
dtype: int64

```

**3.Check if index 'x' is in Series**

判断'e'是否在索引中:

```vim
print('e' in obj2)

>>>TRUE
```

**4.Turn elements from `Dictionary` into `Series`**

```vim
# 先定义一个字典
sdata = {'beijing': 35000, 'shanghai': 71000, 'guangzhou': 16000, 'shenzhen': 54000}

# 再转换成Series
obj3 = Series(sdata)
print(obj3)

>>>
beijing      35000
guangzhou    16000
shanghai     71000
shenzhen     54000
dtype: int64
```

**4.Turn index into different value**

将索引改成缩写：

```vim
obj3.index = ['bj', 'sh','gz', 'sz']

print(obj3)

>>>
bj    35000
sh    16000
gz    71000
sz    54000
dtype: int64
```

**Q: If turning dictionary into series, will it automatically reorder its index?**

将字典转换为Series，会对自动对 index 进行排序么？ 输出的 Series 与字典中的 key 顺序不一样了？

如果python版本低于3.6或pandas版本低于0.23， 会出现重排，参考 [link](http://pandas.pydata.org/pandas-docs/stable/dsintro.html).


### Cleaning data - Reindex Series & auto-fill

**`reindex()` 对当前索引进行重新修改**

```vim
# define 4 elements and their index
# 使用重新索引后新增索引e，所得到的value是NaN


obj = Series([4.5, 7.2, -5.3, 3.5], index=['b', 'd', 'c', 'a'])
obj1 = obj.reindex(['a', 'b', 'c', 'd', 'e'])
print(obj1)

>>>
a    3.5
b    4.5
c   -5.3
d    7.2
e    NaN
dtype: float64
```

**Auto-fill null after reindex 重新索引后将自动新增的空值自动填充为0**

重新索引后新增索引为空值的话，自动填充为0，更方便数据清洗：

`fill_value=0`

```vim
# define 4 elements and their index

obj = Series([4.5, 7.2, -5.3, 3.5], index=['b', 'd', 'c', 'a'])
obj1 = obj4.reindex(['a', 'b', 'c', 'd', 'e'], fill_value=0)
print(obj1)

>>>
a    3.5
b    4.5
c   -5.3
d    7.2
e    0.0
dtype: float64
```

**Auto-fill null with values from previous/next position**

**自动填充靠近相邻的值 - 使用 `method='ffil'` 方法填充当前值的上一值或下一值**

**1.Fill in with previous value 用前面一个值来填充 `ffil`:**

```vim
obj = Series(['blue', 'purple', 'yellow'], index=[0, 2, 4])
print(obj.reindex(range(6)))

print(obj.reindex(range(6), method='ffill'))

>>>
0      blue
1       NaN
2    purple
3       NaN
4    yellow
5       NaN
dtype: object

0      blue
1      blue
2    purple
3    purple
4    yellow
5    yellow
dtype: object
```

**Fill in with value from next position 用后面一个值来填充 `bfil`**

```vim
obj2 = Series(['blue', 'purple', 'yellow'], index=[0, 2, 4])
print(obj2.reindex(range(6)))
print(obj2.reindex(range(6), method='bfill'))

>>>
0      blue
1    purple
2    purple
3    yellow
4    yellow
5       NaN
dtype: object
```

### Cleaning data - Delete NaN

Import `nan` from `numpy` 从 `numpy` 中导入缺失值:

```vim
from numpy import nan as NA

data = Series([1, NA, 2])
print(data)
print(data.dropna())

>>>
0    1.0
1    NaN
2    2.0
dtype: float64

0    1.0
2    2.0
dtype: float64
```
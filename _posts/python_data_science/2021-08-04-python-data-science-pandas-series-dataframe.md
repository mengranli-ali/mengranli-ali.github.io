---
layout: post
title: "Python Data Science: Pandas, Series & Dataframe"
subtitle: ''
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Science
  - Series
  - Dataframe
  - Pandas
---

### Pandas

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




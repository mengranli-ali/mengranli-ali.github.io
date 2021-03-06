---
layout: post
title: "Python Data Science: Dataframe"
subtitle: 'Dataframe, n-dimensional array of pandas'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Science
  - Dataframe
  - Pandas
---

**Pandas最主要的两个数据结构：Series，DataFrame**

**Series提供：index,values,map**

**DataFrame常用的函数：**
- `describe()` 统计性描述
- `drop_duplicates()` 删除重复行
- `rename(columns=...)` 更名
- `dropna()` 删除具有空的行
- `isnull()` 判断空值
- `fillna()` 填充空值
- `apply()` 应用函数
- `merge()` 合并df
- `value_counts()` 统计某列的各类型个数
- `read_excel() to_excel()` 读取和保存excel
- `set_index()` 设置索引
- `cut` 分组


### Dataframe

**`DataFrame` 类型数据结构类似数据库表。**
- 包括了行索引和列索引
- 可以将 `DataFrame` 看成是由相同索引的 `Serie`s 组成的**字典**类型。

**`Dataframe` is multiple-dimensional `array` of `Pandas`.**

The structure of `dataframe` is a `dictionary`; Then it will print out a table.

创建一个字典的dataframe结构 - 生成dataframe结构的表格table:

```vim
# create a variable called data
# structure of data is dictionary

data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

# get a dataframe structure table

frame = DataFrame(data)
print(frame)

>>>
       city  pop  year
0  shanghai  1.5  2016
1  shanghai  1.7  2017
2  shanghai  3.6  2018
3   beijing  2.4  2017
4   beijing  2.9  2018
```

**Example 2: Input candidates' scores on each subject**

- df1: input based on normal index 0, 1, 2, 3...
- df2: input based on selected index & columns in customised order
- 以例子中的 df2 为例，列索引是`[‘English’, ‘Math’, ‘Chinese’]`，行索引是`[‘ZhangFei’, ‘GuanYu’, ‘ZhaoYun’, ‘HuangZhong’, ‘DianWei’]`

```vim
import pandas as pd
from pandas import Series, DataFrame

data = {'Chinese': [66, 95, 93, 90,80],'English': [65, 85, 92, 88, 90],'Math': [30, 98, 96, 77, 90]}
df1= DataFrame(data)
df2 = DataFrame(data, index=['ZhangFei', 'GuanYu', 'ZhaoYun', 'HuangZhong', 'DianWei'], columns=['English', 'Math', 'Chinese'])

print(df1)
print(df2)

>>>
   Chinese  English  Math
0       66       65    30
1       95       85    98
2       93       92    96
3       90       88    77
4       80       90    90

            English  Math  Chinese
ZhangFei         65    30       66
GuanYu           85    98       95
ZhaoYun          92    96       93
HuangZhong       88    77       90
DianWei          90    90       80
```


#### Sorting in dataframe

**Customised Order:** 对dataframe进行排序 - `columns=[]`

优先对 `year` 进行排序:

```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

frame2 = DataFrame(data, columns=['year', 'city', 'pop'])
print(frame2)

>>>
   year      city  pop
0  2016  shanghai  1.5
1  2017  shanghai  1.7
2  2018  shanghai  3.6
3  2017   beijing  2.4
4  2018   beijing  2.9
```

**Sort by index**

`dataframe.sort_index(axis=1)`

**Sort by values**

`dataframe.sort_values(by='xyz')`

**Sort by value list**

dataframe.sort_values(by=['aaa','bbb'])


#### Get value from dataframe

Get one-dimensional value from 2-dimensional dataframe 从二维的dataframe中提取一维value:

Two methods:
```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

frame2 = DataFrame(data, columns=['year', 'city', 'pop'])

# Method 1:
print(frame2['city'])

# Method 2:
print(frame2.city)

>>>
0    shanghai
1    shanghai
2    shanghai
3     beijing
4     beijing
Name: city, dtype: object
```

#### Adding new value to dataframe

1.Adding new value to existing dataframe 

对已有的dataframe新增以及赋予新值:

```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

frame2 = DataFrame(data, columns=['year', 'city', 'pop'])

frame2['new'] = 100
print(frame2)

>>>
   year      city  pop  new
0  2016  shanghai  1.5  100
1  2017  shanghai  1.7  100
2  2018  shanghai  3.6  100
3  2017   beijing  2.4  100
4  2018   beijing  2.9  100
```

2. Adding new value based on pre-conditions

根据已有列的设定条件来自动新增:
- If `city == beijing`, then add a new value of `TRUE`  in a new column; if not, then return `FALSE`


```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

frame2 = DataFrame(data, columns=['year', 'city', 'pop'])

# if city == beijing, then add a new value of TRUE  in a new column, if not, then return FALSE

frame2['capital'] = frame2.city == 'beijing'
print (frame2)

>>>
    year      city  pop  new  capital
0  2016  shanghai  1.5  100    False
1  2017  shanghai  1.7  100    False
2  2018  shanghai  3.6  100    False
3  2017   beijing  2.4  100     True
4  2018   beijing  2.9  100     True
```

#### Nested dictionary

`Nesting Dictionary` means putting a `dictionary` inside another `dictionary`.

使用字典的嵌套：字典中包含另一个字典

```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

pop = {'beijing': {2000:1.5, 2009:2.0},
            'shanghai': {2000:2.0, 2009:3.6}
}

frame3 = DataFrame(pop)
print(frame3)

>>>
        beijing  shanghai
2000      1.5       2.0
2009      2.0       3.6

```

**Reverse columns/rows in input table**

将输出的表格行列转换:

```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

pop = {'beijing': {2000:1.5, 2009:2.0},
       'shanghai': {2000:2.0, 2009:3.6}
}

frame3 = DataFrame(pop)

print(frame3.T)

>>>
           2000  2009
beijing    1.5   2.0
shanghai   2.0   3.6
```

#### Delete values in dataframe

**1.Delete ALL NaN in dataframe**

`dropna()` 删除 `dataframe` 中的所有缺失值:

```vim
data2 = DataFrame([(1.0, 6.5, 3.0), (1.0, NA, NA), (NA, NA, NA)])

print(data2)
print(data2.dropna())

>>>
    0    1    2
0  1.0  6.5  3.0
1  1.0  NaN  NaN
2  NaN  NaN  NaN

     0    1    2
0  1.0  6.5  3.0
```

**2.Delete partial NaN in dataframe**

删除 `dataframe` 中的部分条件缺失值:
- `.dropna(how='all')` delete **rows** with all NaN values
- 删除全是缺失值的一行，保留有部分缺失值的其他行

```vim
data2 = DataFrame([(1.0, 6.5, 3.0), (1.0, NA, NA), (NA, NA, NA)])

print(data2.dropna(how='all'))

>>>
     0    1    2
0  1.0  6.5  3.0
1  1.0  NaN  NaN
```

- `.dropna(axis=1, how='all')` delete **columns** with all NaN values
- 删除全是缺失值的一列，保留有部分缺失值的其他列

```vim
data2 = DataFrame([(1.0, 6.5, 3.0), (1.0, NA, NA), (NA, NA, NA)])
data2[4] = NA

print(data2)
print(data2.dropna(axis=1, how='all'))

>>>
   0    1    2       4
0  1.0  6.5  3.0    NaN
1  1.0  NaN  NaN    NaN
2  NaN  NaN  NaN    NaN

    0    1    2
0  1.0  6.5  3.0
1  1.0  NaN  NaN
2  NaN  NaN  NaN
```

#### Auto-fill NaN values in dataframe 


`fillna(0)` - Fill `NaN` values with `0` 把缺失值填充为0:

**1.Only fill in the copy:**

```vim
data2 = DataFrame([(1.0, 6.5, 3.0), (1.0, NA, NA), (NA, NA, NA)])
data2[4] = NA

# fillna() edit copy of data2
data2.fillna(0)

# thus need to input the whole method here
print(data2.fillna(0))

>>>
    0    1    2    4
0  1.0  6.5  3.0  0.0
1  1.0  0.0  0.0  0.0
2  0.0  0.0  0.0  0.0
```

**2.Edit original values in dataframe:**

`.fillna(0, inplace=True)` - 填充原始的dataframe:

```vim
data2.fillna(0)

print(data2.fillna(0, inplace=True))

print(data2)

>>>
    0    1    2    4
0  1.0  6.5  3.0  0.0
1  1.0  0.0  0.0  0.0
2  0.0  0.0  0.0  0.0
```

#### Multi-layer indexing 层次化索引

使用多层索引：
- 第一层索引有a, b, c, d
- 第二层索引有1，2，3。。

```vim
# 可以根据索引的层次来提取相应数据

from pandas import Series, DataFrame
import pandas as pd
import numpy as np

data = Series(np.random.randn(10),
              index=[['a', 'a', 'a', 'b', 'b', 'b', 'c','c','d', 'd'],
                     [1, 2, 3, 1, 2, 3, 1, 2, 2, 3]])
                     
print(data)

>>>
a  1   -0.202617
   2    0.430599
   3   -0.673567
b  1   -1.988956
   2   -1.258355
   3   -0.337479
c  1    0.539576
   2   -0.174254
d  2   -0.407340
   3    0.292222
dtype: float64
```

**Get values from layer index b**

提取索引b层面下面的数值:

```vim
print (data['b'])

>>>
1   -0.252709
2   -1.937952
3    2.772455
dtype: float64
```

**Get values from multiple layers**

提取多个索引层面下的数值:

```vim
print (data['b':'c'])

>>>
b  1    1.102966
   2    0.419484
   3    0.693002
c  1    0.198791
   2   -0.692139
```

**Turn 1-dimensional Series into 2-dimensional Dataframe**

`.unstack()` 将多层次索引一维Series转换为二维dataframe:

```vim
print (data.unstack())

>>>
        1         2         3
a  0.551714 -0.523543 -0.268379
b  1.538016 -0.013260  1.751864
c  0.422605 -0.165455       NaN
d       NaN -0.086555 -1.660403

```

**Turn Dataframe back to Series**

`.unstack().stack()` 将dataframe再次转换回去Series:

```vim
print (data.unstack().stack())

>>>
a  1   -1.396839
   2    0.026898
   3   -1.322518
b  1   -0.073874
   2   -2.094649
   3    0.495479
c  1    1.659769
   2   -0.463665
d  2   -1.396547
   3   -1.854931
dtype: float64
```

### Import/Output Data

**数据导入和输出:**

`Pandas` allows you to import data from  `xlsx`，`csv` file formats.

`pd.read_excel()`

`Pandas` can also export data to files in `xlsx`, `csv` formats。

`.to_excel()`

If missing packages like `xlrd`, `openpyxl` while running, you can use command `pip install` to install these.

```vim
import pandas as pd
from pandas import Series, DataFrame

score = DataFrame(pd.read_excel('data.xlsx'))
score.to_excel('data1.xlsx')

print(score)

```

### Cleaning Data

**数据清洗：**

**There are several scenarios when cleaning data:**

- Delete unnecessary rows/columns in dataframe
- Rename columns to make it more recognisable
- Drop repetitive values
- Formatting and reformatting

#### Delete unnecessary rows/columns in dataframe

删除 DataFrame 中的不必要的列或行:

`.drop()`

```vim
import pandas as pd
from pandas import Series, DataFrame

data = {'Chinese': [66, 95, 93, 90,80],'English': [65, 85, 92, 88, 90],'Math': [30, 98, 96, 77, 90]}
df1 = DataFrame(data, index=['ZhangFei', 'GuanYu', 'ZhaoYun', 'HuangZhong', 'DianWei'], columns=['English', 'Math', 'Chinese'])

# drop columns
df2 = df1.drop(columns=['Chinese'])

# drop rows/index
df3 = df1.drop(index=['ZhangFei'])

>>>
            English  Math  Chinese
ZhangFei         65    30       66
GuanYu           85    98       95
ZhaoYun          92    96       93
HuangZhong       88    77       90
DianWei          90    90       80

            English  Math
ZhangFei         65    30
GuanYu           85    98
ZhaoYun          92    96
HuangZhong       88    77
DianWei          90    90

            English  Math  Chinese
GuanYu           85    98       95
ZhaoYun          92    96       93
HuangZhong       88    77       90
DianWei          90    90       80

```

#### Rename columns to make it more recognisable

重命名列名 `columns`，让列表名更容易识别:

`.rename(columns=new_names, inplace=True)`

`.rename(columns={'old_names1': 'new_names1', 'old_names2': 'new_names2'})`

Example:

```vim
data = {'Chinese': [66, 95, 93, 90,80],'English': [65, 85, 92, 88, 90],'Math': [30, 98, 96, 77, 90]}
df1 = DataFrame(data, index=['ZhangFei', 'GuanYu', 'ZhaoYun', 'HuangZhong', 'DianWei'], columns=['English', 'Math', 'Chinese'])

df1.rename(columns={'Chinese': 'YuWen', 'English': 'Yingyu'}, inplace = True)
```

#### Drop repetitive values

```drop_duplicates()```

数据采集可能存在重复的行，这时只要使用 `drop_duplicates()` 就会自动把重复的行去掉。

```vim
#去除重复行
df = df.drop_duplicates() 

```

#### Formatting & Reformatting

**1.Change data format 更改数据格式**

`.astype()`

```vim
import pandas as pd
import numpy as np
from pandas import Series, DataFrame

data = {'Chinese': [66, 95, 93, 90,80],'English': [65, 85, 92, 88, 90],'Math': [30, 98, 96, 77, 90]}
df1 = DataFrame(data, index=['ZhangFei', 'GuanYu', 'ZhaoYun', 'HuangZhong', 'DianWei'], columns=['English', 'Math', 'Chinese'])

df4 = df1['Chinese'].astype('str')
df5 = df1['Chinese'].astype(np.int64)

print(df4)
print(df5)

>>>
ZhangFei      66
GuanYu        95
ZhaoYun       93
HuangZhong    90
DianWei       80
Name: Chinese, dtype: object

ZhangFei      66
GuanYu        95
ZhaoYun       93
HuangZhong    90
DianWei       80
Name: Chinese, dtype: int64

```

**2.Turn blank into other values 处理数据间的空格**

有时候我们先把格式转成了 `str` 类型，是为了方便对数据进行操作

这时想要删除数据间的空格，我们就可以使用` strip `函数：

`.map(str.strip)`
`.map(str.lstrip)`
`.map(str.rstrip)`

```vim
#删除左右两边空格
df1['Chinese']=df1['Chinese'].map(str.strip)

#删除左边空格
df1['Chinese']=df1['Chinese'].map(str.lstrip)

#删除右边空格
df1['Chinese']=df1['Chinese'].map(str.rstrip)

```

**Delete special symbols/characters:**

Example: Delete `$` in `Chinese` column

`.str.strip('$')`

```vim
df1['Chinese']=df1['Chinese'].str.strip('$')
```

**Uppercase & Lowercase**

大小写是个比较常见的操作，比如人名、城市名等的统一都可能用到大小写的转换

在 Python 里直接使用 `upper()`, `lower()`,` title()` 函数

```vim
#全部大写
df2.columns = df2.columns.str.upper()

#全部小写
df2.columns = df2.columns.str.lower()

#首字母大写
df2.columns = df2.columns.str.title()

```

**Uppercase in both index & columns**

```vim
import pandas as pd
import numpy as np
from pandas import Series, DataFrame

data = {'Chinese': [66, 95, 93, 90,80],'English': [65, 85, 92, 88, 90],'Math': [30, 98, 96, 77, 90]}
df1 = DataFrame(data, index=['ZhangFei', 'GuanYu', 'ZhaoYun', 'HuangZhong', 'DianWei'], columns=['English', 'Math', 'Chinese'])

df1.columns = df1.columns.str.upper()
df1.index = df1.index.str.upper()

print(df1)

>>>
            ENGLISH  MATH  CHINESE
ZHANGFEI         65    30       66
GUANYU           85    98       95
ZHAOYUN          92    96       93
HUANGZHONG       88    77       90
DIANWEI          90    90       80

```

**Look for null/NaN**

数据量大的情况下，有些字段存在空值 `NaN` 的可能

这时就需要使用 `Pandas` 中的 `isnull` 函数进行查找。

1.Look for null values:

`df.isnull()`

it will return `False`/`True`

2.look for which columns include null values 

`df.isnull().any()`

it will return `False`/`True`

#### Using apply() to clean data

**使用 `apply` 函数对数据进行清洗**

`apply()` 函数是 `Pandas` 中自由度非常高的函数，使用频率也非常高。

比如我们想对 `name` 列的数值都进行大写转化可以用：

```vim
df['name'] = df['name'].apply(str.upper)
```

我们也可以定义个函数，在 `apply` 中进行使用:

比如定义 `double_df` 函数是将原来的数值 `*2` 进行返回。然后对 `df1` 中的“语文”列的数值进行 `*2` 处理

```vim
def double_df(x):
    return 2*x
           
df1[u'语文'] = df1[u'语文'].apply(double_df)

```

也可以定义更复杂的函数 To define more complicated func:

比如对于 DataFrame，我们新增两列:
- 'new1'列是“语文”和“英语”成绩之和的 m 倍
- 'new2'列是“语文”和“英语”成绩之和的 n 倍
- axis=1 代表按照列为轴进行操作
- axis=0 代表按照行为轴进行操作
- args 是传递的两个参数，即 n=2, m=3，在 plus 函数中使用到了 n 和 m，从而生成新的 df

```vim
def plus(df,n,m):
    df['new1'] = (df[u'语文']+df[u'英语']) * m
    df['new2'] = (df[u'语文']+df[u'英语']) * n
    return df
    
df1 = df1.apply(plus,axis=1,args=(2,3,))

>>>

```

### Calculating Data

数据统计:

`Pandas` 和 `NumPy` 一样，都有常用的统计函数,

如果遇到空值 `NaN`，会自动排除。

#### Commonly-used func

- `count()` - count numbers without NaN
- `describe()` - multiple statistics including count, mean, std, min, max etc.
- `min()` - minimum value
- `max()` - maximum value
- `sum()` - total value
- `mean()` - average 平均值
- `median()` - 中位数
- `var()` - variance 方差
- `std()` - standard variation 标准差
- `argmin()` - index position of minimum value 统计最小值的索引位置
- `argmax()` - index position of maximum value 统计最大值的索引位置
- `idxmin()` - index value of minimum value 统计最小值的索引值
- `idxma()` - index value of maximum value 统计最大值的索引值

**Example:** `.describe()`

```vim
import pandas as pd
import numpy as np
from pandas import Series, DataFrame

df1 = DataFrame({'name':['david', 'lily', 'a', 'b', 'c'], 'data1':range(5)})

print(df1)
print(df1.describe())

>>>
       name  data1
0  ZhangFei      0
1    GuanYu      1
2         a      2
3         b      3
4         c      4

          data1
count  5.000000
mean   2.000000
std    1.581139
min    0.000000
25%    1.000000
50%    2.000000
75%    3.000000
max    4.000000
```

### Join Data Tables 

数据表合并:

一个 DataFrame 相当于一个数据库的数据表，那么多个 DataFrame 数据表的合并就相当于多个数据库的表合并。

**How to join two dataframe table?**

`.merge()`

**1. merge dataframes based on one column**

基于指定列进行连接:

`.merge(df1, df2, on='column_name')`

```vim
import pandas as pd
import numpy as np
from pandas import Series, DataFrame

df1 = DataFrame({'name':['ZhangFei', 'GuanYu', 'a', 'b', 'c'], 'data1':range(5)})
df2 = DataFrame({'name':['ZhangFei', 'GuanYu', 'A', 'B', 'C'], 'data2':range(5)})

df3 = pd.merge(df1, df2, on='name')

print(df3)

>>>
       name  data1  data2
0  ZhangFei      0      0
1    GuanYu      1      1
```

**2.use inner to merge dataframes**

inner 内链接是 merge 合并的默认情况
- inner 内连接其实也就是键的交集
- 在这里 df1, df2 相同的键是 name，所以是基于 name 字段做的连接：df3 = pd.merge(df1, df2, how='inner')

`.merge(df1, df2, how='inner')`

```vim
df3 = pd.merge(df1, df2, how='inner')
print(df3)

>>>
       name  data1  data2
0  ZhangFei      0      0
1    GuanYu      1      1
```

**3.use left to merge dataframes**

left 左连接是以第一个 DataFrame 为主进行的连接，第二个 DataFrame 作为补充。

`.merge(df1, df2, how='left')`

```vim
df3 = pd.merge(df1, df2, how='left')
print(df3)

>>>
       name  data1  data2
0  ZhangFei      0    0.0
1    GuanYu      1    1.0
2         a      2    NaN
3         b      3    NaN
4         c      4    NaN

```

**4.use left to merge dataframes**

right 右连接是以第二个 DataFrame 为主进行的连接，第一个 DataFrame 作为补充。

```vim
df3 = pd.merge(df1, df2, how='right')
print(df3)

>>>
       name  data1  data2
0  ZhangFei    0.0      0
1    GuanYu    1.0      1
2         A    NaN      2
3         B    NaN      3
4         C    NaN      4
```

**5.use outer to merge dataframes**

outer 外连接相当于求两个 DataFrame 的并集。

```vim
df3 = pd.merge(df1, df2, how='outer')
print(df3)

>>>
       name  data1  data2
0  ZhangFei    0.0    0.0
1    GuanYu    1.0    1.0
2         a    2.0    NaN
3         b    3.0    NaN
4         c    4.0    NaN
5         A    NaN    2.0
6         B    NaN    3.0
7         C    NaN    4.0
```

### Use SQL to open Pandas

在 Python 里可以直接使用 `SQL` 语句来操作 `Pandas`:

`pandasql` 工具中的主要函数是 `sqldf`，它接收两个参数：一个 `SQL` 查询语句，还有一组环境变量 `globals()` 或 `locals()`。

`lambda sql: sqldf(sql, globals())`
- 输入的参数是 sql，返回的结果是 sqldf 对 sql 的运行结果
- sqldf 中也输入了 globals 全局参数，因为在 sql 中有对全局参数 df1 的使用。

```vim
import pandas as pd
from pandas import DataFrame
from pandasql import sqldf, load_meat, load_births

df1 = DataFrame({'name':['ZhangFei', 'GuanYu', 'a', 'b', 'c'], 'data1':range(5)})
pysqldf = lambda sql: sqldf(sql, globals())
sql = "select * from df1 where name ='ZhangFei'"
print(pysqldf(sql))

>>>
       name  data1
0  ZhangFei      0
```








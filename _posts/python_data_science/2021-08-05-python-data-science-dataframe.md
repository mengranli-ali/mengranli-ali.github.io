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

### Dataframe

`Dataframe` is multiple-dimensional `array` of `Pandas`.

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








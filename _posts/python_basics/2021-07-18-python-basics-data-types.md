---
layout: post
title: "Python Basics 2: Built-in Data Types & Loop"
subtitle: 'Definition of Array, String, List, Dictionary, Loop etc'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Python Built-in Data Types

Variables can store data of different types, and different types can do different things.

- Lists
- Tuple
- Set
- Dictionary



### Array 序列

Definition: Arrays are used to store multiple values in one single variable. You can access the values by referring to an index number.

Python does not have built-in support for Arrays, but Python Lists can be used instead.

指它的成员都有序排列，并可以通过下标偏移量访问到它的一个或几个成员.

Array includes 字符串 `String `，列表 `List` ，元组 `Tup`.

先定义一个字符串来保存生肖 - create a variable:

```vim
chinese_zodiac = 'abcdefghijkl'
print(chinese_zodiac[0:4])
print(chinese_zodiac[-1])

>>>abcd
>>>l
```

#### Array 1： `String` 字符串 `‘abcd'`

```vim
chinese_zodiac = '猴鸡狗猪鼠牛虎兔龙蛇马羊'
year1 = 2018
year2 = 1994
print(chinese_zodiac[year1 % 12])
print(chinese_zodiac[year2 % 12])

>>>狗
>>>狗
```

**序列基本操作1： 成员关系操作符**

in array a / not in array a

```vim
print('狗'in chinese_zodiac)
print('狗'not in chinese_zodiac)"

>>>True
>>>False
```
**序列基本操作2： 连接操作符**

array a + array b （两个字符串可以直接相加）

```vim
print(chinese_zodiac + chinese_zodiac)
print(chinese_zodiac + 'abcd')

>>>猴鸡狗猪鼠牛虎兔龙蛇马羊猴鸡狗猪鼠牛虎兔龙蛇马羊
>>>猴鸡狗猪鼠牛虎兔龙蛇马羊abcd
```

**序列基本操作3： 重复操作符**

array a * integer

```vim
print(chinese_zodiac * 3)
```

**序列基本操作4： 切片操作符**

```vim
array [0:integer]
```

#### Array 2: 元组 `Tup` -  `['abc', 'def']`

`tuple` is similar to  `list` ，but it can't be edited once initialized.

As `tuple` can't be edited, it doesn't include `append()`, `insert()` methods

可以像访问数组一样进行访问，比如 `tuples[0]`，但不能赋值。

```vim
tuples = ('a', 'b')

print(tuples[1])

>>>b
```

**使用lambda从序列a中取出小于b的元素**

_**Using lambda to select elements less than b from array a**_

```vim
a = (1,3,5,7)
b = 4

# 取出a中小于4的元素
print(list(filter(lambda x: x < b, a)))

# 取出a中小于6的元素
b = 6
print(list(filter(lambda x: x < b, a)))

>>>[1, 3]
>>>[1, 3, 5]
```

**使用lambda从序列a中取出小于b的元素的个数**

_**Using lambda to calculate the number of elements less than b selected from array a.**_

```vim
a = (1,3,5,7)

# 取出a中小于4的元素的个数
b = 4
print(len(list(filter(lambda x: x < b, a))))

# 取出a中小于6的元素的个数
b = 6
print(len(list(filter(lambda x: x < b, a))))

>>>2
>>>3
```

**如何使用元组来计算日期属于哪个生肖**

_**Using Tup to calculate which date belongs to which Chinese zodiac.**_

```vim
zodiac_name = ('mojiezuo', 'shuipingzuo','baiyangzuo','jinniuzuo','shuagnyuzuo')

zodiac_days = ((1,20), (2,18),(3,21),(4,25),(5,21))

(month, day) = (3, 15)

zodiac_day = filter(lambda x:x <=(month, day), zodiac_days)
zodiac_len = len(list(zodiac_day)) % 5
print(zodiac_len)
print(zodiac_name[zodiac_len])

>>>2
>>>baiyangzuo
```

#### Array 3: 列表 `List` - `[0, 'abcd']`

列表是 Python 中常用的数据结构，相当于数组，具有增删改查的功能。
- .len() 获得 lists 中元素的个数
- .append() 在尾部添加元素
- .insert() 在列表中插入元素
= .pop() 删除尾部的元素

列表跟元组最大区别是可以增删元素

The main difference between `list` and `tup` is: **`list` can add/remove elements**

**Add elements in list a** _**append - 在列表中增加元素**_

```vim
a_list = [0,'abc', 'xyz']
a_list.append('yyy')
print(a_list)

>>>[0, 'abc', 'xyz', 'yyy']
```

**Add elements with specific index position to the list:**

```vim
list = ['a', 'b', 'c']
list.insert(0,'mmm')
print(list)

>>>['mmm', 'a', 'b', 'c', 'd']
```

**Remove elements from list a** - **_在列表中删除元素_**

```vim
a_list.remove(0)
print(a_list)

>>>['abc', 'xyz', 'yyy']
```

**Remove the last element in the list: **
```vim
list = ['a', 'b', 'c']
list.pop()
print(list)

>>>['a', 'b']
```

### `dictionary {}` 字典

字典其实就是{key, value}。 多次对同一个 key 放入 value，后面的值会把前面的值冲掉。字典也有增删改查。

增加字典的元素相当于赋值，比如 `score[‘zhaoyun’] = 98`

- .pop() to delete element 
- .get() to look for elements 
- .get('xxx', 100) to add a new pair of key & value

```vim
dic = {'beijing': 1000, 'shanghai': 2000, 'london': 5000}

dic['paris'] = 1323
print(dic)
>>>{'beijing': 1000, 'shanghai': 2000, 'london': 5000, 'paris': 1323}

dic.pop('paris')
print(dic)
>>>{'beijing': 1000, 'shanghai': 2000, 'london': 5000}

print('chongqing' in dic)
>>>FALSE

print(dic.get('shanghai'))
>>>2000

print(dic.get('LA', 9999))
>>>9999

```

**mapping type: dictionary**

`{'哈希值'： ‘对象’}`

`{'length': 180, 'width': 80}`

Example:

```vim
dict1 = {}
print(type(dict1))

dict2 = {'x':1, 'y':2}
print(dict2)

dict3 = {'x':1, 'y':2}
dict3['z'] = 3
print(dict3)

>>><class 'dict'>
>>>{'x': 1, 'y': 2}
>>>{'x': 1, 'y': 2, 'z': 3}
>>>{'x': 1, 'y': 2, 'z': 3}

```

### `set ` collection

集合 set 和字典 dictory 类似，不过set只是 key 的集合，不存储 value。 同样可以增删查:
- 增加使用 .add()
- 删除使用 .remove()
- 查询看某个元素是否在这个集合里，使用 in

```vim
s = set(['a', 'b', 'c'])

s.add('d')
s.remove('b')

print(s)
print('c' in s)

>>>{'a', 'd', 'c'}
>>>TRUE
```

### Conditions and Loop 条件与循环

#### Condition - 条件语句 if 

if … else … 是经典的判断语句，需要注意的是在 if expression 后面有个冒号，同样在 else 后面也存在冒号。

Basic syntax:
```vim
if condition a :
        code block
        
if condition a :
        code block a
   elif condition b:
        code block b
   else: 
        code block c
```

Example:
```vim
x = 'abc'
if x == 'abc':
    print('they are the same')
    
>>>they are the same
```
```vim
x = 'abcccc'
if x == 'abc':
    print('they are the same')
else:
   print('they are not the same')
   
>>>they are not the same
```

```vim
score = 99

if score >= 90:
    print('Excellent')
else:
    if score < 60:
        print('Fail')
    else:
        print('Good Job')

>>>Excellent
```

**Exercise: Input year and output its according Chinese zodiac of dog**

_通过input年份来输出年份所对应的生肖_

```vim
chinese_zodiac = '猴鸡狗猪鼠牛虎兔龙蛇马羊'

# transform into int
year = int(input('please input your birth year:'))

if (chinese_zodiac[year % 12]) == '狗':
  print('The YEAR OF THE DOG')
  
>>>please input your birth year:1994
>>>The YEAR OF THE DOG
```

#### Loop - 循环语句 `for` and `while`

**Loop 1: 条件与循环1：`for loop`**

`for `loop 是一种迭代循环机制，迭代即重复相同的逻辑操作。

如果规定循环的次数，我们可以使用 `range` 函数，它在 `for` 循环中比较常用。

`range(11) `代表从 0 到 10，不包括 11，也相当于 `range(0,11)`

`range` 里面还可以增加步长，比如 `range(1,11,2)` 代表的是`[1,3,5,7,9]`。

Basic syntax:
```vim
for 迭代变量 in 可迭代对象：
           代码块
```

Example:

```vim
sum = 0
for num in range(11):
    sum = sum + num
print(sum)

>>>55
```

**1. Using `for` loop to input all elements:** 

Example:
```vim
chinese_zodiac = '猴鸡狗猪鼠牛虎兔龙蛇马羊'

# input all elements from the string using for loop
for x in chinese_zodiac:
    print(x)

>>>
猴
鸡
狗
猪
鼠
牛
虎
兔
龙
蛇
马
羊
```

**2. Using `for` loop to input all numbers from range(0,13), 13 will not be included** 

_使用for loop来input在(0,13)范围内的所有数字_

```vim
for i in range(13):
    print(i)

>>>
0
1
2
3
4
5
6
7
8
9
10
11
12
```

**3. Using `for` loop to input 使用for loop来INPUT 相对应的%字符串 - %s**

```vim
chinese_zodiac = '猴鸡狗猪鼠牛虎兔龙蛇马羊'
    
for year in range(2018,2021):
    print('The year of %s is %s' % (year, chinese_zodiac[year % 12]))

>>>The year of 2018 is 狗
>>>The year of 2019 is 猪
>>>The year of 2020 is 鼠
```

**4. Using `if` condition in `for` loop**

_For 循环语句中的if嵌套_

```vim
a = ('aaa', 'bbb', 'ccc', 'ddd','eee','fff')
b = ((1,12), (2,21),(3,23),(4,23),(5,23),(6,24),(7,28),(8,24),(9,15),(10,12),(11,25),(12,26))

int_month = int (input('please input the month: '))
int_day = int (input('please input the day: '))

for i in range(len(a)):
    if b[i] <= (int_month, int_day):
        print(a[i])
        break

>>>please input the month: 3
>>>please input the day: 22
>>>aaa
```

**Exercise: using `for` loop to calculate Chinese zodiac based on year**

_使用for loop来计算年份所对应的生肖_

```vim
zodiac_name = ('mojiezuo', 'shuipingzuo','baiyangzuo','jinniuzuo','shuagnyuzuo')
zodiac_days = ((1,20), (2,18),(3,21),(4,25),(12,21))

# user input month & day
# transform string into int

int_month = int(input('please input month: '))
int_day = int(input('please input day: '))
print(type(int_month))

for zd_num in range(len(zodiac_days)):

    # compare zd_num with input of month & day
    # figure out the index/position of the array
    if zodiac_days[zd_num] >= (int_month, int_day):
       # then pass the index num to get back the element of the array
        print(zodiac_name[zd_num])
        # if true then break
        break
        
    elif int_month == 12 and int_day > 21:
        print(zodiac_name[0])
        break
        
>>>please input month: 6
>>>please input day: 23
>>><class 'int'>
>>>shuagnyuzuo
```


**Loop 2: 条件与循环2：`while loop`**

`while` loop 是条件循环，在 `while` 循环中对于变量的计算方式更加灵活。因此 `while` 循环适合循环次数不确定的循环，而 `for` 循环的条件相对确定，适合固定次数的循环。

1 到 10 的求和也可以用 `while` 循环来写，这里 `while` 控制了循环的次数。


Basic syntax:

```vim
while True:
    print('a')
    break

>>>a
```

**1. Using `while` loop to input results 6 times, break when it's running in the 7th time**

_使用while loop来print a 六次，直到第七次break_

```vim
#first define a variable

num = 5
while True:
    print('a')
    num += 1

    # keep looping until num > 10, then break
    if num > 10:
        break

>>>
a
a
a
a
a
a  
```
**2. Using while loop to input 5, 4, 2, 1, skip 3 then break at 0**

_使用while loop来input 5, 4, 2, 1, 跳过3, 然后break at 0_

```vim
import time
num = 6
while True:
    num -= 1
    # keep looping until num == 0, then break
    if num == 3:
        continue
    elif num == 0:
        break
    print(num)
    time.sleep(1)

>>>
5
4
2
1
```

**3. Using `if` condition in `while` loop**

_while 循环语句中的if嵌套_

```vim
a = ('aaa', 'bbb', 'ccc', 'ddd','eee','fff')
b = ((1,12), (2,21),(3,23),(4,23),(5,23),(6,24),(7,28),(8,24),(9,15),(10,12),(11,25),(12,26))

int_month = int (input('please input the month: '))
int_day = int (input('please input the day: '))

**# initiate the variable 初始化**
n = 0

while b[n] < (int_month, int_day):
    if int_month == 12 and int_day >26:
        break
    n += 1
print (a[n])

>>>please input the month: 12
>>>please input the day: 27
>>>aaa

```


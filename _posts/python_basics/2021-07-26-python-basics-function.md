---
layout: post
title: "Python Basics 5: Function, Lambda"
subtitle: 'Definition of Function, Lambda'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Definition of Function

**Definition:**
函数 `function` 是对程序逻辑进行结构化的一种编程方法

函数代码块以 `def` 关键词开头，后接函数标识符名称和圆括号

在圆括号`()`里是传进来的参数 `parameter`，然后通过 `return` 进行函数结果得反馈。

**Syntax:**

```vim
def 函数名称（）：
      code block
      return 需要返回的内容

def add(num):
     return num + 1
```

**Call Function:
函数的调用**

```vim
函数名称（）

def add(score):
    return score + 1

print(add(99))
>>>100
```


When you define a `function` you give a name to a set of actions you want the computer to perform. 

When you call a `function` you are telling the computer to run (or execute) that set of actions.

```vim
// Call functions to draw a dotted line of two dashes.

dashSpace();
dashSpace();

function dashSpace(){ 
// Define a function to draw and dash and a space.
  penDown();
  moveForward();
  penUp();
  moveForward();
}
```

**Practice 1 : A + B**

**Input**

The input will consist of a series of pairs of integers a and b,separated by a space, one pair of integers per line.

**Output**

For each pair of input integers a and b you should output the sum of a and b in one line,and with one line of output for each line in input.

输入格式：有一系列的整数对 A 和 B，以空格分开。

输出格式：对于每个整数对 A 和 B，需要给出 A 和 B 的和。

Code:

```vim
while True:
    try:
        line = input()
        a = line.split()
        print(int(a[0]) + int(a[1]))

    except:
        break
>>>1 5
>>>6
>>>2 6
>>>8
>>>4 7
>>>11
>>>13

>>>1 4
>>>5
>>>a 3

Process finished with exit code 0
```

**Practice 2 : Sum up 1+3+5+7...+99**

Question: How to calculate 1+3+5+7+...+99？

求 1+3+5+7+…+99 的求和，用 Python 该如何写？

1-99奇数之和，range中需要设置等差序列的步长为2，否则求出的的是1-99所有整数之和。

```vim
# Solution 1
print(sum(range(1, 100, 2)))

# Solution 2
sum = 0
num = 1
for num in range(1, 100, 2):
    sum = sum + num
    num += 2

print(sum)

# Solution 3

sum = 0
for i in range(1,100,2):
    sum+=i
print(sum)

>>>2500
```

###  Parameter of Function

**参数需要相应的个数:**

```vim
# 定义这个函数
def func(a, b, c):
    print('a = %s' % a)
    print('b = %s' % b)
    print('c = %s' % c)

# 调用这个函数
func(1, 2, 3)

>>>a = 1
>>>b = 2
>>>c = 3
```

**设置参数的灵活性:**

```vim
# *other means other would be optional
def howlong(first, *other):
    # this is equivalent of:
    # print len(first) + len(other)
    print(1 + len(other))

howlong(123)
howlong(123, 22)
howlong(123, 22, 123123)

>>>1
>>>2
>>>3
```

**Scope 函数作用域**

Definition of Scope:

A scope is a textual region of a Python program where a namespace is directly accessible. "Directly accessible" here means that an unqualified reference to a name attempts to find the name in the namespace.

作用域就是一个 Python 程序可以直接访问命名空间的正文区域。

在一个 python 程序中，直接访问一个变量，会从内到外依次访问所有的作用域直到找到，否则会报未定义的错误。

Python 中，程序的变量并不是在哪个位置都可以访问的，访问权限决定于这个变量是在哪里赋值的。

变量的作用域决定了在哪一部分程序可以访问哪个特定的变量名称。Python 的作用域一共有4种，分别是：

**有四种作用域：**

- L（Local）：最内层，包含局部变量，比如一个函数/方法内部。
- E（Enclosing）：包含了非局部(non-local)也非全局(non-global)的变量。比如两个嵌套函数，一个函数（或类） A 里面又包含了一个函数 B ，那么对于 B 中的名称来说 A 中的作用域就为 nonlocal。
- G（Global）：当前脚本的最外层，比如当前模块的全局变量。
- B（Built-in）： 包含了内建的变量/关键字等，最后被搜索。

```vim
g_count = 0  # 全局作用域
def outer():
    o_count = 1  # 闭包函数外的函数中
    def inner():
        i_count = 2  # 局部作用域
```

**Scenario 1: 变量在函数外部**

```vim
var1 = 123

def func():
    print (var1)

func()

>>>123
```


**Scenario 2: 变量在函数内部;作用域就在于函数内部**

```vim
var1 = 123

def func():
    var1 = 456
    print (var1)

func()

>>>456
```

**Scenario 3: 离开函数外部;print作用域就在函数外面**

```vim
var1 = 123

def func():
    var1 = 456
    print (var1)

func()
print(var1)

>>>456
>>>123
```

**Scenario 4: global全局变量;放在函数内部;也对函数外部的输出产生影响**

```vim
var1 = 123

def func():
    global var1
    var1 = 456
    print (var1)

func()
print(var1)

>>>456
>>>456
```

### Iterator

迭代器

```vim
list1 = [1, 2, 3]
it = iter(list1)
print(next(it))
print(next(it))
print(next(it))

# exception
print(next(it))

>>>StopIteration
1
2
3
```

生成器yield

```vim
def frange(start, stop, step):
    x = start
    while x < stop:
        yield x
        x += step


for i in frange(10, 20, 0.5):
    print(i)

>>>
10
10.5
11.0
11.5
12.0
12.5
13.0
13.5
14.0
14.5
15.0
15.5
16.0
16.5
17.0
17.5
18.0
18.5
19.0
19.5
```

### Practice

**Practice: Use function to calculate the number of characters mentioned in the text**

_name.txt_

```vim
諸葛亮|關羽|劉備|曹操|孫權|關羽|張飛|呂布|周瑜|趙雲|龐統|司馬懿|黃忠|馬超
Lily | Lucy | Lily | Lucy | Tom | Sam | Sam | Matt | Alicia | Matt | Matt | Alicia
```

_sanguo.txt_
```vim
ansdnvkkasndkjnskanvkdjsnkvanksljdnkjcnkjnakdjsnjvnkdjnkajnsv
```

**Traditional code:**

```vim
# coding=utf-8
# Read names of the people using '|' to split up
f1 = open('name.txt')
data1 = f1.read()
print(data1.split('|'))

# Read names of the weapons using space line to split up
f2 = open('weapon.txt')
i = 1
for line in f2.readlines():
# 如果行数是奇数，即%2有余数 (偶数的话则为0)
# 那就print奇数那一行
    if i % 2 == 1:
        print(line.strip('\n'))

# 跳出如果语句 在行数上自动加1实现循环
    i += 1

# 读取大段文字里面的内容
f3 = open('sanguo.txt')
# 每行的行符替换成空格 这样可以成为原始格式的文字段落
print(f3.read().replace('\n', ''))

```


_Use `function`:_

```vim
import re
# coding=utf-8

# create a function 函数 called find_item
# count the frequency of 'hero' in data 'sanguo.txt'
# need to import re to count frequency

def find_item(hero):
    with open('sanguo.txt') as f:
        data = f.read().replace('\n', '')
        name_num = re.findall(hero, data)
        print('Hero %s appears %s times' % (hero, len(name_num)))
    # return this variable
    # name_num 是函数find_item执行之后得到的结果，把结果赋值给了name_num
    return name_num


# read info of the people
# 为变量第一次赋值的数据类型确定了该变量的初始类型。
name_dict = {}
with open('name.txt') as f:
    for line in f:
        names = line.split('|')
        for n in names:
            # name_num = find_item(n)
            #name_dict[n] = name_num
            name_dict[n] = find_item(n)

name_sorted = sorted(name_dict.items(), key=lambda item: item[1], reverse=True)
print(name_sorted[0:10])

>>>
Hero 諸葛亮 appears 157 times
Hero 關羽 appears 9 times
Hero 劉備 appears 297 times
Hero 曹操 appears 940 times
Hero 孫權 appears 321 times
Hero 關羽 appears 9 times
Hero 張飛 appears 364 times
Hero 呂布 appears 342 times
Hero 周瑜 appears 240 times
Hero 趙雲 appears 313 times
Hero 龐統 appears 82 times
Hero 司馬懿 appears 287 times
Hero 黃忠 appears 189 times
Hero 馬超 appears 219 times
[('\xe6\x9b\xb9\xe6\x93\x8d', 940), ('\xe5\xbc\xb5\xe9\xa3\x9b', 364), ('\xe5\x91\x82\xe5\xb8\x83', 342), ('\xe5\xad\xab\xe6\xac\x8a', 321), ('\xe8\xb6\x99\xe9\x9b\xb2', 313), ('\xe5\x8a\x89\xe5\x82\x99', 297), ('\xe5\x8f\xb8\xe9\xa6\xac\xe6\x87\xbf', 287), ('\xe5\x91\xa8\xe7\x91\x9c', 240), ('\xe9\xa6\xac\xe8\xb6\x85', 219), ('\xe9\xbb\x83\xe5\xbf\xa0', 189)]
```

### `Lambda` 表达式

**Definition of Lambda:**

A lambda function is a small anonymous function.

A lambda function can take any number of arguments, but can only have one expression.

**Syntax:**

```vim
lambda arguments : expression
```

**Example: Add 10 to argument a, and return the result:**

```vim
x = lambda a : a + 10
print(x(5))

x = lambda a, b : a * b
print(x(5, 6))

>>>15
>>>30
```

**Compared to normal function**

1.`lambda : True`

```vim
def true():
    return True
```

2.`lambda x,y: x + y`

```vim
def add(x,y):
    return x + y
```

3.`lambda x:x<= (month, day)`

```vim
def func1(x):
    return x<= (month, day)
```

4.`lambda item: item[1]`

```vim
def func2(item):
    return item[1]
```

### Built-in Function

**Mostly-used Function:**

`filter()`

```vim
# In the Python console: 
a=[1,2,3,4,5,6,7]
list(filter(lambda x:x>2, a))

>>>[3, 4, 5, 6, 7]
```


`map()`

```vim
a = [1,2,3]
map(lambda x:x, a)
>>>[1, 2, 3]

map(lambda x:x+1, a)
>>>[2, 3, 4]

list(map(lambda x:x+1, a))
>>>[2, 3, 4]

# Two list
# Every element will be added up one by one

a = [1,2,3]
b=[4,5,6]
list(map(lambda x,y:x+y, a,b))
>>>[5, 7, 9]

```

`reduce()`

```vim
reduce(lambda x,y: x+y, [2,3,4],1)
>>>10
```
It means:
1 = initial value

初始值代入lambda表达式后，第二个元素再代入表达式，以此类推

_((1+2)+3)+4_

`zip()`

```vim
for i in zip(1,2,3),(4,5,6):
    print(i)

>>>
(1,4)
(2,5)
(3,6)
```

Example: Swap the key & value in disctionary

```vim
dicta = {'a':'aa', 'b':'bb'}
dictb = zip(dicta.values(), dicta.keys())

print(dictb)
print(dict(dictb))

>>>[('aa', 'a'), ('bb', 'b')]
>>>{'aa': 'a', 'bb': 'b'}

```

### Closure 闭包

**Definition of Closure: 函数的嵌套**

闭包，就是一个封闭的包裹，里面包裹着自由变量，就像在类里面定义的属性值一样，自由变量的可见范围随同包裹，哪里可以访问到这个包裹，哪里就可以访问到这个自由变量。

**Example:**

```vim
def func():
    a = 1
    b = 2
    return a + b

def sum(a):
    def add(b):
        return a + b

    return add

num1 = func()
num2 = sum(2)
num2(4)

print(type(num1))
print(type(num2))
print(num2(4))

>>><type 'int'>
>>><type 'function'>
>>>6
```
Why one is integer, the other is function?

- num2 is a function
- num2(b) - pass in a b parameter


**使用闭包来实现call调用内部的function**

```vim
def counter():
    cnt = [0]
    def add_one():
        cnt[0] += 1
        return cnt[0]

    return add_one


num1 = counter()

print(num1())
print(num1())
print(num1())
print(num1())
print(num1())
print(num1())

>>>
1
2
3
4
5
6
```

num1() - 实际上call 调用add_one() 这个函数

**分开调用多个函数**

FIRST=0 - 没传入值的话，默认传入的值为0; 有传入值的话，就以传入的值开始

```vim
def counter(FIRST=0):
    cnt = [FIRST]
    def add_one():
        cnt[0] += 1
        return cnt[0]

    return add_one

# 每调用一次，自动加1
num5 = counter(5)
# num10是另一个函数
num10 = counter(10)

print(num5())
print(num5())
print(num5())
print(num10())
print(num10())

>>>
6
7
8
11
12
```

**Use of Closure**

从原先传递变量的方式, 到传递函数的方式。这样使用的参数更少, 代码更加优雅。

```vim
def a_line(a,b):
    def arg_y(x):
        return a*x+b
    return arg_y

line1 = a_line(3,5)
print(line1(10))

# 3*10+5 = 35

>>>35
```

```vim
def b_line(a,b):
    return lambda x:a*x+b

line2 = b_line(3,5)
print(line2(10))

# 3*10+5 = 35

>>>35
```

### Decorator 装饰器

Definition: To add some functions without adding extra code

想添加一些功能，但不想添加一些额外的代码

**Example: To calculate the running time of function**

**Traditional code:**

```vim
# coding=utf-8
import time

print(time.time())

# 统计函数运行的功能
# 在函数运行前 记录一个时间
# 在函数运行结束前 再记录一个时间
# 两个相减 得到函数的运行时间

def i_can_sleep():
    # 让函数运行3秒
    time.sleep(3)

start_time = time.time()
i_can_sleep()
stop_time = time.time()
print('this function run %s seconds' % (stop_time - start_time))

>>>1615043914.24
>>>this function run 3.00271201134 seconds

```

**Solution: Using `@Timer` decorator**

使用装饰器@timer: timer是装饰函数

i_can_sleep()是被装饰函数, 这样额外的功能就可以封存在这个装饰功能里面

就可以直接使用I_can_sleep(), 程序就会自动去找这个@timer装饰器

```vim
# coding=utf-8
import time

print(time.time())

def timer(func):
    def wrapper():
        start_time = time.time()
        func()
        stop_time = time.time()
        print('this function run %s seconds' % (stop_time - start_time))
    return wrapper

@timer
def i_can_sleep():
    # 让函数运行3秒
    time.sleep(3)


i_can_sleep()

>>>1615045399.61
>>>this function run 3.00200796127 seconds
```

#### Use of Decorator

1.对于带参数的函数，里面加入一个装饰器:

@tips

```vim
# define a function summing up two elements
def tips(func):
    def inside(a, b):
        print('start')
        func(a, b)
        print('stop')

    return inside


@tips
def add(a, b):
    print(a + b)

@tips
def sub(a, b):
    print(a - b)

print(add(4, 5))
print(sub(5, 4))

>>>
start
9
stop
None

start
1
stop
None
```

2.给装饰器添加参数, 可以把原先的函数封装到新的函数里面

@new_tips('add')

```vim
# define a function summing up two elements
def new_tips(argv):
    def tips(func):
        def inside(a, b):
            print('start %s' %argv)
            func(a, b)
            print('stop')

        return inside
    return tips


@new_tips('add')
def add(a, b):
    print(a + b)


@new_tips('sub')
def sub(a, b):
    print(a - b)


print(add(4, 5))
print(sub(5, 4))

>>>
start add
9
stop
None
start sub
1
stop
None
```

3.取出func add & func sub函数的名字, 然后取出变量__name__

这样不用对变量进行赋值，默认就会取出它对应的值

```vim
# define a function summing up two elements
def new_tips(argv):
    def tips(func):
        def inside(a, b):
            print('start %s %s' %(argv, func.__name__))
            func(a, b)
            print('stop')

        return inside
    return tips


@new_tips('add_module')
def add(a, b):
    print(a + b)


@new_tips('sub_module')
def sub(a, b):
    print(a - b)


print(add(4, 5))
print(sub(5, 4))

>>>
start add_module add
9
stop
None
start sub_module sub
1
stop
None
```


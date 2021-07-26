---
layout: post
title: "Python Basics 5: Function"
subtitle: 'Definition of Function'
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


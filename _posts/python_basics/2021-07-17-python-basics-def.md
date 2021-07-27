---
layout: post
title: "Python Basics 1: Class, Object, Variables, Modules, Packages"
subtitle: 'Definition of Class, Object, etc'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Class & Instance

在专业术语上,我们将类别称做类型(`class`),而个体叫做实例(`instance`)。

存活的实例对象都有个 “唯一” 的 ID 值。

可用 type 返回实例所属类型。

如要判断实例是否属于特定类型,须用 isinstance 函数。

```vim
issubclass(Liger, object)
```

事实上,所有类型都有一个共同祖先类型 object,它为所有类型提供原始模版,以及系统 所需的基本操作方式。

区别在于,所有类型对 象都是 type 的实例,这与继承关系无关。

```vim
>>> issubclass(Liger, object)
True

>>> id(int)
4486772160

>>> type(int)
<class 'type'>
```
### Names have no type, but objects do.

在 Python 这类动态语言里,**Name**和**Object**是两个实体。

名字不但有自己的类型,要分配内存,还会介入实际执行过程。甚至可以说,名字才是其动态执行模型的基础。

**名字必须与目标对象关联起来才有意义。**

**赋值操作步骤：**
*   准备好右值目标对象(比如上例中的整数对象 100)。
*   准备好名字(通常是常量,保存在特定列表里。比如 x)。
*   在名字空间(namespace)里为两者建立关联。

_赋值操作仅仅是让名字在名字空间NameSpaces里重新关联,而非修改原对象。
但是一个名字只能引用一个对象。_

An object is allowed to have multiple names,无论是在相同或不同的名字空间里。
```vim
>>> x = 1234

>>> y = x

>>> x is y 
True
```

相等操作符=并不能确定两个名字指向同一对象

这涉及到操作符重载,或许它被设定为比较值是否相等。

```vim
>>> a = 1234
>>> b = 1234

>>> a is b # 指向 同对象。 
False

>>>a==b # 值相等。 
True
```
### Variable 变量

变量多次赋值:

```vim
# 123赋值给a
a = 123
b = a
```

### 模块（`Module`）、包（`Package`）、库（`Library`）、应用（`Application`）、框架（`Framework`）

模块是在代码量变得相当大之后，为了将需要重复使用的有组织的代码段放在一起，这部分代码可以附加到现有的程序中，附加的过程叫做导入import。

「函数」和「类」组成了「模块」，多个「模块」组成了「包」，多个「包」或者多个「模块」组成了「应用程序」，「应用程序」具有某些特定功能且作为依赖提供给其他项目使用叫作「库」，提供某一领域解决方案的「库」叫框架。

**引用模块 / 包：`import`**

import 的本质是路径搜索。使用`import module_name` 语句导入。

import 引用可以是模块` module`，或者包 `package`。

模块 `module` 和包 `package `是个体和集合的关系: 模块是一个个体，里面包含了函数 `function`。

包 `package` 就是多个模块 `module` 的集合` collection`。

**如何引入？**

针对 module，实际上是引用一个.py 文件。

而针对 package，可以采用 from … import …的方式，这里实际上是从一个目录中引用模块，这时目录结构中必须带有一个 __init__.py 文件。


```vim
# 导入一个模块
import model_name
# 导入多个模块
import module_name1,module_name2
# 导入包中指定模块 
from package_name import moudule_name
# 导入包中所有模块 
from package_name import *

```

### Input and Output 

`raw_input` 是 `Python2.7` 的输入函数，在 `Python3.x `里可以直接使用` input`赋值给变量 name

`print `是输出函数，`%name `代表变量的数值，因为是字符串 `string `类型，所以在前面用的 `%s `作为代替。

如果变量数值是字符串` string` 类型，则用 `%s `代替

如果变量数值是 `integer` 类型，则用` %d `代替

```vim

name = raw_input("What's your name?")
sum = 100+100
print ('hello,%s' %name)
print ('sum = %d' %sum)

_what's your name? _alicia_
hello, alicia
sum = 200_
```

### Comment

注释 `comment` 在 python 中使用 `#`

如果注释中有中文，一般会在代码前添加 ` - coding: utf-8 -`

如果是多行注释，使用三个单引号，或者三个双引号

```vim

# -*- coding: utf-8 -*

'''
这是多行注释，用三个单引号
这是多行注释，用三个单引号 
这是多行注释，用三个单引号
'''"

```









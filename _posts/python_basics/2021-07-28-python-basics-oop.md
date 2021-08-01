---
layout: post
title: "Python Basics 6: Class & Object-oriented Programming(OOP)"
subtitle: 'Definition of OOP, Class and Instance'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Class and Instance

**Class(类):** A Class is like an object constructor.

A user-defined prototype for an object that defines a set of attributes that characterize any object of the class. The attributes are data members (class variables and instance variables) and methods, accessed via dot notation.

用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。

**Object(对象):** A unique instance of a data structure that's defined by its class. An object comprises both data members (class variables and instance variables) and methods.

- Class variables & Instance variables
- Methods

**Instance(实例):** An individual object of a certain class. An object obj that belongs to a class Circle, for example, is an instance of the class Circle.

**Example:**

面向对象编程: 把相同属性的对象归类

self means 把类实例化后的实例本身

```vim
class Player():  #define a class
    def __init__(self, name, hp):
        self.name = name
        self.hp = hp
    def print_role(self):   #define a method
        print('%s: %s' % (self.name, self.hp))

user1 = Player('tom', 100)  #类的实例化
user2 = Player('jerry', 90)

# call methods from the parent class
user1.print_role()
user2.print_role()

>>>
tom: 100
jerry: 90
```

### Adding attributes/methods to class

**1.Adding class attributes**

增加类的属性

```vim
class Player():
    def __init__(self, name, hp, occu):
        self.name = name  #变量被称作属性
        self.hp = hp
        self.occu = occu
    def print_role(self):
        # output
        print('%s: %s %s' % (self.name, self.hp, self.occu))

class Monster():
    #定义monster class
    pass

#增加更多参数，传递到这个player类中，然后给user1增加属性
user1 = Player('tom', 100, 'war')
user2 = Player('jerry', 90, 'master')
user1.print_role()
user2.print_role()

>>>tom: 100 war
>>>jerry: 90 master
```

**2.Adding class methods**

增加类的方法

```vim
# coding=utf-8

class Player():
    def __init__(self, name, hp, occu):
        self.name = name  #变量被称作属性
        self.hp = hp
        self.occu = occu
    def print_role(self):
        # output
        print('%s: %s %s' % (self.name, self.hp, self.occu))

    # add a new method
    def updatedName(self, newname):
        self.name = newname

class Monster():
    #定义monster class
    pass

#增加更多参数，传递到这个player类中，然后给user1增加属性
user1 = Player('tom', 100, 'war')
user2 = Player('jerry', 90, 'master')
user1.print_role()
user2.print_role()

user1.updatedName('wilson')
user1.print_role()

>>>wilson: 100 war
```

**3.Make sure variables wont be changed**

确保变量不会被实例访问并修改。

这样如果想修改某一个属性，只能通过方法来改变属性，而不能通过赋值来改变。

`self.__name = name`

```vim
class Player():
    def __init__(self, name, hp, occu):
        self.__name = name  #变量被称作属性
        self.hp = hp
        self.occu = occu
    def print_role(self):
        # output
        print('%s: %s %s' % (self.__name, self.hp, self.occu))

    # add a new method
    def updatedName(self, newname):
        self.__name = newname

class Monster():
    #定义monster class
    pass

user1 = Player('tom', 100, 'war')
user1.updatedName('wilson')
user1.print_role()
user1.__name = ('Lily')
user1.print_role()

>>>
tom: 100 war
jerry: 90 master
wilson: 100 war
wilson: 100 war
```

### Class Inheritance 类的继承

普通方法是 `parent_class.__init__(self)`

super方法是 `super(child_class, self).__init__()`

Animal is parent_class of Cat class
Cat is child_class of Animal class

猫继承了猫科动物所使用的方法, 因此猫科动物就是猫的父类, 猫就是猫科动物的子类。

```vim
class Monster():
    # 定义monster class
    # 初始属性
    # hp=100 is initial attribute
    def __init__(self, hp=100):
        self.hp = hp

    def run(self):
        print('move to this position')


# let subclass Animal to inherite class Monster
class Animal(Monster):
    # 在子类中定义属性
    def __init__(self, hp=10):
        self.hp = hp

a1 = Monster(200)
print(a1.hp)
print(a1.run())
a2 = Animal(1)
print(a2.hp)
print(a2.run())

>>>
200
move to this position
None
1
move to this position
None
```

#### Super 

super的作用：减少资源的浪费
- 在父类中已经使用的方法 在子类中不必重复输入
- self首先调用自身的方法，如果没有再去父类中找，super是直接从父类中找方法，那你的程序需要后者就需要super()函数了
- 把父类的__init__()在子类 执行一遍，如果父类有__init__()且需要在子类使用，需要增加super这个方法

在子类中hp属性不用重复初始化了:
- 普通方法是 父类.__init__(self)
- super方法是 super(子类, self).__init__()

```vim
class Animal(Monster):
    # 在子类中定义属性
    def __init__(self, hp=10):
        super().__init__(hp)
```

### 多态

如果子类和父类重名，子类会覆盖父类的方法，这个方法在运行过程中有多种状态，称之为多态。

```vim
class Monster():
    # 定义monster class
    # 初始属性
    # hp=100 is initial attribute
    def __init__(self, hp=100):
        self.hp = hp

    def run(self):
        print('move to this position')

    def whoami(self):
        print('I am the parent class Monster')

class Boss(Monster):
    def __init__(self, hp=10000):
        self.hp = hp
    def whoami(self):
        print('I am the monster hahaha')

a3 = Boss(800)
print(a3.hp)
print(a3.whoami())

>>>
800
I am the monster hahaha
None
```

#### Test which is parent class or child class

**1.type**

```vim
print('the type of a1 is %s' % type(a1))
print('the type of a2 is %s' % type(a2))
print('the type of a3 is %s' % type(a3))

>>>
the type of a1 is <type 'instance'>
the type of a2 is <type 'instance'>
the type of a3 is <type 'instance'>

```

**2.isinstance()**

```vim
print(isinstance(a2, Monster))

>>>
TRUE
```

### Customised With

```vim
class Testwith():
    def __enter__(self):
        print 'run'

    def __exit__(self, exc_type, exc_val, exc_tb):
        if exc_tb is None:
            print('ended smoothly')
        else:
            print('has error %s' % exc_tb)


with Testwith():
    print('Test is running')
    raise NameError('testNameError')
    
>>>run
>>>Test is running
>>>has error <traceback object at 0x10faea3f8>
Traceback (most recent call last):
  File ""/Users/limengran/Library/Mobile Documents/com~apple~CloudDocs/PychamProject/with.py"", line 14, in <module>
    raise NameError('testNameError')
NameError: testNameError
```










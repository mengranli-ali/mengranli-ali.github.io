---
layout: post
title: "Python Basics 9: File and Directory Access"
subtitle: 'How to access file or folder in terminal, etc'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis 
---

### File and Directory Access

**使用命令行对文件和文件夹操作**

open Terminal:

1.Check directory 查看当前目录所有文件

`ls`


2.Check which one is file, which one is folder 查看哪些是文件 哪些是文件夹

`ls -l`

If the first letter starts with `-`, it means it's a file, i.e.`-rw-r--r--`

输出如果第一个字符是-开头 表明是文件

If the first letter starts with `d`, it means it's a folder, i.e.`drwxr-xr-x`

输出如果第一个字符是d 表明是文件夹

3.Check current position 查看当前所在位置

`pwd`

4.Access the folder you want to check

`cd foldername/filename`

5.Access the absolute path of current folder 访问当前文件夹的绝对路径根目录并查看

`cd /tmp`

`pwd`

6.Access relative path 访问相对路径

访问到上一级目录:

`cd ..`

`pwd`

```vim
mengrans-MBP:tmp mengran$ cd ..
mengrans-MBP:/ mengran$ pwd
/
mengrans-MBP:/ mengran$ "
```

访问到下一级目录:

`cd ./tmp`

```vim
mengrans-MBP:/ mengran$ cd ./tmp
mengrans-MBP:tmp mengran$ 
```

7.Create a new folder called g 建立新文件夹 

进入新建的g文件夹

`mkdir -p ` 加入后不会出现无文件夹问题

```vim
mengrans-MBP:/ mengran$ mkdir -p /tmp/a/b/c/d/e/f/g
mengrans-MBP:/ mengran$ cd /tmp/a/b/c/d/e/f/g
mengrans-MBP:g mengran$ 
```

8.Access the previous directory of this new folder g

```vim
mengrans-MBP:g mengran$ cd ..
mengrans-MBP:f mengran$ pwd
/tmp/a/b/c/d/e/f
limengrans-MBP:f mengran$ 
```

9.Delete file 删除一个文件夹 

`rmdir`

删除一个文件夹a以及之后所有的文件夹:

`rm -rf/tmp/a`
`ls /tmp`

```vim
mengrans-MBP:f mengran$ rmdir g
mengrans-MBP:f mengran$ pwd
/tmp/a/b/c/d/e/f
mengrans-MBP:f mengran$ rmdir /tmp/a
rmdir: /tmp/a: Directory not empty
mengrans-MBP:f mengran$ rm -rf /tmp/a
mengrans-MBP:f mengran$ pwd
/tmp/a/b/c/d/e/f
mengrans-MBP:f mengran$ ls /tmp
com.sogou.inputmethod       com.google.Keystone
mengrans-MBP:f mengran$ 
```

### `os` library


#### Common pathname manipulations - `os.path` 

1.`os.path.abspath('.')`

根据当前的相对路径的点来获取当前的绝对路径

```vim
import os
from os import path

a = os.path.abspath('.')
print(a)

>>>
/Users/mengran/Library/Mobile Documents/com~apple~CloudDocs/PychamProject

Process finished with exit code 0"
```

2.`os.path.abspath('..')`

根据当前的相对路径的点点来获取当前的上一级目录的绝对路径

```vim
import os
from os import path

a = os.path.abspath('..')
print(a)

>>>
/Users/limengran/Library/Mobile Documents/com~apple~CloudDocs

Process finished with exit code 0
```


3.`os.path.exists()`

查看文件是否存在

4.`os.path.isfile()`

查看文件是否是folder

5.`os.path.isdir()`

查看文件是否是目录

```vim
import os
from os import path

a = os.path.abspath('..')
b = os.path.exists('/Users')
print(b)

c = os.path.isfile('/Users')
d = os.path.isdir('/Users')
print(c)
print(d)

>>>
True
False
True
```

6.`os.path.joint()`

将两个文件合并

```vim
e = os.path.join('/tmp/a/', 'b/c')
print (e)

>>>
/tmp/a/b/c
```

#### Alternative: `pathlib`

1.`from pathlib import Path`

获取相对路径的点的绝对路径

```vim
from pathlib import Path

p = Path('.')
print(p.resolve())

>>>
/Users/limengran/Library/Mobile Documents/com~apple~CloudDocs/PychamProject
```

2.`p.is_dir()`

判断当前文件夹是否是目录

3.Create a new directory a containing a folder b which include file c

新建一个目录a 包括b b中包括c

parents - 如果上一个目录不存在，系统会为你自动创建

```vim
q = Path('/tmp/a/b/c')
Path.mkdir(q, parents=True)

>>>
limengrans-MBP:~ limengran$ ls /tmp/a
b
limengrans-MBP:~ limengran$ ls /tmp/a/b
c
```


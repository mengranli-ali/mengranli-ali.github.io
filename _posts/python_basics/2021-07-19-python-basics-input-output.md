---
layout: post
title: "Python Basics 3: File Handling - Input & Output"
subtitle: 'How to input & output files with Python'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Files Input & Output

**Files Built-in Functions:**

- `open()` - 打开文件 open a file
- `read()` - 输入 read/input a file
- `readline()` - 输入一行 read/input a line
- `seek() `-文件内移动 look for 
- `write()` -输出 output 
- `close()` -关闭文件 close a file
- `mode=w` - 要写入  mode as write
- `mode=r` -要读取  mode as read

**`open()` function**

The `open()` function takes two parameters; filename, and mode.

There are four different methods (modes) for opening a file:

- `"r"` - Read - Default value. Opens a file for reading, error if the file does not exist
- `"a"` - Append - Opens a file for appending, won't overwrite any existing content, creates the file if it does not exist
- `"w"` - Write - Opens a file for writing, overwrites any existing content, creates the file if it does not exist
- `"x"` - Create - Creates the specified file, returns an error if the file exists
- `"t"` - Text - Default value. Text mode
- `"b"` - Binary - Binary mode (e.g. images)

**Scenario 1: Create and open a file, write in and close**

```vim
# open a file and write
# the name.txt will be created
# open() -> write() -> close()

file1 = open('name.txt', 'w')

# write the info in the file
file1.write('Lily')
file1.close()
```

**Scenario 2: Open the existing file and input the content**

```vim
# open the file and read 
# 注意这里没有mode'w' or 'r' or 'a'

file2 = open('name.txt')
print(file2.read())
file2.close()

>>>Lily
```

Scenario 3: Add new content in the existing file, but the rest content remains the same

```vim
# Add another character in the file
# mode 'a'

file3 = open('name.txt', 'a')
file3.write('Luzy')
file3.close()

>>>LilyLucy
```


### File Operations
More specific scenarios of file handling:

**Scenario 4: Read the first line**

```vim
file4 = open('name.txt')
print(file4.readline())

>>>Lily
```

**Scenario 5: Read multiple lines**

```vim
file5 = open('name.txt')
for line in file5.readlines():
    print(line)
    print('=======')
    
>>>Lily
>>>=======
>>>Lucy
>>>=======
```

**Scenario 6: Look for where the file pointer is at **

```vim
file6 = open('name.txt')
# check where the file pointer is at
print(file6.tell())

# move the file pointer to line 2
file.read(1)
print(file6.tell())

# move the file pointer to original line 1
file6.seek(0)
print(file6.tell())

>>>0
>>>1
>>>0
```

**多个参数偏移**

第一个参数代表偏移位置

第二个参数代表：
- 0 - 表示从文件开头偏移
- 1 - 表示从当前位置偏移
- 2 - 表示从文件结尾

```vim
file6.seek(5,0)
```






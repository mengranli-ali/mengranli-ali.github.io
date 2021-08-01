---
layout: post
title: "Python Basics 8: Python Library & Regular Expression"
subtitle: 'Use of Python Library & Regular Expression'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Python Library

**library References**

The **[python standard library]** (https://docs.python.org/3/library/)

### Regular Expression 正则表达式库re

**1.匹配固定字符**

```vim
import re

# match a fixed string
# p to match with
p = re.compile('a')
# to be matched with
ok = p.match('a')
print(ok)

>>>
<_sre.SRE_Match object at 0x10ab71ed0>
```

**2.匹配特殊字符***

```vim
import re

# match a fixed string
# p to match with
p = re.compile('ca*t')
# to be matched with
ok = p.match('caaaaaat')
print(ok)

>>>
<_sre.SRE_Match object at 0x103212100>

```

**3.正则表达式的元字符**

全部符合： `.`

```vim
import re

# .
p = re.compile('.')
ok = p.match('caaaaaat')
print(ok)

>>>
<_sre.SRE_Match object at 0x106ffce68>
```

匹配三个字符： `...`

```vim
import re

# ...
p = re.compile('...')
ok = p.match('cccc')
print(ok)

>>>
<_sre.SRE_Match object at 0x1041f4e68>
```

以xxx开头： `^`

```vim
# ...
p = re.compile('^c')
ok = p.match('bccc')
print(ok)

# ...
p = re.compile('^b')
ok = p.match('bccc')
print(ok)

>>>
None

<_sre.SRE_Match object at 0x10494fe68>
```

以xxx结尾 从后边向前边匹配： `$`

```vim
import re

# ...
p = re.compile('jpg$')
ok = p.match('')
print(ok)

>>>

```

`x* `表示*前面的这个字符出现了0次或多次

```vim
import re

# ...
p = re.compile('ca*t')
ok = p.match('caaaat')
print(ok)

import re

# ...
p = re.compile('ca*t')
ok = p.match('ct')
print(ok)

>>>
<_sre.SRE_Match object at 0x10ea99100>

<_sre.SRE_Match object at 0x10caca100>
```

`x+ `表示+前面的这个字符出现了1次或多次

```vim
import re

# ...
p = re.compile('ca+t')
ok = p.match('cat')
print(ok)

import re

# ...
p = re.compile('ca+t')
ok = p.match('ct')
print(ok)

>>>
<_sre.SRE_Match object at 0x105204100>

None
```

`x?` 表示+前面的这个字符出现了0次或1次

```vim
p = re.compile('ca?t')
ok = p.match('ct')        # Appears 0 times

p = re.compile('ca?t')
ok = p.match('caat')    # Appears 2 times

>>>
<_sre.SRE_Match object at 0x101891100>

None
```

`{x}` 前面的字符出现x次

```vim
import re

# ...
p = re.compile('ca{4}t')
ok = p.match('caaat')
print(ok)

p = re.compile('ca{4}t')
ok = p.match('caaaat')

>>>
None

<_sre.SRE_Match object at 0x1031d4100>
```

`{x, y}` 前面的字符出现x到y次

```vim
import re

# ...
p = re.compile('ca{4,6}t')
ok = p.match('caaaaaat')
print(ok)

>>>
<_sre.SRE_Match object at 0x10d322100>
```

`c.t`
- cat
- cbt
- cct

匹配开头和结尾相同的组合，中间字符不同

```vim
import re

# ...
p = re.compile('c.t')
ok = p.match('cbt')
print(ok)

>>>
<_sre.SRE_Match object at 0x10370de68>
```

`c[bcd]t`
- cbt
- cct
- cdt

```vim
import re

# ...
p = re.compile('c[bcd]t')
ok = p.match('cct')
print(ok)

>>>
<_sre.SRE_Match object at 0x10b8ffe68>
```

### Other symbols

\s 匹配任意空白符

\d 匹配单个数字

\d+ 匹配多个连续数字

\d{5} 匹配指定个数(5个)的数字

\D 匹配不包含的数字

() 小括号
- 2018-03-04提取年月份, 就要分组group
- (2018) - (03) - (04)

^$ 匹配空行

.*? 匹配不适用贪婪模式:加上问号, 只会匹配到第一个image
```vim
<img   /img>
<img   /img>
```

贪婪模式： abc* (_不加问号, 就会匹配所有的image_)

_abcccccd_



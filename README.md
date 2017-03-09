# PEP 8 - Python 代码风格指南
## Contents

* [Introduction - 简介](#1)
* [A Foolish Consistency is the Hobgoblin of Little Minds - 愚蠢的一致性是小心灵的大地精](#2)
* [Code lay-out - 代码布局](#3)
 * [Indentation - 缩进](#3.1)
 * [Tabs or Spaces? - A罩杯还是C罩杯?](#3.2)
 * [Maximum Line Length - 代码行最大长度](#3.3)
 * [Should a line break before or after a binary operator? - 在二元运算符之前还是之后断行?](#3.4)
 * [Blank Lines - 空行](#3.5)
 * [Source File Encoding - 源文件编码](#3.6)
 * [Imports - 导入](#3.7)
 * [Module level dunder names - 模块级 dunder(文中解释) 名称](#3.8)
* [String Quotes - 字符串引号](#4)
* [Whitespace in Expressions and Statements - 表达式和语句中的空格](#5)
 * [Pet Peeves - 心理藏的小烦恼](#5.1)
 * [Other Recommendations - 其他建议](#5.2)
* [When to use trailing commas - 何时使用逗号结尾](#6)
* [Comments - 注释](#7)
 * [Block Comments - 块注释](#7.1)
 * [Inline Comments - 行注释](#7.2)
 * [Documentation Strings - 文档字符串](#7.3)
* [Naming Conventions - 命名约定](#8)
 * [Overriding Principle - 圣经戒律](#8.1)
 * [Descriptive: Naming Styles - 描述的: 命名样式](#8.2)
 * [Prescriptive: Naming Conventions - 规定的: 命名规定](#8.3)
  * [Names to Avoid - 避免的命名](#8.3.1)
  * [Package and Module Names - 包和模块名](#8.3.2)
  * [Class Names - 类名](#8.3.3)
  * [Type variable names - 类型变量名](#8.3.4)
  * [Exception Names - 异常名](#8.3.5)
  * [Global Variable Names - 全局变量名](#8.3.6)
  * [Function Names - 函数名](#8.3.7)
  * [Function and method arguments - 函数和方法参数](#8.3.8)
  * [Method Names and Instance Variables - 方法名和实例变量](#8.3.9)
  * [Constants - 常量](#8.3.10)
  * [Designing for inheritance - 继承的设计](#8.3.11)
  * [Public and internal interfaces - 公共和内部接口](#8.4)
* [Programming Recommendations - 编码建议](#9)
 * [Function Annotations - 函数注释](#9.1)
* [References - 参考文献](#10)
* [Copyright - 版权](#11)

<h4 id="1">简介</h4>
许多工程项目都有自己独有的编码风格指南。如果发生任何规则冲突，当然是与项目级别的代码风格保持一致。美其名曰：入乡随俗，Do what Romans do in Rome，到了罗马就跟着吃马肉，生在唐朝就吃胖点。
<h4 id="2">愚蠢的一致性是小心灵的大地精</h4>
代码风格一致性当然重要，毕竟读起来跟做spa一样爽，但有时也要有自己的判断，不要跟个傻X一样，明明是个90后，非得穿丝袜。  
例如以下场景：  
1、遵循此风格让你的那一小片代码看起来格格不入，清高的不行。  
2、遵循此风格后和其他 python 版本不兼容，甚至出现错误。
<h4 id="3">代码布局</h4>
<h5 id="3.1">缩进</h5>
一个缩进级别四个空格。  
* 连续行使用两种方式使封装元素成为一行：括号内垂直隐式连接和悬挂式缩进，使用悬挂式缩进应该注意第一行不应该有参数，连续行要使用进一步的缩进来区分。
```Python
# Aligned with opening delimiter.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# More indentation included to distinguish this from the rest.
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# Hanging indents should add a level.
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
```
* 当 if 语句过长需要换行时，以下处理方法可以采用。
```Python
# No extra indentation.
if (this_is_one_thing and
    that_is_another_thing):
    do_something()

# Add a comment, which will provide some distinction in editors
# supporting syntax highlighting.
if (this_is_one_thing and
    that_is_another_thing):
    # Since both conditions are true, we can frobnicate.
    do_something()

# Add some extra indentation on the conditional continuation line.
if (this_is_one_thing
        and that_is_another_thing):
    do_something()
```
* 当闭环括号内元素跨行时，可以采用以下方式。
```Python
my_list = [
    1, 2, 3,
    4, 5, 6,
    ]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
    )
```
<h5 id="3.2">A罩杯还是C罩杯?</h5>
除非项目中已经约定了使用 tab 作为缩进，最好使用 space。  
Python 3 不允许 tab 和 space 混用，同时混用了 tab 和 space 的 Python 2 代码应该被转换为仅使用 space。  
<h5 id="3.3">代码行最大长度</h5>
将所有行限制为最多79个字符。  
对于具有较少结构限制（文档字符串或注释）的长文本块，行长度应限制为72个字符。  
当然了，不要问为啥非得是 79,72。我们要兼顾非洲大陆人民的生活。代码是全世界的。  
反斜杠有时可能仍然要用。 例如，又多又长的 with - 语句不能使用隐式连接，这时反斜杠是可以接受的：
```Python
with open('/path/to/some/file/you/want/to/read') as file_1, \
     open('/path/to/some/file/being/written', 'w') as file_2:
    file_2.write(file_1.read())
```
assert 语句也是如此。
<h5 id="3.4">在二元运算符之前还是之后断行?</h5>
算法和程序设计技术先驱，计算机排版系统 TEX 和 METAFONT 的发明者 Donald Knuth，推荐使用以下形式：  
```Python
# Yes: easy to match operators with operands
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
```  
只要保持本地一致性，在二元运算符之前和之后断开都是允许的，但是新的 Python 代码推荐使用 Knuth 形式。  
<h5 id="3.5">空行</h5>
顶层函数和类定义使用两个空行。  
类内方法定义使用一个空行。  
不同函数组之间使用额外的空行隔离。  
总之，空行的作用就是隔离不同函数类等，层次分明。  
<h5 id="3.6">源文件编码</h5>
Python 2 默认ASCII，Python 3 默认UTF-8。  
使用 ASCII 的 Python 2 源文件或使用 UTF-8 的 Python 3 源文件不应该有编码声明。  
源文件最好只使用 ASCII 字符，即使是蹩脚的 Chinglish 亦可，家和万事兴。  

<h5 id="3.7">模块导入</h5>
```Python
YES: from subprocess import Popen, PIPE
     import os
     import sys

NO:  import sys, os
```
模块导入总是位于文件顶部，在模块注释和文档字符串之后，模块全局变量和常量之前。  
导入应该按照以下顺序分组，不同组间用空行隔离。  
* 标准库 imports  
* 相关第三方 imports  
* 本地特定应用／库 imports  
推荐使用绝对导入，标准库代码应总是使用绝对导入。  
```Python
import mypkg.sibling
from mypkg import sibling
from mypkg.sibling import example
```
在包结构比较复杂时，可以使用相对导入。  
```Python
from . import sibling
from .sibling import example
```
在 Python 3 中，相对导入已经被删除，禁止使用。  
类导入：
```Python
from myclass import MyClass
from foo.bar.yourclass import YourClass
```
如果这种方式导致了本地命名冲突，可以使用以下方式：
```Python
import myclass
import foo.bar.yourclass
```
然后使用 myclass.MyClass 和 foo.bar.yourclass.YourClass。  
请不要使用以下方式：
```Python
from <module> import *
```
<h5 id="3.8">模块级别 dunder 名称</h5>
模块级别 “dunders”（即具有两个前导和两个后缀下划线的名称），例如 \_\_all\_\_，\_\_author\_\_，\_\_version\_\_ 等应放在模块 docstring 之后，但在任何 import 语句之前，但是除了 \_\_future\_\_ 导入。 Python 强制 future-imports 必须在除了 docstrings 之外的任何其他代码之前出现在模块中。  
例如：
```Python
"""This is the example module.

This module does stuff.
"""

from __future__ import barry_as_FLUFL

__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'

import os
import sys
```
<h5 id="4">字符串引号</h5>
在 Python 中，单引号和双引号是等价的，只需要坚持使用一种并保持一致即可。  
在双引号中使用单引号，单引号中使用双引号。三引号中使用双引号。

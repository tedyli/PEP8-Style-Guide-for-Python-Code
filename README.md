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
    * [Imports - 模块导入](#3.7)
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
    * [Descriptive: Naming Styles - 描述性: 命名风格](#8.2)
    * [Prescriptive: Naming Conventions - 规定性: 命名习惯](#8.3)
        * [Names to Avoid - 避免的命名](#8.3.1)
        * [Package and Module Names - 包和模块命名](#8.3.2)
        * [Class Names - 类名](#8.3.3)
        * [Type variable names - 类型变量名](#8.3.4)
        * [Exception Names - 异常名](#8.3.5)
        * [Global Variable Names - 全局变量名](#8.3.6)
        * [Function Names - 函数名](#8.3.7)
        * [Function and method arguments - 函数和方法参数](#8.3.8)
        * [Method Names and Instance Variables - 方法名和实例变量](#8.3.9)
        * [Constants - 常量](#8.3.10)
        * [Designing for inheritance - 继承设计](#8.3.11)
        * [Public and internal interfaces - 公共和内部接口](#8.3.12)
* [Programming Recommendations - 编码建议](#9)
     * [Function Annotations - 函数注释](#9.1)

<h2 id="1">简介</h2>

许多工程项目都有自己独有的编码风格指南。如果发生任何规则冲突，当然是与项目级别的代码风格保持一致。美其名曰：入乡随俗，Do what Romans do in Rome，到了罗马就跟着吃马肉。

<h2 id="2">愚蠢的一致性是小心灵的大地精</h2>

代码风格一致性当然重要，毕竟读起来跟大保健一样爽，但有时也要有自己的判断。

例如以下场景：

1、遵循此风格让你的那一小片代码看起来格格不入，清高的不行。

2、遵循此风格后和其他 python 版本不兼容，甚至出现错误。

<h2 id="3">代码布局</h2>

<h3 id="3.1">缩进</h3>

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

<h3 id="3.2">A罩杯还是C罩杯?</h3>

除非项目中已经约定了使用 tab 作为缩进，最好使用 space。

Python 3 不允许 tab 和 space 混用，同时混用了 tab 和 space 的 Python 2 代码应该被转换为仅使用 space。  

<h3 id="3.3">代码行最大长度</h3>

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

<h3 id="3.4">在二元运算符之前还是之后断行?</h3>

算法和程序设计技术先驱，计算机排版系统 TEX 和 METAFONT 的发明者 Donald Knuth，推荐使用以下形式：

```Python
# 是： easy to match operators with operands
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
```  

只要保持本地一致性，在二元运算符之前和之后断开都是允许的，但是新的 Python 代码推荐使用 Knuth 形式。  

<h3 id="3.5">空行</h3>

顶层函数和类定义使用两个空行。

类内方法定义使用一个空行。

不同函数组之间使用额外的空行隔离。

总之，空行的作用就是隔离不同函数类等，层次分明。

<h3 id="3.6">源文件编码</h3>

Python 2 默认ASCII，Python 3 默认UTF-8。

使用 ASCII 的 Python 2 源文件或使用 UTF-8 的 Python 3 源文件不应该有编码声明。

源文件最好只使用 ASCII 字符，即使是蹩脚的 Chinglish 亦可，家和万事兴。

<h3 id="3.7">模块导入</h3>

```Python
是：
    from subprocess import Popen, PIPE
    import os
    import sys

否：
    import sys, os
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

<h3 id="3.8">模块级别 dunder 名称</h3>

模块级别 “dunders”(即具有两个前导和两个后缀下划线的名称)，例如 \_\_all\_\_，\_\_author\_\_，\_\_version\_\_ 等应放在模块 docstring 之后，但在任何 import 语句之前，但是除了 \_\_future\_\_ 导入。 Python 强制 future-imports 必须在除了 docstrings 之外的任何其他代码之前出现在模块中。  
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

<h2 id="4">字符串引号</h2>

在 Python 中，单引号和双引号是等价的，只需要坚持使用一种并保持一致即可。

在双引号中使用单引号，单引号中使用双引号。三引号中使用双引号。

<h2 id="5">表达式和语句中的空格<h2/>

<h3 id="5.1">心理藏的小烦恼</h3>

在以下场景避免不必要的空格

```Python
是： spam(ham[1], {eggs: 2})
否： spam( ham[ 1 ], { eggs: 2 } )

是： foo = (0,)
否： bar = (0, )

是： if x == 4: print x, y; x, y = y, x
否： if x == 4 : print x , y ; x , y = y , x

是：
ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
ham[lower:upper], ham[lower:upper:], ham[lower::step]
ham[lower+offset : upper+offset]
ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
ham[lower + offset : upper + offset]

否：
ham[lower + offset:upper + offset]
ham[1: 9], ham[1 :9], ham[1:9 :3]
ham[lower : : upper]
ham[ : upper]

是： spam(1)
否： spam (1)

是： dct['key'] = lst[index]
否： dct ['key'] = lst [index]

是：
x = 1
y = 2
long_variable = 3

否：
x             = 1
y             = 2
long_variable = 3

```

<h3 id="5.2">其他建议</h3>

在任何地方避免使用尾随空格。

在二元运算符周围使用空格：

```python
是：

i = i + 1
submitted += 1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)

否：

i=i+1
submitted +=1
x = x * 2 - 1
hypot2 = x * x + y * y
c = (a + b) * (a - b)
```
表示关键字参数货默认参数值时，不要使用空格：

```python
是：

def complex(real, imag=0.0):
    return magic(r=real, i=imag)
否：

def complex(real, imag = 0.0):
    return magic(r = real, i = imag)
```
函数注释的场景：

```python
是：

def munge(input: AnyStr): ...
def munge() -> AnyStr: ...

否：

def munge(input:AnyStr): ...
def munge()->PosInt: ...
```

当参数注释和默认值共存时：

```python
是：

def munge(sep: AnyStr = None): ...
def munge(input: AnyStr, sep: AnyStr = None, limit=1000): ...

否：

def munge(input: AnyStr=None): ...
def munge(input: AnyStr, limit = 1000): ...
```

复合声明不建议使用：

```python
是：

if foo == 'blah':
    do_blah_thing()
do_one()
do_two()
do_three()

Rather not:

if foo == 'blah': do_blah_thing()
do_one(); do_two(); do_three()
```

下面这种丑就不多说了：

```python
Rather not:

if foo == 'blah': do_blah_thing()
for x in lst: total += x
while t < 10: t = delay()

Definitely not:

if foo == 'blah': do_blah_thing()
else: do_non_blah_thing()

try: something()
finally: cleanup()

do_one(); do_two(); do_three(long, argument,
                             list, like, this)

if foo == 'blah': one(); two(); three()
```

<h2 id="6">何时使用逗号结尾</h2>

单元素元组强制使用逗号：

```python
是：

FILES = ('setup.cfg',)

OK, but confusing:

FILES = 'setup.cfg',
```
当使用版本控制系统时，一组希望后续扩展的值/参数/改善的条目使用以下形式：
```python
是：

FILES = [
    'setup.cfg',
    'tox.ini',
    ]
initialize(FILES,
           error=True,
           )
否：

FILES = ['setup.cfg', 'tox.ini',]
initialize(FILES, error=True,)
```

<h2 id="7">注释</h2>

糟糕的注释不如没有注释，一定要用 English 注释。

<h3 id="7.1">块注释</h3>

同等级别的一块代码的注释，块注释内每行注释以 \# 开头，内部注释段落之间使用以 \# 开头的空行注释隔开。

<h3 id="7.2">行注释</h3>

行注释和代码声明间至少间隔两个空格，不要使用无聊的行注释，例如：

```python 
Don't do this:

x = x + 1                 # Increment x

But sometimes, this is useful(老外调皮的一腿):

x = x + 1                 # Compensate for border
```

<h3 id="7.3">文档字符串</h3>

为所有公共模块，函数，类和方法编写文档字符串。 对于非公共方法，文本字符串不是必需的，但应该有一个描述该方法的注释。例如：  
```python
"""Return a foobang

Optional plotz says to frobnicate the bizbaz first.
"""
```

<h2 id="8">命名约定</h2>

<h3 id="8.1">圣经戒律</h3>

对用户可见的公共 API 部分的命名应该遵从反应如何使用而不是怎么实现。

<h3 id="8.2">描述性: 命名风格</h3>

以下命名风格通常区分彼此使用：

* b (单个小写字母)

* B (单个大写字母)

* lowercase（小写）

* lower\_case\_with_underscores（带下划线的小写）

* UPPERCASE（大写）

* UPPER\_CASE\_WITH\_UNDERSCORES（带下划线的大写）

* CapitalizedWords（驼峰式，蒙古包式 whatever.）

<blockquote>Note: 使用驼峰式时，缩写全部大写，例如：HTTPServerError 好于 HttpServerError </blockquote>

* mixedCase (乌鬼头)

* Capitalized_Words_With_Underscores (丑！不解释！)

* \_single\_leading\_underscore : 弱地 "内部使用" 指示器. 例如，from M import * 不会导入下划线开头的对象

* single\_trailing\_underscore\_ : 用来避免和 python 关键字冲突, 例如：
```python
Tkinter.Toplevel(master, class_='ClassName')
```
* \_\_double\_leading_underscore : 当对类属性命名时, 调用名改变 (在 FooBar 类内, \_\_boo 变成了 \_FooBar\_\_boo ; 看下面(别想多))

* \_\_double\_leading\_and\_trailing\_underscore\_\_ : "魔幻的" 对象或属性，只生存于用户控制的命名空间。例如， \_\_init\_\_ , \_\_import\_\_ 或 \_\_file\_\_ . 千万不要臆造这种命名; 只在文档中使用。

<h3 id="8.3">规定性: 命名习惯</h3>

<h4 id="8.3.1">避免的命名</h4>

一定不要使用 l(唉欧儿) O（偶） I（艾） 作为单字符变量命名，在某些字体中，这些字母和数字 1 0 无法区分。

<h4 id="8.3.2">包和模块名</h4>

模块应该使用简短并且全小写的命名，下划线也可以使用以提升可读性。

Python 包也应该使用简短的全小写名称，尽管不鼓励使用下划线。

当 C/C++ 编写的扩展模块伴随一个提供更高级别接口的 python 模块时，C/C++ 模块命名应该以下划线开头（例如，\_socket）

<h4 id="8.3.3">类名</h4>

类名通常使用驼峰式命名习惯，在有了接口文档说明并且主要用于调用的情况下，类名也可以使用函数命名风格

<blockquote>Note that there is a separate convention for builtin names: most builtin names are single words (or two words run together), with the CapWords convention used only for exception names and builtin constants.</blockquote>

<h4 id="8.3.4">类型变量名</h4>

Names of type variables introduced in PEP 484 should normally use CapWords preferring short names: T , AnyStr , Num . It is recommended to add suffixes _co or _contra to the variables used to declare covariant or contravariant behavior correspondingly. Examples:

```python
from typing import TypeVar

VT_co = TypeVar('VT_co', covariant=True)
KT_contra = TypeVar('KT_contra', contravariant=True)
```

<h4 id="8.3.5">异常名</h4>

异常应该是类，所以可以使用类命名习惯，但是，如果异常是个错误类，一般加上 "Error" 后缀

<h4 id="8.3.6">全局变量名</h4>

我们假设这些全局变量只在一个模块内使用，这样的话和函数的命名习惯是一样的。

设计为通过 <code>from M import *</code> 导入的类应该使用 __all__ 机制避免导出全局变量，或者可以使用老式的习惯，给这些全局变量名加上下划线作为前缀（表示这是非公有变量）


<h4 id="8.3.7">函数名</h4>

例如，<code>func</code> or <code>func_write_to_file</code>

为了向后兼容性，也可以使用 mixedCase 式命名风格。

<h4 id="8.3.8">函数和方法参数</h4>

实例方法第一个入参一定要是 self

类方法第一个入参一定要是 cls

如果函数入参名和保留关键字冲突，则后缀下划线好过缩写或者糟糕的拼写

e.g, class_ 好过 clss

<h4 id="8.3.9">方法名和实例变量</h4>

使用函数命名风格即可。如果希望是私有方法或实例变量，则前缀下划线。

为避免和子类的命名冲突，请使用双下划线前缀命名。

如果类 Foo 有一个属性变量 __a，那么通过 Foo.__a 是不能被访问的。当然，固执的用户仍然可以通过 Foo._Foo__a 访问），一般来说，双下划线前缀只是在避免子类属性命名冲突的场景下使用。

<h4 id="8.3.10">常量</h4>

常量一般定义在模块级别。命名风格如：MAX_OVERFLOW 或 TOTAL 。

<h4 id="8.3.11">继承设计</h4>

经常去思考类方法和实例变量（属性）应该是公有的还是非公有的（严格意义上，python 没有私有变量）。如果不确定，那就设置成非公有的。

另一类属性类别是子类 API 的一部分，（在其他语言中称"protected"）。有些类天生就是被设计为用来继承的，当设计这种类时，注意哪些属性是公有的，哪些是子类 API 的一部分，哪些是只在基类中使用的。

神谕的指导：

* 公有实例变量不应该有前缀下划线
* 公有实例变量和保留关键字冲突时，变量名加前缀下划线避免，这比使用缩写和其他糟糕的拼写要好（除了 'cls'，当一个变量或入参确定是一个类，特别是作为类方法的第一个入参时，'cls' 更惹人喜爱）。
* 对于简单的公有数据属性，不要使用复杂的存取函数，直接暴露属性名。
* 如果设计继承基类时，不希望子类访问的属性加双下划线前缀。

<h4 id="8.3.12">公共和内部接口</h4>

文档说明的接口一般认为是公共接口，除非文档明确声明为临时或内部接口（为了兼容性等其他原因），所有非文档说明的接口一般为内部接口。

模块应该使用 \_\_all\_\_ 属性明确声明公共 API 名，如果 \_\_all\_\_ 为空，则表明模块没有公共 API。

尽管使用了 \_\_all\_\_ 属性，内部接口（packages, modules, classes, functions, attributes or other names）仍然需要使用前缀下划线。

如果包含的任何一个命名空间（package, module or class）是内部的，那么这个接口也被认为是内部接口。

Imported names should always be considered an implementation detail. Other modules must not rely on indirect access to such imported names unless they are an explicitly documented part of the containing module's API, such as os.path or a package's __init__ module that exposes functionality from submodules.

<h3 id="9">编码建议</h3>

* 代码不应该以一种不利于其他 python 实现（PyPy, Jython, IronPython, Cython, Psyco 诸如此类）的方式编写。 例如：不要使用 a += b 或 a = a + b 来实现就地字符串连接，在库的性能敏感部分，应该使用 ''.join() 的形式，这就能保证在不同的 python 实现中，连接动作可以在线性时间内完成。

* 和例如 None 这类 singleton 的比较，应该使用 is 或 is not 而不是等号符。另外，小心使用 if x 如果你的本意是 if x is not None，如果 x 是个布尔变量值 false，就完蛋了。

* 尽管功能相同，从可读性上考虑：
```python
是：

if foo is not None:

否：

if not foo is None:
```

* When implementing ordering operations with rich comparisons, it is best to implement all six operations ( \_\_eq\_\_ , \_\_ne\_\_ , \_\_lt\_\_ , \_\_le\_\_ , \_\_gt\_\_ , \_\_ge\_\_ ) rather than relying on other code to only exercise a particular comparison.

* 使用 def 语句而不是赋值语句直接绑定一个 lambda 表达式到标志符上：
```python
是：

def f(x): return 2*x

否：

f = lambda x: 2*x
```
The use of the assignment statement eliminates the sole benefit a lambda expression can offer over an explicit def statement (i.e. that it can be embedded inside a larger expression

* 捕获的异常要说明 "错误出在哪里了 ？" 而不是仅仅说明 "哎呀！出问题了！"

* 异常转移时，要讲详细的异常信息保留到新的异常中（Python 2: "raise X" Python 3: "raise X from Y"）

* 当在 Python 2 中抛出异常时，使用<code>raise ValueError('message')</code>而不是<code>raise ValueError, 'message'</code>，这样可以避免行连续符的使用

* 当捕获异常时，尽可能提及具体的异常而不是使用一个裸露的 except 子句，例如：
```python
try:
    import platform_specific_module
except ImportError:
    platform_specific_module = None
```

* 当对捕获的异常重命名时，使用以下语法：
```python
try:
    process_data()
except Exception as exc:
    raise DataProcessingFailedError(str(exc))
```

* 当捕获操作系统错误时，使用 Python 3.3 中介绍的异常层次结构

* 对于所有的 try/except 子句，将 try 子句限制为必需的绝对最小代码量避免隐藏错误
```python
是：

try:
    value = collection[key]
except KeyError:
    return key_not_found(key)
else:
    return handle_value(value)

否：

try:
    # Too broad!
    return handle_value(collection[key])
except KeyError:
    # Will also catch KeyError raised by handle_value()
    return key_not_found(key)
```

* 特定代码块的本地资源使用 with 语句确保使用后立即释放，try/finally 也可以

* 除了申请和释放资源，任何时候都应该使用单独的函数和方法调用 Context managers，例如：
```python
是：

with conn.begin_transaction():
    do_stuff_in_transaction(conn)

否：

with conn:
    do_stuff_in_transaction(conn) 
```

* 返回值要一致，be consistent：
```python
是：

def foo(x):
    if x >= 0:
        return math.sqrt(x)
    else:
        return None

def bar(x):
    if x < 0:
        return None
    return math.sqrt(x)

否：

def foo(x):
    if x >= 0:
        return math.sqrt(x)

def bar(x):
    if x < 0:
        return
    return math.sqrt(x)
```

* 使用 string 方法而不是 string 模块。it's faster。当然，除了 2.0 版本之前 python 代码的向后兼容性

* 使用 ''.startswith() 和 ''.endswith() 而不是字符串切片来检查前缀或后缀，例如：
```python
是： if foo.startswith('bar'):
否： if foo[:3] == 'bar':
```

* 对象类型比较因该使用isinstance() 而不是直接比较，例如：
```python
是： if isinstance(obj, int):
否： if type(obj) is type(1):
```
在 Python 2 中，string 和 unicode 公共基类是 basestring，因此：
```python
if isinstance(obj, basestring):
```

* 对于序列（字符串，列表，元组），空的序列是 false：
```python
是：
    if not seq:
    if seq:

否：
    if len(seq):
    if not len(seq):
```

* 不要使用尾随空格

* 不要使用 == 比较布尔值：
```python
是：
    if greeting:
否：
    if greeting == True:
糟糕：
    if greeting is True:
```

<h2 id="9.1">函数注释</h2>

个人建议：赏心悦目，纷吾既有此内美兮，又重之以修能，即可。

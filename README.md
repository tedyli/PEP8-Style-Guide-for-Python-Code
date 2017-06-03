# PEP 8 - Python 代码风格指南
<blockquote>纷吾既有此内美兮，又重之以修能。 - 屈原《离骚》</blockquote>

* [Introduction - 简介](#1)
* [A Foolish Consistency is the Hobgoblin of Little Minds - 愚蠢的一致性是小心灵的大地精](#2)
* [Code lay-out - 代码布局](#3)
    * [Indentation - 缩进](#3.1)
    * [Tabs or Spaces? - A 罩杯还是 E 罩杯 ？](#3.2)
    * [Maximum Line Length - 代码行最大长度](#3.3)
    * [Should a line break before or after a binary operator? - 在二元运算符之前还是之后断行？](#3.4)
    * [Blank Lines - 空行](#3.5)
    * [Source File Encoding - 源文件编码](#3.6)
    * [Imports - 模块导入](#3.7)
    * [Module level dunder names - 模块级 dunder 名称](#3.8)
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

<h2 id="1">简介</h2>

很多项目都有自己独有的编码风格。如果和本文规则发生任何冲突，优先与项目级别的代码风格保持一致。

美其名曰：入乡随俗，Do what Romans do in Rome，到罗马咱就烤马肉吃。

<h2 id="2">愚蠢的一致性是小心灵的大地精</h2>

代码风格一致性当然重要，想象一下空姐的制服诱惑，是不是赏心悦目呢。但也要有自己的主观判断。

例如以下场景：

1、遵循此风格写的一小片代码看起来和项目内其他代码格格不入，看到就想抠出来喂猪，人人见而曰日之。

2、遵循此风格后和其他 python 版本不兼容，甚至出现错误，这就尴尬了。

3、遵循此风格中的某些条目使代码更不易读，简单说就是丑。

<h2 id="3">代码布局</h2>

<h3 id="3.1">缩进</h3>

一个缩进级别四个空格。

* 连续行使用两种方式使封装元素成为一行：括号内垂直隐式连接 & 悬挂式缩进。 使用悬挂式缩进应该注意第一行不应该有参数，连续行要使用进一步的缩进来区分。

```Python

是：

# 括号内隐式连接，垂直对齐
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# 悬挂缩进，进一步缩进区分其他语句
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# 悬挂缩进，一般是四个空格，但非必须
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)

否：

# 括号内隐式连接，没有垂直对齐时，第一行的参数被禁止
foo = long_function_name(var_one, var_two,
    var_three, var_four)

# 悬挂缩进，需要进一步的缩进区分其他行
def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one)
```

* 当 if 语句过长时，可选的处理方式，但不限于此：

```python
# 不使用额外缩进
if (this_is_one_thing and
    that_is_another_thing):
    do_something()

# 增加注释区分，支持语法高亮
if (this_is_one_thing and
    that_is_another_thing):
    # Since both conditions are true, we can frobnicate.
    do_something()
    
# 条件连续行额外缩进
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
或者
```python
my_list = [
    1, 2, 3,
    4, 5, 6,
]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
)
```

<h3 id="3.2">A 罩杯还是 E 罩杯 ？</h3>

A 罩杯。

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

顶层函数和类定义间使用两个空行。

类内方法定义间使用一个空行。

不同函数组之间使用两个空行隔离。

总之，空行的作用就是隔离不同函数类等，使层次分明。

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
表示关键字参数或默认参数值时，不要使用空格：

```python
是：

    def complex(real, imag=0.0):
        return magic(r=real, i=imag)
否：

    def complex(real, imag = 0.0):
        return magic(r = real, i = imag)
```
函数注解的场景：

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

同行多语句不建议使用：

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

But sometimes, this is useful:

x = x + 1                 # Compensate for border
```

<h3 id="7.3">文档字符串</h3>

为所有公共模块，函数，类和方法编写文档字符串。 对于非公共方法，文本字符串不是必需的，但应该有一个描述该方法的注释。例如：  
```python
"""Return a foobang

Optional plotz says to frobnicate the bizbaz first.
"""

"""only one single docstring line"""
```
<blockquote>
注意当注释为多行时，最终的 """ 单独起一行。
</blockquote>

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

* single\_trailing\_underscore\_ : 用来避免和 python 关键字冲突，例如：
```python
Tkinter.Toplevel(master, class_='ClassName')
```
* \_\_double\_leading_underscore : 当对类属性命名时，调用名改变 (在 FooBar 类内，\_\_boo 变成了 \_FooBar\_\_boo；后面有介绍)

* \_\_double\_leading\_and\_trailing\_underscore\_\_ : "魔幻的" 对象或属性，只生存于用户控制的命名空间。例如， \_\_init\_\_ ，\_\_import\_\_ 或 \_\_file\_\_ 。千万不要臆造这种命名； only use them as documented.

<h3 id="8.3">规定性: 命名习惯</h3>

<h4 id="8.3.1">避免的命名</h4>

一定不要使用 l(唉欧儿) O(偶) I(艾) 作为单字符变量命名，在某些字体中，这些字母和数字 1 0 无法区分。

<h4 id="8.3.2">包和模块名</h4>

模块应该使用简短并且全小写的命名，下划线也可以使用以提升可读性。

Python 包也应该使用简短的全小写名称，尽管不鼓励使用下划线。

当 C/C++ 编写的扩展模块伴随一个提供更高级别接口的 python 模块时，C/C++ 模块命名应该以下划线开头(例如，\_socket)。

<h4 id="8.3.3">类名</h4>

类名通常使用驼峰式命名习惯。

在类的接口有文档说明，并且主要用于 callable 的情况下，类都是 callable 的，call 一个类将返回一个新的类实例，例如 instance = Class()。如果类实现了 \_\_call\_\_() 函数，那么类实例也将是 callable 的，类的命名也可以使用函数命名习惯。

对于 builtin 函数的命名习惯，可以通过 <code>dir(\_\_builtins\_\_)</code> 查看系统函数命名样例。注意区分普通命名，异常名命名和 builtin 常量。

<h4 id="8.3.4">类型变量名</h4>

相对于短名称如：T，AnyStr，Num，类型变量使用驼峰式命名习惯较好。另外建议在变量名前添加 \_co 或 \_contra 前缀响应的声明 covariant 或 contravariant 行为。例如：

```python
from typing import TypeVar

VT_co = TypeVar('VT_co', covariant=True)
KT_contra = TypeVar('KT_contra', contravariant=True)
```

<h4 id="8.3.5">异常名</h4>

异常应该是类，所以可以使用类命名习惯，但是，如果异常是个错误类，一般加上 "Error" 后缀。

<h4 id="8.3.6">全局变量名</h4>

我们假设这些全局变量只在一个模块内使用，这样的话和函数的命名习惯是一样的。

设计为通过 <code>from M import *</code> 导入的类应该使用 \_\_all\_\_ 机制避免导出全局变量，或者可以使用老式的习惯，给这些全局变量名加上下划线作为前缀(表示这是非公有变量)。


<h4 id="8.3.7">函数名</h4>

例如，<code>func</code> or <code>func_write_to_file</code>

为了向后兼容性，也可以使用 mixedCase 式命名风格。

<h4 id="8.3.8">函数和方法参数</h4>

实例方法第一个入参一定要是 self。

类方法第一个入参一定要是 cls。

如果函数入参名和保留关键字冲突，则后缀下划线好过缩写或者糟糕的拼写。

例如，class_ 好过 clss。

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

* 公有实例变量不应该有前缀下划线。
* 公有实例变量和保留关键字冲突时，变量名加前缀下划线避免，这比使用缩写和其他糟糕的拼写要好（除了 'cls'，当一个变量或入参确定是一个类，特别是作为类方法的第一个入参时，'cls' 更惹人喜爱）。
* 对于简单的公有数据属性，不要使用复杂的存取函数，直接暴露属性名。
* 如果设计继承基类时，不希望子类访问的属性加双下划线前缀。

<h4 id="8.3.12">公共和内部接口</h4>

文档说明的接口一般认为是公共接口，除非文档明确声明为临时或内部接口（为了兼容性等其他原因），所有非文档说明的接口一般为内部接口。

模块应该使用 \_\_all\_\_ 属性明确声明公共 API 名，如果 \_\_all\_\_ 为空，则表明模块没有公共 API。

尽管使用了 \_\_all\_\_ 属性，内部接口（packages, modules, classes, functions, attributes or other names）仍然需要使用前缀下划线。

如果包含的任何一个命名空间（package, module or class）是内部的，那么这个接口也被认为是内部接口。

导入名应该总是被视为实现细节。其他导入模块一定不能依赖对此导入名的间接访问，除非它们是包含模块 API 的显式文档说明的部分，例如 os.path 或者一个 package 向子模块暴露函数的 \_\_init\_\_ 模块。

<h3 id="9">编码建议</h3>

* 代码不应该以一种不利于其他 python 实现（PyPy, Jython, IronPython, Cython, Psyco 诸如此类）的方式编写。 例如：不要使用 a += b 或 a = a + b 来实现就地字符串连接，在库的性能敏感部分，应该使用 ''.join() 的形式，这就能保证在不同的 python 实现中，连接动作可以在线性时间内完成。

* 和例如 None 这类 singleton 的比较，应该使用 is 或 is not 而不是 ==。另外，小心使用 <code>if x</code> 如果你的本意是 <code>if x is not None</code>，如果 x 是个布尔变量值 false，那可就完蛋了。

* 尽管功能相同，从可读性上考虑：

```python
是：

    if foo is not None:

否：

    if not foo is None:
```
* 当使用 rich comparisons 实现排序操作时，最好是实现所有六种操作(\_\_eq\_\_,\_\_ne\_\_, \_\_lt\_\_, \_\_le\_\_, \_\_gt\_\_, \_\_ge\_\_)而不要依赖其他的代码去单独实现某一类比较。为了减少劳动，functools.total_ordering() decorator 提供了一个生成缺失比较方法的工具。

* 使用 def 语句而不要使用赋值语句去直接绑定一个 lambda 表达式到标识符上：

```python
是：

    def f(x): return 2*x

否：

    f = lambda x: 2*x
```

赋值语句的使用消除了 lambda 表达式相对于显式 def 语句的唯一好处，那就是它能够嵌入到一个更大的表达式里面。

* 捕获的异常要说明 "错误出在哪里了 ？" 而不是仅仅说明 "哎呀！出问题了！"。

* 正确使用异常链接。在 Python 3 中，应该使用 "raise X from Y" 来表示显式替换并且不会丢失原始追溯。

当有意替换一个内部异常(Python 2: "raise X", Python 3.3+: raise X from Non)时，请确保将相关的详细信息转移到新的异常(例如，将 KeyError 转换为 AttributeError 时保留属性名称，或将原始异常的文本嵌入到新的异常消息中)。

* 当在 Python 2 中抛出异常时，使用 <code>raise ValueError('message')</code> 而不是老式的 <code>raise ValueError, 'message'</code>，后者已经在 Python 3 中废弃。由于使用了括号，可以避免行连续符的使用。

* 当捕获异常时，尽可能提及具体的异常而不是使用一个赤裸裸的 except 子句。一个裸露的 except: 子句将捕获 SystemExit 和 KeyboardInterrupt 异常，这样的话就难于使用 control-c 中断程序，并可能掩盖其他问题。如果想要捕获标志程序错误的所有异常的话，用 except Exception:(裸露的 except 子句等同于 except BaseException:)：

```python
try:
    import platform_specific_module
except ImportError:
    platform_specific_module = None
```

<blockquote>

一个很好的经验法则是将裸露的 except 子句仅用于以下两种情况：  

1、If the exception handler will be printing out or logging the traceback; at least the user will be aware that an error has occurred.

2、If the code needs to do some cleanup work, but then lets the exception propagate upwards with raise . try...finally can be a better way to handle this case.

</blockquote>

* 当对捕获的异常重命名时，使用 2.6 版本引入的语法：

```python
try:
    process_data()
except Exception as exc:
    raise DataProcessingFailedError(str(exc))
```

* 当捕获操作系统错误时，相对于内置的 errno 值，最好是使用 Python 3.3 中介绍的显式异常层次结构。

* 对于所有的 try/except 子句，将 try 子句限制为必需的绝对最小代码量避免隐藏 bug：

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

* 特定代码块的本地资源使用 with 语句确保使用后立即释放，不能自动释放的使用 try/finally 也可以。

* 除了申请和释放资源，任何时候都应该使用单独的函数和方法调用 Context managers，例如：

```python
是：

    with conn.begin_transaction():
        do_stuff_in_transaction(conn)

否：

    with conn:
        do_stuff_in_transaction(conn) 
```

* 函数返回语句要一致。在一个函数内的所有返回语句要么都返回一个表达式，要么都不返回。如果任何一个返回语句返回了表达式，那么其他任何没有返回值的语句应该明确声明为 return None。在函数结束部分必须出现返回语句：
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

* 相对于 string 模块，使用 string 方法要快的多并且与 unicode strings 共享相同的 API。当然了，除了需要考虑 2.0 版本之前 python 代码向后兼容性的情况。

* 使用 ''.startswith() 和 ''.endswith() 而不是字符串切片来检查前缀或后缀，例如：

```python
是： if foo.startswith('bar'):
否： if foo[:3] == 'bar':
```

* 对象类型比较应该使用isinstance() 而不是直接比较：

```python
是： if isinstance(obj, int):
否： if type(obj) is type(1):
```

当检查一个对象是否为字符串时，一定要注意这个对象也可能是 unicode 字符串！在 Python 2 中，string 和 unicode 拥有一个公共基类 basestring，因此可以这么的：

```python
if isinstance(obj, basestring):
```

在 Python 3 中，unicode 和 basestring 已然不复存在(there's only str)，并且 bytes object 也不再视为一种 string 了，而是一个整形序列。

* 对于序列（字符串，列表，元组）的判空操作：
```python
是：
    if not seq:
    if seq:

否：
    if len(seq):
    if not len(seq):
```

* 不要使用尾随空格。

* 不要使用 == 验证布尔值为 Ture 或 False：

```python
是：
      if greeting:
否：
      if greeting == True:
虾扯蛋：
      if greeting is True:
```

## 别扯了，再扯蛋都碎了 。=_=# 

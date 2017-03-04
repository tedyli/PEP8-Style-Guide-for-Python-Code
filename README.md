# PEP 8 - Style Guide for Python Code
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
# 垂直隐式连接对齐，用开放定界符使成一行
foo = func_name(var_one, var_two,
                var_three, var_four)
                
# 悬挂式缩进，函数定义时需要再加一级缩进区分非参数代码行
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)
    
# 函数调用时悬挂式一级缩进
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
```
* 当 if 语句过长需要换行时，以下处理方法可以采用。
```Python
# 没有额外的缩进
if (this_is_one_thing and
    that_is_another_thing):
    do_something()

# 增加注释，用以区分函数体部分
# 支持语法高亮
if (this_is_one_thing and
    that_is_another_thing):
    # Since both conditions are true, we can frobnicate.
    do_something()

# 连续行使用进一步的缩进和其他函数体区分
if (this_is_one_thing
        and that_is_another_thing):
    do_something()
```
* 当闭环括号内元素跨行时，可以采用以下方式
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
<h5 id="3.2">Tabs or Spaces?</h5>
除非项目中已经约定了使用 tab 作为缩进，最好使用 space。  
Python 3 不允许 tab 和 space 混用，同时混用了 tab 和 space 的 Python 2 代码应该被转换为仅使用 space。  
<h5 id="3.3">代码行最大长度</h5>
将所有行限制为最多79个字符。  
对于具有较少结构限制（文档字符串或注释）的长文本块，行长度应限制为72个字符。  
当然了，不要问为啥非得是 79,72。背后也许有一个很是凄惨的故事。
反斜杠有时可能仍然要用。 例如，又多又长的 with - 语句不能使用隐式连接，这时反斜杠是可以接受的：
```Python
with open('/path/to/some/file/you/want/to/read') as file_1, \
     open('/path/to/some/file/being/written', 'w') as file_2:
    file_2.write(file_1.read())
```
assert 语句也是如此。

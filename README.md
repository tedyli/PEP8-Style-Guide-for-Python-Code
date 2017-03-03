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
连续行使用两种方式使封装元素成为一行：括号内隐式连接 和 悬挂式缩进
1、使用大中小括号内的隐式连接
```Python
# 垂直对齐，用开放定界符使成一行
foo = func_name(var_one, var_two,
                var_three, var_four)
                
# 函数定义时需要再加一级缩进区分非参数代码行
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)
    
# 函数调用时悬挂式一级缩进
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
```

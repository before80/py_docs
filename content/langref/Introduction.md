+++
title = "概述"
weight = 10
date = 2023-06-27T09:28:25+08:00
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

# 1. 概述



https://docs.python.org/zh-cn/3.11/reference/introduction.html

本手册仅描述 Python 编程语言，不宜当作教程。

我希望尽可能地保证内容精确无误，但还是选择使用自然词句进行描述，正式的规格定义仅用于句法和词法解析。这样应该能使文档对于普通人来说更易理解，但也可能导致一些歧义。因此，如果你是来自火星并且想凭借这份文档把 Python 重新实现一遍，也许有时需要自行猜测，实际上最终大概会得到一个十分不同的语言。而在另一方面，如果你正在使用 Python 并且想了解有关该语言特定领域的精确规则，你应该能够在这里找到它们。如果你希望查看对该语言更正式的定义，也许你可以花些时间自己写上一份 --- 或者发明一台克隆机器 :-)

在语言参考文档里加入过多的实现细节是很危险的 --- 具体实现可能发生改变，对同一语言的其他实现可能使用不同的方式。而在另一方面，CPython 是得到广泛使用的 Python 实现 (然而其他一些实现的拥护者也在增加)，其中的特殊细节有时也值得一提，特别是当其实现方式导致额外的限制时。因此，你会发现在正文里不时会跳出来一些简短的 "实现注释"。

每种 Python 实现都带有一些内置和标准的模块。相关的文档可参见 [Python 标准库](https://docs.python.org/zh-cn/3.11/library/index.html#library-index) 索引。少数内置模块也会在此提及，如果它们同语言描述存在明显的关联。



## 1.1. 其他实现

虽然官方 Python 实现差不多得到最广泛的欢迎，但也有一些其他实现对特定领域的用户来说更具吸引力。

知名的实现包括:

- CPython

  这是最早出现并持续维护的 Python 实现，以 C 语言编写。新的语言特性通常在此率先添加。

- Jython

  Python implemented in Java. This implementation can be used as a scripting language for Java applications, or can be used to create applications using the Java class libraries. It is also often used to create tests for Java libraries. More information can be found at [the Jython website](https://www.jython.org/).

- Python for .NET

  此实现实际上使用了 CPython 实现，但是属于 .NET 托管应用并且可以引入 .NET 类库。它的创造者是 Brian Lloyd。想了解详情可访问 [Python for .NET 主页](https://pythonnet.github.io/)。

- IronPython

  An alternate Python for .NET. Unlike Python.NET, this is a complete Python implementation that generates IL, and compiles Python code directly to .NET assemblies. It was created by Jim Hugunin, the original creator of Jython. For more information, see [the IronPython website](https://ironpython.net/).

- PyPy

  An implementation of Python written completely in Python. It supports several advanced features not found in other implementations like stackless support and a Just in Time compiler. One of the goals of the project is to encourage experimentation with the language itself by making it easier to modify the interpreter (since it is written in Python). Additional information is available on [the PyPy project's home page](https://www.pypy.org/).

以上这些实现都可能在某些方面与此参考文档手册的描述有所差异，或是引入了超出标准 Python 文档范围的特定信息。请参考它们各自的专门文档，以确定你正在使用的这个实现有哪些你需要了解的东西。



## 1.2. 标注

句法和词法解析的描述采用经过改进的 BNF 语法标注。这包含以下定义样式:

```
name      ::=  lc_letter (lc_letter | "_")*
lc_letter ::=  "a"..."z"
```

第一行表示 `name` 是 `lc_letter` 之后跟零个或多个 `lc_letter` 和下划线。而 `lc_letter` 则是任意单个 `'a'` 至 `'z'` 字符。(实际上在本文档中始终采用此规则来定义词法和语法规则的名称。)

每条规则的开头是一个名称 (即该规则所定义的名称) 加上 `::=`。 竖线 (`|`) 被用来分隔可选项，它是此标注中绑定程度最低的操作符。 星号 (`*`) 表示前一项的零次或多次重复，类似地，加号 (`+`) 表示一次或多次重复，而由方括号括起的内容 (`[ ]`) 表示出现零次或一次 (或者说，这部分内容是可选的)。 `*` 和 `+` 操作符的绑定是最紧密的，圆括号用于分组。 字符串字面值包含在引号内。 空格的作用仅限于分隔形符。 每条规则通常为一行，有许多个可选项的规则可能会以竖线为界分为多行。

在词法定义中 (如上述示例)，还额外使用了两个约定: 由三个点号分隔的两个字符字面值表示在指定 (闭) 区间范围内的任意单个 ASCII 字符。由尖括号 (`<...>`) 括起来的内容是对于所定义符号的非正式描述；即可以在必要时用来说明 '控制字符' 的意图。

虽然所用的标注方式几乎相同，但是词法定义和句法定义是存在很大区别的: 词法定义作用于输入源中单独的字符，而句法定义则作用于由词法分析所生成的形符流。在下一章节 ("词法分析") 中使用的 BNF 全部都是词法定义；在之后的章节中使用的则是句法定义。
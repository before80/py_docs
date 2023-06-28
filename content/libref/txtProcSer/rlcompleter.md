+++
title = "rlcompleter"
weight = 80
date = 2023-06-27T08:38:36+08:00
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

# rlcompleter --- GNU readline 的补全函数

https://docs.python.org/zh-cn/3.11/library/rlcompleter.html

**源代码:** [Lib/rlcompleter.py](https://github.com/python/cpython/tree/3.11/Lib/rlcompleter.py)

------

​	`rlcompeleter` 通过补全有效的 Python 标识符和关键字定义了一个适用于 [`readline`](https://docs.python.org/zh-cn/3.11/library/readline.html#module-readline) 模块的补全函数。

​	当此模块在具有可用的 [`readline`](https://docs.python.org/zh-cn/3.11/library/readline.html#module-readline) 模块的 Unix 平台被导入, 一个 `Completer` 实例将被自动创建并且它的 `complete()` 方法将设置为 [`readline`](https://docs.python.org/zh-cn/3.11/library/readline.html#module-readline) 的补全器.

示例:

\>>>

```
>>> import rlcompleter
>>> import readline
>>> readline.parse_and_bind("tab: complete")
>>> readline. <TAB PRESSED>
readline.__doc__          readline.get_line_buffer(  readline.read_init_file(
readline.__file__         readline.insert_text(      readline.set_completer(
readline.__name__         readline.parse_and_bind(
>>> readline.
```

[`rlcompleter`](https://docs.python.org/zh-cn/3.11/library/rlcompleter.html#module-rlcompleter) 模块是为了使用 Python 的 [交互模式](https://docs.python.org/zh-cn/3.11/tutorial/interpreter.html#tut-interactive) 而设计的。 除非 Python 是通过 [`-S`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#cmdoption-S) 选项运行, 这个模块总是自动地被导入且配置 (参见 [Readline 配置](https://docs.python.org/zh-cn/3.11/library/site.html#rlcompleter-config))。

在没有 [`readline`](https://docs.python.org/zh-cn/3.11/library/readline.html#module-readline) 的平台, 此模块定义的 `Completer` 类仍然可以用于自定义行为.



## Completer 对象

Completer 对象具有以下方法：

- Completer.**complete**(*text*, *state*)

  为 *text* 返回第 *state* 项补全。如果指定的 *text* 不包含句点字符 (`'.'`)，它将根据当前 [`__main__`](https://docs.python.org/zh-cn/3.11/library/__main__.html#module-__main__), [`builtins`](https://docs.python.org/zh-cn/3.11/library/builtins.html#module-builtins) 和保留关键字（定义于 [`keyword`](https://docs.python.org/zh-cn/3.11/library/keyword.html#module-keyword) 模块）所定义的名称进行补全。如果为带有句点的名称执行调用，它将尝试尽量求值直到最后一部分为止而不产生附带影响（函数不会被求值，但它可以生成对 `__getattr__()` 的调用），并通过 [`dir()`](https://docs.python.org/zh-cn/3.11/library/functions.html#dir) 函数来匹配剩余部分。 在对表达式求值期间引发的任何异常都会被捕获、静默处理并返回 [`None`](https://docs.python.org/zh-cn/3.11/library/constants.html#None)。
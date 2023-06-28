+++
title = "内置常量"
weight = 30
date = 2023-06-27T08:31:54+08:00
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

# 内置常量

https://docs.python.org/zh-cn/3.11/library/constants.html

​	有少数的常量存在于内置命名空间中。 它们是：

## False

​	[`bool`](https://docs.python.org/zh-cn/3.11/library/functions.html#bool) 类型的假值。 给 `False` 赋值是非法的并会引发 [`SyntaxError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#SyntaxError)。

## True

​	[`bool`](https://docs.python.org/zh-cn/3.11/library/functions.html#bool) 类型的真值。 给 `True` 赋值是非法的并会引发 [`SyntaxError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#SyntaxError)。

## None

​	通常被用来代表空值的对象，例如在未向某个函数传入默认参数时。 给 `None` 赋值是非法的并会引发 [`SyntaxError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#SyntaxError)。 `None` 是 `NoneType` 类型的唯一实例。

## NotImplemented

​	应当由双目运算特殊方法（如 `__eq__()`, `__lt__()`, `__add__()`, `__rsub__()` 等）返回的特殊值，用于表明运算没有针对其他类型的实现；也可由原地双目运算特殊方法（如 `__imul__()`, `__iand__()` 等）出于同样的目的而返回。 它不应在布尔运算中被求值。 `NotImplemented` 是 [`types.NotImplementedType`](https://docs.python.org/zh-cn/3.11/library/types.html#types.NotImplementedType) 类型的唯一实例。

> 备注 
>
> ​	当二进制（或就地）方法返回``NotImplemented``时，解释器将尝试对另一种类型（或其他一些回滚操作，取决于运算符）的反射操作。 如果所有尝试都返回``NotImplemented``，则解释器将引发适当的异常。 错误返回的``NotImplemented``将导致误导性错误消息或返回到Python代码中的``NotImplemented``值。参见 [实现算术运算](https://docs.python.org/zh-cn/3.11/library/numbers.html#implementing-the-arithmetic-operations) 为例。

> 备注 
>
> ​	`NotImplementedError` 和 `NotImplemented` 不可互换，即使它们有相似的名称和用途。 有关何时使用它的详细信息，请参阅 [`NotImplementedError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#NotImplementedError)。

​	*在 3.9 版更改:* 作为布尔值来解读 `NotImplemented` 已被弃用。 虽然它目前会被解读为真值，但将同时发出 [`DeprecationWarning`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#DeprecationWarning)。 它将在未来的 Python 版本中引发 [`TypeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#TypeError)。



## Ellipsis

​	与省略号字面值 "`...`" 相同。 该特殊值主要是与用户定义的容器数据类型的扩展切片语法结合使用。 `Ellipsis` 是 [`types.EllipsisType`](https://docs.python.org/zh-cn/3.11/library/types.html#types.EllipsisType) 类型的唯一实例。

## `__debug__`

​	如果 Python 没有以 [`-O`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#cmdoption-O) 选项启动，则此常量为真值。 另请参见 [`assert`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#assert) 语句。

> 备注 
>
> ​	变量名 [`None`](https://docs.python.org/zh-cn/3.11/library/constants.html#None)，[`False`](https://docs.python.org/zh-cn/3.11/library/constants.html#False)，[`True`](https://docs.python.org/zh-cn/3.11/library/constants.html#True) 和 `__ debug__` 无法重新赋值（赋值给它们，即使是属性名，将引发 [`SyntaxError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#SyntaxError) ），所以它们可以被认为是"真正的"常数。
>

## 由 `site`模块添加的常量

​	[`site`](https://docs.python.org/zh-cn/3.11/library/site.html#module-site) 模块（在启动期间自动导入，除非给出 [`-S`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#cmdoption-S) 命令行选项）将几个常量添加到内置命名空间。 它们对交互式解释器 shell 很有用，并且不应在程序中使用。

### quit(code=None)

### exit(code=None)

​	当打印此对象时，会打印出一条消息，例如"Use quit() or Ctrl-D (i.e. EOF) to exit"，当调用此对象时，将使用指定的退出代码来引发 [`SystemExit`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#SystemExit)。

### copyright

### credits

​	打印或调用的对象分别打印版权或作者的文本。

### license

​	当打印此对象时，会打印出一条消息"Type license() to see the full license text"，当调用此对象时，将以分页形式显示完整的许可证文本（每次显示一屏）。
+++
title = "执行模型"
weight = 40
date = 2023-06-27T09:30:20+08:00
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

# 4. 执行模型

https://docs.python.org/zh-cn/3.11/reference/executionmodel.html



## 4.1. 程序的结构

Python 程序是由代码块构成的。 *代码块* 是被作为一个单元来执行的一段 Python 程序文本。 以下几个都属于代码块：模块、函数体和类定义。 交互式输入的每条命令都是代码块。 一个脚本文件（作为标准输入发送给解释器或是作为命令行参数发送给解释器的文件）也是代码块。 一条脚本命令（通过 [`-c`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#cmdoption-c) 选项在解释器命令行中指定的命令）也是代码块。 通过在命令行中使用 [`-m`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#cmdoption-m) 参数作为最高层级脚本（即 `__main__` 模块）运行的模块也是代码块。 传递给内置函数 [`eval()`](https://docs.python.org/zh-cn/3.11/library/functions.html#eval) 和 [`exec()`](https://docs.python.org/zh-cn/3.11/library/functions.html#exec) 的字符串参数也是代码块。

代码块在 *执行帧* 中被执行。 一个帧会包含某些管理信息（用于调试）并决定代码块执行完成后应前往何处以及如何继续执行。



## 4.2. 命名与绑定



### 4.2.1. 名称的绑定

*名称* 用于指代对象。 名称是通过名称绑定操作来引入的。

下面的结构将名字绑定:

- 函数的正式参数，
- 类定义，
- 函数定义，
- 赋值表达式,
- 如果在一个赋值中出现，则为标识符的 [目标](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#assignment) :
  - [`for`](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#for) 循环头,
  - after `as` in a [`with`](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#with) statement, [`except`](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#except) clause, [`except*`](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#except-star) clause, or in the as-pattern in structural pattern matching,
  - 在结构模式匹配中的捕获模式
- [`import`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#import) 语句。

形式为 `from ... import *` 的 `import` 语句绑定所有在导入的模块中定义的名字，除了那些以下划线开头的名字。这种形式只能在模块级别上使用。

[`del`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#del) 语句的目标也被视作一种绑定（虽然其实际语义为解除名称绑定）。

每条赋值或导入语句均发生于类或函数内部定义的代码块中，或是发生于模块层级（即最高层级的代码块）。

如果名称绑定在一个代码块中，则为该代码块的局部变量，除非声明为 [`nonlocal`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#nonlocal) 或 [`global`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#global)。 如果名称绑定在模块层级，则为全局变量。 (模块代码块的变量既为局部变量又为全局变量。) 如果变量在一个代码块中被使用但不是在其中定义，则为 *自由变量*。

每个在程序文本中出现的名称是指由以下名称解析规则所建立的对该名称的 *绑定*。



### 4.2.2. 名称的解析

*作用域* 定义了一个代码块中名称的可见性。 如果代码块中定义了一个局部变量，则其作用域包含该代码块。 如果定义发生于函数代码块中，则其作用域会扩展到该函数所包含的任何代码块，除非有某个被包含代码块引入了对该名称的不同绑定。

当一个名称在代码块中被使用时，会由包含它的最近作用域来解析。 对一个代码块可见的所有这种作用域的集合称为该代码块的 *环境*。

当一个名称完全找不到时，将会引发 [`NameError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#NameError) 异常。 如果当前作用域为函数作用域，且该名称指向一个局部变量，而此变量在该名称被使用的时候尚未绑定到特定值，将会引发 [`UnboundLocalError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#UnboundLocalError) 异常。 [`UnboundLocalError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#UnboundLocalError) 为 [`NameError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#NameError) 的一个子类。

If a name binding operation occurs anywhere within a code block, all uses of the name within the block are treated as references to the current block. This can lead to errors when a name is used within a block before it is bound. This rule is subtle. Python lacks declarations and allows name binding operations to occur anywhere within a code block. The local variables of a code block can be determined by scanning the entire text of the block for name binding operations. See [the FAQ entry on UnboundLocalError](https://docs.python.org/zh-cn/3.11/faq/programming.html#faq-unboundlocalerror) for examples.

如果 [`global`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#global) 语句出现在一个代码块中，则所有对该语句所指定名称的使用都是在最高层级命名空间内对该名称绑定的引用。 名称在最高层级命名内的解析是通过全局命名空间，也就是包含该代码块的模块的命名空间，以及内置命名空间即 [`builtins`](https://docs.python.org/zh-cn/3.11/library/builtins.html#module-builtins) 模块的命名空间。 全局命名空间会先被搜索。 如果未在其中找到指定名称，再搜索内置命名空间。 `global` 语句必须位于所有对其所列出名称的使用之前。

[`global`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#global) 语句与同一代码块中名称绑定具有相同的作用域。 如果一个自由变量的最近包含作用域中有一条 global 语句，则该自由变量也会被当作是全局变量。

[`nonlocal`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#nonlocal) 语句会使得相应的名称指向之前在最近包含函数作用域中绑定的变量。 如果指定名称不存在于任何包含函数作用域中则将在编译时引发 [`SyntaxError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#SyntaxError)。

模块的作用域会在模块第一次被导入时自动创建。 一个脚本的主模块总是被命名为 [`__main__`](https://docs.python.org/zh-cn/3.11/library/__main__.html#module-__main__)。

类定义代码块以及传给 [`exec()`](https://docs.python.org/zh-cn/3.11/library/functions.html#exec) 和 [`eval()`](https://docs.python.org/zh-cn/3.11/library/functions.html#eval) 的参数是名称解析上下文中的特殊情况。 类定义是可能使用并定义名称的可执行语句。 这些引用遵循正常的名称解析规则，例外之处在于未绑定的局部变量将会在全局命名空间中查找。 类定义的命名空间会成为该类的属性字典。 在类代码块中定义的名称的作用域会被限制在类代码块中；它不会扩展到方法的代码块中 -- 这也包括推导式和生成器表达式，因为它们都是使用函数作用域实现的。 这意味着以下代码将会失败:

```
class A:
    a = 42
    b = list(a + i for i in range(10))
```



### 4.2.3. 内置命名空间和受限的执行

**CPython 实现细节：** 用户不应该接触 `__builtins__`，严格说来它属于实现细节。 用户如果要重载内置命名空间中的值则应该 [`import`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#import) [`builtins`](https://docs.python.org/zh-cn/3.11/library/builtins.html#module-builtins) 并相应地修改该模块中的属性。

与一个代码块的执行相关联的内置命名空间实际上是通过在其全局命名空间中搜索名称 `__builtins__` 来找到的；这应该是一个字典或一个模块（在后一种情况下会使用该模块的字典）。 默认情况下，当在 [`__main__`](https://docs.python.org/zh-cn/3.11/library/__main__.html#module-__main__) 模块中时，`__builtins__` 就是内置模块 [`builtins`](https://docs.python.org/zh-cn/3.11/library/builtins.html#module-builtins)；当在任何其他模块中时，`__builtins__` 则是 [`builtins`](https://docs.python.org/zh-cn/3.11/library/builtins.html#module-builtins) 模块自身的字典的一个别名。



### 4.2.4. 与动态特性的交互

自由变量的名称解析发生于运行时而不是编译时。 这意味着以下代码将打印出 42:

```
i = 10
def f():
    print(i)
i = 42
f()
```

[`eval()`](https://docs.python.org/zh-cn/3.11/library/functions.html#eval) 和 [`exec()`](https://docs.python.org/zh-cn/3.11/library/functions.html#exec) 函数没有对完整环境的访问权限来解析名称。 名称可以在调用者的局部和全局命名空间中被解析。 自由变量的解析不是在最近包含命名空间中，而是在全局命名空间中。 [1](https://docs.python.org/zh-cn/3.11/reference/executionmodel.html#id3) [`exec()`](https://docs.python.org/zh-cn/3.11/library/functions.html#exec) 和 [`eval()`](https://docs.python.org/zh-cn/3.11/library/functions.html#eval) 函数有可选参数用来重载全局和局部命名空间。 如果只指定一个命名空间，则它会同时作用于两者。



## 4.3. 异常



异常是中断代码块的正常控制流程以便处理错误或其他异常条件的一种方式。 异常会在错误被检测到的位置 *引发*，它可以被当前包围代码块或是任何直接或间接发起调用发生错误的代码块的其他代码块所 *处理*。

Python 解析器会在检测到运行时错误（例如零作为被除数）的时候引发异常。 Python 程序也可以通过 [`raise`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#raise) 语句显式地引发异常。 异常处理是通过 [`try`](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#try) ... [`except`](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#except) 语句来指定的。 该语句的 [`finally`](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#finally) 子句可被用来指定清理代码，它并不处理异常，而是无论之前的代码是否发生异常都会被执行。

Python 的错误处理采用的是“终止”模型：异常处理器可以找出发生了什么问题，并在外层继续执行，但它不能修复错误的根源并重试失败的操作（除非通过从顶层重新进入出错的代码片段）。

当一个异常完全未被处理时，解释器会终止程序的执行，或者返回交互模式的主循环。 无论是哪种情况，它都会打印栈回溯信息，除非是当异常为 [`SystemExit`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#SystemExit) 的时候。

异常是通过类实例来标识的。 [`except`](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#except) 子句会依据实例的类来选择：它必须引用实例的类或是其所属的 [非虚基类](https://docs.python.org/zh-cn/3.11/glossary.html#term-abstract-base-class) 。 实例可通过处理器被接收，并可携带有关异常条件的附加信息。

备注

 

异常消息不是 Python API 的组成部分。 其内容可能在 Python 升级到新版本时不经警告地发生改变，不应该被需要在多版本解释器中运行的代码所依赖。

另请参看 [try 语句](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#try) 小节中对 [`try`](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#try) 语句的描述以及 [raise 语句](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#raise) 小节中对 [`raise`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#raise) 语句的描述。

备注

- [1](https://docs.python.org/zh-cn/3.11/reference/executionmodel.html#id1)

  出现这样的限制是由于通过这些操作执行的代码在模块被编译的时候并不可用。
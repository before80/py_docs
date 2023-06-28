+++
title = "内置函数"
weight = 20
date = 2023-06-27T08:31:29+08:00
type = "docs"
description = ""
isCJKLanguage = true
draft = false

+++

# 内置函数

https://docs.python.org/zh-cn/3.11/library/functions.html

​	Python 解释器内置了很多函数和类型，任何时候都能使用。以下按字母顺序给出列表。

| 内置函数                                                     |                                                              |                                                              |                                                              |
| :----------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **A**[`abs()`](#absx)[`aiter()`](#aiterasync_iterable)[`all()`](#alliterable)[`any()`](#anyiterable)[`anext()`](#awaitable-anextasync_iterator-default)[`ascii()`](#asciiobject) **B**[`bin()`](#binx)[`bool()`](#class-boolxfalse)[`breakpoint()`](#breakpointargs-kws)[`bytearray()`](#class-bytearraysourceb)[`bytes()`](#class-bytessourceb) **C**[`callable()`](#callable)[`chr()`](#chr)[`classmethod()`](#classmethod)[`compile()`](#compile)[`complex()`](#complex) **D**[`delattr()`](#delattr)[`dict()`](#func-dict)[`dir()`](#dir)[`divmod()`](#divmod) | **E**[`enumerate()`](#enumerate)[`eval()`](#eval)[`exec()`](#exec) **F**[`filter()`](#filter)[`float()`](#float)[`format()`](#format)[`frozenset()`](#func-frozenset) **G**[`getattr()`](#getattr)[`globals()`](#globals) **H**[`hasattr()`](#hasattr)[`hash()`](#hash)[`help()`](#help)[`hex()`](#hex) **I**[`id()`](#id)[`input()`](#input)[`int()`](#int)[`isinstance()`](#isinstance)[`issubclass()`](#issubclass)[`iter()`](#iter) | **L**[`len()`](#len)[`list()`](#func-list)[`locals()`](#locals) **M**[`map()`](#map)[`max()`](#max)[`memoryview()`](#func-memoryview)[`min()`](#min) **N**[`next()`](#next) **O**[`object()`](#object)[`oct()`](#oct)[`open()`](#open)[`ord()`](#ord) **P**[`pow()`](#pow)[`print()`](#print)[`property()`](#property) | **R**[`range()`](#func-range)[`repr()`](#repr)[`reversed()`](#reversed)[`round()`](#round) **S**[`set()`](#func-set)[`setattr()`](#setattr)[`slice()`](#slice)[`sorted()`](#sorted)[`staticmethod()`](#staticmethod)[`str()`](#func-str)[`sum()`](#sum)[`super()`](#super) **T**[`tuple()`](#func-tuple)[`type()`](#type) **V**[`vars()`](#vars) **Z**[`zip()`](#zip) **_**[`__import__()`](#import__) |

## abs(*x*)

​	返回一个数的绝对值。 参数可以是整数、浮点数或任何实现了 `__abs__()` 的对象。 如果参数是一个复数，则返回它的模。

## aiter(async_iterable)

​	返回 [asynchronous iterable](https://docs.python.org/zh-cn/3.11/glossary.html#term-asynchronous-iterable) 的 [asynchronous iterator](https://docs.python.org/zh-cn/3.11/glossary.html#term-asynchronous-iterator) 。相当于调用 `x.__aiter__()`。注意：与 [`iter()`](https://docs.python.org/zh-cn/3.11/library/functions.html#iter) 不同，[`aiter()`](https://docs.python.org/zh-cn/3.11/library/functions.html#aiter) 没有两个参数的版本。*3.10 新版功能.*

## all(iterable)

​	如果 *iterable* 的所有元素均为真值（或可迭代对象为空）则返回 `True` 。 等价于：

```python
def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True
```

## awaitable anext(async_iterator)

## awaitable anext(async_iterator, default)

​	当进入 await 状态时，从给定 [asynchronous iterator](https://docs.python.org/zh-cn/3.11/glossary.html#term-asynchronous-iterator) 返回下一数据项，迭代完毕则返回 *default*。

​	这是内置函数 [`next()`](https://docs.python.org/zh-cn/3.11/library/functions.html#next) 的异步版本，类似于：

​	调用 *async_iterator* 的 [`__anext__()`](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#object.__anext__) 方法，返回一个 [awaitable](https://docs.python.org/zh-cn/3.11/glossary.html#term-awaitable)。等待返回迭代器的下一个值。若有给出 *default*，则在迭代完毕后会返回给出的值，否则会触发 [`StopAsyncIteration`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#StopAsyncIteration)。*3.10 新版功能.*

## any(iterable)

​	如果 *iterable* 的任一元素为真值则返回 `True`。 如果可迭代对象为空，返回 `False`。 等价于:

```python
def any(iterable):
    for element in iterable:
        if element:
            return True
    return False
```

## ascii(object)

​	与 [`repr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#repr) 类似，返回一个字符串，表示对象的可打印形式，但在 [`repr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#repr) 返回的字符串中，非 ASCII 字符会用 `\x`、`\u` 和 `\U` 进行转义。生成的字符串类似于 Python 2 中 [`repr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#repr) 的返回结果。

## bin(x)

​	将整数转变为以"0b"前缀的二进制字符串。结果是一个合法的 Python 表达式。如果 *x* 不是 Python 的 [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 对象，它必须定义 `__index__()` 方法，以便返回整数值。下面是一些例子：

```python
bin(3) # '0b11'

bin(-10) # '-0b1010'
```

​	若要控制是否显示前缀"0b"，可以采用以下两种方案：

```python
format(14, '#b'), format(14, 'b') # ('0b1110', '1110')

f'{14:#b}', f'{14:b}' # ('0b1110', '1110')
```

​	另见 [`format()`](https://docs.python.org/zh-cn/3.11/library/functions.html#format) 获取更多信息。

## class bool(x=False)

​	返回布尔值，`True` 或 `False`。*x* 用标准的 [真值测试过程](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#truth) 进行转换。如果 *x* 为 False 或省略，则返回 `False`；否则返回 `True`。 [`bool`](https://docs.python.org/zh-cn/3.11/library/functions.html#bool) 类是 [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 的子类（见 [数字类型 --- int, float, complex](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesnumeric) ）。它不能再被继承。它唯一的实例就是 `False` 和 `True` （参阅 [布尔值](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bltin-boolean-values) ）。

​	*在 3.7 版更改:* *x* 现在只能作为位置参数。

## breakpoint(*args, **kws)

​	This function drops you into the debugger at the call site. Specifically, it calls [`sys.breakpointhook()`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.breakpointhook), passing `args` and `kws` straight through. By default, `sys.breakpointhook()` calls [`pdb.set_trace()`](https://docs.python.org/zh-cn/3.11/library/pdb.html#pdb.set_trace) expecting no arguments. In this case, it is purely a convenience function so you don't have to explicitly import [`pdb`](https://docs.python.org/zh-cn/3.11/library/pdb.html#module-pdb) or type as much code to enter the debugger. However, [`sys.breakpointhook()`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.breakpointhook) can be set to some other function and [`breakpoint()`](https://docs.python.org/zh-cn/3.11/library/functions.html#breakpoint) will automatically call that, allowing you to drop into the debugger of choice. If [`sys.breakpointhook()`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.breakpointhook) is not accessible, this function will raise [`RuntimeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#RuntimeError).

​	By default, the behavior of [`breakpoint()`](https://docs.python.org/zh-cn/3.11/library/functions.html#breakpoint) can be changed with the [`PYTHONBREAKPOINT`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#envvar-PYTHONBREAKPOINT) environment variable. See [`sys.breakpointhook()`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.breakpointhook) for usage details.

​	Note that this is not guaranteed if [`sys.breakpointhook()`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.breakpointhook) has been replaced.引发一个 [审计事件](https://docs.python.org/zh-cn/3.11/library/sys.html#auditing) `builtins.breakpoint` 并附带参数 `breakpointhook`。

​	*3.7 新版功能.*

## class bytearray(source=b'')

## class bytearray(source, encoding)

## class bytearray(source, encoding, errors)

​	返回一个新的 bytes 数组。 [`bytearray`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bytearray) 类是一个可变序列，包含范围为 0 <= x < 256 的整数。它有可变序列大部分常见的方法，见 [可变序列类型](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesseq-mutable) 的描述；同时有 [`bytes`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bytes) 类型的大部分方法，参见 [bytes 和 bytearray 操作](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bytes-methods)。

​	可选形参 *source* 可以用不同的方式来初始化数组：

- 如果是一个 *string*，您必须提供 *encoding* 参数（*errors* 参数仍是可选的）；[`bytearray()`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bytearray) 会使用 [`str.encode()`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#str.encode) 方法来将 string 转变成 bytes。

- 如果是一个 *integer*，会初始化大小为该数字的数组，并使用 null 字节填充。

- 如果是一个遵循 [缓冲区接口](https://docs.python.org/zh-cn/3.11/c-api/buffer.html#bufferobjects) 的对象，该对象的只读缓冲区将被用来初始化字节数组。

- 如果是一个 *iterable* 可迭代对象，它的元素的范围必须是 `0 <= x < 256` 的整数，它会被用作数组的初始内容。

​	如果没有实参，则创建大小为 0 的数组。

​	另见 [二进制序列类型 --- bytes, bytearray, memoryview](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#binaryseq) 和 [bytearray 对象](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typebytearray)。



## class bytes(source=b'')

## class bytes(source, encoding)

## class bytes(source, encoding, errors)

​	返回一个新的"bytes"对象，这是一个不可变序列，包含范围为 `0 <= x < 256` 的整数。[`bytes`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bytes) 是 [`bytearray`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bytearray) 的不可变版本——带有同样不改变序列的方法，支持同样的索引、切片操作。

​	因此，构造函数的实参和 [`bytearray()`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bytearray) 相同。

​	字节对象还可以用字面值创建，参见 [字符串与字节串字面值](https://docs.python.org/zh-cn/3.11/reference/lexical_analysis.html#strings)。

​	另见 [二进制序列类型 --- bytes, bytearray, memoryview](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#binaryseq)，[bytes 对象](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typebytes) 和 [bytes 和 bytearray 操作](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bytes-methods)。

## callable(object)

​	如果参数 *object* 是可调用的就返回 [`True`](https://docs.python.org/zh-cn/3.11/library/constants.html#True)，否则返回 [`False`](https://docs.python.org/zh-cn/3.11/library/constants.html#False)。 如果返回 `True`，调用仍可能失败，但如果返回 `False`，则调用 *object* 将肯定不会成功。 请注意类是可调用的（调用类将返回一个新的实例）；如果实例所属的类有 `__call__()` 则它就是可调用的。

*3.2 新版功能:* 这个函数一开始在 Python 3.0 被移除了，但在 Python 3.2 被重新加入。

## chr(i)

​	返回 Unicode 码位为整数 *i* 的字符的字符串格式。例如，`chr(97)` 返回字符串 `'a'`，`chr(8364)` 返回字符串 `'€'`。这是 [`ord()`](https://docs.python.org/zh-cn/3.11/library/functions.html#ord) 的逆函数。实参的合法范围是 0 到 1,114,111（16 进制表示是 0x10FFFF）。如果 *i* 超过这个范围，会触发 [`ValueError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#ValueError) 异常。

## @classmethod

​	把一个方法封装成类方法。类方法隐含的第一个参数就是类，就像实例方法接收实例作为参数一样。要声明一个类方法，按惯例请使用以下方案：

```python
class C:
    @classmethod
    def f(cls, arg1, arg2): ...
```

​	`@classmethod` 这样的形式称为函数的 [decorator](https://docs.python.org/zh-cn/3.11/glossary.html#term-decorator) -- 详情参阅 [函数定义](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#function)。

​	类方法的调用可以在类上进行 (例如 `C.f()`) 也可以在实例上进行 (例如 `C().f()`)。 其所属类以外的类实例会被忽略。 如果类方法在其所属类的派生类上调用，则该派生类对象会被作为隐含的第一个参数被传入。

​	类方法与 C++ 或 Java 中的静态方法不同。 如果你需要后者，请参阅本节中的 [`staticmethod()`](https://docs.python.org/zh-cn/3.11/library/functions.html#staticmethod)。 有关类方法的更多信息，请参阅 [标准类型层级结构](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#types)。

​	*在 3.9 版更改:* 类方法现在可以包装其他 [描述器](https://docs.python.org/zh-cn/3.11/glossary.html#term-descriptor) 例如 [`property()`](https://docs.python.org/zh-cn/3.11/library/functions.html#property)。

​	*在 3.10 版更改:* 类方法现在继承了方法的属性（`__module__`、`__name__`、`__qualname__`、`__doc__` 和 `__annotations__`），并拥有一个新的``__wrapped__`` 属性。

​	*在 3.11 版更改:* Class methods can no longer wrap other [descriptors](https://docs.python.org/zh-cn/3.11/glossary.html#term-descriptor) such as [`property()`](https://docs.python.org/zh-cn/3.11/library/functions.html#property).

## compile(source, filename, mode, flags=0, dont_inherit=False, optimize=- 1)

​	将 *source* 编译成代码或 AST 对象。代码对象可以被 [`exec()`](https://docs.python.org/zh-cn/3.11/library/functions.html#exec) 或 [`eval()`](https://docs.python.org/zh-cn/3.11/library/functions.html#eval) 执行。*source* 可以是常规的字符串、字节字符串，或者 AST 对象。参见 [`ast`](https://docs.python.org/zh-cn/3.11/library/ast.html#module-ast) 模块的文档了解如何使用 AST 对象。

​	*filename* 实参需要是代码读取的文件名；如果代码不需要从文件中读取，可以传入一些可辨识的值（经常会使用 `'<string>'`）。

​	*mode* 实参指定了编译代码必须用的模式。如果 *source* 是语句序列，可以是 `'exec'`；如果是单一表达式，可以是 `'eval'`；如果是单个交互式语句，可以是 `'single'`。（在最后一种情况下，如果表达式执行结果不是 `None` 将会被打印出来。）

​	可选参数 *flags* 和 *dont_inherit* 控制应当激活哪个 [编译器选项](https://docs.python.org/zh-cn/3.11/library/ast.html#ast-compiler-flags) 以及应当允许哪个 [future 特性](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#future)。 如果两者都未提供 (或都为零) 则代码会应用与调用 [`compile()`](https://docs.python.org/zh-cn/3.11/library/functions.html#compile) 的代码相同的旗标来编译。 如果给出了 *flags* 参数而未给出 *dont_inherit* (或者为零) 则会在无论如何都将被使用的旗标之外还会额外使用 *flags* 参数所指定的编译器选项和 future 语句。 如果 *dont_inherit* 为非零整数，则只使用 *flags* 参数 -- 外围代码中的旗标 (future 特性和编译器选项) 会被忽略。

​	编译器选项和 future 语句是由比特位来指明的。 比特位可以通过一起按位 OR 来指明多个选项。 指明特定 future 特性所需的比特位可以在 [`__future__`](https://docs.python.org/zh-cn/3.11/library/__future__.html#module-__future__) 模块的 `_Feature` 实例的 `compiler_flag` 属性中找到。 [编译器旗标](https://docs.python.org/zh-cn/3.11/library/ast.html#ast-compiler-flags) 可以在 [`ast`](https://docs.python.org/zh-cn/3.11/library/ast.html#module-ast) 模块中查找带有 `PyCF_` 前缀的名称。

​	*optimize* 实参指定编译器的优化级别；默认值 `-1` 选择与解释器的 [`-O`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#cmdoption-O) 选项相同的优化级别。显式级别为 `0` （没有优化；`__debug__` 为真）、`1` （断言被删除， `__debug__` 为假）或 `2` （文档字符串也被删除）。

​	如果编译的源码不合法，此函数会触发 [`SyntaxError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#SyntaxError) 异常；如果源码包含 null 字节，则会触发 [`ValueError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#ValueError) 异常。

​	如果您想分析 Python 代码的 AST 表示，请参阅 [`ast.parse()`](https://docs.python.org/zh-cn/3.11/library/ast.html#ast.parse)。

​	引发一个 [审计事件](https://docs.python.org/zh-cn/3.11/library/sys.html#auditing) `compile` 附带参数 `source`, `filename`。

> 备注 
>
> ​	在 `'single'` 或 `'eval'` 模式编译多行代码字符串时，输入必须以至少一个换行符结尾。 这使 [`code`](https://docs.python.org/zh-cn/3.11/library/code.html#module-code) 模块更容易检测语句的完整性。

> 警告 
>
> ​	在将足够大或者足够复杂的字符串编译成 AST 对象时，Python 解释器有可能因为 Python AST 编译器的栈深度限制而崩溃。

​	*在 3.2 版更改:* Windows 和 Mac 的换行符均可使用。而且在 `'exec'` 模式下的输入不必再以换行符结尾了。另增加了 *optimize* 参数。

​	*在 3.5 版更改:* 之前 *source* 中包含 null 字节的话会触发 [`TypeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#TypeError) 异常。

​	*3.8 新版功能:* `ast.PyCF_ALLOW_TOP_LEVEL_AWAIT` 现在可在旗标中传入以启用对最高层级 `await`, `async for` 和 `async with` 的支持。

## class complex(real=0, imag=0)

## class complex(string)

​	返回值为 `real + imag*1j` 的复数，或将字符串或数字转换为复数。如果第一个形参是字符串，则它被解释为一个复数，并且函数调用时必须没有第二个形参。第二个形参不能是字符串。每个实参都可以是任意的数值类型（包括复数）。如果省略了 *imag*，则默认值为零，构造函数会像 [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 和 [`float`](https://docs.python.org/zh-cn/3.11/library/functions.html#float) 一样进行数值转换。如果两个实参都省略，则返回 `0j`。

​	对于一个普通 Python 对象 `x`，`complex(x)` 会委托给 `x.__complex__()`。 如果 `__complex__()` 未定义则将回退至 `__float__()`。 如果 `__float__()` 未定义则将回退至 `__index__()`。

> 备注 
>
> ​	当从字符串转换时，字符串在 `+` 或 `-` 的周围必须不能有空格。例如 `complex('1+2j')` 是合法的，但 `complex('1 + 2j')` 会触发 [`ValueError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#ValueError) 异常。

​	[数字类型 --- int, float, complex](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesnumeric) 描述了复数类型。*在 3.6 版更改:* 您可以使用下划线将代码文字中的数字进行分组。*在 3.8 版更改:* 如果 `__complex__()` 和 `__float__()` 未定义则回退至 `__index__()`。

## delattr(object, name)

​	This is a relative of [`setattr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#setattr). The arguments are an object and a string. The string must be the name of one of the object's attributes. The function deletes the named attribute, provided the object allows it. For example, `delattr(x, 'foobar')` is equivalent to `del x.foobar`. *name* need not be a Python identifier (see [`setattr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#setattr)).



## class dict(**kwarg)

## class dict(mapping, **kwarg)

## class dict(iterable, **kwarg)

​	创建一个新的字典。[`dict`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#dict) 对象是一个字典类。参见 [`dict`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#dict) 和 [映射类型 --- dict](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesmapping) 了解这个类。

​	其他容器类型，请参见内置的 [`list`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#list)、[`set`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#set) 和 [`tuple`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#tuple) 类，以及 [`collections`](https://docs.python.org/zh-cn/3.11/library/collections.html#module-collections) 模块。

## dir()

## dir(object)

​	如果没有实参，则返回当前本地作用域中的名称列表。如果有实参，它会尝试返回该对象的有效属性列表。

​	如果对象有一个名为 `__dir__()` 的方法，那么该方法将被调用，并且必须返回一个属性列表。这允许实现自定义 `__getattr__()` 或 `__getattribute__()` 函数的对象能够自定义 [`dir()`](https://docs.python.org/zh-cn/3.11/library/functions.html#dir) 来报告它们的属性。

​	如果对象未提供 `__dir__()` 方法，该函数会尽量从对象的 [`__dict__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#object.__dict__) 属性和其类型对象中收集信息。得到的列表不一定是完整，如果对象带有自定义 `__getattr__()` 方法时，结果可能不准确。

​	默认的 [`dir()`](https://docs.python.org/zh-cn/3.11/library/functions.html#dir) 机制对不同类型的对象行为不同，它会试图返回最相关而不是最全的信息：

- 如果对象是模块对象，则列表包含模块的属性名称。
- 如果对象是类型或类对象，则列表包含它们的属性名称，并且递归查找所有基类的属性。
- 否则，列表包含对象的属性名称，它的类属性名称，并且递归查找它的类的所有基类的属性。

​	返回的列表按字母表排序。例如：

```python
import struct
dir()   # show the names in the module namespace  

dir(struct)   # show the names in the struct module 


class Shape:
    def __dir__(self):
        return ['area', 'perimeter', 'location']
s = Shape()
dir(s) # ['area', 'location', 'perimeter']
```

> 备注 
>
> ​	因为 [`dir()`](https://docs.python.org/zh-cn/3.11/library/functions.html#dir) 主要是为了便于在交互式时使用，所以它会试图返回人们感兴趣的名字集合，而不是试图保证结果的严格性或一致性，它具体的行为也可能在不同版本之间改变。例如，当实参是一个类时，metaclass 的属性不包含在结果列表中。



## divmod(a, b)

​	以两个（非复数）数字为参数，在作整数除法时，返回商和余数。若操作数为混合类型，则适用二进制算术运算符的规则。对于整数而言，结果与 `(a // b, a % b)` 相同。对于浮点数则结果为

```python
``(q, a % b)``
```

，其中 *q* 通常为 `math.floor(a / b)`，但可能比它小 1。在任何情况下，`q * b + a % b` 都非常接近 *a*，如果 `a % b` 非零，则结果符号与 *b* 相同，并且 `0 <= abs(a % b) < abs(b)`。

## enumerate(iterable, start=0)

​	返回一个枚举对象。*iterable* 必须是一个序列，或 [iterator](https://docs.python.org/zh-cn/3.11/glossary.html#term-iterator)，或其他支持迭代的对象。 [`enumerate()`](https://docs.python.org/zh-cn/3.11/library/functions.html#enumerate) 返回的迭代器的 [`__next__()`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#iterator.__next__) 方法返回一个元组，里面包含一个计数值（从 *start* 开始，默认为 0）和通过迭代 *iterable* 获得的值。

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
list(enumerate(seasons)) # [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]

list(enumerate(seasons, start=1)) # [(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
```

等价于:

```python
def enumerate(iterable, start=0):
    n = start
    for elem in iterable:
        yield n, elem
        n += 1
```

## eval(expression, globals=None, locals=None)

​	实参是一个字符串，以及可选的 globals 和 locals。*globals* 实参必须是一个字典。*locals* 可以是任何映射对象。

​	表达式解析参数 *expression* 并作为 Python 表达式进行求值（从技术上说是一个条件列表），采用 *globals* 和 *locals* 字典作为全局和局部命名空间。 如果存在 *globals* 字典，并且不包含 `__builtins__` 键的值，则在解析 *expression* 之前会插入以该字符串为键以对内置模块 [`builtins`](https://docs.python.org/zh-cn/3.11/library/builtins.html#module-builtins) 的字典的引用为值的项。 这样就可以在将 *globals* 传给 [`eval()`](https://docs.python.org/zh-cn/3.11/library/functions.html#eval) 之前通过向其传入你自己的 `__builtins__` 字典来控制可供被执行代码可以使用哪些内置模块。 如果 *locals* 字典被省略则它默认为 *globals* 字典。 如果两个字典都被省略，则将使用调用 [`eval()`](https://docs.python.org/zh-cn/3.11/library/functions.html#eval) 的环境中的 *globals* 和 *locals* 来执行该表达式。 注意，*eval()* 无法访问闭包环境中的 [嵌套作用域](https://docs.python.org/zh-cn/3.11/glossary.html#term-nested-scope) (非局部变量)。

​	返回值就是表达式的求值结果。 语法错误将作为异常被报告。 例如：

```python
x = 1
eval('x+1') # 2
```

​	该函数还可用于执行任意代码对象（比如由 [`compile()`](https://docs.python.org/zh-cn/3.11/library/functions.html#compile) 创建的对象）。 这时传入的是代码对象，而非一个字符串了。如果代码对象已用参数为 *mode* 的 `'exec'` 进行了编译，那么 [`eval()`](https://docs.python.org/zh-cn/3.11/library/functions.html#eval) 的返回值将为 `None`。

​	提示： [`exec()`](https://docs.python.org/zh-cn/3.11/library/functions.html#exec) 函数支持语句的动态执行。 [`globals()`](https://docs.python.org/zh-cn/3.11/library/functions.html#globals) 和 [`locals()`](https://docs.python.org/zh-cn/3.11/library/functions.html#locals) 函数分别返回当前的全局和本地字典，可供传给 [`eval()`](https://docs.python.org/zh-cn/3.11/library/functions.html#eval) 或 [`exec()`](https://docs.python.org/zh-cn/3.11/library/functions.html#exec) 使用。

​	如果给出的源数据是个字符串，那么其前后的空格和制表符将被剔除。

​	另外可以参阅 [`ast.literal_eval()`](https://docs.python.org/zh-cn/3.11/library/ast.html#ast.literal_eval)，该函数可以安全执行仅包含文字的表达式字符串。

​	引发一个 [审计事件](https://docs.python.org/zh-cn/3.11/library/sys.html#auditing) `exec` 附带参数 `code_object`。



## exec(object, globals=None, locals=None, /, *, closure=None)

​	这个函数支持动态执行 Python 代码。 *object* 必须是字符串或者代码对象。 如果是字符串，那么该字符串将被解析为一系列 Python 语句并执行（除非发生语法错误）。 [1](https://docs.python.org/zh-cn/3.11/library/functions.html#id2) 如果是代码对象，它将被直接执行。 在任何情况下，被执行的代码都应当是有效的文件输入（见参考手册中的 [文件输入](https://docs.python.org/zh-cn/3.11/reference/toplevel_components.html#file-input) 一节）。 请注意即使在传递给 [`exec()`](https://docs.python.org/zh-cn/3.11/library/functions.html#exec) 函数的代码的上下文中，[`nonlocal`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#nonlocal), [`yield`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#yield) 和 [`return`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#return) 语句也不能在函数定义以外使用。 该函数的返回值是 `None`。

​	无论在什么情况下，如果省略了可选部分，代码将运行于当前作用域中。如果只提供了 *globals*，则必须为字典对象（而不能是字典的子类），同时用于存放全局变量和局部变量。如果提供了 *globals* 和 *locals*，则将分别用于全局变量和局部变量。*locals* 可以是任意字典映射对象。请记住，在模块级别，globals 和 locals 是同一个字典。如果 exec 获得两个独立的对象作为 *globals* 和 *locals*，代码执行起来就像嵌入到某个类定义中一样。

​	如果 *globals* 字典不包含 `__builtins__` 键值，则将为该键插入对内建 [`builtins`](https://docs.python.org/zh-cn/3.11/library/builtins.html#module-builtins) 模块字典的引用。因此，在将执行的代码传递给 [`exec()`](https://docs.python.org/zh-cn/3.11/library/functions.html#exec) 之前，可以通过将自己的 `__builtins__` 字典插入到 *globals* 中来控制可以使用哪些内置代码。

​	The *closure* argument specifies a closure--a tuple of cellvars. It's only valid when the *object* is a code object containing free variables. The length of the tuple must exactly match the number of free variables referenced by the code object.

​	引发一个 [审计事件](https://docs.python.org/zh-cn/3.11/library/sys.html#auditing) `exec` 附带参数 `code_object`。

> 备注 
>
> ​	内置 [`globals()`](https://docs.python.org/zh-cn/3.11/library/functions.html#globals) 和 [`locals()`](https://docs.python.org/zh-cn/3.11/library/functions.html#locals) 函数各自返回当前的全局和本地字典，因此可以将它们传递给 [`exec()`](https://docs.python.org/zh-cn/3.11/library/functions.html#exec) 的第二个和第三个实参。

> 备注 
>
> ​	默认情况下，*locals* 的行为如下面 [`locals()`](https://docs.python.org/zh-cn/3.11/library/functions.html#locals) 函数描述的一样：不要试图改变默认的 *locals* 字典。 如果您需要在 [`exec()`](https://docs.python.org/zh-cn/3.11/library/functions.html#exec) 函数返回时查看代码对 *locals* 的影响，请明确地传递 *locals* 字典。*在 3.11 版更改:* Added the *closure* parameter.

## filter(function, iterable)

​	Construct an iterator from those elements of *iterable* for which *function* is true. *iterable* may be either a sequence, a container which supports iteration, or an iterator. If *function* is `None`, the identity function is assumed, that is, all elements of *iterable* that are false are removed.

​	请注意， `filter(function, iterable)` 相当于一个生成器表达式，当 function 不是 `None` 的时候为 `(item for item in iterable if function(item))`；function 是 `None` 的时候为 `(item for item in iterable if item)` 。

​	See [`itertools.filterfalse()`](https://docs.python.org/zh-cn/3.11/library/itertools.html#itertools.filterfalse) for the complementary function that returns elements of *iterable* for which *function* is false.

## class float(x=0.0)

​	返回从数字或字符串 *x* 生成的浮点数。

​	If the argument is a string, it should contain a decimal number, optionally preceded by a sign, and optionally embedded in whitespace. The optional sign may be `'+'` or `'-'`; a `'+'` sign has no effect on the value produced. The argument may also be a string representing a NaN (not-a-number), or positive or negative infinity. More precisely, the input must conform to the `floatvalue` production rule in the following grammar, after leading and trailing whitespace characters are removed:

```python
sign        ::=  "+" | "-"
infinity    ::=  "Infinity" | "inf"
nan         ::=  "nan"
digitpart   ::=  digit (["_"] digit)*
number      ::=  [digitpart] "." digitpart | digitpart ["."]
exponent    ::=  ("e" | "E") ["+" | "-"] digitpart
floatnumber ::=  number [exponent]
floatvalue  ::=  [sign] (floatnumber | infinity | nan)
```

​	Here `digit` is a Unicode decimal digit (character in the Unicode general category `Nd`). Case is not significant, so, for example, "inf", "Inf", "INFINITY", and "iNfINity" are all acceptable spellings for positive infinity.

​	另一方面，如果实参是整数或浮点数，则返回具有相同值（在 Python 浮点精度范围内）的浮点数。如果实参在 Python 浮点精度范围外，则会触发 [`OverflowError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#OverflowError)。对于一个普通 Python 对象 `x`，`float(x)` 会委托给 `x.__float__()`。 如果 `__float__()` 未定义则将回退至 `__index__()`。如果没有实参，则返回 `0.0` 。

示例:

```python
float('+1.23') # 1.23

float('   -12345\n') # -12345.0

float('1e-003') # 0.001

float('+1E6') # 1000000.0

float('-Infinity') # -inf
```

​	[数字类型 --- int, float, complex](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesnumeric) 描述了浮点类型。

​	*在 3.6 版更改:* 您可以使用下划线将代码文字中的数字进行分组。

​	*在 3.7 版更改:* *x* 现在只能作为位置参数。

​	*在 3.8 版更改:* 如果 `__float__()` 未定义则回退至 `__index__()`。



## format(value, format_spec='')

​	将 *value* 转换为"格式化后"的形式，格式由 *format_spec* 进行控制。*format_spec* 的解释方式取决于 *value* 参数的类型；但大多数内置类型使用一种标准的格式化语法： [格式规格迷你语言](https://docs.python.org/zh-cn/3.11/library/string.html#formatspec)。

​	默认的 *format_spec* 是一个空字符串，它通常给出与调用 [`str(value)`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#str) 相同的结果。

​	调用 `format(value, format_spec)` 会转换成 `type(value).__format__(value, format_spec)` ，所以实例字典中的 `__format__()` 方法将不会调用。如果方法搜索回退到 [`object`](https://docs.python.org/zh-cn/3.11/library/functions.html#object) 类但 *format_spec* 不为空，或者如果 *format_spec* 或返回值不是字符串，则会触发 [`TypeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#TypeError) 异常。

​	*在 3.4 版更改:* 当 *format_spec* 不是空字符串时， `object().__format__(format_spec)` 会触发 [`TypeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#TypeError)。



## class frozenset(iterable=set())

​	返回一个新的 [`frozenset`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#frozenset) 对象，它包含可选参数 *iterable* 中的元素。 `frozenset` 是一个内置的类。有关此类的文档，请参阅 [`frozenset`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#frozenset) 和 [集合类型 --- set, frozenset](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#types-set)。

​	请参阅内建的 [`set`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#set)、[`list`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#list)、[`tuple`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#tuple) 和 [`dict`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#dict) 类，以及 [`collections`](https://docs.python.org/zh-cn/3.11/library/collections.html#module-collections) 模块来了解其它的容器。

## getattr(object, name)

## getattr(object, name, default)

Return the value of the named attribute of *object*. *name* must be a string. If the string is the name of one of the object's attributes, the result is the value of that attribute. For example, `getattr(x, 'foobar')` is equivalent to `x.foobar`. If the named attribute does not exist, *default* is returned if provided, otherwise [`AttributeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#AttributeError) is raised. *name* need not be a Python identifier (see [`setattr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#setattr)).

> 备注 
>
> ​	由于 [私有名称混合](https://docs.python.org/zh-cn/3.11/reference/expressions.html#private-name-mangling) 发生在编译时，因此必须 手动混合私有属性（以两个下划线打头的属性）名称以使使用 [`getattr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#getattr) 来提取它。

## globals()

​	返回实现当前模块命名空间的字典。对于函数内的代码，这是在定义函数时设置的，无论函数在哪里被调用都保持不变。

## hasattr(object, name)

​	该实参是一个对象和一个字符串。如果字符串是对象的属性之一的名称，则返回 `True`，否则返回 `False`。（此功能是通过调用 `getattr(object, name)` 看是否有 [`AttributeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#AttributeError) 异常来实现的。）

## hash(object)

​	返回该对象的哈希值（如果它有的话）。哈希值是整数。它们在字典查找元素时用来快速比较字典的键。相同大小的数字变量有相同的哈希值（即使它们类型不同，如 1 和 1.0）。

> 备注 
>
> ​	如果对象实现了自己的 `__hash__()` 方法，请注意，[`hash()`](https://docs.python.org/zh-cn/3.11/library/functions.html#hash) 根据机器的字长来截断返回值。另请参阅 `__hash__()`。

## help()

## help(request)

​	启动内置的帮助系统（此函数主要在交互式中使用）。如果没有实参，解释器控制台里会启动交互式帮助系统。如果实参是一个字符串，则在模块、函数、类、方法、关键字或文档主题中搜索该字符串，并在控制台上打印帮助信息。如果实参是其他任意对象，则会生成该对象的帮助页。

​	请注意，如果在调用 [`help()`](https://docs.python.org/zh-cn/3.11/library/functions.html#help) 时，目标函数的形参列表中存在斜杠（/），则意味着斜杠之前的参数只能是位置参数。详情请参阅 [有关仅限位置形参的 FAQ 条目](https://docs.python.org/zh-cn/3.11/faq/programming.html#faq-positional-only-arguments)。

​	该函数通过 [`site`](https://docs.python.org/zh-cn/3.11/library/site.html#module-site) 模块加入到内置命名空间。

​	*在 3.4 版更改:* [`pydoc`](https://docs.python.org/zh-cn/3.11/library/pydoc.html#module-pydoc) 和 [`inspect`](https://docs.python.org/zh-cn/3.11/library/inspect.html#module-inspect) 的变更使得可调用对象的签名信息更加全面和一致。

## hex(x)

​	将整数转换为以"0x"为前缀的小写十六进制字符串。如果 *x* 不是 Python [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 对象，则必须定义返回整数的 `__index__()` 方法。一些例子：

```python
hex(255) # '0xff'

hex(-42) # '-0x2a'
```

​	如果要将整数转换为大写或小写的十六进制字符串，并可选择有无"0x"前缀，则可以使用如下方法：

```python
'%#x' % 255, '%x' % 255, '%X' % 255  # ('0xff', 'ff', 'FF')

format(255, '#x'), format(255, 'x'), format(255, 'X') # ('0xff', 'ff', 'FF')

f'{255:#x}', f'{255:x}', f'{255:X}' # ('0xff', 'ff', 'FF')
```

​	另见 [`format()`](https://docs.python.org/zh-cn/3.11/library/functions.html#format) 获取更多信息。

​	另请参阅 [`int()`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 将十六进制字符串转换为以 16 为基数的整数。

> 备注 
>
> ​	如果要获取浮点数的十六进制字符串形式，请使用 [`float.hex()`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#float.hex) 方法。

## id(object)

​	返回对象的"标识值"。该值是一个整数，在此对象的生命周期中保证是唯一且恒定的。两个生命期不重叠的对象可能具有相同的 [`id()`](https://docs.python.org/zh-cn/3.11/library/functions.html#id) 值。

​	**CPython 实现细节：** This is the address of the object in memory.

​	引发一个 [审计事件](https://docs.python.org/zh-cn/3.11/library/sys.html#auditing) `builtins.id`，附带参数 `id`。

## input()

## input(prompt)

​	如果存在 *prompt* 实参，则将其写入标准输出，末尾不带换行符。接下来，该函数从输入中读取一行，将其转换为字符串（除了末尾的换行符）并返回。当读取到 EOF 时，则触发 [`EOFError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#EOFError)。例如:

```python
s = input('--> ')   # --> Monty Python's Flying Circus

s  # "Monty Python's Flying Circus"
```

​	如果加载了 [`readline`](https://docs.python.org/zh-cn/3.11/library/readline.html#module-readline) 模块，[`input()`](https://docs.python.org/zh-cn/3.11/library/functions.html#input) 将使用它来提供复杂的行编辑和历史记录功能。

​	引发一个 [审计事件](https://docs.python.org/zh-cn/3.11/library/sys.html#auditing) `builtins.input` 附带参数 `prompt`。

​	在成功读取输入之后引发一个 [审计事件](https://docs.python.org/zh-cn/3.11/library/sys.html#auditing) `builtins.input/result` 附带结果。

## class int(x=0)

## class int(x, base=10)

​	返回一个基于数字或字符串 *x* 构造的整数对象，或者在未给出参数时返回 `0`。 如果 *x* 定义了 `__int__()`，`int(x)` 将返回 `x.__int__()`。 如果 *x* 定义了 `__index__()`，它将返回 `x.__index__()`。 如果 *x* 定义了 `__trunc__()`，它将返回 `x.__trunc__()`。 对于浮点数，它将向零舍入。

​	If *x* is not a number or if *base* is given, then *x* must be a string, [`bytes`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bytes), or [`bytearray`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bytearray) instance representing an integer in radix *base*. Optionally, the string can be preceded by `+` or `-` (with no space in between), have leading zeros, be surrounded by whitespace, and have single underscores interspersed between digits.

​	A base-n integer string contains digits, each representing a value from 0 to n-1. The values 0--9 can be represented by any Unicode decimal digit. The values 10--35 can be represented by `a` to `z` (or `A` to `Z`). The default *base* is 10. The allowed bases are 0 and 2--36. Base-2, -8, and -16 strings can be optionally prefixed with `0b`/`0B`, `0o`/`0O`, or `0x`/`0X`, as with integer literals in code. For base 0, the string is interpreted in a similar way to an [integer literal in code](https://docs.python.org/zh-cn/3.11/reference/lexical_analysis.html#integers), in that the actual base is 2, 8, 10, or 16 as determined by the prefix. Base 0 also disallows leading zeros: `int('010', 0)` is not legal, while `int('010')` and `int('010', 8)` are.

​	整数类型定义请参阅 [数字类型 --- int, float, complex](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesnumeric) 。

​	*在 3.4 版更改:* 如果 *base* 不是 [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 的实例，但 *base* 对象有 [`base.__index__`](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#object.__index__) 方法，则会调用该方法来获取进制数。以前的版本使用 [`base.__int__`](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#object.__int__) 而不是 [`base.__index__`](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#object.__index__)。

​	*在 3.6 版更改:* 您可以使用下划线将代码文字中的数字进行分组。

​	*在 3.7 版更改:* *x* 现在只能作为位置参数。

​	*在 3.8 版更改:* 如果 `__int__()` 未定义则回退至 `__index__()`。

​	*在 3.11 版更改:* The delegation to `__trunc__()` is deprecated.

​	*在 3.11 版更改:* [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) string inputs and string representations can be limited to help avoid denial of service attacks. A [`ValueError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#ValueError) is raised when the limit is exceeded while converting a string *x* to an [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) or when converting an [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) into a string would exceed the limit. See the [integer string conversion length limitation](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#int-max-str-digits) documentation.

## isinstance(object, classinfo)

Return `True` if the *object* argument is an instance of the *classinfo* argument, or of a (direct, indirect, or [virtual](https://docs.python.org/zh-cn/3.11/glossary.html#term-abstract-base-class)) subclass thereof. If *object* is not an object of the given type, the function always returns `False`. If *classinfo* is a tuple of type objects (or recursively, other such tuples) or a [union 类型](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#types-union) of multiple types, return `True` if *object* is an instance of any of the types. If *classinfo* is not a type or tuple of types and such tuples, a [`TypeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#TypeError) exception is raised. [`TypeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#TypeError) may not be raised for an invalid type if an earlier check succeeds.

​	*在 3.10 版更改:* *classinfo* 可以是一个 [union 类型](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#types-union)。

## issubclass(class, classinfo)

​	如果 *class* 是 *classinfo* 的子类（直接、间接或 [虚的](https://docs.python.org/zh-cn/3.11/glossary.html#term-abstract-base-class) ），则返回 `True`。类将视为自己的子类。*classinfo* 可为类对象的元组（或递归地，其他这样的元组）或 [union 类型](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#types-union)，这时如果 *class* 是 *classinfo* 中任何条目的子类，则返回 `True` 。任何其他情况都会触发 [`TypeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#TypeError) 异常。

​	*在 3.10 版更改:* *classinfo* 可以是一个 [union 类型](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#types-union)。

## iter(object)

## iter(object, sentinel)

​	返回一个 [iterator](https://docs.python.org/zh-cn/3.11/glossary.html#term-iterator) 对象。根据是否存在第二个实参，第一个实参的解释是非常不同的。如果没有第二个实参，*object* 必须是支持 [iterable](https://docs.python.org/zh-cn/3.11/glossary.html#term-iterable) 协议（有 `__iter__()` 方法）的集合对象，或必须支持序列协议（有 `__getitem__()` 方法，且数字参数从 `0` 开始）。如果它不支持这些协议，会触发 [`TypeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#TypeError)。如果有第二个实参 *sentinel*，那么 *object* 必须是可调用的对象。这种情况下生成的迭代器，每次迭代调用它的 [`__next__()`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#iterator.__next__) 方法时都会不带实参地调用 *object*；如果返回的结果是 *sentinel* 则触发 [`StopIteration`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#StopIteration)，否则返回调用结果。

​	另请参阅 [迭代器类型](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typeiter)。

​	适合 [`iter()`](https://docs.python.org/zh-cn/3.11/library/functions.html#iter) 的第二种形式的应用之一是构建块读取器。 例如，从二进制数据库文件中读取固定宽度的块，直至到达文件的末尾:

```python
from functools import partial
with open('mydata.db', 'rb') as f:
    for block in iter(partial(f.read, 64), b''):
        process_block(block)
```

## len(s)

​	返回对象的长度（元素个数）。实参可以是序列（如 string、bytes、tuple、list 或 range 等）或集合（如 dictionary、set 或 frozen set 等）。

​	**CPython 实现细节：** `len` 对于大于 [`sys.maxsize`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.maxsize) 的长度如 [`range(2 ** 100)`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#range) 会引发 [`OverflowError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#OverflowError)。



## class list

## class list(iterable)

​	虽然被称为函数，[`list`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#list) 实际上是一种可变序列类型，详情请参阅 [列表](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesseq-list) 和 [序列类型 --- list, tuple, range](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesseq)。

## locals()

​	更新并返回表示当前本地符号表的字典。 在函数代码块但不是类代码块中调用 [`locals()`](https://docs.python.org/zh-cn/3.11/library/functions.html#locals) 时将返回自由变量。 请注意在模块层级上，[`locals()`](https://docs.python.org/zh-cn/3.11/library/functions.html#locals) 和 [`globals()`](https://docs.python.org/zh-cn/3.11/library/functions.html#globals) 是同一个字典。

> 备注 
>
> ​	不要更改此字典的内容；更改不会影响解释器使用的局部变量或自由变量的值。

## map(function, iterable, *iterables)

​	Return an iterator that applies *function* to every item of *iterable*, yielding the results. If additional *iterables* arguments are passed, *function* must take that many arguments and is applied to the items from all iterables in parallel. With multiple iterables, the iterator stops when the shortest iterable is exhausted. For cases where the function inputs are already arranged into argument tuples, see [`itertools.starmap()`](https://docs.python.org/zh-cn/3.11/library/itertools.html#itertools.starmap).

## max(iterable, *, key=None)

## max(iterable, *, default, key=None)

## max(arg1, arg2, *args, key=None)

​	返回可迭代对象中最大的元素，或者返回两个及以上实参中最大的。

​	如果只提供了一个位置参数，它必须是非空 [iterable](https://docs.python.org/zh-cn/3.11/glossary.html#term-iterable)，返回可迭代对象中最大的元素；如果提供了两个及以上的位置参数，则返回最大的位置参数。

​	有两个可选只能用关键字的实参。*key* 实参指定排序函数用的参数，如传给 [`list.sort()`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#list.sort) 的。*default* 实参是当可迭代对象为空时返回的值。如果可迭代对象为空，并且没有给 *default* ，则会触发 [`ValueError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#ValueError)。

​	如果有多个最大元素，则此函数将返回第一个找到的。这和其他稳定排序工具如 `sorted(iterable, key=keyfunc, reverse=True)[0]` 和 `heapq.nlargest(1, iterable, key=keyfunc)` 保持一致。

​	*3.4 新版功能:* keyword-only 实参 *default* 。

​	*在 3.8 版更改:* *key* 可以为 `None`。



## class memoryview(object)

​	返回由给定实参创建的"内存视图"对象。有关详细信息，请参阅 [内存视图](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typememoryview)。

## min(iterable, *, key=None)

## min(iterable, *, default, key=None)

## min(arg1, arg2, *args, key=None)

​	返回可迭代对象中最小的元素，或者返回两个及以上实参中最小的。

​	如果只提供了一个位置参数，它必须是 [iterable](https://docs.python.org/zh-cn/3.11/glossary.html#term-iterable)，返回可迭代对象中最小的元素；如果提供了两个及以上的位置参数，则返回最小的位置参数。

​	有两个可选只能用关键字的实参。*key* 实参指定排序函数用的参数，如传给 [`list.sort()`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#list.sort) 的。*default* 实参是当可迭代对象为空时返回的值。如果可迭代对象为空，并且没有给 *default* ，则会触发 [`ValueError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#ValueError)。

​	如果有多个最小元素，则此函数将返回第一个找到的。这和其他稳定排序工具如 `sorted(iterable, key=keyfunc)[0]` 和 `heapq.nsmallest(1, iterable, key=keyfunc)` 保持一致。

​	*3.4 新版功能:* keyword-only 实参 *default* 。*在 3.8 版更改:* *key* 可以为 `None`。

## next(iterator)

## next(iterator, default)

​	通过调用 [iterator](https://docs.python.org/zh-cn/3.11/glossary.html#term-iterator) 的 [`__next__()`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#iterator.__next__) 方法获取下一个元素。如果迭代器耗尽，则返回给定的 *default*，如果没有默认值则触发 [`StopIteration`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#StopIteration)。

## class object

​	返回一个不带特征的新对象。[`object`](https://docs.python.org/zh-cn/3.11/library/functions.html#object) 是所有类的基类。它带有所有 Python 类实例均通用的方法。本函数不接受任何参数。

> 备注 
>
> ​	由于 [`object`](https://docs.python.org/zh-cn/3.11/library/functions.html#object) 没有 [`__dict__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#object.__dict__)，因此无法将任意属性赋给 [`object`](https://docs.python.org/zh-cn/3.11/library/functions.html#object) 的实例。

## oct(x)

​	将一个整数转变为一个前缀为"0o"的八进制字符串。结果是一个合法的 Python 表达式。如果 *x* 不是 Python 的 [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 对象，那它需要定义 `__index__()` 方法返回一个整数。一些例子：

```python
oct(8) # '0o10'

oct(-56) # '-0o70'
```

​	若要将整数转换为八进制字符串，并可选择是否带有"0o"前缀，可采用如下方法：

```python
'%#o' % 10, '%o' % 10 # ('0o12', '12')

format(10, '#o'), format(10, 'o') # ('0o12', '12')

f'{10:#o}', f'{10:o}' # ('0o12', '12')
```

​	另见 [`format()`](https://docs.python.org/zh-cn/3.11/library/functions.html#format) 获取更多信息。

## open(file, mode='r', buffering=- 1, encoding=None, errors=None, newline=None, closefd=True, opener=None)

​	打开 *file* 并返回对应的 [file object](https://docs.python.org/zh-cn/3.11/glossary.html#term-file-object)。 如果该文件不能被打开，则引发 [`OSError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#OSError)。 请参阅 [读写文件](https://docs.python.org/zh-cn/3.11/tutorial/inputoutput.html#tut-files) 获取此函数的更多用法示例。*file* 是一个 [path-like object](https://docs.python.org/zh-cn/3.11/glossary.html#term-path-like-object)，表示将要打开的文件的路径（绝对路径或者相对当前工作目录的路径），也可以是要封装文件对应的整数类型文件描述符。（如果给出的是文件描述符，则当返回的 I/O 对象关闭时它也会关闭，除非将 *closefd* 设为 `False` 。）

​	*mode* is an optional string that specifies the mode in which the file is opened. It defaults to `'r'` which means open for reading in text mode. Other common values are `'w'` for writing (truncating the file if it already exists), `'x'` for exclusive creation, and `'a'` for appending (which on *some* Unix systems, means that *all* writes append to the end of the file regardless of the current seek position). In text mode, if *encoding* is not specified the encoding used is platform-dependent: [`locale.getencoding()`](https://docs.python.org/zh-cn/3.11/library/locale.html#locale.getencoding) is called to get the current locale encoding. (For reading and writing raw bytes use binary mode and leave *encoding* unspecified.) The available modes are:

| 字符  | 含意                                       |
| :---- | :----------------------------------------- |
| `'r'` | 读取（默认）                               |
| `'w'` | 写入，并先截断文件                         |
| `'x'` | 排它性创建，如果文件已存在则失败           |
| `'a'` | 打开文件用于写入，如果文件存在则在末尾追加 |
| `'b'` | 二进制模式                                 |
| `'t'` | 文本模式（默认）                           |
| `'+'` | 打开用于更新（读取与写入）                 |

​	默认模式为 `'r'` （打开文件用于读取文本，与 `'rt'` 同义）。`'w+'` 和 `'w+b'` 模式将打开文件并清空内容。而 `'r+'` 和 `'r+b'` 模式将打开文件但不清空内容。

​	正如在 [概述](https://docs.python.org/zh-cn/3.11/library/io.html#io-overview) 中提到的，Python区分二进制和文本I/O。以二进制模式打开的文件（包括 *mode* 参数中的 `'b'` ）返回的内容为 [`bytes`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bytes) 对象，不进行任何解码。在文本模式下（默认情况下，或者在 *mode* 参数中包含 `'t'` ）时，文件内容返回为 [`str`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#str) ，首先使用指定的 *encoding* （如果给定）或者使用平台默认的的字节编码解码。

> 备注 
>
> ​	Python不依赖于底层操作系统的文本文件概念;所有处理都由Python本身完成，因此与平台无关。

​	*buffering* 是一个可选的整数，用于设置缓冲策略。 传入 0 来关闭缓冲（只允许在二进制模式下），传入 1 来选择行缓冲（只在文本模式下可用），传入一个整数 > 1 来表示固定大小的块缓冲区的字节大小。注意，这样指定缓冲区的大小适用于二进制缓冲的 I/O ，但 `TextIOWrapper` （即用 `mode='r+'` 打开的文件）会有另一种缓冲。要禁用在 `TextIOWrapper` 缓冲，考虑使用 [`io.TextIOWrapper.reconfigure()`](https://docs.python.org/zh-cn/3.11/library/io.html#io.TextIOWrapper.reconfigure) 的 `write_through` 标志来。当没有给出 *buffering* 参数时，默认的缓冲策略工作如下。

- 二进制文件以固定大小的块进行缓冲；使用启发式方法选择缓冲区的大小，尝试确定底层设备的"块大小"或使用 [`io.DEFAULT_BUFFER_SIZE`](https://docs.python.org/zh-cn/3.11/library/io.html#io.DEFAULT_BUFFER_SIZE)。在许多系统上，缓冲区的长度通常为4096或8192字节。

- "交互式"文本文件（ [`isatty()`](https://docs.python.org/zh-cn/3.11/library/io.html#io.IOBase.isatty) 返回 `True` 的文件）使用行缓冲。其他文本文件使用上述策略用于二进制文件。

  

​	*encoding* is the name of the encoding used to decode or encode the file. This should only be used in text mode. The default encoding is platform dependent (whatever [`locale.getencoding()`](https://docs.python.org/zh-cn/3.11/library/locale.html#locale.getencoding) returns), but any [text encoding](https://docs.python.org/zh-cn/3.11/glossary.html#term-text-encoding) supported by Python can be used. See the [`codecs`](https://docs.python.org/zh-cn/3.11/library/codecs.html#module-codecs) module for the list of supported encodings.

​	*errors* 是一个可选的字符串参数，用于指定如何处理编码和解码错误 - 这不能在二进制模式下使用。可以使用各种标准错误处理程序（列在 [错误处理方案](https://docs.python.org/zh-cn/3.11/library/codecs.html#error-handlers) ），但是使用 [`codecs.register_error()`](https://docs.python.org/zh-cn/3.11/library/codecs.html#codecs.register_error) 注册的任何错误处理名称也是有效的。标准名称包括:

- 如果存在编码错误，`'strict'` 会引发 [`ValueError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#ValueError) 异常。 默认值 `None` 具有相同的效果。

- `'ignore'` 忽略错误。请注意，忽略编码错误可能会导致数据丢失。

- `'replace'` 会将替换标记（例如 `'?'` ）插入有错误数据的地方。

- `'surrogateescape'` 将把任何不正确的字节表示为 U+DC80 至 U+DCFF 范围内的下方替代码位。 当在写入数据时使用 `surrogateescape` 错误处理句柄时这些替代码位会被转回到相同的字节。 这适用于处理具有未知编码格式的文件。

- 只有在写入文件时才支持 `'xmlcharrefreplace'`。编码不支持的字符将替换为相应的XML字符引用 `&#nnn;`。

- `'backslashreplace'` 用Python的反向转义序列替换格式错误的数据。

- `'namereplace'` （也只在编写时支持）用 `\N{...}` 转义序列替换不支持的字符。

​	*newline* determines how to parse newline characters from the stream. It can be `None`, `''`, `'\n'`, `'\r'`, and `'\r\n'`. It works as follows:

- 从流中读取输入时，如果 *newline* 为 `None`，则启用通用换行模式。输入中的行可以以 `'\n'`，`'\r'` 或 `'\r\n'` 结尾，这些行被翻译成 `'\n'` 在返回呼叫者之前。如果它是 `''`，则启用通用换行模式，但行结尾将返回给调用者未翻译。如果它具有任何其他合法值，则输入行仅由给定字符串终止，并且行结尾将返回给未调用的调用者。

- 将输出写入流时，如果 *newline* 为 `None`，则写入的任何 `'\n'` 字符都将转换为系统默认行分隔符 [`os.linesep`](https://docs.python.org/zh-cn/3.11/library/os.html#os.linesep)。如果 *newline* 是 `''` 或 `'\n'`，则不进行翻译。如果 *newline* 是任何其他合法值，则写入的任何 `'\n'` 字符将被转换为给定的字符串。

​	如果 *closefd* 为 `False` 且给出的不是文件名而是文件描述符，那么当文件关闭时，底层文件描述符将保持打开状态。如果给出的是文件名，则 *closefd* 必须为 `True` （默认值），否则将触发错误。

​	可以通过传递可调用的 *opener* 来使用自定义开启器。然后通过使用参数（ *file*，*flags* ）调用 *opener* 获得文件对象的基础文件描述符。 *opener* 必须返回一个打开的文件描述符（使用 [`os.open`](https://docs.python.org/zh-cn/3.11/library/os.html#os.open) as *opener* 时与传递 `None` 的效果相同）。

​	新创建的文件是 [不可继承的](https://docs.python.org/zh-cn/3.11/library/os.html#fd-inheritance)。

​	下面的示例使用 [`os.open()`](https://docs.python.org/zh-cn/3.11/library/os.html#os.open) 函数的 [dir_fd](https://docs.python.org/zh-cn/3.11/library/os.html#dir-fd) 的形参，从给定的目录中用相对路径打开文件:

```python
import os
dir_fd = os.open('somedir', os.O_RDONLY)
def opener(path, flags):
    return os.open(path, flags, dir_fd=dir_fd)

with open('spamspam.txt', 'w', opener=opener) as f:
    print('This will be written to somedir/spamspam.txt', file=f)

os.close(dir_fd)  # don't leak a file descriptor
```

​	[`open()`](https://docs.python.org/zh-cn/3.11/library/functions.html#open) 函数所返回的 [file object](https://docs.python.org/zh-cn/3.11/glossary.html#term-file-object) 类型取决于所用模式。 当使用 [`open()`](https://docs.python.org/zh-cn/3.11/library/functions.html#open) 以文本模式 (`'w'`, `'r'`, `'wt'`, `'rt'` 等) 打开文件时，它将返回 [`io.TextIOBase`](https://docs.python.org/zh-cn/3.11/library/io.html#io.TextIOBase) (具体为 [`io.TextIOWrapper`](https://docs.python.org/zh-cn/3.11/library/io.html#io.TextIOWrapper)) 的一个子类。 当使用缓冲以二进制模式打开文件时，返回的类是 [`io.BufferedIOBase`](https://docs.python.org/zh-cn/3.11/library/io.html#io.BufferedIOBase) 的一个子类。 具体的类会有多种：在只读的二进制模式下，它将返回 [`io.BufferedReader`](https://docs.python.org/zh-cn/3.11/library/io.html#io.BufferedReader)；在写入二进制和追加二进制模式下，它将返回 [`io.BufferedWriter`](https://docs.python.org/zh-cn/3.11/library/io.html#io.BufferedWriter)，而在读/写模式下，它将返回 [`io.BufferedRandom`](https://docs.python.org/zh-cn/3.11/library/io.html#io.BufferedRandom)。 当禁用缓冲时，则会返回原始流，即 [`io.RawIOBase`](https://docs.python.org/zh-cn/3.11/library/io.html#io.RawIOBase) 的一个子类 [`io.FileIO`](https://docs.python.org/zh-cn/3.11/library/io.html#io.FileIO)。

​	另请参阅文件操作模块，如 [`fileinput`](https://docs.python.org/zh-cn/3.11/library/fileinput.html#module-fileinput)、[`io`](https://docs.python.org/zh-cn/3.11/library/io.html#module-io) （声明了 [`open()`](https://docs.python.org/zh-cn/3.11/library/functions.html#open)）、[`os`](https://docs.python.org/zh-cn/3.11/library/os.html#module-os)、[`os.path`](https://docs.python.org/zh-cn/3.11/library/os.path.html#module-os.path)、[`tempfile`](https://docs.python.org/zh-cn/3.11/library/tempfile.html#module-tempfile) 和 [`shutil`](https://docs.python.org/zh-cn/3.11/library/shutil.html#module-shutil)。

​	引发一个 [审计事件](https://docs.python.org/zh-cn/3.11/library/sys.html#auditing) `open` 附带参数 `file`, `mode`, `flags`。

​	`mode` 与 `flags` 参数可以在原始调用的基础上被修改或传递。

​	*在 3.3 版更改:*

- 增加了 *opener* 形参。
- 增加了 `'x'` 模式。
- 过去触发的 [`IOError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#IOError)，现在是 [`OSError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#OSError) 的别名。
- 如果文件已存在但使用了排它性创建模式（ `'x'` ），现在会触发 [`FileExistsError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#FileExistsError)。

​	*在 3.4 版更改:*

- 文件现在禁止继承。

​	*在 3.5 版更改:*

- 如果系统调用被中断，但信号处理程序没有触发异常，此函数现在会重试系统调用，而不是触发 [`InterruptedError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#InterruptedError) 异常 (原因详见 [**PEP 475**](https://peps.python.org/pep-0475/))。
- 增加了 `'namereplace'` 错误处理接口。

​	*在 3.6 版更改:*

- 增加对实现了 [`os.PathLike`](https://docs.python.org/zh-cn/3.11/library/os.html#os.PathLike) 对象的支持。
- 在 Windows 上，打开一个控制台缓冲区将返回 [`io.RawIOBase`](https://docs.python.org/zh-cn/3.11/library/io.html#io.RawIOBase) 的子类，而不是 [`io.FileIO`](https://docs.python.org/zh-cn/3.11/library/io.html#io.FileIO)。

​	*在 3.11 版更改:* The `'U'` mode has been removed.

## ord(c)

​	对表示单个 Unicode 字符的字符串，返回代表它 Unicode 码点的整数。例如 `ord('a')` 返回整数 `97`， `ord('€')` （欧元符号）返回 `8364` 。这是 [`chr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#chr) 的逆函数。

## pow(base, exp, mod=None)

​	返回 *base* 的 *exp* 次幂；如果 *mod* 存在，则返回 *base* 的 *exp* 次幂对 *mod* 取余（比 `pow(base, exp) % mod` 更高效）。 两参数形式 `pow(base, exp)` 等价于乘方运算符: `base**exp`。

​	参数必须为数值类型。 对于混用的操作数类型，则适用二元算术运算符的类型强制转换规则。 对于 [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 操作数，结果具有与操作数相同的类型（转换后），除非第二个参数为负值；在这种情况下，所有参数将被转换为浮点数并输出浮点数结果。 例如，`pow(10, 2)` 返回 `100`，但 `pow(10, -2)` 返回 `0.01`。 对于 [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 或 [`float`](https://docs.python.org/zh-cn/3.11/library/functions.html#float) 类型的负基和一个非整数的指数，会产生一个复杂的结果。 例如， `pow(-9, 0.5)` 返回一个接近于 `3j` 的值。

​	对于 [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 操作数 *base* 和 *exp*，如果给出 *mod*，则 *mod* 必须为整数类型并且 *mod* 必须不为零。 如果给出 *mod* 并且 *exp* 为负值，则 *base* 必须相对于 *mod* 不可整除。 在这种情况下，将会返回 `pow(inv_base, -exp, mod)`，其中 *inv_base* 为 *base* 的倒数对 *mod* 取余。下面的例子是 `38` 的倒数对 `97` 取余:

```python
pow(38, -1, mod=97) # 23

23 * 38 % 97 == 1 # True
```

​	*在 3.8 版更改:* 对于 [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 操作数，三参数形式的 `pow` 现在允许第二个参数为负值，即可以计算倒数的余数。

​	*在 3.8 版更改:* 允许关键字参数。 之前只支持位置参数。

## print(*objects, sep=' ', end='\n', file=None, flush=False)

​	将 *objects* 打印输出至 *file* 指定的文本流，以 *sep* 分隔并在末尾加上 *end*。 *sep* 、 *end* 、 *file* 和 *flush* 必须以关键字参数的形式给出。

​	所有非关键字参数都会被转换为字符串，就像是执行了 [`str()`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#str) 一样，并会被写入到流，以 *sep* 且在末尾加上 *end*。 *sep* 和 *end* 都必须为字符串；它们也可以为 `None`，这意味着使用默认值。 如果没有给出 *objects*，则 [`print()`](https://docs.python.org/zh-cn/3.11/library/functions.html#print) 将只写入 *end*。

​	*file* 参数必须是一个具有 `write(string)` 方法的对象；如果参数不存在或为 `None`，则将使用 [`sys.stdout`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.stdout)。 由于要打印的参数会被转换为文本字符串，因此 [`print()`](https://docs.python.org/zh-cn/3.11/library/functions.html#print) 不能用于二进制模式的文件对象。 对于这些对象，应改用 `file.write(...)`。

​	Output buffering is usually determined by *file*. However, if *flush* is true, the stream is forcibly flushed.

​	*在 3.3 版更改:* 增加了 *flush* 关键字参数。

## class property(fget=None, fset=None, fdel=None, doc=None)

​	返回 property 属性。*fget* 是获取属性值的函数。 *fset* 是用于设置属性值的函数。 *fdel* 是用于删除属性值的函数。并且 *doc* 为属性对象创建文档字符串。一个典型的用法是定义一个托管属性 `x`:

```python
class C:
    def __init__(self):
        self._x = None

    def getx(self):
        return self._x

    def setx(self, value):
        self._x = value

    def delx(self):
        del self._x

    x = property(getx, setx, delx, "I'm the 'x' property.")
```

​	如果 *c* 为 *C* 的实例，`c.x` 将调用 getter，`c.x = value` 将调用 setter， `del c.x` 将调用 deleter。

​	如果给出，*doc* 将成为该 property 属性的文档字符串。 否则该 property 将拷贝 *fget* 的文档字符串（如果存在）。 这令使用 [`property()`](https://docs.python.org/zh-cn/3.11/library/functions.html#property) 作为 [decorator](https://docs.python.org/zh-cn/3.11/glossary.html#term-decorator) 来创建只读的特征属性可以很容易地实现:

```python
class Parrot:
    def __init__(self):
        self._voltage = 100000

    @property
    def voltage(self):
        """Get the current voltage."""
        return self._voltage
```

​	以上 `@property` 装饰器会将 `voltage()` 方法转化为一个具有相同名称的只读属性的 "getter"，并将 *voltage* 的文档字符串设置为 "Get the current voltage."

​	特征属性对象具有 `getter`, `setter` 以及 `deleter` 方法，它们可用作装饰器来创建该特征属性的副本，并将相应的访问函数设为所装饰的函数。 这最好是用一个例子来解释:

```python
class C:
    def __init__(self):
        self._x = None

    @property
    def x(self):
        """I'm the 'x' property."""
        return self._x

    @x.setter
    def x(self, value):
        self._x = value

    @x.deleter
    def x(self):
        del self._x
```

​	上述代码与第一个例子完全等价。 注意一定要给附加函数与原始的特征属性相同的名称 (在本例中为 `x`。)

​	返回的特征属性对象同样具有与构造器参数相对应的属性 `fget`, `fset` 和 `fdel`。

​	*在 3.5 版更改:* 特征属性对象的文档字符串现在是可写的。

## class range(stop)

## class range(start, stop, step=1)

​	虽然被称为函数，但 [`range`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#range) 实际上是一个不可变的序列类型，参见在 [range 对象](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesseq-range) 与 [序列类型 --- list, tuple, range](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesseq) 中的文档说明。

## repr(object)

Return a string containing a printable representation of an object. For many types, this function makes an attempt to return a string that would yield an object with the same value when passed to [`eval()`](https://docs.python.org/zh-cn/3.11/library/functions.html#eval); otherwise, the representation is a string enclosed in angle brackets that contains the name of the type of the object together with additional information often including the name and address of the object. A class can control what this function returns for its instances by defining a `__repr__()` method. If [`sys.displayhook()`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.displayhook) is not accessible, this function will raise [`RuntimeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#RuntimeError).

## reversed(seq)

​	返回一个反向的 [iterator](https://docs.python.org/zh-cn/3.11/glossary.html#term-iterator)。 *seq* 必须是一个具有 `__reversed__()` 方法的对象或者是支持该序列协议（具有从 `0` 开始的整数类型参数的 `__len__()` 方法和 `__getitem__()` 方法）。

## round(number, ndigits=None)

​	返回 *number* 舍入到小数点后 *ndigits* 位精度的值。 如果 *ndigits* 被省略或为 `None`，则返回最接近输入值的整数。

​	对于支持 [`round()`](https://docs.python.org/zh-cn/3.11/library/functions.html#round) 方法的内置类型，结果值会舍入至最接近的 10 的负 *ndigits* 次幂的倍数；如果与两个倍数同样接近，则选用偶数。因此，`round(0.5)` 和 `round(-0.5)` 均得出 `0` 而 `round(1.5)` 则为 `2`。*ndigits* 可为任意整数值（正数、零或负数）。如果省略了 *ndigits* 或为 `None` ，则返回值将为整数。否则返回值与 *number* 的类型相同。

​	对于一般的 Python 对象 `number`, `round` 将委托给 `number.__round__`。

> 备注 
>
> ​	对浮点数执行 [`round()`](https://docs.python.org/zh-cn/3.11/library/functions.html#round) 的行为可能会令人惊讶：例如，`round(2.675, 2)` 将给出 `2.67` 而不是期望的 `2.68`。 这不算是程序错误：这一结果是由于大多数十进制小数实际上都不能以浮点数精确地表示。 请参阅 [浮点算术：争议和限制](https://docs.python.org/zh-cn/3.11/tutorial/floatingpoint.html#tut-fp-issues) 了解更多信息。



## class set

## class set(iterable)

​	返回一个新的 [`set`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#set) 对象，可以选择带有从 *iterable* 获取的元素。 `set` 是一个内置类型。 请查看 [`set`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#set) 和 [集合类型 --- set, frozenset](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#types-set) 获取关于这个类的文档。

​	有关其他容器请参看内置的 [`frozenset`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#frozenset), [`list`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#list), [`tuple`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#tuple) 和 [`dict`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#dict) 类，以及 [`collections`](https://docs.python.org/zh-cn/3.11/library/collections.html#module-collections) 模块。

## setattr(object, name, value)

​	本函数与 [`getattr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#getattr) 相对应。其参数为一个对象、一个字符串和一个任意值。字符串可以为某现有属性的名称，或为新属性。只要对象允许，函数会将值赋给属性。如 `setattr(x, 'foobar', 123)` 等价于 `x.foobar = 123`。

​	*name* need not be a Python identifier as defined in [标识符和关键字](https://docs.python.org/zh-cn/3.11/reference/lexical_analysis.html#identifiers) unless the object chooses to enforce that, for example in a custom [`__getattribute__()`](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#object.__getattribute__) or via [`__slots__`](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#object.__slots__). An attribute whose name is not an identifier will not be accessible using the dot notation, but is accessible through [`getattr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#getattr) etc..

> 备注 
>
> ​	由于 [私有名称混合](https://docs.python.org/zh-cn/3.11/reference/expressions.html#private-name-mangling) 发生在编译时，因此必须手动混合私有属性（以两个下划线打头的属性）名称以便使用 [`setattr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#setattr) 来设置它。

## class slice(stop)

## class slice(start, stop, step=1)

​	返回一个 [slice](https://docs.python.org/zh-cn/3.11/glossary.html#term-slice) 对象，代表由 `range(start, stop, step)` 指定索引集的切片。 其中参数 *start* 和 *step* 的默认值为 `None`。切片对象具有只读数据属性 `start` 、`stop` 和 `step`，只是返回对应的参数值（或默认值）。这几个属性没有其他明确的功能；不过 NumPy 和其他第三方扩展会用到。在使用扩展索引语法时，也会生成切片对象。例如： `a[start:stop:step]` 或 `a[start:stop, i]`。 另一种方案是返回迭代器对象，可参阅 [`itertools.islice()`](https://docs.python.org/zh-cn/3.11/library/itertools.html#itertools.islice) 。

## sorted(iterable, /, *, key=None, reverse=False)

​	根据 *iterable* 中的项返回一个新的已排序列表。

​	具有两个可选参数，它们都必须指定为关键字参数。

​	*key* 指定带有单个参数的函数，用于从 *iterable* 的每个元素中提取用于比较的键 (例如 `key=str.lower`)。 默认值为 `None` (直接比较元素)。

​	*reverse* 为一个布尔值。 如果设为 `True`，则每个列表元素将按反向顺序比较进行排序。

​	使用 [`functools.cmp_to_key()`](https://docs.python.org/zh-cn/3.11/library/functools.html#functools.cmp_to_key) 可将老式的 *cmp* 函数转换为 *key* 函数。

​	内置的 [`sorted()`](https://docs.python.org/zh-cn/3.11/library/functions.html#sorted) 确保是稳定的。 如果一个排序确保不会改变比较结果相等的元素的相对顺序就称其为稳定的 --- 这有利于进行多重排序（例如先按部门、再按薪级排序）。

​	排序算法只使用 `<` 在项目之间比较。 虽然定义一个 [`__lt__()`](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#object.__lt__) 方法就足以进行排序，但 [**PEP 8**](https://peps.python.org/pep-0008/) 建议实现所有六个 [富比较](https://docs.python.org/zh-cn/3.11/reference/expressions.html#comparisons) 。 这将有助于避免在与其他排序工具（如 [`max()`](https://docs.python.org/zh-cn/3.11/library/functions.html#max) ）使用相同的数据时出现错误，这些工具依赖于不同的底层方法。实现所有六个比较也有助于避免混合类型比较的混乱，因为混合类型比较可以调用反射到 [`__gt__()`](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#object.__gt__) 的方法。

​	有关排序示例和简要排序教程，请参阅 [排序指南](https://docs.python.org/zh-cn/3.11/howto/sorting.html#sortinghowto) 。

## @staticmethod

​	将方法转换为静态方法。静态方法不会接收隐式的第一个参数。要声明一个静态方法，请使用此语法

```python
class C:
    @staticmethod
    def f(arg1, arg2, argN): ...
```

​	`@staticmethod`这样的形式称为函数的 [decorator](https://docs.python.org/zh-cn/3.11/glossary.html#term-decorator) -- 详情参阅 [函数定义](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#function)。

​	静态方法既可以由类中调用（如 `C.f()`），也可以由实例中调用（如```C().f()``）。此外，还可以作为普通的函数进行调用（如``f()``）。

​	Python 的静态方法与 Java 或 C++ 类似。另请参阅 [`classmethod()`](https://docs.python.org/zh-cn/3.11/library/functions.html#classmethod) ，可用于创建另一种类构造函数。

​	像所有装饰器一样，也可以像常规函数一样调用 `staticmethod` ，并对其结果执行某些操作。比如某些情况下需要从类主体引用函数并且您希望避免自动转换为实例方法。对于这些情况，请使用此语法:

```python
def regular_function():
    ...

class C:
    method = staticmethod(regular_function)
```

​	想了解更多有关静态方法的信息，请参阅 [标准类型层级结构](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#types) 。

​	*在 3.10 版更改:* 静态方法继承了方法的多个属性（`__module__`、`__name__`、`__qualname__`、`__doc__` 和 `__annotations__`），还拥有一个新的``__wrapped__`` 属性，并且现在还可以作为普通函数进行调用。



## class str(object='')

## class str(object=b'', encoding='utf-8', errors='strict')

​	返回一个 [`str`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#str) 版本的 *object* 。有关详细信息，请参阅 [`str()`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#str) 。

​	`str` 是内置字符串 [class](https://docs.python.org/zh-cn/3.11/glossary.html#term-class) 。更多关于字符串的信息查看 [文本序列类型 --- str](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#textseq)。

## sum(iterable, /, start=0)

​	从 *start* 开始自左向右对 *iterable* 的项求和并返回总计值。 *iterable* 的项通常为数字，而 start 值则不允许为字符串。

​	对某些用例来说，存在 [`sum()`](https://docs.python.org/zh-cn/3.11/library/functions.html#sum) 的更好替代。 拼接字符串序列的更好更快方式是调用 `''.join(sequence)`。 要以扩展精度对浮点值求和，请参阅 [`math.fsum()`](https://docs.python.org/zh-cn/3.11/library/math.html#math.fsum)。 要拼接一系列可迭代对象，请考虑使用 [`itertools.chain()`](https://docs.python.org/zh-cn/3.11/library/itertools.html#itertools.chain)。

​	*在 3.8 版更改:* *start* 形参可用关键字参数形式来指定。

## class super

## class super(type, object_or_type=None)

​	返回一个代理对象，它会将方法调用委托给 *type* 的父类或兄弟类。 这对于访问已在类中被重载的继承方法很有用。

​	The *object_or_type* determines the [method resolution order](https://docs.python.org/zh-cn/3.11/glossary.html#term-method-resolution-order) to be searched. The search starts from the class right after the *type*.

​	For example, if [`__mro__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#class.__mro__) of *object_or_type* is `D -> B -> C -> A -> object` and the value of *type* is `B`, then [`super()`](https://docs.python.org/zh-cn/3.11/library/functions.html#super) searches `C -> A -> object`.

​	The [`__mro__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#class.__mro__) attribute of the *object_or_type* lists the method resolution search order used by both [`getattr()`](https://docs.python.org/zh-cn/3.11/library/functions.html#getattr) and [`super()`](https://docs.python.org/zh-cn/3.11/library/functions.html#super). The attribute is dynamic and can change whenever the inheritance hierarchy is updated.

​	如果省略第二个参数，则返回的超类对象是未绑定的。 如果第二个参数为一个对象，则 `isinstance(obj, type)` 必须为真值。 如果第二个参数为一个类型，则 `issubclass(type2, type)` 必须为真值（这适用于类方法）。

​	*super* 有两个典型用例。 在具有单继承的类层级结构中，*super* 可用来引用父类而不必显式地指定它们的名称，从而令代码更易维护。 这种用法与其他编程语言中 *super* 的用法非常相似。

​	第二个用例是在动态执行环境中支持协作多重继承。 此用例为 Python 所独有而不存在于静态编码语言或仅支持单继承的语言当中。 这使用实现"菱形图"成为可能，即有多个基类实现相同的方法。 好的设计强制要求这样的方法在每个情况下都具有相同的调用签名（因为调用顺序是在运行时确定的，也因为这个顺序要适应类层级结构的更改，还因为这个顺序可能包括在运行时之前未知的兄弟类）。

​	对于以上两个用例，典型的超类调用看起来是这样的:

```python
class C(B):
    def method(self, arg):
        super().method(arg)    # This does the same thing as:
                               # super(C, self).method(arg)
```

​	除了方法查找之外，[`super()`](https://docs.python.org/zh-cn/3.11/library/functions.html#super) 也可用于属性查找。 一个可能的应用场合是在上级或同级类中调用 [描述器](https://docs.python.org/zh-cn/3.11/glossary.html#term-descriptor)。

​	请注意 [`super()`](https://docs.python.org/zh-cn/3.11/library/functions.html#super) 是作为显式加点属性查找的绑定过程的一部分来实现的，例如 `super().__getitem__(name)`。 它做到这一点是通过实现自己的 `__getattribute__()` 方法，这样就能以可预测的顺序搜索类，并且支持协作多重继承。 对应地，[`super()`](https://docs.python.org/zh-cn/3.11/library/functions.html#super) 在像 `super()[name]` 这样使用语句或操作符进行隐式查找时则未被定义。

​	还要注意的是，除了零个参数的形式以外，[`super()`](https://docs.python.org/zh-cn/3.11/library/functions.html#super) 并不限于在方法内部使用。 两个参数的形式明确指定参数并进行相应的引用。 零个参数的形式仅适用于类定义内部，因为编译器需要填入必要的细节以正确地检索到被定义的类，还需要让普通方法访问当前实例。

​	对于有关如何使用 [`super()`](https://docs.python.org/zh-cn/3.11/library/functions.html#super) 来如何设计协作类的实用建议，请参阅 [使用 super() 的指南](https://rhettinger.wordpress.com/2011/05/26/super-considered-super/)。



## class tuple

## class tuple(iterable)

​	虽然被称为函数，但 [`tuple`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#tuple) 实际上是一个不可变的序列类型，参见在 [元组](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesseq-tuple) 与 [序列类型 --- list, tuple, range](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#typesseq) 中的文档说明。

## class type(object)

## class type(name, bases, dict, **kwds)

​	传入一个参数时，返回 *object* 的类型。 返回值是一个 type 对象，通常与 [`object.__class__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#instance.__class__) 所返回的对象相同。

​	推荐使用 [`isinstance()`](https://docs.python.org/zh-cn/3.11/library/functions.html#isinstance) 内置函数来检测对象的类型，因为它会考虑子类的情况。

​	传入三个参数时，返回一个新的 type 对象。 这在本质上是 [`class`](https://docs.python.org/zh-cn/3.11/reference/compound_stmts.html#class) 语句的一种动态形式，*name* 字符串即类名并会成为 [`__name__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#definition.__name__) 属性；*bases* 元组包含基类并会成为 [`__bases__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#class.__bases__) 属性；如果为空则会添加所有类的终极基类 [`object`](https://docs.python.org/zh-cn/3.11/library/functions.html#object)。 *dict* 字典包含类主体的属性和方法定义；它在成为 [`__dict__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#object.__dict__) 属性之前可能会被拷贝或包装。 下面两条语句会创建相同的 [`type`](https://docs.python.org/zh-cn/3.11/library/functions.html#type) 对象:

```python
class X:
    a = 1

X = type('X', (), dict(a=1))
```

​	另请参阅 [类型对象](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#bltin-type-objects)。提供给三参数形式的关键字参数会被传递给适当的元类机制 (通常为 [`__init_subclass__()`](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#object.__init_subclass__))，相当于类定义中关键字 (除了 *metaclass*) 的行为方式。

​	另请参阅 [自定义类创建](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#class-customization)。

​	*在 3.6 版更改:* [`type`](https://docs.python.org/zh-cn/3.11/library/functions.html#type) 的子类如果未重载 `type.__new__`，将不再能使用一个参数的形式来获取对象的类型。

## vars()

## vars(object)

​	返回模块、类、实例或任何其它具有 [`__dict__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#object.__dict__) 属性的对象的 [`__dict__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#object.__dict__) 属性。

​	模块和实例这样的对象具有可更新的 [`__dict__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#object.__dict__) 属性；但是，其它对象的 [`__dict__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#object.__dict__) 属性可能会设为限制写入（例如，类会使用 [`types.MappingProxyType`](https://docs.python.org/zh-cn/3.11/library/types.html#types.MappingProxyType) 来防止直接更新字典）。

​	不带参数时，[`vars()`](https://docs.python.org/zh-cn/3.11/library/functions.html#vars) 的行为类似 [`locals()`](https://docs.python.org/zh-cn/3.11/library/functions.html#locals)。 请注意，locals 字典仅对于读取起作用，因为对 locals 字典的更新会被忽略。

​	如果指定了一个对象但它没有 [`__dict__`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#object.__dict__) 属性（例如，当它所属的类定义了 [`__slots__`](https://docs.python.org/zh-cn/3.11/reference/datamodel.html#object.__slots__) 属性时）则会引发 [`TypeError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#TypeError) 异常。

## zip(*iterables, strict=False)

​	在多个迭代器上并行迭代，从每个迭代器返回一个数据项组成元组。示例:

```python
for item in zip([1, 2, 3], ['sugar', 'spice', 'everything nice']):
    print(item) 
# (1, 'sugar')
# (2, 'spice')
# (3, 'everything nice')
```

​	更正式的说法： [`zip()`](https://docs.python.org/zh-cn/3.11/library/functions.html#zip) 返回元组的迭代器，其中第 *i* 个元组包含的是每个参数迭代器的第 *i* 个元素。

​	不妨换一种方式认识 [`zip()`](https://docs.python.org/zh-cn/3.11/library/functions.html#zip) ：它会把行变成列，把列变成行。这类似于 [矩阵转置](https://en.wikipedia.org/wiki/Transpose) 。

[`zip()`](https://docs.python.org/zh-cn/3.11/library/functions.html#zip) 是延迟执行的：直至迭代时才会对元素进行处理，比如 `for` 循环或放入 [`list`](https://docs.python.org/zh-cn/3.11/library/stdtypes.html#list) 中。

​	值得考虑的是，传给 [`zip()`](https://docs.python.org/zh-cn/3.11/library/functions.html#zip) 的可迭代对象可能长度不同；有时是有意为之，有时是因为准备这些对象的代码存在错误。Python 提供了三种不同的处理方案：

- 默认情况下，[`zip()`](https://docs.python.org/zh-cn/3.11/library/functions.html#zip) 在最短的迭代完成后停止。较长可迭代对象中的剩余项将被忽略，结果会裁切至最短可迭代对象的长度：

  ```python
  list(zip(range(3), ['fee', 'fi', 'fo', 'fum'])) 
  # [(0, 'fee'), (1, 'fi'), (2, 'fo')]
  
  ```

- 通常 [`zip()`](https://docs.python.org/zh-cn/3.11/library/functions.html#zip) 用于可迭代对象等长的情况下。这时建议用 `strict=True` 的选项。输出与普通的 [`zip()`](https://docs.python.org/zh-cn/3.11/library/functions.html#zip) 相同：

  ```python
  list(zip(('a', 'b', 'c'), (1, 2, 3), strict=True)) 
  # [('a', 1), ('b', 2), ('c', 3)] 
  ```

  Unlike the default behavior, it raises a [`ValueError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#ValueError) if one iterable is exhausted before the others:

  ```python
  for item in zip(range(3), ['fee', 'fi', 'fo', 'fum'], strict=True): 
      print(item)
      
  # (0, 'fee')
  # (1, 'fi')
  # (2, 'fo')
  # Traceback (most recent call last):
  #   ...
  # ValueError: zip() argument 2 is longer than argument 1
  ```

  如果未指定 `strict=True` 参数，所有导致可迭代对象长度不同的错误都会被抑制，这可能会在程序的其他地方表现为难以发现的错误。

- 为了让所有的可迭代对象具有相同的长度，长度较短的可用常量进行填充。这可由 [`itertools.zip_longest()`](https://docs.python.org/zh-cn/3.11/library/itertools.html#itertools.zip_longest) 来完成。


​	极端例子是只有一个可迭代对象参数，[`zip()`](https://docs.python.org/zh-cn/3.11/library/functions.html#zip) 会返回一个一元组的迭代器。如果未给出参数，则返回一个空的迭代器。

​	小技巧：

- 可确保迭代器的求值顺序是从左到右的。这样就能用 `zip(*[iter(s)]*n, strict=True)` 将数据列表按长度 n 进行分组。这将重复 *相同* 的迭代器 `n` 次，输出的每个元组都包含 `n` 次调用迭代器的结果。这样做的效果是把输入拆分为长度为 n 的块。

- [`zip()`](https://docs.python.org/zh-cn/3.11/library/functions.html#zip) 与 `*` 运算符相结合可以用来拆解一个列表:

  ```python
  x = [1, 2, 3]
  y = [4, 5, 6]
  list(zip(x, y)) # [(1, 4), (2, 5), (3, 6)]
  
  x2, y2 = zip(*zip(x, y))
  x == list(x2) and y == list(y2) # True
  ```

​	*在 3.10 版更改:* 增加了 `strict` 参数。

## `__import__`(name, globals=None, locals=None, fromlist=(), level=0)

> 备注 
>
> ​	与 [`importlib.import_module()`](https://docs.python.org/zh-cn/3.11/library/importlib.html#importlib.import_module) 不同，这是一个日常 Python 编程中不需要用到的高级函数。

​	此函数会由 [`import`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#import) 语句发起调用。 它可以被替换 (通过导入 [`builtins`](https://docs.python.org/zh-cn/3.11/library/builtins.html#module-builtins) 模块并赋值给 `builtins.__import__`) 以便修改 `import` 语句的语义，但是 **强烈** 不建议这样做，因为使用导入钩子 (参见 [**PEP 302**](https://peps.python.org/pep-0302/)) 通常更容易实现同样的目标，并且不会导致代码问题，因为许多代码都会假定所用的是默认实现。 同样也不建议直接使用 [`__import__()`](https://docs.python.org/zh-cn/3.11/library/functions.html#import__) 而应该用 [`importlib.import_module()`](https://docs.python.org/zh-cn/3.11/library/importlib.html#importlib.import_module)。

​	本函数会导入模块 *name*，利用 *globals* 和 *locals* 来决定如何在包的上下文中解释该名称。*fromlist* 给出了应从 *name* 模块中导入的对象或子模块的名称。标准的实现代码完全不会用到 *locals* 参数，只用到了 *globals* 用于确定 [`import`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#import) 语句所在的包上下文。*level* 指定是使用绝对还是相对导入。 `0` (默认值) 意味着仅执行绝对导入。 

​	*level* 为正数值表示相对于模块调用 [`__import__()`](https://docs.python.org/zh-cn/3.11/library/functions.html#import__) 的目录，将要搜索的父目录层数 (详情参见 [**PEP 328**](https://peps.python.org/pep-0328/))。

​	当 *name* 变量的形式为 `package.module` 时，通常将会返回最高层级的包（第一个点号之前的名称），而 *不是* 以 *name* 命名的模块。 但是，当给出了非空的 *fromlist* 参数时，则将返回以 *name* 命名的模块。

​	例如，语句 `import spam` 的结果将为与以下代码作用相同的字节码:

```python
spam = __import__('spam', globals(), locals(), [], 0)
```

​	语句 `import spam.ham` 的结果将为以下调用:

```python
spam = __import__('spam.ham', globals(), locals(), [], 0)
```

​	请注意在这里 [`__import__()`](https://docs.python.org/zh-cn/3.11/library/functions.html#import__) 是如何返回顶层模块的，因为这是通过 [`import`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#import) 语句被绑定到特定名称的对象。

​	另一方面，语句 `from spam.ham import eggs, sausage as saus` 的结果将为

```python
_temp = __import__('spam.ham', globals(), locals(), ['eggs', 'sausage'], 0)
eggs = _temp.eggs
saus = _temp.sausage
```

​	在这里， `spam.ham` 模块会由 [`__import__()`](https://docs.python.org/zh-cn/3.11/library/functions.html#import__) 返回。 要导入的对象将从此对象中提取并赋值给它们对应的名称。

​	如果您只想按名称导入模块（可能在包中），请使用 [`importlib.import_module()`](https://docs.python.org/zh-cn/3.11/library/importlib.html#importlib.import_module)

​	*在 3.3 版更改:* *level* 的值不再支持负数（默认值也修改为0）。

​	*在 3.9 版更改:* 当使用了命令行参数 [`-E`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#cmdoption-E) 或 [`-I`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#cmdoption-I) 时，环境变量 [`PYTHONCASEOK`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#envvar-PYTHONCASEOK) 现在将被忽略。

> 备注
>
> - [1](https://docs.python.org/zh-cn/3.11/library/functions.html#id1)
>
>   解析器只接受 Unix 风格的行结束符。如果您从文件中读取代码，请确保用换行符转换模式转换 Windows 或 Mac 风格的换行符。
+++
title = "概述"
weight = 10
date = 2023-06-27T08:30:57+08:00
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

# 概述

https://docs.python.org/zh-cn/3.11/library/intro.html

​	"Python 库"中包含了几种不同的组件。

​	它包含通常被视为语言“核心”中的一部分的数据类型，例如数字和列表。对于这些类型，Python语言核心定义了文字的形式，并对它们的语义设置了一些约束，但没有完全定义语义。（另一方面，语言核心确实定义了语法属性，如操作符的拼写和优先级。）

​	这个库也包含了内置函数和异常 --- 不需要 [`import`](https://docs.python.org/zh-cn/3.11/reference/simple_stmts.html#import) 语句就可以在所有Python代码中使用的对象。有一些是由语言核心定义的，但是许多对于核心语义不是必需的，并且仅在这里描述。

​	不过这个库主要是由一系列的模块组成。这些模块集可以不同方式分类。有些模块是用 C 编写并内置于 Python 解释器中；另一些模块则是用 Python 编写并以源码形式导入。有些模块提供专用于 Python 的接口，例如打印栈追踪信息；有些模块提供专用于特定操作系统的接口，例如操作特定的硬件；另一些模块则提供针对特定应用领域的接口，例如万维网。有些模块在所有更新和移植版本的 Python 中可用；另一些模块仅在底层系统支持或要求时可用；还有些模块则仅当编译和安装 Python 时选择了特定配置选项时才可用。

​	本手册以 "从内到外" 的顺序组织：首先描述内置函数、数据类型和异常，最后是根据相关性进行分组的各种模块。

​	这意味着如果你从头开始阅读本手册，并在感到厌烦时跳到下一章，你仍能对 Python 库的可用模块和所支持的应用领域有个大致了解。当然，你并非 *必须* 如同读小说一样从头读到尾 --- 你也可以先浏览内容目录 (在手册开头)，或在索引 (在手册末尾) 中查找某个特定函数、模块或条目。最后，如果你喜欢随意学习某个主题，你可以选择一个随机页码 (参见 [`random`](https://docs.python.org/zh-cn/3.11/library/random.html#module-random) 模块) 并读上一两小节。无论你想以怎样的顺序阅读本手册，还是建议先从 [内置函数](https://docs.python.org/zh-cn/3.11/library/functions.html#built-in-funcs) 这一章开始，因为本手册的其余内容都需要你熟悉其中的基本概念。

​	让我们开始吧！



## 可用性注释

- 如果出现“适用：Unix”注释，意味着相应函数通常存在于 Unix 系统中。 但这并不保证其存在于某个特定的操作系统中。
- 如果没有单独说明，所有注明 "可用性: Unix" 的函数都在 macOS 上受到支持，因为此系统是基于 Unix 内核的。
- If an availability note contains both a minimum Kernel version and a minimum libc version, then both conditions must hold. For example a feature with note *Availability: Linux >= 3.17 with glibc >= 2.27* requires both Linux 3.17 or newer and glibc 2.27 or newer.



### WebAssembly platforms

The [WebAssembly](https://webassembly.org/) platforms `wasm32-emscripten` ([Emscripten](https://emscripten.org/)) and `wasm32-wasi` ([WASI](https://wasi.dev/)) provide a subset of POSIX APIs. WebAssembly runtimes and browsers are sandboxed and have limited access to the host and external resources. Any Python standard library module that uses processes, threading, networking, signals, or other forms of inter-process communication (IPC), is either not available or may not work as on other Unix-like systems. File I/O, file system, and Unix permission-related functions are restricted, too. Emscripten does not permit blocking I/O. Other blocking operations like [`sleep()`](https://docs.python.org/zh-cn/3.11/library/time.html#time.sleep) block the browser event loop.

The properties and behavior of Python on WebAssembly platforms depend on the [Emscripten](https://emscripten.org/)-SDK or [WASI](https://wasi.dev/)-SDK version, WASM runtimes (browser, NodeJS, [wasmtime](https://wasmtime.dev/)), and Python build time flags. WebAssembly, Emscripten, and WASI are evolving standards; some features like networking may be supported in the future.

For Python in the browser, users should consider [Pyodide](https://pyodide.org/) or [PyScript](https://pyscript.net/). PyScript is built on top of Pyodide, which itself is built on top of CPython and Emscripten. Pyodide provides access to browsers' JavaScript and DOM APIs as well as limited networking capabilities with JavaScript's `XMLHttpRequest` and `Fetch` APIs.

- Process-related APIs are not available or always fail with an error. That includes APIs that spawn new processes ([`fork()`](https://docs.python.org/zh-cn/3.11/library/os.html#os.fork), [`execve()`](https://docs.python.org/zh-cn/3.11/library/os.html#os.execve)), wait for processes ([`waitpid()`](https://docs.python.org/zh-cn/3.11/library/os.html#os.waitpid)), send signals ([`kill()`](https://docs.python.org/zh-cn/3.11/library/os.html#os.kill)), or otherwise interact with processes. The [`subprocess`](https://docs.python.org/zh-cn/3.11/library/subprocess.html#module-subprocess) is importable but does not work.
- The [`socket`](https://docs.python.org/zh-cn/3.11/library/socket.html#module-socket) module is available, but is limited and behaves differently from other platforms. On Emscripten, sockets are always non-blocking and require additional JavaScript code and helpers on the server to proxy TCP through WebSockets; see [Emscripten Networking](https://emscripten.org/docs/porting/networking.html) for more information. WASI snapshot preview 1 only permits sockets from an existing file descriptor.
- Some functions are stubs that either don't do anything and always return hardcoded values.
- Functions related to file descriptors, file permissions, file ownership, and links are limited and don't support some operations. For example, WASI does not permit symlinks with absolute file names.
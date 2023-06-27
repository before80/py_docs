+++
title = "配置 Python"
weight = 30
date = 2023-06-27T09:53:19+08:00
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

# 3. 配置 Python

https://docs.python.org/zh-cn/3.11/using/configure.html



## 3.1. 配置参数

用以下方式列出脚本 `./configure` 的所有参数：

```
./configure --help
```

参阅 Python 源代码中的 `Misc/SpecialBuilds.txt` 。

### 3.1.1. 常用参数

- **--enable-loadable-sqlite-extensions**

  支持 `_sqlite` 扩展模块中的可加载扩展（默认为否）。参见 [`sqlite3.Connection.enable_load_extension()`](https://docs.python.org/zh-cn/3.11/library/sqlite3.html#sqlite3.Connection.enable_load_extension) 方法的 [`sqlite3`](https://docs.python.org/zh-cn/3.11/library/sqlite3.html#module-sqlite3) 模块。*3.6 新版功能.*

- **--disable-ipv6**

  禁用 IPv6 支持（若开启支持则默认启用），见 [`socket`](https://docs.python.org/zh-cn/3.11/library/socket.html#module-socket) 模块。

- **--enable-big-digits**=[15|30]

  定义 Python [`int`](https://docs.python.org/zh-cn/3.11/library/functions.html#int) 数字的比特大小：15或30比特By default, the digit size is 30.定义 `PYLONG_BITS_IN_DIGIT` 为 `15` 或 `30`。参见 [`sys.int_info.bits_per_digit`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.int_info) 。

- **--with-cxx-main**

  

- **--with-cxx-main**=COMPILER

  编译 Python `main()` 函数，用 C++ 编译器链接 Python 可执行文件： $CXX` 或 *COMPILER*。

- **--with-suffix**=SUFFIX

  将 Python 的可执行文件后缀设置为 *SUFFIX*。The default suffix is `.exe` on Windows and macOS (`python.exe` executable), `.js` on Emscripten node, `.html` on Emscripten browser, `.wasm` on WASI, and an empty string on other platforms (`python` executable).*在 3.11 版更改:* The default suffix on WASM platform is one of `.js`, `.html` or `.wasm`.

- **--with-tzpath**=<list of absolute paths separated by pathsep>

  为 [`zoneinfo.TZPATH`](https://docs.python.org/zh-cn/3.11/library/zoneinfo.html#zoneinfo.TZPATH) 选择默认的时区搜索路径。 参见 [`zoneinfo`](https://docs.python.org/zh-cn/3.11/library/zoneinfo.html#module-zoneinfo) 模块的 [编译时配置](https://docs.python.org/zh-cn/3.11/library/zoneinfo.html#zoneinfo-data-compile-time-config)。默认：`/usr/share/zoneinfo:/usr/lib/zoneinfo:/usr/share/lib/zoneinfo:/etc/zoneinfo`参阅 [`os.pathsep`](https://docs.python.org/zh-cn/3.11/library/os.html#os.pathsep) 路径分隔符。*3.9 新版功能.*

- **--without-decimal-contextvar**

  编译 `_decimal` 扩展模块时使用线程本地上下文，而不是协程本地上下文（默认），参见 [`decimal`](https://docs.python.org/zh-cn/3.11/library/decimal.html#module-decimal) 模块。参见 [`decimal.HAVE_CONTEXTVAR`](https://docs.python.org/zh-cn/3.11/library/decimal.html#decimal.HAVE_CONTEXTVAR) 和 [`contextvars`](https://docs.python.org/zh-cn/3.11/library/contextvars.html#module-contextvars) 模块。*3.9 新版功能.*

- **--with-dbmliborder**=<list of backend names>

  覆盖 [`dbm`](https://docs.python.org/zh-cn/3.11/library/dbm.html#module-dbm) 模块的 db 后端检查顺序。合法值是用冒号（`:`）分隔的字符串，包含后端名称。`ndbm` ；`gdbm` ；`bdb` 。

- **--without-c-locale-coercion**

  禁用 C 语言对 UTF-8 的强制要求（默认为启用）。不定义 `PY_COERCE_C_LOCALE` 宏。参阅 [`PYTHONCOERCECLOCALE`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#envvar-PYTHONCOERCECLOCALE) 和 [**PEP 538**](https://peps.python.org/pep-0538/)。

- **--with-platlibdir**=DIRNAME

  Python 库目录名（默认为 `lib`）。Fedora 和 SuSE 在64 位平台用 `lib64` 。参阅 [`sys.platlibdir`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.platlibdir) 。*3.9 新版功能.*

- **--with-wheel-pkg-dir**=PATH

  [`ensurepip`](https://docs.python.org/zh-cn/3.11/library/ensurepip.html#module-ensurepip) 模块用到的 wheel 包目录（默认为无）。某些 Linux 发行版的打包策略建议不要捆绑依赖关系。如 Fedora 在``/usr/share/python-wheels/`` 目录下安装 wheel 包，而不安装 `ensurepip._bundled` 包。*3.10 新版功能.*

- **--with-pkg-config**=[check|yes|no]

  Whether configure should use **pkg-config** to detect build dependencies.`check` (default): **pkg-config** is optional`yes`: **pkg-config** is mandatory`no`: configure does not use **pkg-config** even when present*3.11 新版功能.*

- **--enable-pystats**

  Turn on internal statistics gathering.The statistics will be dumped to a arbitrary (probably unique) file in `/tmp/py_stats/`, or `C:\temp\py_stats\` on Windows.Use `Tools/scripts/summarize_stats.py` to read the stats.*3.11 新版功能.*

### 3.1.2. WebAssembly Options

- **--with-emscripten-target**=[browser|node]

  Set build flavor for `wasm32-emscripten`.`browser` (default): preload minimal stdlib, default MEMFS.`node`: NODERAWFS and pthread support.*3.11 新版功能.*

- **--enable-wasm-dynamic-linking**

  Turn on dynamic linking support for WASM.Dynamic linking enables `dlopen`. File size of the executable increases due to limited dead code elimination and additional features.*3.11 新版功能.*

- **--enable-wasm-pthreads**

  Turn on pthreads support for WASM.*3.11 新版功能.*

### 3.1.3. 安装时的选项

- **--prefix**=PREFIX

  Install architecture-independent files in PREFIX. On Unix, it defaults to `/usr/local`.This value can be retrived at runtime using [`sys.prefix`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.prefix).As an example, one can use `--prefix="$HOME/.local/"` to install a Python in its home directory.

- **--exec-prefix**=EPREFIX

  Install architecture-dependent files in EPREFIX, defaults to [`--prefix`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-prefix).This value can be retrived at runtime using [`sys.exec_prefix`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.exec_prefix).

- **--disable-test-modules**

  不编译和安装 test 模块，如 [`test`](https://docs.python.org/zh-cn/3.11/library/test.html#module-test) 包或 `_testcapi` 扩展模块（默认会编译并安装）。*3.10 新版功能.*

- **--with-ensurepip**=[upgrade|install|no]

  选择 Python 安装时运行的 [`ensurepip`](https://docs.python.org/zh-cn/3.11/library/ensurepip.html#module-ensurepip) 命令。`upgrade` （默认）：运行 `python -m ensurepip --altinstall --upgrade` 命令。`install` ：运行 `python -m ensurepip --altinstall` 命令。`no` ：不运行 ensurepip。*3.6 新版功能.*

### 3.1.4. 性能选项

建议用 `--enable-optimizations --with-lto` （PGO + LTO）配置 Python，以便实现最佳性能。

- **--enable-optimizations**

  用 [`PROFILE_TASK`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-PROFILE_TASK) 启用以配置文件主导的优化（PGO）（默认为禁用）。C 编译器 Clang 需要用到 `llvm-profdata` 程序进行 PGO。在 macOS 上，GCC 也需要用到它：在 macOS 上 GCC 只是 Clang 的别名而已。如果使用 `--enable-shared` 和 GCC ，还可以禁用 libpython 中的语义插值：在编译器和链接器的标志中加入 `-fno-semantic-interposition` 。*3.6 新版功能.**在 3.10 版更改:* 在 GCC 上使用 `-fno-semantic-interposition` 。

- **PROFILE_TASK**

  Makefile 用到的环境变量：PGO 用到的 Python 命令行参数。默认为：`-m test --pgo --timeout=$(TESTTIMEOUT)` 。*3.8 新版功能.*

- **--with-lto**=[full|thin|no|yes]

  在编译过程中启用链接时间优化（LTO）（默认为禁用）。LTO 时 C 编译器 Clang 需要用到 `llvm-ar` 参数（在 macOS 则为 `ar`），以及支持 LTO 的链接器（`ld.gold` 或 `lld`）。*3.6 新版功能.**3.11 新版功能:* To use ThinLTO feature, use `--with-lto=thin` on Clang.

- **--with-computed-gotos**

  在求值环节启用 goto 计数（在支持的编译器上默认启用）。

- **--without-pymalloc**

  禁用特定的 Python 内存分配器 [pymalloc](https://docs.python.org/zh-cn/3.11/c-api/memory.html#pymalloc) （默认为启用）。参见环境变量 [`PYTHONMALLOC`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#envvar-PYTHONMALLOC) 。

- **--without-doc-strings**

  禁用静态文档字符串以减少内存占用（默认启用）。Python 中定义的文档字符串不受影响。不定义 `PY_COERCE_C_LOCALE` 宏。参阅宏 `PyDoc_STRVAR()` 。

- **--enable-profiling**

  用 `gprof` 启用 C 语言级的代码评估（默认为禁用）。



### 3.1.5. Python 调试级编译

调试版本 Python 是指带有 [`--with-pydebug`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-with-pydebug) 参数的编译。

调试版本的效果：

- 默认显示所有警告：在 [`warnings`](https://docs.python.org/zh-cn/3.11/library/warnings.html#module-warnings) 模块中，默认警告过滤器的列表是空的。
- 在 [`sys.abiflags`](https://docs.python.org/zh-cn/3.11/library/sys.html#sys.abiflags) 中加入 `d` 标记。
- 加入 `sys.gettotalrefcount()` 函数。
- 命令行参数加入 [`-X showrefcount`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#cmdoption-X) 。
- 环境变量加入 [`PYTHONTHREADDEBUG`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#envvar-PYTHONTHREADDEBUG) 。
- Add support for the `__lltrace__` variable: enable low-level tracing in the bytecode evaluation loop if the variable is defined.
- 安装 [内存分配调试钩子](https://docs.python.org/zh-cn/3.11/c-api/memory.html#default-memory-allocators) ，以便检测缓冲区溢出和其他内存错误。
- 定义宏 `Py_DEBUG` 和 `Py_REF_DEBUG` 。
- Add runtime checks: code surrounded by `#ifdef Py_DEBUG` and `#endif`. Enable `assert(...)` and `_PyObject_ASSERT(...)` assertions: don't set the `NDEBUG` macro (see also the [`--with-assertions`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-with-assertions) configure option). Main runtime checks:
  - 增加了对函数参数的合理性检查。
  - 创建 Unicode 和 int 对象时，内存按某种模式进行了填充，用于检测是否使用了未初始化的对象。
  - 确保有能力清除或替换当前异常的函数在调用时不会引发异常。
  - Check that deallocator functions don't change the current exception.
  - 垃圾收集器（[`gc.collect()`](https://docs.python.org/zh-cn/3.11/library/gc.html#gc.collect) 函数）对对象的一致性进行一些基本检查。
  - 从较宽类型转换到较窄类型时，`Py_SAFE_DOWNCAST()` 宏会检查整数下溢和上溢的情况。

参见 [Python 开发模式](https://docs.python.org/zh-cn/3.11/library/devmode.html#devmode) 和配置参数 [`--with-trace-refs`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-with-trace-refs) 。

*在 3.8 版更改:* 发布版和调试版的编译现在是 ABI 兼容的：定义了 `Py_DEBUG` 宏不再意味着同时定义了 `Py_TRACE_REFS` 宏（参见 [`--with-trace-refs`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-with-trace-refs) 参数），这引入了唯一一处不是 ABI 兼容的地方。

### 3.1.6. 调试选项

- **--with-pydebug**

  [在调试模式下编译 Python](https://docs.python.org/zh-cn/3.11/using/configure.html#debug-build): 定义宏 `Py_DEBUG` (默认为禁用)。

- **--with-trace-refs**

  为了调试而启用引用的跟踪（默认为禁用）。效果如下：定义 `Py_TRACE_REFS` 宏。加入 `sys.getobjects()` 函数。环境变量加入 [`PYTHONDUMPREFS`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#envvar-PYTHONDUMPREFS) 。此版本与发布模式（默认编译模式）或调试模式（`Py_DEBUG` 和 `Py_REF_DEBUG` 宏）不具备 ABI 兼容性。*3.8 新版功能.*

- **--with-assertions**

  编译时启用 C 断言：`assert(...);` 和 `_PyObject_ASSERT(...);` （默认不启用）。如果设置此参数，则在 [`OPT`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-OPT) 编译器变量中不定义 `NDEBUG` 宏。参阅 [`--with-pydebug`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-with-pydebug) 选项（[调试编译模式](https://docs.python.org/zh-cn/3.11/using/configure.html#debug-build)），它也可以启用断言。*3.6 新版功能.*

- **--with-valgrind**

  启用 Valgrind （默认禁用）。

- **--with-dtrace**

  启用 DTrace（默认禁用）。参阅 [用 DTrace 和 SystemTap 测试 CPython](https://docs.python.org/zh-cn/3.11/howto/instrumentation.html#instrumentation)。*3.6 新版功能.*

- **--with-address-sanitizer**

  启用 AddressSanitizer 内存错误检测 `asan`，（默认为禁用）。*3.6 新版功能.*

- **--with-memory-sanitizer**

  启用 MemorySanitizer 内存错误检测 `msan`，（默认为禁用）。*3.6 新版功能.*

- **--with-undefined-behavior-sanitizer**

  启用 undefinedBehaviorSanitizer 未定义行为检测 `ubsan`，（默认为禁用）。*3.6 新版功能.*

### 3.1.7. 链接器选项

- **--enable-shared**

  启用共享 Python 库 `libpython` 的编译（默认为禁用）。

- **--without-static-libpython**

  不编译 `libpythonMAJOR.MINOR.a`，也不安装 `python.o` (默认会编译并安装)。*3.10 新版功能.*

### 3.1.8. 库选项

- **--with-libs**='lib1 ...'

  链接附加库（默认不会）。

- **--with-system-expat**

  用已安装的 `expat` 库编译 `pyexpat` 模块（默认为否）。

- **--with-system-ffi**

  用已安装的 `ffi` 库编译 `_ctypes` 扩展模块，参见 [`ctypes`](https://docs.python.org/zh-cn/3.11/library/ctypes.html#module-ctypes) 模块（默认情况视系统而定）。

- **--with-system-libmpdec**

  用已安装的 `mpdec` 库编译 `_decimal` 扩展模块，参见 [`decimal`](https://docs.python.org/zh-cn/3.11/library/decimal.html#module-decimal) 模块（默认为否）。*3.3 新版功能.*

- **--with-readline**=editline

  用 `editline` 库作为 [`readline`](https://docs.python.org/zh-cn/3.11/library/readline.html#module-readline) 模块的后端。定义 `WITH_EDITLINE` 宏。*3.10 新版功能.*

- **--without-readline**

  不编译 [`readline`](https://docs.python.org/zh-cn/3.11/library/readline.html#module-readline) 模块（默认会）。不定义 `HAVE_LIBREADLINE` 宏。*3.10 新版功能.*

- **--with-libm**=STRING

  将 `libm` 数学库覆盖为 *STRING* (默认情况视系统而定)。

- **--with-libc**=STRING

  将 `libc` C 库覆盖为 *STRING* (默认情况视系统而定)。

- **--with-openssl**=DIR

  OpenSSL 的根目录。*3.7 新版功能.*

- **--with-openssl-rpath**=[no|auto|DIR]

  设置 OpenSSL 库的运行时库目录（rpath）。`no` (默认): 不设置 rpath。`auto`：根据 [`--with-openssl`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-with-openssl) 和 `pkg-config` 自动检测 rpath。*DIR* ：直接设置 rpath。*3.10 新版功能.*

### 3.1.9. 安全性选项

- **--with-hash-algorithm**=[fnv|siphash13|siphash24]

  选择 `Python/pyhash.c` 采用的哈希算法。`siphash13` (default);`siphash24`;`fnv`.*3.4 新版功能.**3.11 新版功能:* `siphash13` is added and it is the new default.

- **--with-builtin-hashlib-hashes**=md5,sha1,sha256,sha512,sha3,blake2

  内置哈希模块：`md5`。`sha1`。`sha256`。`sha512`。`sha3` (带 shake)。`blake2`。*3.9 新版功能.*

- **--with-ssl-default-suites**=[python|openssl|STRING]

  覆盖 OpenSSL 默认的密码套件字符串。`python` (默认值): 采用 Python 推荐选择。`openssl`：保留 OpenSSL 默认值不动。*STRING* ：采用自定义字符串。参见 [`ssl`](https://docs.python.org/zh-cn/3.11/library/ssl.html#module-ssl) 模块。*3.7 新版功能.**在 3.10 版更改:* 设置 `python` 和 *STRING* 也会把 TLS 1.2 设为最低版本的协议。

### 3.1.10. macOS 选项

参见 `Mac/README.rst` 。

- **--enable-universalsdk**

  

- **--enable-universalsdk**=SDKDIR

  创建通用的二进制版本。*SDKDIR* 指定应采用的 macOS SDK （默认为否）。

- **--enable-framework**

  

- **--enable-framework**=INSTALLDIR

  创建 Python.framework ，而不是传统的 Unix 安装版。可选参数 *INSTALLDIR* 指定了安装路径（(默认为否）。

- **--with-universal-archs**=ARCH

  指定应创建何种通用二进制文件。该选项仅当设置了 [`--enable-universalsdk`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-1) 时才有效。可选项：`universal2`。`32-bit`。`64-bit`。`3-way`。`intel`。`intel-32`。`intel-64`。`all`。

- **--with-framework-name**=FRAMEWORK

  为 macOS 中的 python 框架指定名称，仅当设置了 [`--enable-framework`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-2) 时有效（默认：`Python`）。

### 3.1.11. Cross Compiling Options

Cross compiling, also known as cross building, can be used to build Python for another CPU architecture or platform. Cross compiling requires a Python interpreter for the build platform. The version of the build Python must match the version of the cross compiled host Python.

- **--build**=BUILD

  configure for building on BUILD, usually guessed by **config.guess**.

- **--host**=HOST

  cross-compile to build programs to run on HOST (target platform)

- **--with-build-python**=path/to/python

  path to build `python` binary for cross compiling*3.11 新版功能.*

- **CONFIG_SITE**=file

  An environment variable that points to a file with configure overrides.Example *config.site* file:`# config.site-aarch64 ac_cv_buggy_getaddrinfo=no ac_cv_file__dev_ptmx=yes ac_cv_file__dev_ptc=no `

Cross compiling example:

```
CONFIG_SITE=config.site-aarch64 ../configure \
    --build=x86_64-pc-linux-gnu \
    --host=aarch64-unknown-linux-gnu \
    --with-build-python=../x86_64/python
```

## 3.2. Python 构建系统

### 3.2.1. 构建系统的主要文件

- `configure.ac` => `configure`;
- `Makefile.pre.in` => `Makefile` (由 `configure` 创建);
- `pyconfig.h` (由 `configure` 创建);
- `Modules/Setup`: 由Makefile 使用 `Module/makesetup` shell 脚本构建的 C 扩展;
- `setup.py`: 使用 [`distutils`](https://docs.python.org/zh-cn/3.11/library/distutils.html#module-distutils) 模块构建的 C 扩展。

### 3.2.2. 主要构建步骤

- C文件（ `.c` ）是作为对象文件（ `.o` ）构建的。
- 一个静态库 `libpython` （ `.a` ）是由对象文件创建的。
- `python.o` 和静态库 `libpython` 被链接到最终程序 `python` 中。
- C 扩展由 Makefile （参见 `Modules/Setup` ） 和 `python setup.py build` 构建。

### 3.2.3. 主要 Makefile 目标

- `make` ：用标准库构建Python。
- `make platform:` ：构建 `python` 程序，但不构建标准库扩展模块。
- `make profile-opt` ：使用 Profile Guided Optimization (PGO) 构建 Python 。你可以使用 configure 的 [`--enable-optimizations`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-enable-optimizations) 选项来使其成为 `make` 命令的默认目标（ `make all` 或只是 `make` ）。
- `make buildbottest` ：构建 Python 并运行 Python 测试套件，与 buildbots 测试 Python 的方式相同。设置变量 `TESTTIMEOUT` （单位：秒）来改变测试超时时间（默认为 1200 即 20 分钟）。
- `make install`：构建并安装 Python 。
- `make regen-all` ：重新生成（几乎）所有生成的文件； `make regen-stdlib-module-names` 和 `autoconf` 必须对其余生成的文件单独运行。
- `make clean` ：移除构建的文件。
- `make distclean` ：与 `make clean` 相同，但也删除由配置脚本创建的文件。

### 3.2.4. C 扩展

一些 C 扩展是作为内置模块构建的，比如模块 `sys` 。它们是在定义了宏 `Py_BUILD_CORE_BUILTIN` 的情况下构建的。内置模块没有 `__file__` 属性:

\>>>

```
>>> import sys
>>> sys
<module 'sys' (built-in)>
>>> sys.__file__
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: module 'sys' has no attribute '__file__'
```

Other C extensions are built as dynamic libraries, like the `_asyncio` module. They are built with the `Py_BUILD_CORE_MODULE` macro defined. Example on Linux x86-64:

\>>>

```
>>> import _asyncio
>>> _asyncio
<module '_asyncio' from '/usr/lib64/python3.9/lib-dynload/_asyncio.cpython-39-x86_64-linux-gnu.so'>
>>> _asyncio.__file__
'/usr/lib64/python3.9/lib-dynload/_asyncio.cpython-39-x86_64-linux-gnu.so'
```

`Modules/Setup` 用于生成 Makefile 目标，以构建 C 扩展。在文件的开头， C 被构建为内置模块。在标记 `*shared*` 之后定义的扩展被构建为动态库。

`setup.py` 脚本只使用 [`distutils`](https://docs.python.org/zh-cn/3.11/library/distutils.html#module-distutils) 模块将 C 构建为共享库。

宏 `PyAPI_FUNC()` ， `PyAPI_API()` 和 `PyMODINIT_FUNC()` 在 `Include/pyport.h` 中的定义不同，取决于是否定义宏 `Py_BUILD_CORE_MODULE` 。

- 如果 `Py_BUILD_CORE_MODULE` 定义了，使用 `Py_EXPORTED_SYMBOL` 。
- 否则使用 `Py_IMPORTED_SYMBOL` 。

如果宏 `Py_BUILD_CORE_BUILTIN` 被错误地用在作为共享库构建的 C 扩展上，它的函数 `PyInit_xxx()` 就不会被导出，导致导入时出现 [`ImportError`](https://docs.python.org/zh-cn/3.11/library/exceptions.html#ImportError) 。

## 3.3. 编译器和链接器的标志

脚本 `./configure` 和环境变量设置的选项，并被 `Makefile` 使用。

### 3.3.1. 预处理器的标志

- **CONFIGURE_CPPFLAGS**

  变量 [`CPPFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-CPPFLAGS) 的值被传递给 `./configure` 脚本。*3.6 新版功能.*

- **CPPFLAGS**

  （ Objective ） C/C++ 预处理器标志，例如，使用 `-I<include dir>` 如果你的头文件在一个非标准的目录 `<include dir>` 中 、[`CPPFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-CPPFLAGS) 和 [`LDFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-LDFLAGS) 都需要包含shell的值，以便 setup.py 能够使用环境变量中指定的目录构建扩展模块。

- **BASECPPFLAGS**

  *3.4 新版功能.*

- **PY_CPPFLAGS**

  为构建解释器对象文件增加了额外的预处理器标志。默认为： `$(BASECPPFLAGS) -I. -I$(srcdir)/Include $(CONFIGURE_CPPFLAGS) $(CPPFLAGS)` 。*3.2 新版功能.*

### 3.3.2. 编译器标志

- **CC**

  C 编译器指令。例如： `gcc -pthread` 。

- **MAINCC**

  C编译器命令用于构建像 `python` 这样的程序的 `main()` 函数。由配置脚本的 [`--with-cxx-main`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-0) 选项设置的变量。默认为： `$(CC)` 。

- **CXX**

  C++ 编译器指令。如果使用了 [`--with-cxx-main`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-0) 选项，则使用。例如： `g++ -pthread` 。

- **CFLAGS**

  C 编译器标志。

- **CFLAGS_NODIST**

  [`CFLAGS_NODIST`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-CFLAGS_NODIST) 用于构建解释器和 stdlib C 扩展。当 Python 安装后，编译器标志 *不* 应该成为 distutils [`CFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-CFLAGS) 的一部分时，可以使用它 （ [bpo-21121](https://bugs.python.org/issue?@action=redirect&bpo=21121) ）。In particular, [`CFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-CFLAGS) should not contain:the compiler flag `-I` (for setting the search path for include files). The `-I` flags are processed from left to right, and any flags in [`CFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-CFLAGS) would take precedence over user- and package-supplied `-I` flags.hardening flags such as `-Werror` because distributions cannot control whether packages installed by users conform to such heightened standards.*3.5 新版功能.*

- **EXTRA_CFLAGS**

  而外的 C 编译器指令。

- **CONFIGURE_CFLAGS**

  变量 [`CFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-CFLAGS) 的值传递给 `./configure` 脚本。*3.2 新版功能.*

- **CONFIGURE_CFLAGS_NODIST**

  变量 [`CFLAGS_NODIST`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-CFLAGS_NODIST) 的值传递给 `./configure` 脚本。*3.5 新版功能.*

- **BASECFLAGS**

  基础编译器标志。

- **OPT**

  优化标志。

- **CFLAGS_ALIASING**

  严格或不严格的别名标志，用于编译 `Python/dtoa.c` 、*3.7 新版功能.*

- **CCSHARED**

  用于构建共享库的编译器标志。例如， `-fPIC` 在 Linux 和 BSD 上使用。

- **CFLAGSFORSHARED**

  为构建解释器对象文件增加了额外的 C 标志。，默认为： `$(CCSHARED)` ，当 [`--enable-shared`](https://docs.python.org/zh-cn/3.11/using/configure.html#cmdoption-enable-shared) 被使用时，则为空字符串

- **PY_CFLAGS**

  默认为： `$(BASECFLAGS) $(OPT) $(CONFIGURE_CFLAGS) $(CFLAGS) $(EXTRA_CFLAGS)` 。

- **PY_CFLAGS_NODIST**

  默认为： `$(CONFIGURE_CFLAGS_NODIST) $(CFLAGS_NODIST) -I$(srcdir)/Include/internal` 。*3.5 新版功能.*

- **PY_STDMODULE_CFLAGS**

  用于构建解释器对象文件的 C 标志。默认为： `$(PY_CFLAGS) $(PY_CFLAGS_NODIST) $(PY_CPPFLAGS) $(CFLAGSFORSHARED)`。*3.7 新版功能.*

- **PY_CORE_CFLAGS**

  默认为 `$(PY_STDMODULE_CFLAGS) -DPy_BUILD_CORE` 。*3.2 新版功能.*

- **PY_BUILTIN_MODULE_CFLAGS**

  编译器标志，将标准库的扩展模块作为内置模块来构建，如 [`posix`](https://docs.python.org/zh-cn/3.11/library/posix.html#module-posix) 模块默认为： `$(PY_STDMODULE_CFLAGS) -DPy_BUILD_CORE_BUILTIN` 。*3.8 新版功能.*

- **PURIFY**

  Purify 命令。 Purify 是一个内存调试程序。默认为：空字符串（不使用）。

### 3.3.3. 链接器标志位

- **LINKCC**

  用于构建如 `python` 和 `_testembed` 的程序的链接器命令。默认为： `$(PURIFY) $(MAINCC)` 。

- **CONFIGURE_LDFLAGS**

  变量 [`LDFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-LDFLAGS) 的值被传递给 `./configure` 脚本。避免指定 [`CFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-CFLAGS) ， [`LDFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-LDFLAGS) 等，这样用户就可以在命令行上使用它们来追加这些值，而不用触碰到预设的值。*3.2 新版功能.*

- **LDFLAGS_NODIST**

  [`LDFLAGS_NODIST`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-LDFLAGS_NODIST) 的使用方式与 [`CFLAGS_NODIST`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-CFLAGS_NODIST) 相同。当 Python 安装后，链接器标志 *不* 应该成为 distutils [`LDFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-LDFLAGS) 的一部分时，可以使用它（ [bpo-35257](https://bugs.python.org/issue?@action=redirect&bpo=35257) ）。In particular, [`LDFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-LDFLAGS) should not contain:the compiler flag `-L` (for setting the search path for libraries). The `-L` flags are processed from left to right, and any flags in [`LDFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-LDFLAGS) would take precedence over user- and package-supplied `-L` flags.

- **CONFIGURE_LDFLAGS_NODIST**

  变量 [`LDFLAGS_NODIST`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-LDFLAGS_NODIST) 的值传递给 `./configure` 脚本。*3.8 新版功能.*

- **LDFLAGS**

  链接器标志，例如，如果你的库在一个非标准的目录 `<lib dir>` 中，则使用 `-L<lib dir>` 。[`CPPFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-CPPFLAGS) 和 [`LDFLAGS`](https://docs.python.org/zh-cn/3.11/using/configure.html#envvar-LDFLAGS) 都需要包含shell的值，以便 setup.py 能够使用环境变量中指定的目录构建扩展模块。

- **LIBS**

  链接器标志，在链接 Python 可执行文件时将库传递给链接器。例如： `-lrt` 。

- **LDSHARED**

  构建一个共享库的命令。默认为： `@LDSHARED@ $(PY_LDFLAGS)` 。

- **BLDSHARED**

  构建共享库 `libpython` 的命令。默认为： `@BLDSHARED@ $(PY_CORE_LDFLAGS)` 。

- **PY_LDFLAGS**

  默认为： `$(CONFIGURE_LDFLAGS) $(LDFLAGS)` 。

- **PY_LDFLAGS_NODIST**

  默认为： `$(CONFIGURE_LDFLAGS_NODIST) $(LDFLAGS_NODIST)` 。*3.8 新版功能.*

- **PY_CORE_LDFLAGS**

  用于构建解释器对象文件的链接器标志。*3.8 新版功能.*
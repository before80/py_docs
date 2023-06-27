+++
title = "在 Mac 上使用 Python"
weight = 50
date = 2023-06-27T09:55:02+08:00
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

# 5. 在 Mac 上使用 Python

https://docs.python.org/zh-cn/3.11/using/mac.html

- 作者

  Bob Savage <[bobsavage@mac.com](mailto:bobsavage@mac.com)>

在运行 macOS 的 Mac 上的 Python 原则上与在其他 Unix 平台上的 Python 非常相似，但有一些额外的特性，如 IDE 和包管理器，值得指出。



## 5.1. 获取和安装 MacPython

macOS used to come with Python 2.7 pre-installed between versions 10.8 and [12.3](https://developer.apple.com/documentation/macos-release-notes/macos-12_3-release-notes#Python). You are invited to install the most recent version of Python 3 from the Python website ([https://www.python.org](https://www.python.org/)). A current "universal binary" build of Python, which runs natively on the Mac's new Intel and legacy PPC CPU's, is available there.

你安装后得到的东西有：

- A `Python 3.12` folder in your `Applications` folder. In here you find IDLE, the development environment that is a standard part of official Python distributions; and PythonLauncher, which handles double-clicking Python scripts from the Finder.
- 框架 `/Library/Frameworks/Python.framework` ，包括 Python 可执行文件和库。安装程序将此位置添加到 shell 路径。 要卸载 MacPython ，你可以简单地移除这三个项目。 Python 可执行文件的符号链接放在 /usr/local/bin/ 中。

Apple 提供的 Python 版本分别安装在 `/System/Library/Frameworks/Python.framework` 和 `/usr/bin/python` 中。 你永远不应修改或删除这些内容，因为它们由 Apple 控制并由 Apple 或第三方软件使用。 请记住，如果你选择从 python.org 安装较新的 Python 版本，那么你的计算机上将安装两个不同但都有用的 Python ，因此你的路径和用法与你想要执行的操作一致非常重要。

IDLE 包含一个帮助菜单，允许你访问 Python 文档。 如果您是 Python 的新手，你应该开始阅读该文档中的教程介绍。

如果你熟悉其他 Unix 平台上的 Python ，那么你应该阅读有关从 Unix shell 运行 Python 脚本的部分。

### 5.1.1. 如何运行 Python 脚本

你在 macOS 上开始使用 Python 的最好方法是通过 IDLE 集成开发环境，参见章节 [IDE](https://docs.python.org/zh-cn/3.11/using/mac.html#ide) 以及在IDE运行时使用帮助菜单。

If you want to run Python scripts from the Terminal window command line or from the Finder you first need an editor to create your script. macOS comes with a number of standard Unix command line editors, **vim** and **emacs** among them. If you want a more Mac-like editor, **BBEdit** or **TextWrangler** from Bare Bones Software (see http://www.barebones.com/products/bbedit/index.html) are good choices, as is **TextMate** (see https://macromates.com/). Other editors include **Gvim** (https://macvim.org/macvim/) and **Aquamacs** (http://aquamacs.org/).

要从终端窗口运行脚本，必须确保:file:/usr/local/bin 位于 shell 搜索路径中。

要从 Finder 运行你的脚本，你有两个选择：

- 把脚本拖拽到 **PythonLauncher**
- 选择 **PythonLauncher** 作为通过 finder Info 窗口打开脚本（或任何 .py 脚本）的默认应用程序，然后双击脚本。 **PythonLauncher** 有各种首选项来控制脚本的启动方式。 拖拽方式允许你为一次调用更改这些选项，或使用其“首选项”菜单全局更改内容。



### 5.1.2. 运行有图形界面的脚本

对于旧版本的 Python ，有一个需要注意的 macOS 特殊问题：与 Aqua 窗口管理器通信的程序（换句话说，任何有 GUI 的程序）需要以特殊的方式运行。使用 **pythonw** 而不是 **python** 来启动此类脚本。

对于 Python 3.9，你可以使用 **python** 或者 **pythonw**。

### 5.1.3. 配置

macOS 上的 Python 遵循所有标准的 Unix 环境变量，例如 [`PYTHONPATH`](https://docs.python.org/zh-cn/3.11/using/cmdline.html#envvar-PYTHONPATH) ，但是为从 Finder 启动的程序设置这些变量是不标准的，因为 Finder 在启动时不会读取你的 `.profile` 或 `.cshrc` 。你需要创建一个文件 `~/.MacOSX/environment.plist` 。详情请看苹果的技术文件QA1067。

更多关于在 MacPython 中安装 Python 包的信息，参阅 [安装额外的 Python 包](https://docs.python.org/zh-cn/3.11/using/mac.html#mac-package-manager) 部分。



## 5.2. IDE

MacPython 附带标准的 IDLE 开发环境。 有关使用 IDLE 的详细介绍，请访问 http://www.hashcollision.org/hkn/python/idle_intro/index.html 。



## 5.3. 安装额外的 Python 包

有几个方法可以安装额外的 Python 包：

- 可以通过标准的 Python distutils 模式（ `python setup.py install` ）安装软件包。
- 许多包也可以通过 **setuptools** 扩展或 **pip** 包装器安装，请参阅 https://pip.pypa.io/ 。

## 5.4. Mac 上的图形界面编程

使用 Python 在 Mac 上构建 GUI 应用程序有多种选择。

*PyObjC* 是一个 Python 到 Apple 的 Objective-C/Cocoa 框架的绑定，这是大多数现代 Mac 开发的基础。 有关 PyObjC 的信息，请访问 https://pypi.org/project/pyobjc/。

标准的 Python GUI 工具包是 [`tkinter`](https://docs.python.org/zh-cn/3.11/library/tkinter.html#module-tkinter) ，基于跨平台的 Tk 工具包（ [https://www.tcl.tk](https://www.tcl.tk/) ）。 Apple 的 OS X 捆绑了 Aqua 原生版本的 Tk ，最新版本可以从 [https://www.activestate.com](https://www.activestate.com/) 下载和安装；它也可以从源代码构建。

*wxPython* 是另一个流行的跨平台 GUI 工具包，可以在 macOS 上原生运行。软件包和文档可从 [https://www.wxpython.org](https://www.wxpython.org/) 获取。

*PyQt* 是另一个流行的跨平台 GUI 工具包，可以在 MacOS 上原生运行。更多信息可以在 https://riverbankcomputing.com/software/pyqt/intro 找到。

## 5.5. 在 Mac 上分发 Python 应用程序

在 Mac 上部署独立 Python 应用程序的标准工具是 **py2app** 。关于安装和使用 py2app 的更多信息可以在 https://pypi.org/project/py2app/ 找到。

## 5.6. 其他资源

MacPython 邮件列表是 Mac 上 Python 用户和开发人员的优秀支持资源：

https://www.python.org/community/sigs/current/pythonmac-sig/

另一个有用的资源是 MacPython wiki ：

https://wiki.python.org/moin/MacPython
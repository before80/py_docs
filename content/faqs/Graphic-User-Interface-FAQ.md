+++
title = "图形用户界面（GUI）常见问题"
weight = 70
date = 2023-06-27T10:27:03+08:00
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

# 图形用户界面（GUI）常见问题

https://docs.python.org/zh-cn/3.11/faq/gui.html

## 图形界面常见问题

## Python 有哪些 GUI 工具包？

Python 的标准构建包括一个指向 Tcl/Tk 部件集的面向对象的接口，称为 [tkinter](https://docs.python.org/zh-cn/3.11/library/tk.html#tkinter) 。 这可能是最容易安装（因为它包含在大多数 Python 的 [二进制发行版](https://www.python.org/downloads/) 中）和使用的。关于 Tk 的更多信息，包括指向源代码的信息，见 [Tcl/Tk 主页](https://www.tcl.tk/) 。 Tcl/Tk 可以完全移植到 macOS 、 Windows 和 Unix 平台。

存在多种选项，具体取决于你的目标平台。 Python Wiki 上提供了一个 [跨平台](https://wiki.python.org/moin/GuiProgramming#Cross-Platform_Frameworks) 和 [平台专属](https://wiki.python.org/moin/GuiProgramming#Platform-specific_Frameworks) 的 GUI 框架列表。

## 有关Tkinter的问题

### 我怎样“冻结”Tkinter程序？

Freeze （意为 “冻结”）是一个用来创建独立应用程序的工具。 当 “冻结” Tkinter 程序时，程序并不是真的能够独立运行，因为程序仍然需要 Tcl 和 Tk 库。

一种解决方法是将程序与 Tcl 和 Tk 库一同发布，并且在运行时使用环境变量 `TCL_LIBRARY` 和 `TK_LIBRARY` 指向他们的位置。

To get truly stand-alone applications, the Tcl scripts that form the library have to be integrated into the application as well. One tool supporting that is SAM (stand-alone modules), which is part of the Tix distribution (https://tix.sourceforge.net/).

在启用 SAM 时编译 Tix ，在 Python 文件 `Modules/tkappinit.c` 中执行对 `Tclsam_init()` 等的适当调用，并且将程序与 libtclsam 和 libtksam 相链接（可能也要包括 Tix 的库）。

### 在等待 I/O 操作时能够处理 Tk 事件吗？

在 Windows 以外的其他平台上可以，你甚至不需要使用线程！ 但是你必须稍微修改一下你的 I/O 代码。 Tk 有与 Xt 的 `XtAddInput()` 对应的调用，它允许你注册一个回调函数，当一个文件描述符可以进行 I/O 操作的时候，Tk 主循环将会调用这个回调函数。 参见 [文件处理程序。

### 在Tkinter中键绑定不工作：为什么？

经常听到的抱怨是：已经通过 `bind()` 方法绑定了事件的处理程序，但是，当按下相关的按键后，这个处理程序却没有执行。

最常见的原因是，那个绑定的控件没有“键盘焦点”。请在 Tk 文档中查找 focus 指令。通常一个控件要获得“键盘焦点”，需要点击那个控件（而不是标签；请查看 takefocus 选项）。
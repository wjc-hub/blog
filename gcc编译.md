@[TOC](这里写自定义目录标题)

# Linux下使用GCC进行编译

GCC 原名为 GNU C 语言编译器（GNU C Compiler），因为它原本只能处理C语言。GCC 很快地扩展，变得可处理 C++。后来又扩展为能够支持更多编程语言，如Fortran、Pascal、Objective-C、Java、Ada、Go以及各类处理器架构上的汇编语言等，所以改名GNU编译器套件（GNU Compiler Collection）。 

**gcc命令下各选项的含义**

-E：仅作预处理，不进行编译、汇编和链接

-S：仅编译到汇编语言，不进行汇编和链接

-c：编译、汇编到目标代码（也就是计算机可识别的二进制）

-o：执行命令后文件的命名

-g：生成调试信息

-w：不生成任何警告

-Wall：生成所有的警告

## 1. 安装GCC

输入指令：`sudo apt install -y build-essential`

​                    `sudo apt install openjdk-11-jak`  <!--#20.04-->

## 2. 编辑hello.c

`vi hello.c`  <!--#至少一次函数调用-->

## 3. 逐步编译并查看结果

**gcc编译的四个步骤** 

1. 预处理：`gcc -E hello.c -o hello.i`
2. 编译：    `gcc -S hello.i -o hellot.s`
3. 汇编：    `gcc -c hello.s -o hello.o`
4. 链接生成可执行文件： `gcc hello.o -o hello`

![Ubuntu 64 位 - VMware Workstation 2022_3_23 18_23_53](https://s2.loli.net/2022/03/28/pu5mSL683CljcxK.png)

## 4. 查看运行结果

./hello

## 5. 使用gdb调试函数调用

1. **借助 GDB调试器可以实现以下几个功能：**

- 程序启动时，可以按照我们自定义的要求运行程序，例如设置参数和环境变量；

- 可使被调试程序在指定代码处暂停运行，并查看当前程序的运行状态（例如当前变量的值，函数的执行结果等），即支持断点调试；

- 程序执行过程中，可以改变某个变量的值，还可以改变代码的执行顺序，从而尝试修改程序中出现的逻辑错误。

2. **GDB的用法**
   GDB 的主要功能就是监控程序的执行流程。这也就意味着，只有当源程序文件编译为可执行文件并执行时，并且该文件中必须包含必要的调试信息，GDB才会派上用场。所以在编译时需要使用 gcc/g++ -g 选项编译源文件，才可生成满足 GDB 要求的可执行文件

**调试命令 (缩写)**	                             **作用**
(gdb) break (b)	      在源代码指定的某一行设置断点，其中xxx用于指定具体打断点位置
(gdb) run (r）	        执行被调试的程序，其会自动在第一个断点处暂停执行。
(gdb) continue (c）   当程序在某一断点处停止后，用该指令可以继续执行，直至遇到断点或者程序结束。
(gdb) next (n)	          令程序一行代码一行代码的执行。
(gdb) step（s）	      如果有调用函数，进入调用的函数内部；否则，和 next 命令的功能一样。
(gdb) print (p）	       打印指定变量的值，其中 xxx 指的就是某一变量名。
(gdb) list (l)	              显示源程序代码的内容，包括各行代码所在的行号。
(gdb) finish（fi）	     结束当前正在执行的函数，并在跳出函数后暂停程序的执行。
(gdb) return（return）	结束当前调用函数并返回指定值，到上一层函数调用处停止程序执行。
(gdb) jump（j)	       使程序从当前要执行的代码处，直接跳转到指定位置处继续执行后续的代码。
(gdb) quit (q)	           终止调试。

![](https://s2.loli.net/2022/03/28/137Ga6uirE9x2Nz.png)

![Ubuntu 64 位 - VMware Workstation 2022_3_23 18_53_48](https://s2.loli.net/2022/03/28/wL41kV6YKEmMiOh.png)

![上机 020 - gcc,makefile,gdb,ide,eclipse i.pdf 和另外 16 个页面 - 个人 - Microsoft Edge 2022_3_23 19_13_57](https://s2.loli.net/2022/03/28/xgNBeyV9DWuokzR.png)

## 6. gcc过程改为makefile管理

 make命令执行时，需要一个 Makefile 文件，以告诉make命令需要怎么样的去编译和链接程序。

1. makefile的命名（两种）

   makefile
   Makefile

2. makefile的规则
   规则的三个要素：目标、依赖、命令

3. makefile的变量

- 自定义变量

  比如  obj=main.o add.o sub.o   ，引用的时候直接使用 $(obj)

-   自动变量

  $< :   规则中的第一个依赖

  $@：规则中的目标

  $^：  规则中所有的依赖

![Ubuntu 64 位 - VMware Workstation 2022_3_28 23_32_26](https://s2.loli.net/2022/03/28/FcitTo2XCGEdhbe.png)

注意：命令需要使用**【TAB】**代替空格

# 参考文章

[(15条消息) Linux下gcc命令详解_ENSHADOWER的博客-CSDN博客_linux的gcc](https://blog.csdn.net/ENSHADOWER/article/details/82951131)

[(15条消息) GDB调试命令详解_小桥流水人家_的博客-CSDN博客_gdb调试](https://blog.csdn.net/qq_28351609/article/details/114855630)

[(15条消息) Makefile教程（绝对经典，所有问题看这一篇足够了）_GUYUEZHICHENG的博客-CSDN博客_makefile](https://blog.csdn.net/weixin_38391755/article/details/80380786)

## 一、GDB简介

GNU工具集中的调试器是GDB（GNU Debugger），该程序是一个交互式工具，工作在字符模式。

GDB(GNU Debugger)是一个用来调试C/C++程序的功能强大的调试器，是Linux系统开发C/C++最常用的调试器

程序员可以使用GDB来跟踪程序中的错误，从而减少程序员的工作量。

Linux  开发C/C++ 一定要熟悉 GDB

VSCode是通过调用GDB调试器来实现C/C++的调试工作的；

Windows 系统中，常见的集成开发环境（IDE），如 VS、VC等，

它们内部已经嵌套了相应的调试器

除gdb外，linux下比较有名的调试器还有xxgdb, ddd, kgdb, ups。

GDB主要功能：

设置断点(断点可以是条件表达式)

使程序在指定的代码行上暂停执行，便于观察

单步执行程序，便于调试

查看程序中变量值的变化

动态改变程序的执行环境

分析崩溃程序产生的core文件

安装GDB：

```bash
sudo apt update
sudo apt install build-essential gdb
```


 GDB安装成功确认：

```bash
gdb --version
wyr@iZm5e9phbzdxx0lysrv9t2Z:~$ gdb --version
GNU gdb (Ubuntu 9.2-0ubuntu1~20.04.1) 9.2
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
wyr@iZm5e9phbzdxx0lysrv9t2Z:~$ 
```


GDB主要帮忙你完成下面四个方面的功能：

启动程序，可以按照你的自定义的要求随心所欲的运行程序。
可让被调试的程序在你所指定的调置的断点处停住。（断点可以是条件表达式）
当程序被停住时，可以检查此时你的程序中所发生的事。
动态的改变你程序的执行环境。
常用调试命令参数
调试开始：执行gdb [exefilename] ，进入gdb调试程序，其中exefilename为要调试的可执行文件名

以下命令后括号内为命令的简化使用，比如run（r），直接输入命令 r 就代表命令run

```bash
$(gdb)help(h)        # 查看命令帮助，具体命令查询在gdb中输入help + 命令 
$(gdb)run(r)         # 重新开始运行文件（run-text：加载文本文件，run-bin：加载二进制文件）
$(gdb)start          # 单步执行，运行程序，停在第一行执行语句 
$(gdb)list(l)        # 查看原代码（list-n,从第n行开始查看代码。list+ 函数名：查看具体函数）
$(gdb)set            # 设置变量的值
$(gdb)next(n)        # 单步调试（逐过程，函数直接执行）
$(gdb)step(s)        # 单步调试（逐语句：跳入自定义函数内部执行）
$(gdb)backtrace(bt)  # 查看函数的调用的栈帧和层级关系
$(gdb)frame(f)       # 切换函数的栈帧
$(gdb)info(i)        # 查看函数内部局部变量的数值
$(gdb)finish         # 结束当前函数，返回到函数调用点
$(gdb)continue(c)    # 继续运行
$(gdb)print(p)       # 打印值及地址
$(gdb)quit(q)        # 退出gdb
$(gdb)break+num(b)                 # 在第num行设置断点
$(gdb)info breakpoints             # 查看当前设置的所有断点
$(gdb)delete breakpoints num(d)    # 删除第num个断点
$(gdb)display                      # 追踪查看具体变量值
$(gdb)undisplay                    # 取消追踪观察变量
$(gdb)watch                        # 被设置观察点的变量发生修改时，打印显示
$(gdb)i watch                      # 显示观察点
$(gdb)enable breakpoints           # 启用断点
$(gdb)disable breakpoints          # 禁用断点
$(gdb)x                            # 查看内存x/20xw 显示20个单元，16进制，4字节每单元
$(gdb)run argv[1] argv[2]          # 调试时命令行传参
$(gdb)set follow-fork-mode child   # Makefile项目管理：选择跟踪父子进程（fork()）
```

Tips:

编译程序时需要加上-g，之后才能用gdb进行调试：gcc -g main.c -o main

回车键：重复上一命令

给出一段简单代码，准备调试。

```c++
#include <iostream>
using namespace std;
 
 int main(int argc,char **argv)
 {
    int N = 100;
     int sum = 0;
    int i = 1;
 
// calculate sum from 1 to 100
    while (i <= N)
   {
        sum = sum + i;
        i = i + 1;
    }

   cout << "sum = " << sum << endl;
    cout << "The program is over."   << endl;

    return 0;
}
```

## 二、生成调试信息

一般来说GDB主要调试的是C/C++的程序。要调试C/C++的程序，首先在编译时，我们必须要把调试信息加到可执行文件中。使用编译器（cc/gcc/g++）的 -g 参数可以做到这一点。如：

```bash
gcc -g hello.c -o hello

g++ -g hello.cpp -o hello
```

如果没有-g，你将看不见程序的函数名、变量名，所代替的全是运行时的内存地址。

## 三、启动GDB

```bash
启动gdb：gdb program

program 也就是你的执行文件，一般在当前目录下。

设置运行参数

set args 可指定运行时参数。（如：set args 10 20 30 40 50 ）

show args 命令可以查看设置好的运行参数。

启动程序

run： 程序开始执行，如果有断点，停在第一个断点处

start： 程序向下执行一行。
```



## 四、显示源代码

用list命令来打印程序的源代码。默认打印10行。

Ø list linenum： 打印第linenm行的上下文内容.

Ø list function： 显示函数名为function的函数的源程序。

Ø list： 显示当前行后面的源程序。

Ø list -： 显示当前行前面的源程序。

一般是打印当前行的上5行和下5行，如果显示函数是是上2行下8行，默认是10行，当然，你也可以定制显示的范围，使用下面命令可以设置一次显示源程序的行数。

Ø set listsize count：设置一次显示源代码的行数。

Ø show listsize： 查看当前listsize的设置。

## 五、断点操作

### 1）简单断点

```bash
break 设置断点，可以简写为b

Ø b 10 设置断点，在源程序第10行

Ø b func 设置断点，在func函数入口处
```



### 2）多文件设置断点

```bash
C++中可以使用class::function或function(type,type)格式来指定函数名。

如果有名称空间，可以使用namespace::class::function或者function(type,type)格式来指定函数名。

Ø break filename:linenum -- 在源文件filename的linenum行处停住

Ø break filename:function -- 在源文件filename的function函数的入口处停住

Ø break class::function或function(type,type) -- 在类class的function函数的入口处停住

Ø break namespace::class::function -- 在名称空间为namespace的类class的function函数的入口处停住
```

### 3）查询所有断点

```bash
info b
info break
i break
i b
```



## 六、条件断点

```bash
一般来说，为断点设置一个条件，我们使用if关键词，后面跟其断点条件。

设置一个条件断点：

b test.c:8 if Value == 5
```



## 七、维护断点

### 1）delete [range...] 删除指定的断点，其简写命令为d。

如果不指定断点号，则表示删除所有的断点。range表示断点号的范围（如：3-7）。
比删除更好的一种方法是disable停止点，disable了的停止点，GDB不会删除，当你还需要时，enable即可，就好像回收站一样。

### 2） disable [range...] 使指定断点无效，简写命令是dis。

如果什么都不指定，表示disable所有的停止点。

### 3） enable [range...] 使无效断点生效，简写命令是ena。

如果什么都不指定，表示enable所有的停止点。

## 八、调试代码

```bash
run 		# 运行程序，可简写为r
next 		# 单步跟踪，函数调用当作一条简单语句执行，可简写为n
step 		# 单步跟踪，函数调进入被调用函数体内，可简写为s
finish 		# 退出进入的函数
until 		# 在一个循环体内单步跟踪时，这个命令可以运行程序直到退出循环体,可简写为u。
continue 	# 继续运行程序，停在下一个断点的位置，可简写为c
quit 		# 退出gdb，可简写为q
```



## 九、数据查看

### 1）查看运行时数据

```bash
print 		# 打印变量、字符串、表达式等的值，可简写为p

p count 	# 打印count的值
```



## 十、自动显示

你可以设置一些自动显示的变量，当程序停住时，或是在你单步跟踪时，这些变量会自动显示。相关的GDB命令是display。

```bash
display 		# 变量名
info display  	# 查看display设置的自动显示的信息。
undisplay num	#（info display时显示的编号）
delete display dnums… # 删除自动显示，dnums意为所设置好了的自动显式的编号。如果要同时删除几个，编号可以用空格分隔，如果要删除一个范围内的编号，可以用减号表示（如：2-5）
disable display dnums…
enable display dnums…
disable和enalbe 	# 不删除自动显示的设置，而只是让其失效和恢复。
```



## 十一、查看修改变量的值

```bash
1）ptype width -- 查看变量width的类型

type = double

2）p width -- 打印变量width 的值

$4 = 13

你可以使用set var命令来告诉GDB，width不是你GDB的参数，而是程序的变量名，如：

set var width=47 // 将变量var值设置为47

```


# Makefile和g++学习笔记

## g++ 部分

学习c和g++的都知道，gcc 时一款夸平台的 c/c++ 编译器，可以在 Linux/Windows 平台下使用，具有十分强大的功能，结构也十分灵活，并且可以通过不同的前端模块来支持各种语言，如 Java，Fortran, Pascal, Modula-3 和 Ada 的编译。许多有名的工程和库都是使用 gcc 进行编译的，如 nginx, libevent 等。

g++ 可以在命令行使用，也可以通过配置 IDE 的编译环境来调用系统配置的 g++ 环境。

### 1、g++ 编译过程

g++ 在对源程序执行编译工作时，需要经过以下四个步骤：

#### **1、预处理**：

对原程序中的宏定义，包含头文件等进行处理，生成后缀名为 .i 的文件（使用）

使用格式：

```c++
g++ -E hello.cpp -o hello.i 
```

hello.cpp 是需要编译的源文件， -o 选项指定输出的文件名。这里使用 -E 选项编译生成 hello.i 文件。

#### **2、转话为汇编文件：**

使用 -S 选项，可以将预处理之后的 .i 文件转喊为目标机器的汇编代码 .S 文件。

使用格式：

```c++
g++ -S hello.i -o hello.s
```

使用该参数可以将 .i 文件编译成 .s 文件，输出文件名同样使用 -o 选项指定。

#### **3、汇编文件->目标文件：**

即转换为机器代码： 使用 -c 选项

使用格式：

```c++
g++ -c hello.s -o hello.o
```

#### **4、链接：**

将上一步产生的目标文件链接为可执行文件，使用 -o 参数

使用格式：

```c++
g++ hello.o - o hello
```

以上过程就是 g++ 工具编译 cpp 原程序的具体过程，在实际使用时可以不用按照流程一步步编译，可以一步到位将原程序编译为可执行文件，只需要使用如下命令：

```c++
g++ hello.cpp -o hello
```

### **2、g++常用编译选项**

在使用g++工具进行编译时，可以附加一些编译选项让编译更加智能，从而方便查看编译错误和警告。g++ 提供了许多有用的编译选项，以下做一些总结：

-o FILE: 指定输出文件名，在编译为目标代码时，这一选项不是不许的。如果FILE 没有指定，缺省文件名是 a.out

-c： 只编译生成目标文件，不链接。

-m486: 针对 486 进行代码优化

-Wall：允许发出 gcc 能提供的所有有用的警告，也可以用 -W (warning) 来标记指定警告。

使用格式：

```c++
g++ -Wall hello.cpp -o hello
```

-Werrof：把所有警告转换为错误，以警告发生时中止编译错误；

-v：显式在编译过程中每一步中用到的命令；

-static：链接静态库，即执行静态链接， g++ 默认是链接动态库，如果需要链接静态库需要使用本选项进行指定；

-g：在可执行过程中包含标准调试信息，使用该选项生成的可执行文件可以用 gdb 工具进行调试；

-w：关闭所有警告，建议不要使用该选项

-shared：生成共享目标文件。通常用在建立共享库时。

-On：这是一个优化选项，如果在编译时指定该选项，则编译器会根据 n 的值（n 取 0 到 3 之间）对代码进行不同程度的优化，其中 -O0 表示不优化， n 的值越大，优化程度越高；

-L： 库文件依赖选项，该选项用于指定编译的源代码依赖的库文件路径，库文件可以是静态链接库，也可以是动态链接库，Linux 系统默认的库路径是 /usr/lib，如果需要的库文件不在这个路径下就要用 -L 指定。

```c++
g++ goo.cpp -L/home/lib -lfoo -o foo
```

-I： 该选型用于指定编译程序时依赖的头文件路径，Linux平台默认头文件路径 /usr/include 下，如果不在该目录下，则编译时需要使用该选项指定头文件所在路径。

```c++
gcc foo.cpp -I /home/include -o foo
```

### **3、编译动态库**

g++ 除了可以编译原程序生成可执行文件，也可以编译动态链接库，方法如下：

1. 分步完成

```bash
gcc -fPIC -c func.cpp -o func.o
gcc -shared -o libfunc.so func.o
```

2. 一步完成

```bash
gcc -fPIC -shared -o libfunc.so func.cpp 
```

#### **静态库的制作**

```bash
ar -crv libx.a f1.o f2.o  #利用 f1.o 和 f2.o 产生静态文件 libx.a
```

#### 静态库的链接

```bash
gcc hello.c -o hello -static -L . -l x 
#将hello.c 与 在当前目录下的名为libx.a的静态库文件链接，生产hello可执行文件  编译器会自动补齐 x库文件的前缀和后缀，即 lib 和 .a 与 x 组合成 libx.a 的完整库文件名。
```

#### 动态库的制作

```js
gcc -fPIC shared -o libxx.so f1.c f2.c #利用 f1.o 和 f2.o 产生动态库文件 libxx.so
```

#### 动态库的链接

```bash
gcc hello.c -o hello -L . -l xx 
# 将hello.c 与 在当前目录下的名为libxx.so的静态库文件链接，生产hello可执行文件  编译器会自动补齐 xx库文件的前缀和后缀，即 lib 和 .a 与 xx 组合成 libxx.so 的完整库文件名。
```

但是此时如果直接运行生产的可执行文件还不能正常运行，因为动态库文件没有加入到系统默认的动态库文件中，需要运行如下命令来查看当前系统的动态库文件夹，并将动态库文件加入到该文件夹。

```js
ldd hello #查看名为 hello 的可执行文件依赖的动态库（也叫共享库）文件夹所在位置
cp libxx.so /lib/x85_64-linux-gum/ #将动态链接库复制到上面的输出的文件中。
```

大功告成，程序可以顺利运行了。

#### 编译时进行宏定义（一般用于条件编译）

-D ： 可以使用 -D 选项来在编译时进行一个宏定义，假设在代码中定义了一个条件编译当定义 DEBUG 时就可以启用，就可以在编译时加上如下代码：

```c++
gcc xxxxx -D
```

### Makefile部分

Makefile的命令结构如下：

```c++
目标：依赖
    @达成目标所需要运行的命令  #@可以让这条命令不显示命令本身，只输出结果，也可以不加。
```

Makefile 可以利用文件的时间来判断文件是否更新。判断依赖和目标文件的最后修改时间，当目标文件依赖文件旧时，则会重新编译目标文件。

#### Makefile 的通配符

- %.o：表示一个 xx.o 文件
- $@：表示目标文件
- $<：表示第一个依赖文件
- $^：表示所有依赖

#### Makefile 的运行

Makefile 后面可以加一个空格，再加上目标的名称，则生成该目标，若没有目标则默认生成第一个目标。

#### Makefile的假象目标

通常情况下，可以用这个明林来清除之前Makef的结构，中间文件和可执行文件等。

```Makefile
# 上面还有其他内容被省略
clean:
	rm *.o test
```

但是文件夹中有，名为 clean 的文件时，根据 Makefile 的规则，clean 文件已经存在并且它的依赖都比较旧（实际上是没有依赖）所有不会运行以下的代码，也就不会达到想要的效果，这种时候就需要用到假象目标这种语法了。

```Makefile
# 上面还有其他内容被省略
clean: 
	rm *.o test
	.PHONY: clean
```

这样做能够运行 clean 了

#### Makefile 的变量

Makefile 的变量分为两种：

- := ：即时变量，该变量的值即刻确定，在**定义时**就被确定了。
- = ：延时变量，该变量的值，在**使用时**才确定。
- ?= ：延时变量，如果时**第一次定义**才起效，如果前面被定义过了就忽略这句。
- += ：附加，它是即时变量还是延时变量取决于前面的定义。

#### 示例1

```makefile
A:=$(c)
B=$(c)
c=abc #1

all:
	@echo A = $(A)
	@echo B = $(B)
c=123 #2

# A =    
# B = 123
```

#### 示例2

```makefile
A:=$(c)
B=$(c)
c=abc#1

all:
	@echo A = $(A)
	@echo B = $(B)
c=123#1
c+=123#2

# A =
# B = 123 123
```

### makefile 函数

#### 函数遍历

==**$(foreach val, list, text):**==对于 list（通常用空格隔开）里的每一变量执行 text 操作

```makefile
A= a b c
B=$(foreach f, $(A), $(f).o) #用f代表A中的各个变量，执行第三个参数的操作

all:
	@echo B=$(B)
# 输出
# B= a.o b.o c.o
```

### **filter 函数过滤**

==**$(filter pattern..., text)：**==在text里面取出符合 pattern 格式的值

==**$(filter-out pattern..., texit)：**==在 text 里面取出不符合 pattern 格式的值

```makefile
C= a b c d/
D=$(filter %/, $(C)) # 取出符合 / 格式的值
E=$(filter-out %/, $(C)) # 取出不符合 / 格式的值

all:
	@echo D=$(D)
	@echo E=$(E)
# 输出
# D=d/
# E=a b c
```

#### wildcard 函数查找

==**$(wildcard pattern)：**== pattern 定义了文件名， wildcard 取出其中存在的文件

```makefile
files = $(wildcard *.c)
files2=a.c b.c c.c d.c e.c
file3 = $(wildcard $(files2))
all:
	@echo files=$(files)
	@echo files3=$(files3)


```

#### patsubst 函数替换

==**$(patsubst pattern, replacement, $(var))：**==从var中符合 patern格式的内容，替换为 replacement。

```makefile
files2=a.c b.c c.c d.c e.c abc
# 从 files2 找出符合 .c 格式的 然后替换为 .d 的格式。
dep_files=$(patsubst %.c, %.d, $(files2))
all:
	@echo dep_files=$(dep_files)
# dep_files= a.d b.d c.d d.d e.d abc
```

#### 头文件依赖

以下情况，当修改了 c.h 中的内容，不加如新一行，则 c.h 中的更改不会被编译，因为 make 人为对于 c.o(%.o) 这个目标，它的依赖 c.c(%.c)，并没有更改，所以就需要手动加入新的一行来解决这个问题，当要 make 时，运行到新加入的一行，发现 c.h 发生了修改，生成新的目标 c.o，如何生成呢，在下面 ==**%.c: %.c**==下面告诉了如何生成：

```makefile
test: a.o b.o c.o
	g++ -o tese $
c.o: c.c c.h #加入后可以解决

%.o:%.c
	g++ -c -o $  $
clean: 
	re *,o test
.PHONY:clean
```

但不能对每一个文件都这样操作，这样操作使用通配符将逝去意义，工作量也会回到最初的起点。这个时候，就可以用 g++ 一个工具，它可以查看依赖，并生成文件：

```makefile
g++ -M c.c #打印出 c,c 的依赖
g++ -M -MF c.d c.c #把依赖文件写入文件 c.d
g++ -c -o c.o c.c -MD - MF c.d #编译 c.o ， 把依赖写入文件 c.d
```

需要注意的生成的 .d 文件时隐藏的文件。也就是说它前面还有一个点。==**.xx.o.d**==

具体做法如下：

```makefile
objs = a.o b.o c.o
dep_filss := $(patsubst %, .%.d, $(objs)) #将 objs 中俄所有文件替换成 .%.d 的形式，使用 := 时因为下一步不这样会出现递归调用。
dep_files := $(wildcard $(dep_files)) #将 dep_files 中确实存在的文件取出，赋给自己，这里用 := 即时变量时因为这个语法中用到了它本身，但是如果使用 = 延时变量的话，会在用到 dep_files 时才生成 dep_files，但是用到的时候还没有，所以是错误的。
test: $(objs)
	g++ -o test $^
ifneq ($(dep_files),) #如果这个变量不等于空
include $(dep_files)
ednif

%.o : %.c
	g++ -c -o $@ $< -MD -MF .$@.d
	
clean:
	rm *.o test
distclean:
	re $(dep_files)
	
.PHONY : clean
```

#### CFLAGS

==**CFLAFS=-Werror：**==会把所有报警当成错误

==**CFLAGS=-Iinclude：**==将 include 目录添加到 g++ 搜索头文件默认的路径。
## 系统分析工具

### CPU

- top：用于实现监控系统的进程活动和系统资源使用情况，包括 CPU，内存，磁盘和网络。
- htop：类似于 top， 但提供了更多的交互式功能和信息提示，如进程树，进程排序和颜色标识。
- vmstat：用于报告系统的虚拟内存统计信息，包括内存使用、交互空间、CPU 上下文切换和运行对列。

### 内存

- free：用于查看内存的使用情况，内存总量，已使用内存，空闲 内存以及缓存和交换空间信息。
- top：（查看第四行）
- vmstat：（查看 memory 列）

### 硬盘

- df：用于查看文件系统的磁盘空间使用情况，显示系统的总容量，已使用空间，可用空间以及文件系统的挂载点。
- iostat：用于监视系统的磁盘 I/O 活动，包括读写速率，I/O 请求和响应时间等。
- iotop：用于监视系统中磁盘 I/O 的实时情况，可以显示正在运行的磁盘 I/O 操作和各个进程的磁盘活动情况。
- vmstat： （查看 io 列）

### 网络流量

- iftop： 用于实时网络流量检测工具，可以实时显示网络接口的流量信息，包括每个网络的源ip地址，目标地址，端口号，传输速率。
- iptraf：是一个基于命令的实时网络流量检测工具，用于分析和监视网络接口的活动，提供了对网络流量，tcp/ip连接，网络接口统计和报文信息的详细视图。
- lsof：用于列出打开文件和网络连接的工具，可以检查那些进程正在使用特定的文件或网络端口。
- tcpdump：网络数据包捕获工具，用于监视和分析网络流量，可以帮助诊断网络问题。

### 网络连接

- netstat：用于显示活动的网络连接，网络接口统计信息和路由表等网络相关信息，可以提供实时的网络状态监视和诊断工具。
- ss：用于显示活动的套接字（socket）信息，包括网络连接，监听端口、进程与套接字的关联。

### 进程

- ps：用于查看当前运行在系统中的进程信息，可以显示当前活动的进程表，包括进程的 id，状态，所属用户，使用的 cpu 资源，内存占用。
- dstat：综合性能监视工具，可以提供包括 cpu，内存，磁盘，网络和系统负载等多个方面的性能指标。
- perf：linux性能分析工具包，包括 perf stat，perf record 和 perf report 等，用于收集和分析系统的硬件和软件性能数据。





## 开启网卡（自动获取ip）：

> linux 设置 dhcp

```shell
# 1、进入网络脚本配置目录：  
cd  /etc/sysconfig/network-scripts/

# 2、打开网卡配置文件：  
vi  ifcfg-ens33

# 3、修改配置文件：
将最后一行“ONBOOT=no”   修改为“ONBOOT=yes” 

# 4、保存退出
# 5、重启网络服务： 
service network restart

# 6、查看分配到的ip地址：ip addr                              
（2：ens33：*** inet 后面紧跟ip地址）
```

## 设置终端字体

> 如何修改 centos7 终端字体的大小

```shell
# 1、 首先进入管理员模式
sudo su

# 2、进入到系统的字体库中
cd /lib/kbd/consolefonts

# 3、查看自己需要的字体 ls -l （推荐使用 sun12x22 这个字体）
setfont sun12x22

# 4、需要设置开机自动生效
echo "setfont sun12x22" >> /etc/profile

# 5、重启虚拟机
reboot

# 注意：需要登录到账号后才能看到字体变化

# 6、卸载 oh-my-zsh
	# ubuntu :
		apt-get remove zsh
	# centos :
		yum remove zsh
```

## zsh配置/终端美化

> **安装zsh**

```shell
# 1、安装前查看当前系统下可用 shell
[root@localhost ~]# cat /etc/shells
/bin/sh
/bin/bash
/usr/bin/sh
/usr/bin/bash

# 2、使用命令安装 zsh
	# ubuntu :
		apt install zsh
	# centos :
		yum install zsh
		
# 3、查看 /etc/shells 会发现有了 zsh 这个 shell
[root@localhost ~]# cat /etc/shells
/bin/sh
/bin/bash
/usr/bin/sh
/usr/bin/bash
/bin/zsh


# 4、运行 zsh 
```

> **使用 oh-my-zsh 配置 zsh**

**oh-my-zsh 是大佬封装好的 zsh 配置，直接用就完事了。**

```shell
# 1、将项目 down 到本地的 ~/.oh-my-zsh 中
git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
	https://github.com/ohmyzsh/ohmyzsh.git

git clone https://github.com/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh	

# 2、使用模板替换，zsh 自带的配置文件
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

# 3、让新配置文件生效
source ~/.zshrc

# 4、再 .zshrc 中选择自己喜欢的主题，所有主题都在这里
# 修改 .zshrc 中 ZSH_THEME 变量的引号内内容既可

# 5、关闭终端才开发现还是 bash 下，使用 zsh 命令后，使用命令修改默认终端
chsh -s /bin/zsh

# 6、重启
reboot
```

> **添加插件**

**oh-my-zsh 的自带插件都储存在`~/.oh-my-zsh/plugins` 目录中，如果你希望安装一个插件，可以在 "~/.zshrc" 的 plugins=(xxx xxx ...) 这一行里加入插件名称** 

```shell
# 1、语法高亮
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh}/plugins/zsh-syntax-highlighting

# 2、语法提示
git clone https://github.com/zsh-users/zsh-autosuggestions.git ${ZSH_CUSTOM:-~/.oh-my-zsh}/plugins/zsh-autosuggestions


# 4、修改 .zshrc
plugins=(git zsh-syntax-highlighting zsh-autosuggestions)

# 5、在次运行 zsh 使得新配置文件生效
```

> 安装 lolcat 彩虹着色

系统环境： centos 7

```shell
1、首先安装
yum install ruby -y

2、查看 ruby 版本
ruby --version

3、安装 gem
gem --version			# 查看
yum install gem -y		# 安装

4、安装 lolcat
wget https://github.com/busyloop/lolcat/archive/master.zip  # 下载
unzip master.zip		# 解压
cd lolcat-master		# 进入目录
gem install lolcat		# 安装
lolcat --version		# 确认安装
```

测试：

![image-20230621122553557](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230621122553557.png)

## 获取文件路径

### 使用 readlink 获取文件路径

readlink 的最初用途是解析符号链接，不过我们可以用它来显示文件的完整路径，如下为其语法结构：

```bash
readlink -f filename
```

如下为一个例子：

```bash
$ readlink -f sample.txt
/home/gliu/sample.txt
```

### 使用 realpath 获取文件的完整路径

realpath 原用于解析绝对文件名，在这里我们也可以用它来显示文件的完整路径：

```bash
realpath filename
```

下面是一个例子：

```bash
$ realpath sample.txt
/home/gliu/sample.txt
```

如果使用符号链接，它将显示原始文件的实际路径。你可以强制它不跟随符号链接（即显示当前文件的路径）：

```
realpath -s filename
```

下面是一个示例，默认情况下它显示了源文件的完整路径，然后我强制它显示符号链接，而不是原始文件：

```bash
$ realpath linking-park
/home/gliu/Documents/ubuntu-commands.md
$ realpath -s linking-park
/home/gliu/linking-park
```

### 使用 find 命令获取文件绝对路径

下面是使用 find 命令获取文件路径的方法。

在 find 命令中，如果给定的路径是一个点 . ，那么它将显示相对路径；如果给定的是一个绝对路径，那么就可以获取搜索文件的绝对路径。 使用命令占位符与 find 命令一起使用，如下：

```bash
find $(pwd) -name filename
```

我们可以使用这种方式来获取单一文件的绝对路径：

```bash
$ find $(pwd) -name sample.txt
/home/gliu/sample.txt
```

或者，可以使用匹配模式（比如星号 *）来获取一组文件的路径：

```bash
$ find $(pwd) -name "*.pdf"
/home/gliu/Documents/eBooks/think-like-a-programmer.pdf
/home/gliu/Documents/eBooks/linux-guide.pdf
/home/gliu/Documents/eBooks/absolute-open-bsd.pdf
/home/gliu/Documents/eBooks/theory-of-fun-for-game-design.pdf
/home/gliu/Documents/eBooks/Ubuntu 1804 english.pdf
/home/gliu/Documents/eBooks/computer_science_distilled_v1.4.pdf
/home/gliu/Documents/eBooks/the-art-of-debugging-with-gdb-and-eclipse.pdf
```

### 使用 ls 命令打印完整路径

使用 ls 命令来获取文件的绝对路径，稍微优点复杂。 我们可以在 ls 命令中使用环境变量PWD来显示文件和目录的绝对路径，如下：

```bash
ls -ld $PWD/*
```

使用上述命令，会得到如下输出：

```bash
$ ls -ld $PWD/*
-r--rw-r-- 1 gliu gliu 0 Jul 27 16:57 /home/gliu/test/file2.txt
drwxrwxr-x 2 gliu gliu 4096 Aug 22 16:58 /home/gliu/test/new
```

要使用上述命令打印某个文件的完整路径，可以如下使用：

```bash
ls -l $PWD/filename
```

这虽然不是最好的解决方案，但是很有效，看下面的例子：

```bash
$ ls -l $PWD/sample.txt
-rw-r--r-- 1 gliu gliu 12813 Sep 7 11:50 /home/gliu/sample.txt
```





### 配置静态IP地址

1. 编辑网络配置文件：

```shell
sudo vim /etc/netplan/50-cloud-init.yaml
```

2. 在文件中找到网卡配置部分，并将其修改为静态IP地址

```shell

network:
  renderer: networkd
  ethernets:
    enp2s0:	# 替换为你的网络接口名称
      dhcp4: false
      dhcp6: false
      addresses: [192.168.124.12/24]	# 静态 IP 地址和子网掩码
      routes:
        - to: default
          via: 192.168.124.1	# 网关地址
      nameservers:
        addresses:	# DNS 服务器地址
          - 8.8.8.8
          - 8.8.4.4
  version: 2

```

- `enp2s0` 是网卡接口名称,根据实际情况进行修改。
- `addresses` 是静态 IP 地址和子网掩码。
- `gateway4` 是默认网关地址。
- `nameservers` 是 DNS 服务器地址。

3. 应用网络配置

```shell
sudo netplan apply
```

4. 验证配置是否生效

```shell
ip addr show
```




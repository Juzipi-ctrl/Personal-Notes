# Linux BIOS设置和查看

## 一. 前言

### 1.1 BIOS的概念和组成

BIOS （Basic Input/Output System）是一组固化到计算机内主板上一个ROM芯片上的程序， 其主要功能是为计算机提供最底层的、最直接的硬件设置和控制。BIOS设置程序是储存在BIOS芯片中的，只有在开机时才可以进行设置。

BIOS中主要存放：

（1）自诊断程序：通过读取CMOS RAM中的内容识别硬件配置，并对其进行自检和初始化；

（2）CMOS设置程序：引导过程中，用特殊热键启动，进行设置后，存入CMOS RAM中；

（3）系统自举装载程序：在自检成功后将磁盘相对0道0扇区上的引导程序装入内存；

（4）主要I／O设备的驱动程序和中断服务；

### **1.2 BIOS 分类**

目前 BIOS 分为两种，一种是传统的 BIOS，另一种就是主流的 UEFI BIOS，即Legacy BIOS 和 UEFI BIOS。BIOS 使用主引导记录 （MBR） 来保存有关硬盘数据的信息，而 UEFI 使用 GUID 分区表 （GPT）

1. UEFI BIOS

UEFI全称为：Unified Extensible Firmware Interface（统一的可扩展固件接口），UEFI 引导模式是指 UEFI 固件使用的引导过程。UEFI 将有关初始化和启动的所有信息存储在保存在名为 EFI 系统分区 （ESP） 的特殊分区上的 .efi 文件中。在开机自检过程中，UEFI 固件会扫描连接到系统的所有可引导存储设备，以查找有效的 GUID 分区表 （GPT）。

作为Legacy BIOS的替代和继任技术 UEFI，UEFI 具有以下优点：

（1）UEFI 使用户能够处理大于 2 TB 的驱动器，而旧的旧版 BIOS 无法处理大型存储驱动器，得益于GPT分区。

（2）UEFI 使用 GUID 分区表支持 4 个以上的主分区,得益于GPT分区。

（3）使用 UEFI 固件的计算机的启动过程比 BIOS 快。UEFI 中的各种优化和增强功能可以帮助您的系统启动速度比以前更快。

（4）UEFI 支持安全启动，这意味着可以检查操作系统的有效性，以确保没有恶意软件篡改启动过程。

（5）UEFI 支持UEFI固件本身的联网功能，有助于远程故障排除和UEFI配置。

（6）UEFI 具有更简单的图形用户界面，并且比传统 BIOS 具有更丰富的设置菜单。

## **二.BIOS设置和信息获取**

### 2.1 Linux进入BIOS方法

BIOS的设置对于现在的年轻人来说并不是什么问题，这里对使用linux系统中命令行重启机器进入BIOS设置界面的方法做一下总结，一共有以下5种方法：

1. ```shell
   使用reboot命令进入BIOS
   
   使用shutdown命令进入BIOS
      shutdown -r now
      
    使用grub-reboot命令进入BIOS
    
    使用efibootmgr命令进入BIOS
      对于使用UEFI引导的计算机，可以使用efibootmgr命令来进入BIOS设置界面。
      该命令可以列出当前的引导选项，并提供进入BIOS的选项
      
    使用systemctl命令进入BIOS
   ```

### 2.2 efibootmgr：UEFI启动程序管理工具

可能有人在实际工作中会产生这样的疑问，是否可以在linux系统中设置BIOS，目前看来是不可以的，对于Legacy BIOS的设置都要通过重启进入BIOS设置界面才能对其设置进行修改。对于UEFI BIOS可以在linux系统使用指定的工具修改BIOS中一部分功能。

==efibootmgr==是一种用于管理UEFI启动程序的命令行工具。它可以列出、添加、删除、编辑和显示UEFI启动列表，efibootmgr工具还有许多功能（比如隐藏启动项、修改启动项、删除无用的启动项、超时时间等）,例如：

```shell
efibootmgr -v    // 列出启动程序
efibootmgr -b 0000    // 显示第0号(0000)启动程序
efibootmgr -B -b 0000    // 删除第0号(0000)启动程序
efibootmgr -c -L "GRUB" -l "\EFI\ubuntu\grubx64.efi"    // 创建名为“GRUB”、路径为“\EFI\ubuntu\grubx64.efi”的新的启动程序
```



输入==efibootmgr==可以得到当前的启动顺序:

```shell
BootCurrent: 0002

Timeout: 2 seconds

BootOrder: 0001,0000,0002,0018

Boot0000* Windows Boot Manager

Boot0001* Ubuntu

Boot0002* Centos

Boot0018* USB CD
```

输入==efibootmgr -o 0002,0000,0001,0018==，修改启动顺序，执行完毕后，可以看到启动顺序已经改变了

```shell
BootCurrent: 0002

Timeout: 2 seconds

BootOrder: 0002,0000,0001,0018

Boot0000* Windows Boot Manager

Boot0001* Ubuntu

Boot0002* Centos

Boot0018* USB CD
```



### 2.3 Linux dmidecode命令

除了在开机启动时进入到BIOS之外，还可以在Linux系统中直接查看BIOS的信息，一般可以使用dmidecode命令（还有biosdecode命令可参考）；dmidecode的作用是将DMI数据库中的信息进行解码，然后以可读的方式显示。DMI（Desktop Management Interface, DMI）就是帮助收集电脑系统信息的管理系统，DMI信息的收集必须严格按照SMBIOS规范的前提下进行。SMBIOS（System Management BIOS）是主板或系统制造者以标准格式显示产品管理信息所需遵循的统一规范。SMBIOS和DMI是由行业指导机构Desktop Management Task Force （DMTF）起草的开放性技术标准，其中DMI设计适用于任何的平台和操作系统。通过DMI，用户可以获取服务器的序列号、电脑厂商、串口信息以及其他的系统配件信息。

下面的命令将显示当前的BIOS版本和发布日期：

```shell
dmidecode -s bios-version

dmidecode -s bios-release-date
```
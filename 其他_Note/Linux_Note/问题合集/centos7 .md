## centos7 

### 问题1：使用 su 无法切换超级用户

1. 权限问题：

- 确保有切换到目标用户的权限。普通用户无法使用 su 切换到 root 用户，除非 root 用户明确了授权了权限。
- 检查目标用户的 `/etc/passwd` 文件种是否有正确的 shell 设置。

- 再查看 `/etc/sudoers`文件是否配置了与超级用户同样的权限。

2. 环境变量问题:

- 切换用户后,一些环境变量可能没有正确继承。这会导致命令无法正确执行。
- 可以尝试使用 `su - username` 命令,在切换用户的同时加载目标用户的完整环境。

3. 身份验证问题:

- 确保您输入的密码正确。有时候切换用户会要求输入当前用户或目标用户的密码。
- 检查目标用户的密码是否已过期或被锁定。



### 问题2：如何配置用户文件

1. `/etc/passwd` 文件

   - 这是用户账户的主要配置文件,包含了用户名、UID、GID、家目录路径、shell 等信息。
   - 每行代表一个用户账户,各字段以冒号分隔。
   - 您可以使用 `useradd` 命令添加新用户,也可以手动编辑此文件。

2. `/etc/shadow` 文件

   - 这个文件包含了用户的加密密码信息,以及密码相关的其他设置。
   - 出于安全考虑,普通用户无法直接访问此文件。
   - 您可以使用 `passwd` 命令修改用户密码,而不是直接编辑此文件。

3. `/etc/group` 文件

   - 这个文件定义了系统中的用户组,包括组名、GID 和组成员。
   - 您可以使用 `groupadd`、`groupdel` 和 `usermod` 命令来管理用户组。
   - 编辑此文件时要小心,因为它会影响用户的权限。

4. `/etc/sudoers` 文件

   - 这个文件定义了哪些用户可以使用 `sudo` 命令获取 root 权限。

   - 编辑此文件需要小心,因为它可能会影响系统的安全性。

     



### 问题3：如何配置普通用户拥有超级用户权限

1. 将用户添加到 wheel 组：

- `wheel` 组是一个特殊的组,其中的用户可以使用 `sudo` 命令以 root 用户的身份执行命令。
- 使用以下命令将普通用户添加到 `wheel` 组:

```shell
usermod -aG wheel username
```

- 添加完成后，该用户就可以使用 sudo 命令执行需要的 root 权限操作。

2. 修改 `/etc/sudoers` 文件：

- 这个文件定义了那些用户（或组）可以使用 sudo 命令。
- 使用 `vim` 命令编辑 `/ect/sodoers`文件，并添加以下行：

```shell
username ALL=(ALL) ALL
```

- 这样就允许名为 `username` 的用户以 root 用户的身份执行任何命令。
- 您也可以使用 `%wheel ALL=(ALL) ALL` 来允许 `wheel` 组中的所有用户使用 `sudo` 命令。

3. 设置用户密码与 root 用户一致:

- 为普通用户设置与 root 用户相同的密码,这样该用户就可以直接切换到 root 用户。
- 使用以下命令设置用户密码:

```shell
passwd username
```

- 这种方法不太安全,因为它暴露了 root 用户的密码,不建议在生产环境中使用。（因为将普通用户密码于超级用户密码设置一样）。



### 问题4：无法安装软件包

1. 手动替换新的软件源地址

- 备份原有的 CentOS 软件源配置文件:

```shell
sudo cp /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

- 下载并使用阿里云或者其他镜像站提供的 CentOS 软件源配置文件:

```shell
sudo wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

里以阿里云的 CentOS 7 软件源为例。您也可以选择其他镜像站,如清华大学、中科大等。

- 清除已下载的缓存数据,并重新生成缓存

```shell
sudo yum clean all  # 缓存清理
sudo yum makecache	# 重新生成
```

- 现在可以使用新的软件源更新系统了

```shell
sudo yum update
```

2. 启用 EPEL (Extra Packages for Enterprise Linux) 软件源:

- EPEL 软件源包含了许多开发工具和依赖包,安装"Development Tools"软件包需要它。
- 可以使用以下命令安装 EPEL 软件源:

```shell
sudo yum install epel-release
```

3. 安装 "Development Tools" 软件包组:

- 这个软件包组包含了一系列常用的开发工具,如 gcc、make、gdb 等。
- 使用以下命令安装:

```shell
sudo yum groupinstall "Development Tools"
```

4. 安装其他可能需要的依赖包:

- 根据您的具体需求,可能还需要安装一些其他的依赖包,例如:

```shell
sudo yum install kernel-devel
sudo yum install kernel-headers
```


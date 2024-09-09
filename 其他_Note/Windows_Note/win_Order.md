## 批量更改文件名字

在 Windows 10 的命令行中，你可以使用 `ren` 命令（即 `rename` 的简写）来批量更改文件的特定名字。

下面是一些示例命令来演示如何批量更改文件名：

1. 更改指定文件的单个文件名：

   ```powershell
   ren "原文件名" "新文件名"
   ```

   例如，要将文件 `file1.txt` 更名为 `newfile1.txt`，可以执行以下命令：

   ```powershell
   ren file1.txt newfile1.txt
   ```

2. 批量更改文件名：

   ```powershell
   ren "原文件名前缀*.*" "新文件名前缀*.*"
   ```

   例如，要将所有以 `file` 开头的文件名更改为以 `newfile` 开头，可以执行以下命令：

   ```powershell
   ren file* newfile*
   ```

   这将更改所有以 `file` 开头的文件名，保留原始文件名的其余部分。

3. 批量移除文件名中的特定部分：

   ```powershell
   ren "原文件名" "新文件名"
   ```

   例如，要从文件名中移除 `-backup`，可以执行以下命令：

   ```powershell
   ren *-backup.* *.*
   ```

   这将移除所有文件名中的 `-backup` 部分，并保留原始文件的扩展名。



## 跟踪路由

Tracert==跟踪路由==是路由跟踪实用程序，用于确定 IP数据包访问目标所采取的路径。 

使用 cmd ip config /flushdns 打开网络自动获取dns



## 查看未知网站的IP

**nslookup**

后面带上要查看的某一个网站地址







## win11右键

将 Windows11 右键菜单修改为 Windows10 风格

1. 按住 win+r 打开运行窗口。
2. 输入cmd，打开控制台。
3. 在控制台输入以下代码

```bash
# 开启旧版右键菜单：
reg add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve

# 恢复 Windows11 新版右键菜单：
reg delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}" /f
```

4. 重新运行资源管理器



## WSL



```powershell
wsl --list --online 	# 列出可用的 Linux 发行版

wsl --list --verbose	# 列出已安装的 Linux 发行版

wsl --set-version <distribution name> <versionNumber>	# 将 wsl 版本设置为1或2

wsl --set-default-version <Version>		# 设置默认 wsl 版本

wsl --set-default <Distribution Name>	# 设置默认 Linux 发行版

wsl ~				# 将目录更改为主页

wsl --distribution <Distribution Name> --user <User Name>	# 通过 PowerShell 或 CMD 运行特定的 Linux 发行版

wsl --update		# 更新 wsl

wsl --status		# 检查 wsl 状态

wsl --version		# 检查 wsl 版本

wsl --help			# 帮助命令

wsl -u <Username>`, `wsl --user <Username>		# 以特定用户的身份运行

<DistributionName> config --default-user <Username>		# 更改发行版的默认用户
例如：ubuntu config --default-user johndoe 会将 Ubuntu 发行版的默认用户更改为“johndoe”用户。

wsl --shutdown		# 关闭

wsl --unregister <DistributionName>		# 注销或卸载 Linux 发行版

```

## 启用和停用网卡

在 Windows 10 的命令行中，你可以使用以下命令来启用和停用网卡（网络适配器）：

1. 启用网卡：

   ```powershell
   netsh interface set interface "网卡名称" admin=enable
   ```

   在命令中，将 "网卡名称" 替换为要启用的网卡的实际名称。要查看可用网卡的列表及其名称，可以运行以下命令：

   ```powershell
   netsh interface show interface
   ```

   例如，要启用名为 "以太网" 的网卡，可以执行以下命令：

   ```
   netsh interface set interface "以太网" admin=enable
   ```

2. 停用网卡：

   ```powershell
   netsh interface set interface "网卡名称" admin=disable
   ```

   同样，将 "网卡名称" 替换为要停用的网卡的实际名称。例如，要停用名为 "Wi-Fi" 的网卡，可以执行以下命令：

   ```powershell
   netsh interface set interface "Wi-Fi" admin=disable
   ```

请注意，执行这些命令需要管理员权限。确保在命令行中以管理员身份运行这些命令，或者在命令行前面加上 `runas /user:Administrator` 以提升权限。



## 释放和获取 IP

在 Windows 10 的命令行中，你可以使用以下命令来释放和获取 IP 地址：

1. 释放 IP 地址：

   ```powershell
   ipconfig /release
   ```

   这个命令将释放当前计算机上所有网络适配器（网卡）的 IP 地址。

2. 获取 IP 地址：

   ```powershell
   ipconfig /renew
   ```

   这个命令将尝试为当前计算机上的所有网络适配器获取新的 IP 地址。


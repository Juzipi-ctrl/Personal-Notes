## Windows 10和vscode终端美化

### 1. 准备工作

```bash
允许powershell执行脚本，如果不允许的话，后续执行安装命令会报错* 设置->隐私和安全性->开发者选项->powershell，点击应用* 
一款 Nerd Font，Nerd Font字体中包含了很多特殊的图标，如果不使用Nerd Font的话，后面设置了终端的主题后会乱码* 这里我以Hasklig字体为例，下载链接。下载后会得到个Hasklig.zip的文件，解压后可以看到里面包含了很多字体。直接ctrl + A，然后右键选择安装全部字体* 
```

### 2. 安装oh-my-posh

```shell
在Windows Terminal里执行下面命令

Set-ExecutionPolicy Bypass -Scope Process -Force; 
Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://ohmyposh.dev/install.ps1')); 
```

### 3. 在终端里应用oh-my-posh并自定义主题

```shell
在Windows Terminal里执行下面命令

oh-my-posh init pwsh | Invoke-Expression 

这时oh-my-posh会设置一个默认的主题（只要看到彩色的字体，应该就是设置成功啦）

如果想要设置其它主题的话，可以在执行

Get-PoshThemes 
```

## 查看所有可设置的主题

    在执行Get-PoshThemes完命令输出所有主题的样式后，会在最后告诉我们所有主题文件的路径，以及怎么设置主题；
    
    以我本机为例，可以在上图看到

所有主题文件的路径： C:\Users\aifuxi\AppData\Local\Programs\oh-my-posh\themes* 设置主题的命令：

```bash
oh-my-posh init pwsh --config C:\Users\aifuxi\AppData\Local\Programs\oh-my-posh\themes/jandedobbeleer.omp.json | Invoke-Expression 
jandedobbeleer.omp.json就是主题的配置文件，jandedobbeleer是主题名。比如我想设置ys这个主题，只需要把上面命令中的jandedobbeleer.omp.json改成ys.omp.json`

oh-my-posh init pwsh --config C:\Users\Administrator\AppData\Local\Programs\oh-my-posh\themes\sim-web.omp.json | Invoke-Expression 


oh-my-posh init pwsh --config C:\Users\Administrator\AppData\Local\Programs\oh-my-posh\themes\sorin.omp.json | Invoke-Expression 
```

就可以了。在Windows Terminal里执行设置主题的命令，只是临时改变主题，要想每次打开都自动设置主题我们就得编辑个配置文件了。

### 3.1 编辑配置文件

​    在Windows Terminal里执行下面命令编辑或新建一个配置文件

 notepad $PROFILE 

如果在path里安装了vscode也可以用下面命令打开 `code $PROFILE `

```bash
以我自己为例，我想设置主题为1_shell这个主题，那么就可以在刚刚打开的配置文件里加上这句话然后保存并重启Windows Terminal

oh-my-posh init pwsh --config C:\Users\anovice\AppData\Local\Programs\oh-my-posh\themes\amro.omp.json | Invoke-Expression 

注意：这里的C:\Users\aifuxi\AppData\Local\Programs\oh-my-posh\themes/1_shell.omp.json这个路径是我本机的路径，每个人的电脑的配置文件路径都是不一样的，请根据实际情况进行修改，不要盲目复制。 这是设置主题为1_shell的效果，还是挺好看的。 
```

### 3.2 vscode的设置

```bash
修改vscode配置文件settings.json

{ 
    // 代码字体，可根据实际情况进行设置
    "editor.fontFamily": "'Hasklug Nerd Font Mono',Menlo, Monaco, 'Courier New', monospace",
    // 终端字体，我这里是设置的Hasklug Nerd Font Mono，可根据实际安装的Nerd Font进行设置
    "terminal.integrated.fontFamily": "Hasklug Nerd Font Mono",
} 

"font":
{
    "face": "MesloLGM NF"
}
```

### 3.3 报错问题

1. 以管理员身份打开 PowerShell 控制台。
2. 执行以下命令查看当前的执行策略:

```shell
Get-ExecutionPolicy
```

3. 如果执行策略是 "Restricted"(默认值),则需要将其更改为允许运行脚本的策略。可以使用以下命令:

```shell
Set-ExecutionPolicy RemoteSigned
```

这个命令将执行策略设置为 "RemoteSigned",允许运行本地创建的脚本。



### 1. 安装PSReadLine

```bash
PSReadLine：github.com/PowerShell/…

PSReadLine模块取代了 PowerShell 版本 3 及更高版本的命令行编辑体验。它提供：

语法着色
简单语法错误通知
良好的多线体验（编辑和历史）
可定制的键绑定
Cmd 和 emacs 模式（都没有完全实现，但都可以使用）
许多配置选项
Bash 样式完成（在 Cmd 模式下可选，在 Emacs 模式下默认）
Bash/zsh 风格的交互式历史搜索 (CTRL-R)
Emacs yank/kill ring
基于 PowerShell 令牌的“单词”移动和杀死
撤销重做
自动保存历史记录，包括跨实时会话共享历史记录
通过 Ctrl+Space 完成“菜单”完成（有点像 Intellisense，用箭头选择完成）
“开箱即用”的体验意味着 PowerShell 用户非常熟悉 - 不需要学习任何新的击键。
上面是github里的介绍，但其实我们主要用到PSReadLine的功能就是

自动保存历史记录，敲过一个命令后，后面只需要敲前几个字母就能提示出命令，按【→】键就可以自动补全命令
语法着色 PSReadLine的作用就和oh-my-zsh里面的那个autocomplete的那个插件差不多，用来提示和补全命令的 
```

### 4.1 安装PSReadLine

```bash
以管理员身份运行Windows Terminal，执行下面命令：
Install-Module PSReadLine -Force 

没有以管理员身份运行Windows Terminal时会报错 
```

### 4.2 添加配置项到配置文件

```bash
在Windows Terminal里执行下面命令编辑配置文件
notepad $PROFILE# 如果在path里安装了vscode也可以用下面命令打开code $PROFILE 

添加下面几行配置
Set-PSReadLineOption -PredictionSource History # 设置预测文本来源为历史记录
Set-PSReadlineKeyHandler -Key Tab -Function Complete # 设置 Tab 键补全
Set-PSReadLineKeyHandler -Key "Ctrl+d" -Function MenuComplete # 设置 Ctrl+d 为菜单补全和 Intellisense
Set-PSReadLineKeyHandler -Key "Ctrl+z" -Function Undo # 设置 Ctrl+z 为撤销
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward # 设置向上键为后向搜索历史记录
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward # 设置向下键为前向搜索历史纪录 

保存后，关闭Windows Terminal后再重新打开，验证配置是否生效
安装时遇到的问题
为什么不是执行Install-Module -Name PSReadLine -AllowPrerelease来安装PSReadLine？ 其实开始的时候我是用这条命令来安装的，是根据 @i树 兄弟提供的链接来的， 但是报错了 
Install-Module -Name PSReadLine -AllowPrerelease中-AllowPrerelease是PowerShellGet这个模块提供的能力，首先得安装PowerShellGet
```

## 先安装PowerShellGet

```bash
Install-Module -Name PowerShellGet -Force
```

## 然后再这条命令安装PSReadLine

```bash
Install-Module PSReadLine -AllowPrerelease -Force 
```

### 1. 隐藏烦人的copyright

```bash
每次打开Windows Terminal都会出现烦人的copyright

Windows PowerShell 版权所有（C） Microsoft Corporation。保留所有权利。

安装最新的 PowerShell，了解新功能和改进！aka.ms/PSWindows
```

### 5.1 Windows Terminal

```bash
打开Windows Terminal设置，Windows PowerShell -> 命令行，在路径后面添加上 -nologo
```

### 5.2 vscode

```bash
修改vscode配置文件settings.json，加上terminal.integrated.profiles.windows这个字段就好了

{
    "terminal.integrated.profiles.windows": {
    "PowerShell": {
        "source": "PowerShell",
        "args": ["-noLogo"]
}},
} 
```

## 记录：Windows10 安装 Screenfetch（neofetch）

### 以管理员权限打开 PowerShell

```bash
输入 Install-Module -Name windows-screenfetch，回车（输入Y，接受）
Install-Module -Name windows-screenfetch

输入 Set-ExecutionPolicy -ExecutionPolicy Unrestricted，回车（输入Y，接受）
Set-ExecutionPolicy -ExecutionPolicy Unrestricted

输入 Import-Module windows-screenfetch
Import-Module windows-screenfetch

输入 Screenfetch 测试！
```

## Windows10任务栏无须安装第三方插件实现全透明化

打开注册表命令：regedit

1. 需要修改注册表以下数据

[**HKEY_CURRENT_USER**\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced]

2. 修改TaskbarAcrylicOpacity 为 0，默认是没有的，请自己手动添加一个，类型为DWORD

[**HKEY_LOCAL_MACHINE**\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced]

3. 如果存在UseOLEDTaskbarTransparency数据，将其修改为0，或者删除

4. 重启explorer.exe





## 使用命令设置环境变量

1. 设置环境变量

- 在Windows上，使用 setx 命令可以设置全局环境变量。示例：

```shell
setx NEW_PATH "文件目录"
```

- 在 macOS和Linux上，可以使用 export 命令设置环境变量。示例：

```shell
export NEW_PATH="文件目录"
```

2. 使输出更适合阅读

- 在Windows上，使用 echo 命令结合管道符 | 和 more 命令可以分页显示输出。示例：

```shell
echo %PATH:;=&echo.%
```

- 在 macOS和Linux上，使用 echo 命令结合管道符 | 和 less 命令可以分页显示。示例：

```shell 
echo $PATH | tr ':' '\n'
```





## windows 注册表控制任务栏显示秒数

1.`win+R`打开运行对话框，输入 `regedit`回车，打开注册表编辑器

2.在注册表编辑器中找到

```shell
HKEY_CURRENT_USER > SOFTWARE > Microsoft > Windows > CurrentVersion > Explorer > Advanced
```

3.在右侧窗口右键点击新建 DWORD(32位)值，并命名为ShowSecondsInSystemClock，双击打开将数值数据改为1，然后重启电脑即可。


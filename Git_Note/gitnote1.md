# Git

### Git 的基本操作

```shell
# 1、新建文件夹
	mkdir digist
# 2、初始化 git
	git init
# 3、与原创 git 仓库建立连接
	git remote add origin hhtp://xxx
# 4、将远程 master 分支同步到本地 git 分支
	git fetch origin master
# 5、将代码拉取下来
	git pull origin master
# 6、查看远程和本地分支及当前所分支
	git branch -a
# 7、切换远程 test 分支点到本地并命令为 test 分支
	git checkout -b test origin/test
# 8、查看 git 用户名邮箱
	git config user.name 
	git config user.email
```

## Git环境配置

> 软件下载

打开[Git官网]https://git-scm.com/，下载git对应操作系统版本。

> Git 配置

```shell
查看配置： 
	git config -l

查看系统配置： 
	git config --system --list

查看用户配置：
	git config --global --list 
```

### Git 相关的配置文件

1. C:\Program Files\Git\etc\gitconfig:	Git 安装目录的 gitconfig	--system 系统级
2. C:\Users\Value.DESKTOP-F8NSHR6\.gitconfig 只使用于当前登录用户的配置 --global 全局

> `设置用户名与邮箱（用户表示，必要）`

当安装完毕后首先要做的是设置用户名称和 e-mail 地址。非常重要！

```shell
git config --global user.name " "  		# 名称
git config --global user.email [地址]		# 邮箱
```

## Git 基本理论（核心）

> 工作区域

Git本地有三个工作区域：

- 工作目录（Working Directory）
- 暂存区（Stage/index）
- 资源库（Pepository或Git Directory）

如果在加上远程的 git 仓库（Remote Directory）既可以分为四个工作区。

文件在这四个区域之间的转换关系如下：

![image-20230611221625318](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230611221625318.png)

> 工作流程

git 的工作流程一般是这样的：

1. 在工作目录中添加、修改文件；		UserMapper.xml
2. 将需要进行版本管理的文件放入暂存区域；          git add
3. 将暂存区域的文件提交到 git 仓库。         git commit

因此，git管理的文件有三种状态，已修改（modified），已暂存（staged），已提交（committed）。

## Git 项目搭建

> 创建工作目录与常用指令

工作目录（WorkSpace）一般即使希望git帮助管理的文件夹，可以是项目的目录，也可以是一个空目录，建议不要有中文。

日常使用只要记住以下图6个命令：

![image-20230611224748844](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230611224748844.png)

> 本地仓库搭建

1、创建全新的仓库，需要使用Git管理的项目的根目录执行：

```shell
# 在当前目录新建一个Git仓库
$ git init
```

2、执行后可以看到，仅仅在项目目录多出了一个.git目录，关于版本等的所有信息都在这个目录里面。



> 克隆远程仓库

1、另一种方式是克隆远程目录，由于是将远程服务器上的仓库完全镜像一份至本地。

```shell
# 克隆一个项目和它的整个代码历史（版本信息）
$ git clone [url]
```

## Git文件操作

> 文件4种状态

版本控制就是对文件的版本控制，要对文件进行修改、提交等操作，首先要知道文件当前在什么状态，不然可能会提交了现在还不想提交的文件，或者要提交的文件没提交上。

- **Untracked:**未跟踪，此文件在文件夹中，但并没有加入到Git库，不参与版本控制，通过 ==Git add==状态变为==staged==。
- **Unmodify:**文件已经加入库，未修改，即版本库中的文件快照内容与文件夹中完全一致，这种类型的文件有两种去处，如果它被修改，而变为 ==Midified==。如果使用==git rm==移出版本库，则成为==Untracked==文件。
- **Modified:**文件已修改，仅仅是修改，并没有进行其他操作，这个文件也有两个去处，通过==git add==可进入暂存==staged==状态，使用==git checkout==则丢弃修改过，返回到==unmodify==状态，这个==git checkout==即从库中取出文件，覆盖当前修改！
- **Staged:**暂存状态，执行==git commit==则将修改同步到库中，这时库中的文件和本次文件又变为一致，文件为==Unmodify==状态，执行==git reset HEAD filename==取消暂存，文件状态为 ==Modified==。

> 查看文件状态

上面说的四种状态，通过如下命令可以查看到文件的状态：

```shell
# 查看指定文件状态
	git status [filename]

# 查看所有文件状态
	git status

# 添加所有文件到暂存区
	git add .
	
# 提交暂存区中的内容到本地仓库
	git commit -m "消息内容"
	git commit -m "new file test.txt"


```

设置本机绑定ssh 公钥

```shell
# 进入 C:\Users\Value.DESKTOP-F8NSHR6\.ssh 目录
# 生成公钥
# -t 后面可以跟上加密算法，例如：rsa
ssh-keygen 
```

## `说明：`Git 分支

**git 分支常用的命令：**

```shell
# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

# 新建一个分支，并切换到该分支
git chackout -b [branch]

# 合并指定分支到当前分支
git merge [branch]

# 删除分支
git branch -d [branch-name]

# 删除远程分支
git push origin --delete [branch-name]
git branch -dr [remote/branch]
```

如果同一个文件在合并分支时都被修改了则会引起冲突：解决的办法是可以修改冲突文件后重提交！选择保留他的代码还是你的代码！

==master主分支应该非常稳定，用来发布版本，一般情况下不允许在上面工作，工作一般情况下在新建的dev分支上工作，工作完后。==








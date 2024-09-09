

# 一般工作流程如下

克隆 Git 资源作为工作目录。
在克隆的资源上添加或修改文件。
如果其他人修改了，你可以更新资源。
在提交前查看修改。
提交修改。
在修改完成后，如果发现错误，可以撤回提交并再次修改并提交。

## 先来理解下 Git 工作区、暂存区和版本库概念

工作区：就是你在电脑里能看到的目录。
暂存区：英文叫 stage 或 index。一般存放在 .git 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
版本库：工作区有一个隐藏目录 .git，这个不算工作区，而是 Git 的版本库。

当对工作区修改（或新增）的文件执行 git add 命令时，暂存区的目录树被更新，
同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。

当执行提交操作（git commit）时，暂存区的目录树写到版本库（对象库）中，master 分支会做应的更新。
即 master 指向的目录树就是提交时暂存区的目录树。

当执行 git reset HEAD 命令时，暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。

```bash
当执行 git rm --cached<file>命令时，会直接从暂存区删除文件，工作区则不做出改变
当执行 git checkout . 或者 git checkout -- <file> 命令时，会用暂存区全部或指定的文件替换工作区的文件。
这个操作很危险，会清除工作区中未添加到暂存区中的改动。
当执行 git checkout HEAD . 或者 git checkout HEAD <file> 命令时，会用 HEAD 指向的master 
分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，
也会清除暂存区中未提交的改动。
```

## Git 创建仓库

本章节我们将为大家介绍如何创建一个 Git 仓库。

你可以使用一个已经存在的目录作为 Git 仓库。

```bash
git init
Git 使用 git init 命令来初始化一个 Git 仓库，Git 的很多命令都需要在 Git 的仓库中运行，所以 git init 是使用 Git 的第一个命令。

在执行完成 git init 命令后，Git 仓库会生成一个 .git 目录，该目录包含了资源的所有元数据，其他的项目目录保持不变。

使用方法
使用当前目录作为 Git 仓库，我们只需使它初始化。

git init
该命令执行完后会在当前目录生成一个 .git 目录。

使用我们指定目录作为Git仓库。

git init newrepo
初始化后，会在 newrepo 目录下会出现一个名为 .git 的目录，所有 Git 需要的数据和资源都存放在这个目录中。

如果当前目录下有几个文件想要纳入版本控制，需要先用 git add 命令告诉 Git 开始对这些文件进行跟踪，然后提交：

$ git add *.c
$ git add README
$ git commit -m '初始化项目版本'
以上命令将目录下以 .c 结尾及 README 文件提交到仓库中。

注： 在 Linux 系统中，commit 信息使用单引号 '，Windows 系统，commit 信息使用双引号 "。'

所以在 git bash 中 git commit -m '提交说明' 这样是可以的，在 Windows 命令行中就要使用双引号 git commit -m "提交说明"。

git clone
我们使用 git clone 从现有 Git 仓库中拷贝项目（类似 svn checkout）。

克隆仓库的命令格式为：

git clone <repo>
如果我们需要克隆到指定的目录，可以使用以下命令格式：

git clone <repo> <directory>
参数说明：

repo:Git 仓库。
directory:本地目录。
比如，要克隆 Ruby 语言的 Git 代码仓库 Grit，可以用下面的命令：

$ git clone git://github.com/schacon/grit.git
执行该命令后，会在当前目录下创建一个名为grit的目录，其中包含一个 .git 的目录，用于保存下载下来的所有版本记录。

如果要自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字：
$ git clone git://github.com/schacon/grit.git mygrit
配置
git 的设置使用 git config 命令。

显示当前的 git 配置信息：
$ git config --list
credential.helper=osxkeychain
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true编辑 git 配置文件:
$ git config -e    # 针对当前仓库 
或者：

$ git config -e --global   # 针对系统上所有仓库
设置提交代码时的用户信息：

$ git config --global user.name "runoob"
$ git config --global user.email test@runoob.com
如果去掉 --global 参数只对当前仓库有效。


创建仓库命令
	1、git init 命令
  Git 基本操作Git 基本操作

​```javascript
	git init 命令用于在目录中创建新的 Git 仓库。

	在目录中执行 git init 就可以创建一个 Git 仓库了。

	例如我们在当前目录下创建一个名为 runoob 的项目：

	实例
	$ mkdir runoob
	$ cd runoob/
	$ git init
	Initialized empty Git repository in /Users/tianqixin/www/runoob/.git/
	# 初始化空 Git 仓库完毕。
	现在你可以看到在你的项目中生成了 .git 这个子目录，这就是你的 Git 仓库了，所有有关你的此项目的快照数据都存放在这里。

	.git 默认是隐藏的，可以用 ls -a 命令查看：

	ls -a
	.    ..    .git
```

### 2、git clone 命令

Git 基本操作Git 基本操作

```bash
	git clone 拷贝一个 Git 仓库到本地，让自己能够查看该项目，或者进行修改。

	拷贝项目命令格式如下：

	 git clone [url]
	[url] 是你要拷贝的项目。

	例如我们拷贝 Github 上的项目：

	$ git clone https://github.com/tianqixin/runoob-git-test
	Cloning into 'runoob-git-test'...
	remote: Enumerating objects: 12, done.
	remote: Total 12 (delta 0), reused 0 (delta 0), pack-reused 12
	Unpacking objects: 100% (12/12), done.
	拷贝完成后，在当前目录下会生成一个 runoob-git-test 目录：

	$ cd simplegit/
	$ ls
	README.md    runoob-test.txt    test.txt
	上述操作将复制该项目的全部记录。

	$ ls -a
	.        ..        .git        README.md    runoob-test.txt    test.txt
	$ cd .git 
	$ ls
	HEAD        description    index        logs        packed-refs
	config        hooks        info        objects        refs
		默认情况下，Git 会按照你提供的 URL 所指向的项目的名称创建你的本地项目目录。 通常就是该 URL 最后一个 / 之后的项目名称。
	如果你想要一个不一样的名字， 你可以在该命令后加上你想要的名称。

	例如，以下实例拷贝远程 git 项目，本地项目名为 another-runoob-name：

	$ git clone https://github.com/tianqixin/runoob-git-test another-runoob-name
	Cloning into 'another-runoob-name'...
	remote: Enumerating objects: 12, done.
	remote: Total 12 (delta 0), reused 0 (delta 0), pack-reused 12
	Unpacking objects: 100% (12/12), done.
```

### 提交与修改

Git 的工作就是创建和保存你的项目的快照及与之后的快照进行对比。

```bash
1、git add 命令
	Git 基本操作Git 基本操作

	git add 命令可将该文件添加到暂存区。

	添加一个或多个文件到暂存区：

	git add [file1] [file2] ...
	添加指定目录到暂存区，包括子目录：

	git add [dir]
	添加当前目录下的所有文件到暂存区：

	git add .
	以下实例我们添加两个文件：

	$ touch README                # 创建文件
	$ touch hello.php             # 创建文件
	$ ls
	README        hello.php
	$ git status -s
	?? README
	?? hello.php
	$ 
```


```bash
	git status 命令用于查看项目的当前状态。

	接下来我们执行 git add 命令来添加文件：

	$ git add README hello.php 
	现在我们再执行 git status，就可以看到这两个文件已经加上去了。

	$ git status -s
	A  README
	A  hello.php
	$ 
```


```bash
	新项目中，添加所有文件很普遍，我们可以使用 git add . 命令来添加当前项目的所有文件。

	现在我们修改 README 文件：

	$ vim README
	在 README 添加以下内容：# Runoob Git 测试，然后保存退出。

	再执行一下 git status：

	$ git status -s
	AM README
	A  hello.php
```


```bash
	AM 状态的意思是这个文件在我们将它添加到缓存之后又有改动。改动后我们再执行 git add . 命令将其添加到缓存中：

	$ git add .
	$ git status -s
	A  README
	A  hello.php
	文件修改后，我们一般都需要进行 git add 操作，从而保存历史版本。
```


```bash
2、git status 命令
	Git 基本操作Git 基本操作

	git status 命令用于查看在你上次提交之后是否有对文件进行再次修改。

	$ git status
	On branch master

	Initial commit

	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)

	    new file:   README
	    new file:   hello.php
	通常我们使用 -s 参数来获得简短的输出结果：

	$ git status -s
	AM README
	A  hello.php
```


		AM 状态的意思是这个文件在我们将它添加到缓存之后又有改动。


```bash

	Git 基本操作Git 基本操作

	git diff 命令比较文件的不同，即比较文件在暂存区和工作区的差异。

	git diff 命令显示已写入暂存区和已经被修改但尚未写入暂存区文件的区别。

	git diff 有两个主要的应用场景。

	尚未缓存的改动：git diff
	查看已缓存的改动： git diff --cached
	查看已缓存的与未缓存的所有改动：git diff HEAD
	显示摘要而非整个 diff：git diff --stat
	显示暂存区和工作区的差异:

	$ git diff [file]
	显示暂存区和上一次提交(commit)的差异:

	$ git diff --cached [file]
	或
	$ git diff --staged [file]
	显示两次提交之间的差异:

	$ git diff [first-branch]...[second-branch]
	在 hello.php 文件中输入以下内容：

	<?php
	echo '菜鸟教程：www.runoob.com';
	?>
	使用 git status 查看状态：

	$ git status -s
	A  README
	AM hello.php
	$ git diff
	diff --git a/hello.php b/hello.php
	index e69de29..69b5711 100644
	--- a/hello.php
	+++ b/hello.php
	@@ -0,0 +1,3 @@
	+<?php
	+echo '菜鸟教程：www.runoob.com';
	+?>
	git status 显示你上次提交更新后的更改或者写入缓存的改动， 而 git diff 一行一行地显示这些改动具体是啥。

	接下来我们来查看下 git diff --cached 的执行效果：

	$ git add hello.php
	$ git status -s
	A  README
	A  hello.php
	$ git diff --cached
	diff --git a/README b/README
	new file mode 100644
	index 0000000..8f87495
	--- /dev/null
	+++ b/README
	@@ -0,0 +1 @@
	+# Runoob Git 测试
	diff --git a/hello.php b/hello.php
	new file mode 100644
	index 0000000..69b5711
	--- /dev/null
	+++ b/hello.php
	@@ -0,0 +1,3 @@
	+<?php
	+echo '菜鸟教程：www.runoob.com';
	+?>
```

###4、git commit 命令

```bash

	Git 基本操作Git 基本操作

	前面章节我们使用 git add 命令将内容写入暂存区。

	git commit 命令将暂存区内容添加到本地仓库中。

	提交暂存区到本地仓库中:

	git commit -m [message]
	[message] 可以是一些备注信息。

	提交暂存区的指定文件到仓库区：

	$ git commit [file1] [file2] ... -m [message]
	-a 参数设置修改文件后不需要执行 git add 命令，直接来提交

	$ git commit -a
	设置提交代码时的用户信息
	开始前我们需要先设置提交的用户信息，包括用户名和邮箱：

	$ git config --global user.name 'runoob'
	$ git config --global user.email test@runoob.com
	如果去掉 --global 参数只对当前仓库有效。

	提交修改
	接下来我们就可以对 hello.php 的所有改动从暂存区内容添加到本地仓库中。

	以下实例，我们使用 -m 选项以在命令行中提供提交注释。

	$ git add hello.php
	$ git status -s
	A  README
	A  hello.php
	$ git commit -m '第一次版本提交'
	[master (root-commit) d32cf1f] 第一次版本提交
	 2 files changed, 4 insertions(+)
	 create mode 100644 README
	 create mode 100644 hello.php
	 
	现在我们已经记录了快照。如果我们再执行 git status:

	$ git status
	# On branch master
	nothing to commit (working directory clean)
	以上输出说明我们在最近一次提交之后，没有做任何改动，是一个 "working directory clean"，翻译过来就是干净的工作目录。

	如果你没有设置 -m 选项，Git 会尝试为你打开一个编辑器以填写提交信息。 如果 Git 在你对它的配置中找不到相关信息，默认会打开 vim。屏幕会像这样：

	# Please enter the commit message for your changes. Lines starting
	# with '#' will be ignored, and an empty message aborts the commit.
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	# modified:   hello.php
	#
	~
	~
	".git/COMMIT_EDITMSG" 9L, 257C
	如果你觉得 git add 提交缓存的流程太过繁琐，Git 也允许你用 -a 选项跳过这一步。命令格式如下：

	git commit -a
	我们先修改 hello.php 文件为以下内容：

	<?php
	echo '菜鸟教程：www.runoob.com';
	echo '菜鸟教程：www.runoob.com';
	?>
	再执行以下命令：

	$ git commit -am '修改 hello.php 文件'
	[master 71ee2cb] 修改 hello.php 文件
	 1 file changed, 1 insertion(+)
```

###5、 git reset 命令

```bash

	Git 基本操作Git 基本操作

	git reset 命令用于回退版本，可以指定退回某一次提交的版本。

	git reset 命令语法格式如下：

	git reset [--soft | --mixed | --hard] [HEAD]
	--mixed 为默认，可以不用带该参数，用于重置暂存区的文件与上一次的提交(commit)保持一致，工作区文件内容保持不变。

	git reset  [HEAD] 
	实例：

	$ git reset HEAD^            # 回退所有内容到上一个版本  
	$ git reset HEAD^ hello.php  # 回退 hello.php 文件的版本到上一个版本  
	$ git  reset  052e           # 回退到指定版本
	--soft 参数用于回退到某个版本：

	git reset --soft HEAD
	实例：

	$ git reset --soft HEAD~3 # 回退上上上一个版本
	--hard 参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本，并删除之前的所有信息提交：

	git reset --hard HEAD
	实例：

	$ git reset –hard HEAD~3  # 回退上上上一个版本  
	$ git reset –hard bae128  # 回退到某个版本回退点之前的所有信息。 
	$ git reset --hard origin/master    # 将本地的状态回退到和远程的一样 
	注意：谨慎使用 –hard 参数，它会删除回退点之前的所有信息。

	HEAD 说明：

	HEAD 表示当前版本

	HEAD^ 上一个版本

	HEAD^^ 上上一个版本

	HEAD^^^ 上上上一个版本

	以此类推...

	可以使用 ～数字表示
	HEAD~0 表示当前版本

	HEAD~1 上一个版本

	HEAD^2 上上一个版本

	HEAD^3 上上上一个版本

	以此类推...

	git reset HEAD
	git reset HEAD 命令用于取消已缓存的内容。

	我们先改动文件 README 文件，内容如下：

	# Runoob Git 测试
	# 菜鸟教程 
	hello.php 文件修改为：

	<?php
	echo '菜鸟教程：www.runoob.com';
	echo '菜鸟教程：www.runoob.com';
	echo '菜鸟教程：www.runoob.com';
	?>
	现在两个文件修改后，都提交到了缓存区，我们现在要取消其中一个的缓存，操作如下：

	$ git status -s
	    M README
	    M hello.php
	$ git add .
	$ git status -s
	M  README
	M  hello.php
	$ git reset HEAD hello.php 
	Unstaged changes after reset:
	M    hello.php
	$ git status -s
	M  README
	    M hello.php
	现在你执行 git commit，只会将 README 文件的改动提交，而 hello.php 是没有的。

	$ git commit -m '修改'
	[master f50cfda] 修改
	    1 file changed, 1 insertion(+)
	$ git status -s
	    M hello.php
	可以看到 hello.php 文件的修改并未提交。

	这时我们可以使用以下命令将 hello.php 的修改提交：

	$ git commit -am '修改 hello.php 文件'
	[master 760f74d] 修改 hello.php 文件
	    1 file changed, 1 insertion(+)
	$ git status
	On branch master
	nothing to commit, working directory clean
	简而言之，执行 git reset HEAD 以取消之前 git add 添加，但不希望包含在下一提交快照中的缓存。
```

###6、git rm 命令


```bash

	Git 基本操作Git 基本操作

	git rm 命令用于删除文件。

	如果只是简单地从工作目录中手工删除文件，运行 git status 时就会在 Changes not staged for commit 的提示。

	git rm 删除文件有以下几种形式：

	1、将文件从暂存区和工作区中删除：

	git rm <file>
	以下实例从暂存区和工作区中删除 runoob.txt 文件：

	git rm runoob.txt 
	如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f。

	强行从暂存区和工作区中删除修改后的 runoob.txt 文件：

	git rm -f runoob.txt 
	如果想把文件从暂存区域移除，但仍然希望保留在当前工作目录中，换句话说，仅是从跟踪清单中删除，使用 --cached 选项即可：

	git rm --cached <file>
	以下实例从暂存区中删除 runoob.txt 文件：

	git rm --cached runoob.txt
	实例
	删除 hello.php 文件：

	$ git rm hello.php 
	rm 'hello.php'
	$ ls
	README
	文件从暂存区域移除，但工作区保留：

	$ git rm --cached README 
	rm 'README'
	$ ls
	README
	可以递归删除，即如果后面跟的是一个目录做为参数，则会递归删除整个目录中的所有子目录和文件：

	git rm –r * 
	进入某个目录中，执行此语句，会删除该目录下的所有文件和子目录。
```


```bash
6、git mv 命令
	Git 基本操作Git 基本操作

	git mv 命令用于移动或重命名一个文件、目录或软连接。

	git mv [file] [newfile]
	如果新文件名已经存在，但还是要重命名它，可以使用 -f 参数：

	git mv -f [file] [newfile]
	我们可以添加一个 README 文件（如果没有的话）：

	$ git add README 
	然后对其重命名:

	$ git mv README  README.md
	$ ls
	README.md
```



###提交日志

```bash
	Git 查看提交历史
	Git 提交历史一般常用两个命令：
	git log - 查看历史提交记录。
	git blame <file> - 以列表形式查看指定文件的历史修改记录。
	git log
	在使用 Git 提交了若干更新之后，又或者克隆了某个项目，想回顾下提交历史，我们可以使用 git log 命令查看。

	针对我们前一章节的操作，使用 git log 命令列出历史提交记录如下：

	$ git log
	commit d5e9fc2c811e0ca2b2d28506ef7dc14171a207d9 (HEAD -> master)
	Merge: c68142b 7774248
	Author: runoob <test@runoob.com>
	Date:   Fri May 3 15:55:58 2019 +0800

	    Merge branch 'change_site'

	commit c68142b562c260c3071754623b08e2657b4c6d5b
	Author: runoob <test@runoob.com>
	Date:   Fri May 3 15:52:12 2019 +0800

	    修改代码

	commit 777424832e714cf65d3be79b50a4717aea51ab69 (change_site)
	Author: runoob <test@runoob.com>
	Date:   Fri May 3 15:49:26 2019 +0800

	    changed the runoob.php

	commit c1501a244676ff55e7cccac1ecac0e18cbf6cb00
	Author: runoob <test@runoob.com>
	Date:   Fri May 3 15:35:32 2019 +0800
	我们可以用 --oneline 选项来查看历史记录的简洁的版本。

	$ git log --oneline
	$ git log --oneline
	d5e9fc2 (HEAD -> master) Merge branch 'change_site'
	c68142b 修改代码
	7774248 (change_site) changed the runoob.php
	c1501a2 removed test.txt、add runoob.php
	3e92c19 add test.txt
	3b58100 第一次版本提交
	这告诉我们的是，此项目的开发历史。

	我们还可以用 --graph 选项，查看历史中什么时候出现了分支、合并。以下为相同的命令，开启了拓扑图选项：

	*   d5e9fc2 (HEAD -> master) Merge branch 'change_site'
	|\  
	| * 7774248 (change_site) changed the runoob.php
	* | c68142b 修改代码
	|/  
	* c1501a2 removed test.txt、add runoob.php
	* 3e92c19 add test.txt
	* 3b58100 第一次版本提交
	现在我们可以更清楚明了地看到何时工作分叉、又何时归并。

	你也可以用 --reverse 参数来逆向显示所有日志。

	$ git log --reverse --oneline
	3b58100 第一次版本提交
	3e92c19 add test.txt
	c1501a2 removed test.txt、add runoob.php
	7774248 (change_site) changed the runoob.php
	c68142b 修改代码
	d5e9fc2 (HEAD -> master) Merge branch 'change_site'
	如果只想查找指定用户的提交日志可以使用命令：git log --author , 例如，比方说我们要找 Git 源码中 Linus 提交的部分：

	$ git log --author=Linus --oneline -5
	81b50f3 Move 'builtin-*' into a 'builtin/' subdirectory
	3bb7256 make "index-pack" a built-in
	377d027 make "git pack-redundant" a built-in
	b532581 make "git unpack-file" a built-in
	112dd51 make "mktag" a built-in
	如果你要指定日期，可以执行几个选项：--since 和 --before，但是你也可以用 --until 和 --after。

	例如，如果我要看 Git 项目中三周前且在四月十八日之后的所有提交，我可以执行这个（我还用了 --no-merges 选项以隐藏合并提交）：

	$ git log --oneline --before={3.weeks.ago} --after={2010-04-18} --no-merges
	5469e2d Git 1.7.1-rc2
	d43427d Documentation/remote-helpers: Fix typos and improve language
	272a36b Fixup: Second argument may be any arbitrary string
	b6c8d2d Documentation/remote-helpers: Add invocation section
	5ce4f4e Documentation/urls: Rewrite to accomodate transport::address
	00b84e9 Documentation/remote-helpers: Rewrite description
	03aa87e Documentation: Describe other situations where -z affects git diff
	77bc694 rebase-interactive: silence warning when no commits rewritten
	636db2c t3301: add tests to use --format="%N"
	更多 git log 命令可查看：http://git-scm.com/docs/git-log

	git blame
	如果要查看指定文件的修改记录可以使用 git blame 命令，格式如下：
	git blame <file>
	git blame 命令是以列表形式显示修改记录，如下实例：

	$ git blame README 
	^d2097aa (tianqixin 2020-08-25 14:59:25 +0800 1) # Runoob Git 测试
	db9315b0 (runoob    2020-08-25 16:00:23 +0800 2) # 菜鸟教程 
```



### 远程操作

####1、git remote 命令

```bash

	Git 基本操作Git 基本操作

	git remote 命令用于在远程仓库的操作。

	本章节内容我们将以 Github 作为远程仓库来操作，所以阅读本章节前需要先阅读关于 Github 的相关内容：Git 远程仓库(Github)。

	显示所有远程仓库：

	git remote -v
	以下我们先载入远程仓库，然后查看信息：

	$ git clone https://github.com/tianqixin/runoob-git-test
	$ cd runoob-git-test
	$ git remote -v
	origin  https://github.com/tianqixin/runoob-git-test (fetch)
	origin  https://github.com/tianqixin/runoob-git-test (push)
	origin 为远程地址的别名。

	显示某个远程仓库的信息：

	git remote show [remote]
	例如：

	$ git remote show https://github.com/tianqixin/runoob-git-test
	* remote https://github.com/tianqixin/runoob-git-test
	  Fetch URL: https://github.com/tianqixin/runoob-git-test
	  Push  URL: https://github.com/tianqixin/runoob-git-test
	  HEAD branch: master
	  Local ref configured for 'git push':
	    master pushes to master (local out of date)
	添加远程版本库：

	git remote add [shortname] [url]
	shortname 为本地的版本库，例如：

	# 提交到 Github
	$ git remote add origin git@github.com:tianqixin/runoob-git-test.git
	$ git push -u origin master
	其他相关命令：

	git remote rm name  # 删除远程仓库
	git remote rename old_name new_name  # 修改仓库名
	更多内容可以查看：Git 远程仓库(Github)。
```

####2、 git fetch 命令

```bash

	Git 基本操作Git 基本操作

	git fetch 命令用于从远程获取代码库。

	本章节内容我们将以 Github 作为远程仓库来操作，所以阅读本章节前需要先阅读关于 Github 的相关内容：Git 远程仓库(Github)。

	该命令执行完后需要执行 git merge 远程分支到你所在的分支。

	从远端仓库提取数据并尝试合并到当前分支：

	git merge
	该命令就是在执行 git fetch 之后紧接着执行 git merge 远程分支到你所在的任意分支。

	假设你配置好了一个远程仓库，并且你想要提取更新的数据，你可以首先执行:

	git fetch [alias]
	以上命令告诉 Git 去获取它有你没有的数据，然后你可以执行：

	git merge [alias]/[branch]
	以上命令将服务器上的任何更新（假设有人这时候推送到服务器了）合并到你的当前分支。

	本章节以 https://github.com/tianqixin/runoob-git-test 为例。

	接下来我们在 Github 上点击 README.md 并在线修改它:
```



```bash
	然后我们在本地更新修改。

	$ git fetch origin
	remote: Counting objects: 3, done.
	remote: Compressing objects: 100% (2/2), done.
	remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
	Unpacking objects: 100% (3/3), done.
	From github.com:tianqixin/runoob-git-test
	   0205aab..febd8ed  master     -> origin/master
	以上信息"0205aab..febd8ed master -> origin/master" 说明 master 分支已被更新，我们可以使用以下命令将更新同步到本地：

	$ git merge origin/master
	Updating 0205aab..febd8ed
	Fast-forward
	 README.md | 1 +
	 1 file changed, 1 insertion(+)
	查看 README.md 文件内容：

	$ cat README.md 
	# 菜鸟教程 Git 测试
	## 第一次修改内容
```

####3、 git pull 命令

```bash

	Git 基本操作Git 基本操作

	git pull 命令用于从远程获取代码并合并本地的版本。

	git pull 其实就是 git fetch 和 git merge FETCH_HEAD 的简写。

	命令格式如下：

	git pull <远程主机名> <远程分支名>:<本地分支名>
	实例
	更新操作：

	$ git pull
	$ git pull origin
	将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并。

	git pull origin master:brantest
	如果远程分支是与当前分支合并，则冒号后面的部分可以省略。

	git pull origin master
	上面命令表示，取回 origin/master 分支，再与本地的 brantest 分支合并。

	上面的 pull 操作用 fetch 表示为：

	以我的 https://github.com/tianqixin/runoob-git-test 为例，远程载入合并本地分支。

	$ git remote -v  # 查看信息
	origin    https://github.com/tianqixin/runoob-git-test (fetch)
	origin    https://github.com/tianqixin/runoob-git-test (push)

	$ git pull origin master
	From https://github.com/tianqixin/runoob-git-test
	 * branch            master     -> FETCH_HEAD
	Already up to date.
	上面命令表示，取回 origin/master 分支，再与本地的 master 分支合并。
```

####4、 git push 命令

```bash

	Git 基本操作Git 基本操作

	git push 命用于从将本地的分支版本上传到远程并合并。

	命令格式如下：

	git push <远程主机名> <本地分支名>:<远程分支名>如果本地分支名与远程分支名相同，则可以省略冒号：
	git push <远程主机名> <本地分支名>
	实例
	以下命令将本地的 master 分支推送到 origin 主机的 master 分支。

	$ git push origin master
	相等于：

	$ git push origin master:master
	如果本地版本与远程版本有差异，但又要强制推送可以使用 --force 参数：

	git push --force origin master
	删除主机的分支可以使用 --delete 参数，以下命令表示删除 origin 主机的 master 分支：

	git push origin --delete master
	以我的 https://github.com/tianqixin/runoob-git-test 为例，本地添加文件：

	$ touch runoob-test.txt      # 添加文件
	$ git add runoob-test.txt 
	$ git commit -m "添加到远程"
	master 69e702d] 添加到远程
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 runoob-test.txt

	$ git push origin master    # 推送到 Github
	将本地的 master 分支推送到 origin 主机的 master 分支。

	重新回到我们的 Github 仓库，可以看到文件已经提交上来了：
```




###Git 分支管理
		几乎每一种版本控制系统都以某种形式支持分支，一个分支代表一条独立的开发线。

使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的同时继续工作。

Git 分支实际上是指向更改快照的指针。

有人把 Git 的分支模型称为必杀技特性，而正是因为它，将 Git 从版本控制系统家族里区分出来。

###创建分支命令：

```bash
	git branch (branchname)
	切换分支命令:

	git checkout (branchname)
	当你切换分支的时候，Git 会用该分支的最后提交的快照替换你的工作目录的内容， 所以多个分支不需要多个目录。

	合并分支命令:

	git merge 
	你可以多次合并到统一分支， 也可以选择在合并之后直接删除被并入的分支。

	开始前我们先创建一个测试目录：

	$ mkdir gitdemo
	$ cd gitdemo/
	$ git init
	Initialized empty Git repository...
	$ touch README
	$ git add README
	$ git commit -m '第一次版本提交'
	[master (root-commit) 3b58100] 第一次版本提交
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 README
```
###Git 分支管理
```bash
列出分支
列出分支基本命令：

git branch
没有参数时，git branch 会列出你在本地的分支。

$ git branch

* master
  此例的意思就是，我们有一个叫做 master 的分支，并且该分支是当前分支。

当你执行 git init 的时候，默认情况下 Git 就会为你创建 master 分支。

如果我们要手动创建一个分支。执行 git branch (branchname) 即可。

$ git branch testing
$ git branch

* master
  testing
  现在我们可以看到，有了一个新分支 testing。

当你以此方式在上次提交更新之后创建了新分支，如果后来又有更新提交， 然后又切换到了 testing 分支，Git 将还原你的工作目录到你创建分支时候的样子。

接下来我们将演示如何切换分支，我们用 git checkout (branch) 切换到我们要修改的分支。

$ ls
README
$ echo 'runoob.com' > test.txt
$ git add .
$ git commit -m 'add test.txt'
[master 3e92c19] add test.txt
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
$ ls
README        test.txt
$ git checkout testing
Switched to branch 'testing'
$ ls
README
当我们切换到 testing 分支的时候，我们添加的新文件 test.txt 被移除了。切换回 master 分支的时候，它们又重新出现了。

$ git checkout master
Switched to branch 'master'
$ ls
README        test.txt
我们也可以使用 git checkout -b (branchname) 命令来创建新分支并立即切换到该分支下，从而在该分支中操作。

$ git checkout -b newtest
Switched to a new branch 'newtest'
$ git rm test.txt 
rm 'test.txt'
$ ls
README
$ touch runoob.php
$ git add .
$ git commit -am 'removed test.txt、add runoob.php'
[newtest c1501a2] removed test.txt、add runoob.php
 2 files changed, 1 deletion(-)
 create mode 100644 runoob.php
 delete mode 100644 test.txt
$ ls
README        runoob.php
$ git checkout master
Switched to branch 'master'
$ ls
README        test.txt
如你所见，我们创建了一个分支，在该分支上移除了一些文件 test.txt，并添加了 runoob.php 文件，然后切换回我们的主分支，删除的 test.txt 文件又回来了，且新增加的 runoob.php 不存在主分支中。

使用分支将工作切分开来，从而让我们能够在不同开发环境中做事，并来回切换。

删除分支
删除分支命令：

git branch -d (branchname)
例如我们要删除 testing 分支：

$ git branch

* master
  testing
  $ git branch -d testing
  Deleted branch testing (was 85fc7e7).
  $ git branch
* master
  分支合并
  一旦某分支有了独立内容，你终究会希望将它合并回到你的主分支。 你可以使用以下命令将任何分支合并到当前分支中去：

git merge
$ git branch

* master
  newtest
  $ ls
  README        test.txt
  $ git merge newtest
  Updating 3e92c19..c1501a2
  Fast-forward
   runoob.php | 0
   test.txt   | 1 -
   2 files changed, 1 deletion(-)
   create mode 100644 runoob.php
   delete mode 100644 test.txt
  $ ls
  README        runoob.php
  以上实例中我们将 newtest 分支合并到主分支去，test.txt 文件被删除。

合并完后就可以删除分支:

$ git branch -d newtest
Deleted branch newtest (was c1501a2).
删除后， 就只剩下 master 分支了：

$ git branch

* master
  合并冲突
  合并并不仅仅是简单的文件添加、移除的操作，Git 也会合并修改。

$ git branch

* master
  $ cat runoob.php
  首先，我们创建一个叫做 change_site 的分支，切换过去，我们将 runoob.php 内容改为:

<?php
echo 'runoob';
?>
创建 change_site 分支：

$ git checkout -b change_site
Switched to a new branch 'change_site'
$ vim runoob.php
$ head -3 runoob.php
<?php
echo 'runoob';
?>
$ git commit -am 'changed the runoob.php'
[change_site 7774248] changed the runoob.php
 1 file changed, 3 insertions(+)

将修改的内容提交到 change_site 分支中。 现在，假如切换回 master 分支我们可以看内容恢复到我们修改前的(空文件，没有代码)，我们再次修改 runoob.php 文件。

$ git checkout master
Switched to branch 'master'
$ cat runoob.php
$ vim runoob.php    # 修改内容如下
$ cat runoob.php
<?php
echo 1;
?>
$ git diff
diff --git a/runoob.php b/runoob.php
index e69de29..ac60739 100644
--- a/runoob.php
+++ b/runoob.php
@@ -0,0 +1,3 @@
+<?php
+echo 1;
+?>
$ git commit -am '修改代码'
[master c68142b] 修改代码
 1 file changed, 3 insertions(+)
现在这些改变已经记录到我的 "master" 分支了。接下来我们将 "change_site" 分支合并过来。

$ git merge change_site
Auto-merging runoob.php
CONFLICT (content): Merge conflict in runoob.php
Automatic merge failed; fix conflicts and then commit the result.

$ cat runoob.php     # 打开文件，看到冲突内容
<?php
<<<<<<< HEAD


=======
```

###分支

echo 'runoob';
>>>>>>> change_site
?>
我们将前一个分支合并到 master 分支，一个合并冲突就出现了，接下来我们需要手动去修改它。

$ vim runoob.php 
$ cat runoob.php
<?php
echo 1;
echo 'runoob';
?>
$ git diff
diff --cc runoob.php
index ac60739,b63d7d7..0000000
--- a/runoob.php
+++ b/runoob.php
@@@ -1,3 -1,3 +1,4 @@@
  <?php
 +echo 1;
+ echo 'runoob';
  ?>
在 Git 中，我们可以用 git add 要告诉 Git 文件冲突已经解决

$ git status -s
UU runoob.php
$ git add runoob.php
$ git status -s
M  runoob.php
$ git commit
[master 88afe0e] Merge branch 'change_site'
现在我们成功解决了合并中的冲突，并提交了结果




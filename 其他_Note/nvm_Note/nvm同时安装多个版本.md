## nvm 同时安装多个版本 node.js

要在的系统上同时安装多个版本的 Node.js，您可以使用 Node Version Manager (nvm) 工具。以下是使用 nvm 安装多个 Node.js 版本的一般步骤：

1. 下载和安装 nvm：

   - 对于 Windows 用户，可以从 nvm 的 GitHub 存储库[github](https://github.com/coreybutler/nvm-windows/releases)下载最新的可执行文件，并按照安装指南进行安装。

   - 对于 macOS 和 Linux 用户，可以使用以下命令在终端中安装 nvm：

     ```bash
     curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
     ```

2. 在新的终端窗口或会话中启用 nvm。这将加载 nvm 的环境变量和函数。对于 Windows 用户，您可以使用命令：

   ```shell
   nvm on
   ```

   对于 macOS 和 Linux 用户，可以使用命令：

   ```shell
   source ~/.nvm/nvm.sh
   ```

3. 安装所需的 Node.js 版本。您可以使用以下命令列出可用的 Node.js 版本：

   ```shell
   nvm ls
   ```

   ![image-20240312192138835](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240312192138835.png)

   - 然后，使用以下命令安装特定版本的 Node.js：

   ```shell
   nvm install <version>
   ```

   - 例如，要安装 Node.js 的 14.17.0 版本，可以运行：

   ```shell
   nvm install 14.17.0
   ```

4. 安装其他所需的 Node.js 版本，重复步骤 3。

5. 切换使用不同的 Node.js 版本。您可以使用以下命令切换到已安装的版本：

   ```shell
   nvm use <version>
   ```

   - 例如，要切换到 Node.js 的 14.17.0 版本，可以运行：

   
   ```shell
   nvm use 14.17.0
   ```
   
   - 如果您希望将该版本设置为默认版本，也可以使用以下命令：
   
   ```shell
   nvm alias default 14.17.0
   ```
   
   这将将 14.17.0 版本设置为默认版本，以便在没有指定版本的情况下使用。

通过执行上述步骤，您应该能够在您的系统上成功安装和管理多个 Node.js 版本。可以随时使用 `nvm use` 命令切换到所需的版本，并在不同的项目中使用不同的 Node.js 版本。

6. 如果安装错误，可以使用 nvm uninstall <版本号> 卸载指定版本的 node.js

```bash
nvm uninstall <version>		// 卸载指定版本的 node.js
```

nvm 其他一些常用的命令：

```bash
nvm install stable  //安装最新版 node
nvm install [node版本号]  //安装指定版本的node
nvm ls // 查看已安装版本
nvm use [node版本号]  //切换到指定版本的node
nvm alias default [node版本号] //设置默认版本
nvm list installed 查看已经安装的版本
nvm list available 查看网络可以安装的版本
nvm version 查看当前的版本
nvm install 安装最新版本nvm
nvm use <version> ## 切换使用指定的版本node
nvm current显示当前版本
nvm alias <name> <version> ## 给不同的版本号添加别名
nvm unalias <name> ## 删除已定义的别名
nvm reinstall-packages <version> ## 在当前版本node环境下，重新全局安装指定版本号的npm包
nvm on 打开nodejs控制
nvm off 关闭nodejs控制
nvm proxy 查看设置与代理
nvm node_mirror [url] 设置或者查看setting.txt中的node_mirror，如果不设置的默认是 https://nodejs.org/dist/
nvm npm_mirror [url] 设置或者查看setting.txt中的npm_mirror,如果不设置的话默认的是：https://github.com/npm/npm/archive/
nvm uninstall <version> 卸载制定的版本
nvm use [version] [arch] 切换制定的node版本和位数
nvm root [path] 设置和查看root路径

```


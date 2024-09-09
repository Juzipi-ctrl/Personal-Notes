## volta 命令使用方法

要使用 volta 管理 node.版本，可以按照以下步骤来进行设置和使用：

1. 安装 volta：可以从 volta 的官方网站 [Volta](https://volta.sh/) 下载适合于你操作系统的安装程序，并按照安装指南进行安装。

```bash
https://volta.sh/
```

2. 初始化 volta：在命令行终端中运行以下命令，以初始化并启动 volta：

```bash
volta setup
```

3. 安装 node.js：使用 volta 安装所需的 node.js 版本。例如，要安装 node.js 的  14.17.0 版本，可以运行以下命令：

```bash
volta install node@14.17.0
```

4. 使用 node.js：通过 volta 使用已经安装的 node.js版本。如果在全局范围内使用 node.js，可以直接运行 node 命令。例如：

```bash
node --version
```

![image-20240312194623584](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240312194623584.png)

5. 如果在项目中使用特定的 node.js 版本，可以进入项目目录，并使用 volta pin 命令，将该版本绑定到该项目。例如：

```bash
cd /path/to/project
volta pin node@14.17.0
```

这将确保项目在目录中使用特定的 node.js版本。

6. 管理 node.js 版本：使用 volta 进行其他 node.js 版本管理操作。例如，可以使用以下命令列出已经安装的 node.js 版本：

```bash
volta list
```

![image-20240312200914943](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240312200914943.png)

7. 如果安装错误，可以使用 volta uninstall 命令来删除已经安装在 volta install 中的任何全局包。

   ```bash
   volta unistall <version>		// 卸载指定的 node.js 版本。
   ```

   
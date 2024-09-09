## 在Windows10上卸载 webpack 并重新安装

1. 打开命令模式或powershell。也可以使用 win+x，选择命令提示符选择 Windows powershell。

2. 在命令行中输入，以下命令来卸载和全局安装 webpack：

```bash
npm uninstall webpack -g
```

这将卸载全局安装的 webpack包。

3. 接下来，如果你在项目中使用了局部安装的Webpack，进入你的项目目录。在命令提示符或PowerShell中，使用以下命令卸载局部安装的Webpack：

```bash
npm uninstall webpack
```

这将卸载项目中的Webpack包。

4. 确保你还卸载了与Webpack相关的其他依赖项。你可以使用类似的命令来卸载它们。例如：

```bash
npm uninstall webpack-cli
npm uninstall webpack-dev-server
```

这将卸载Webpack的CLI和开发服务器（如果有安装的话）。

5. 现在，Webpack已经被完全卸载了。你可以重新安装Webpack。

- 如果你只想在项目中使用Webpack，进入项目目录，并使用以下命令重新安装Webpack：

  ```bash
  npm install webpack --save-dev
  ```

  这将在项目中安装Webpack作为开发依赖项。

- 如果你想全局安装Webpack，可以使用以下命令：

  ```
  npm install webpack -g
  ```

  这将全局安装Webpack。

6. 安装完成后，你可以验证Webpack是否已正确安装。在命令提示符或PowerShell中，输入以下命令来检查Webpack的版本：

```bash
webpack --version
```

如果Webpack的版本号显示出来，说明安装成功。

现在，你已经成功卸载了Webpack并重新安装了它。你可以开始使用Webpack来构建你的项目了。
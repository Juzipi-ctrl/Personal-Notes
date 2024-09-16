## Python3 pip

pip 是 Python 包管理工具，该工具提供了对 Python 包的查找、下载、安装、卸载的功能。

软件包也可以在 https://pypi.org/ 中找到。

目前最新的 Python 版本已经预装了 pip。

查看是否已经安装 pip 可以使用以下命令：

```sh
pip --version
```

下载安装包使用以下命令：

```sh
pip install some-package-name
```

例如我们安装 numpy 包：

```sh
pip install numpy
```

我们也可以轻易地通过以下的命令来移除软件包：

```sh
pip uninstall some-package-name
```

例如我们移除 numpy 包：

```sh
pip uninstall numpy
```

如果要查看我们已经安装的软件包，可以使用以下命令：

```sh
pip list
```

## 导出当前 Python 环境的配置

要导出当前 Python 环境的配置，你可以使用 **pip freeze** 命令。

**pip freeze** 命令会列出当前环境中已安装的所有 Python 包及其版本信息，你可以将其保存到文件中，例如 requirements.txt，如下所示：

```sh
pip freeze > requirements.txt
```

以上命令将在当前目录下创建一个名为 **requirements.txt** 的文件，其中包含当前环境中已安装的所有包及其版本信息。

然后，你可以在其他地方使用该文件来重新创建相同的环境，运行以下命令：

```sh
pip install -r requirements.txt
```

以上命令会根据 **requirements.txt** 中列出的包及其版本信息重新安装所有必需的包，从而重建相同的环境。




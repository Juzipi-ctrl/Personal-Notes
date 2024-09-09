## npm 常用命令

npm是Node.js的包管理器，提供了一系列常用的命令来管理和操作Node.js包和项目。以下是一些常用的npm命令：

1. 初始化一个新的npm项目：

```shell
npm init		## 初始化
```

该命令将引导您创建一个新的npm项目，并生成一个`package.json`文件，用于描述项目的元数据和依赖项。

2. 安装项目依赖：

```shell
npm install		## 安装项目依赖
```

该命令将根据`package.json`文件中的依赖列表，安装项目所需的依赖包。

3. 安装特定的依赖包（作为项目的依赖）：

```shell
npm install package-name		## 指定项目依赖
```

该命令将安装指定的依赖包，并将其添加到项目的`package.json`文件中的`dependencies`部分。

- 例如，要安装一个名为`lodash`的包作为项目的依赖项，可以运行以下命令：

  ```shell
  npm install lodash
  ```

  希望这些说明能帮助您使用`npm install package-name`命令安装特定的包。

4. 安装特定的依赖包（作为开发依赖）：

```shell
npm install package-name --save-dev
```

该命令将安装指定的依赖包，并将其添加到项目的`package.json`文件中的`devDependencies`部分。开发依赖通常是项目开发、构建和测试所需的依赖。

- 使用 `jest` 来编写和运行测试。您可以使用以下命令安装 `jest` 作为开发依赖项：

  ```shell
  npm install jest --save-dev
  ```

  此命令将从npm注册表下载并安装 `jest` 包，然后将其添加到 `package.json` 文件的 `devDependencies` 部分。

  在安装完成后，您可以在项目中使用 `jest` 进行测试，例如编写测试用例并运行测试。

  在 `package.json` 文件中，您会看到类似以下的 `devDependencies` 部分：

  ```json
  "devDependencies": {
    "jest": "^27.0.6"
  }
  ```

  这表明 `jest` 已经作为开发依赖项添加到项目中。

5. 全局安装一个包：

```shell
npm install -g package-name
```

该命令将全局安装指定的包，使其在系统上可供全局使用。

6. 运行项目脚本：

```shell
npm run script-name
```

该命令将运行项目中定义的脚本。脚本定义在`package.json`文件的`scripts`部分。

7. 更新依赖包：

```shell
npm update
```

该命令将检查项目中的依赖，然后更新它们到最新版本。

8. 卸载依赖包：

```shell
npm uninstall package-name
```

该命令将卸载指定的依赖包，并从项目的`package.json`文件中删除相关的依赖项。

这些是一些常用的npm命令，用于管理Node.js包和项目。您可以根据自己的需求和项目要求使用这些命令。您可以通过运行`npm help`命令或查阅npm文档来获取更多关于npm命令的详细信息。
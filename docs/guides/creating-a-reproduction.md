# 创建复制品

复制是bug的简化版本，展示了特定的
错误发生的场景。它包括所有必要的最低设置
以及说明，在演示的同时应尽可能简单
问题。

## 指南

### 环境 <small>optional</small> { #environment }

我们建议使用[虚拟环境]，这是一个独立的Python运行时环境。
如果您在虚拟环境中，您安装或升级的任何软件包
将与环境融为一体。如果你遇到问题，你可以
只需删除并重新创建环境。设置起来很简单：

-   使用以下工具创建新的虚拟环境：

    ```
    python3 -m venv venv
    ```

-   通过以下方式激活环境：

    === ":material-apple: macOS"

        ``` sh
        . venv/bin/activate
        ```

    === ":fontawesome-brands-windows: Windows"

        ``` sh
        . venv/Scripts/activate
        ```

    === ":material-linux: Linux"

        ``` sh
        . venv/bin/activate
        ```


    您的终端现在应该在提示符前打印“（venv）”，这就是您
    知道你在刚刚创建的虚拟环境中。

-   使用以下命令退出环境：

    ```
    deactivate
    ```

  [virtual environment]: https://realpython.com/what-is-pip/#using-pip-in-a-python-virtual-environment

### 最小繁殖

按照以下说明，您将设置一个骨架项目来创建
复制品。如上所述，我们建议使用[虚拟环境]，
因此，在您的工作目录和新的虚拟环境中创建一个新文件夹
里面。下一个：

1.  正如我们的[错误报告指南]中提到的，请确保您正在运行
    最新版本的MkDocs材料，其中可能已经包含了对
    bug：

    ```
    pip install --upgrade --force-reinstall mkdocs-material
    ```

2.  使用`mkdocs`可执行文件启动一个新的文档项目，
    你用它作为复制的基础。创建一个
    为此新建空项目：

    ```
    mkdocs new .
    ```

    首先在`mkdocs.yml`中添加[最小配置]：

    ``` yaml
    theme:
      name: material
    ```

3.  现在，只需在`mkdocs.yml`中添加必要的设置，即可保持
    繁殖最少。如果您正在为渲染创建复制品
    bug，只创建必要数量的Markdown文档。__重复这个
    逐步执行，直到可以观察到要报告的错误。__

4.  作为最后一步，在将所有内容打包到“.zip”文件之前，请仔细检查
    所有设置和文档，如果它们对复制至关重要
    意味着当它们被省略时，错误不会发生。移除所有
    非必要的行和文件。

  [bug reporting guide]: ../contributing/reporting-a-bug.md#upgrade-to-latest-version
  [minimal configuration]: ../creating-your-site.md#minimal-configuration

### 创建“.zip”文件

MkDocs 9.0.0的材料包括一个专门用于创建
错误报告的复制品。启用内置信息插件后，MkDocs
将所有相关文件添加到“.zip”中，将摘要打印到终端，然后
出口。将以下行添加到`mkdocs.yml`中：

``` yaml
plugins:
  - info
```

现在，当运行`mkdocs-build`时，会自动生成一个名为`example.zip `的文件
已创建，包含可以直接附加到bug的最小复制
报告。

```
INFO     -  Started archive creation for bug report
INFO     -  Archive successfully created:

  example/.dependencies.json 859.0 B
  example/.versions.log 83.0 B
  example/docs/index.md 282.0 B
  example/mkdocs.yml 56.0 B

  example.zip 1.8 kB
```

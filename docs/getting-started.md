# 开始

Material for MkDocs是[MkDocs]之上的一个强大的文档框架，
用于项目文档的静态站点生成器。[^1]如果你熟悉
Python，你可以用[`pip`][pip]安装MkDocs的Material，Python
包管理器。如果没有，我们建议使用[`docker`][docker]。

  [^1]:
    2016年，Material for MkDocs开始是一个简单的MkDocs主题，但
    在几年的时间里，现在的情况远不止如此——
    许多内置插件、设置和无数自定义功能，
    Material for MkDocs现在是最简单、最强大的框架之一
    为您的项目创建文档。

  [MkDocs]: https://www.mkdocs.org
  [pip]: #with-pip
  [docker]: #with-docker

## 安装

### with pip <small>recommended</small> { #with-pip data-toc-label="with pip" }

Material for MkDocs以[Python package]的形式发布，可以安装
`pip`，理想情况下是通过使用[virtual environment]。打开终端并安装
Material for MkDocs，包括：

=== "Latest"

    ``` sh
    pip install mkdocs-material
    ```

=== "9.x"

    ``` sh
    pip install mkdocs-material=="9.*" # (1)!
    ```

    1.  Material for MkDocs使用[semantic versioning][^2]，这就是为什么它是一个
        将升级限制在当前主要版本是个好主意。

        这将确保您不会意外[升级到下一个
        主要版本]，其中可能包括破坏那些默默破坏的更改
        您的网站。此外，你可以使用`pip freeze`来创建一个锁文件，
        因此，构建在任何时候都是可重复的：

        ```
        pip freeze > requirements.txt
        ```

        Now, the lockfile can be used for installation:

        ```
        pip install -r requirements.txt
        ```

  [^2]:
    请注意，现有功能的改进有时会发布为
    补丁发布，例如改进内容选项卡的呈现，如
    它们不被认为是新功能。

这将自动安装所有依赖项的兼容版本：
[MkDocs], [Markdown], [Pygments]和[Python Markdown Extensions]。Material for MkDocs
始终致力于支持最新版本，因此没有必要
单独安装这些软件包。

---

:fontawesome-brands-youtube:{ style="color: #EE0F0F" }
__[How to set up Material for MkDocs]__ by @james-willett – :octicons-clock-24:
27m – 了解如何使用Material for MkDocs创建和托管文档网站
GitHub Pages上的分步指南。

  [How to set up Material for MkDocs]: https://www.youtube.com/watch?v=xlABhbnNrfI

---

!!! tip

    如果你之前没有Python的经验，我们建议你阅读
    [Using Python's pip to Manage Your Projects' Dependencies]，这是一个
    对Python包管理机制和
    帮助您在遇到错误时进行故障排除。

  [Python package]: https://pypi.org/project/mkdocs-material/
  [virtual environment]: https://realpython.com/what-is-pip/#using-pip-in-a-python-virtual-environment
  [semantic versioning]: https://semver.org/
  [upgrade to the next major version]: upgrade.md
  [Markdown]: https://python-markdown.github.io/
  [Pygments]: https://pygments.org/
  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/
  [Using Python's pip to Manage Your Projects' Dependencies]: https://realpython.com/what-is-pip/

### with docker

官方的[Docker image]是一个很好的启动和运行方式
分钟，因为它预装了所有依赖项。打开终端
并使用以下命令拉取图像：

=== "Latest"

    ```
    docker pull squidfunk/mkdocs-material
    ```

=== "9.x"

    ```
    docker pull squidfunk/mkdocs-material:9
    ```

`mkdocs`可执行文件作为入口点提供，`serve`是
默认命令。如果你不熟悉Docker，别担心，我们有你
将在以下章节中介绍。

以下插件与Docker镜像捆绑在一起：

- [mkdocs-minify-plugin]
- [mkdocs-redirects]

  [Docker image]: https://hub.docker.com/r/squidfunk/mkdocs-material/
  [mkdocs-minify-plugin]: https://github.com/byrnereese/mkdocs-minify-plugin
  [mkdocs-redirects]: https://github.com/datarobot/mkdocs-redirects

???+ warning

    Docker容器仅用于本地预览目的
    不适合部署。这是因为使用的web服务器
    用于实时预览的MkDocs不是为生产使用而设计的，可能具有
    安全漏洞。

??? question "如何向Docker镜像添加插件？"

    Material for MkDocs仅捆绑选定的插件以保持大小
    官方形象较小。如果您要使用的插件未包含在内，
    您可以轻松添加它们：

    === "Material for MkDocs"

        创建一个`Dockerfile`并扩展官方镜像：

        ``` Dockerfile title="Dockerfile"
        FROM squidfunk/mkdocs-material
        RUN pip install mkdocs-macros-plugin
        RUN pip install mkdocs-glightbox
        ```

    === "Insiders"

        Clone or fork Insiders存储库，并创建一个名为
        `user-requirements.txt`存储库根目录中。然后，添加
        应安装到文件中的插件，例如：

        ``` txt title="user-requirements.txt"
        mkdocs-macros-plugin
        mkdocs-glightbox
        ```

    接下来，使用以下命令构建映像：

    ```
    docker build -t squidfunk/mkdocs-material .
    ```

    新映像将安装其他软件包，可以使用
    就像官方形象一样。

### with git

Material for MkDocs 可以通过克隆直接从[GitHub]使用
将存储库放入项目根目录的子文件夹中，如果您
想要使用最新版本：

```
git clone https://github.com/squidfunk/mkdocs-material.git
```

接下来，使用以下命令安装主题及其依赖项：

```
pip install -e mkdocs-material
```

  [GitHub]: https://github.com/squidfunk/mkdocs-material

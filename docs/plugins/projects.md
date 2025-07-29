---
title: Built-in projects plugin
icon: material/folder-open
---

# 内置项目插件

项目插件增加了将主项目拆分为多个项目的能力
不同的项目，同时构建它们，并将它们作为一个整体一起预览。
这在创建多语言项目时特别有用，但也可以
用于将非常大的项目拆分为更小的部分。

---

`sponsors` __Sponsors only__ – this plugin is currently reserved to
[our awesome sponsors].

  [our awesome sponsors]: ../insiders/index.md

## Objective

### 工作原理

该插件扫描已配置的[`projects`目录][config.projects_dir]以查找
`mkdocs.yml`文件，标识所有嵌套项目并同时构建它们。
如果没有其他配置，插件希望您的项目具有
以下目录布局，例如用于多语言项目：

``` { .sh .no-copy }
.
├─ docs/
├─ projects/
│  ├─ en/
│  │  ├─ docs/
│  │  └─ mkdocs.yml
│  └─ de/
│     ├─ docs/
│     └─ mkdocs.yml
└─ mkdocs.yml
```

该插件最有用和最有趣的功能之一是它允许
从主项目中[预览您的网站]，同时仍然可以预览
并单独构建每个项目。这对于以下情况特别有用
多语言项目。

如果在[预览您的网站]时更改了其中一个项目中的文件
插件仅重建此项目，并确保MkDocs也会重新加载
相关文件。这也为拆分您的
将主项目拆分为多个项目，以获得更好的编辑体验。

有一些[限制]，但我们正在努力消除它们。

  [previewing your site]: ../creating-your-site.md#previewing-as-you-write
  [limitations]: #limitations

### 何时使用

该插件的出现是因为我们需要一个方便且可扩展的
构建我们的[示例]存储库的方法，该存储库具有许多自包含的特性
以及用户可以在以下情况下下载和使用的可运行项目
启动一个新项目或[创建复制品]。

当你想创建一个多语言项目，或者有一个非常大的现有项目时
在项目中，您可能会考虑使用该插件，因为它可以进行管理、编辑
让建筑更舒适。

  [examples]: https://github.com/mkdocs-material/examples
  [creating a reproduction]: ../guides/creating-a-reproduction.md

## 配置

`sponsors`
`version insiders-4.38.0`
`plugin [projects] – built-in`
`flag experimental`

为了开始使用项目插件，只需添加以下行
将主项目拆分为几个不同的项目
可以同时构建：

``` yaml
plugins:
  - projects
```

项目插件内置于MkDocs的Material中，不需要
安装。

  [projects]: projects.md

### 一般的

以下设置可用：

---

#### `setting config.enabled`

`sponsors`
`version insiders-4.38.0`
`default _true_`

使用此设置可在[构建项目]时启用或禁用插件。
如果你想禁用插件，例如，对于本地构建，你可以使用
`mkdocs.yml`中的[环境变量][mkdocs.env]：

``` yaml
plugins:
  - projects:
      enabled: !ENV [CI, false]
```

此配置仅在持续集成（CI）期间启用插件。

  [building your project]: ../creating-your-site.md#building-your-site

---

#### `setting config.concurrency`

`sponsors`
`version insiders-4.38.0`
`default available CPUs - 1`

有了更多的CPU可用，插件可以并行执行更多的工作，因此
更快地构建项目。如果你想完全禁用并发处理，
使用：

``` yaml
plugins:
  - projects:
      concurrency: 1
```

默认情况下，该插件使用所有可用的CPU-1，最小值为1。

### 缓存

该插件实现了[智能缓存]机制，确保
只有当项目内容发生变化时，才会重建项目。虽然最初的构建可能
花点时间，使用缓存是个好主意，因为它会加快连续运行的速度
建筑。

以下设置可用于缓存：

  [intelligent caching]: requirements/caching.md

---

#### `setting config.cache`

`sponsors`
`version insiders-4.38.0`
`default _true_`

使用此设置指示插件绕过缓存，以便
重建所有项目，即使缓存可能没有过时。通常不会
必须指定此设置，调试插件本身时除外。
可以通过以下方式禁用缓存：

``` yaml
plugins:
  - projects:
      cache: false
```

---

#### `setting config.cache_dir`

`sponsors`
`version insiders-4.38.0`
`default _.cache/plugin/projects_`

通常不需要指定此设置，除非您需要
更改根目录中缓存元数据的路径。
如果你想更改它，请使用：

``` yaml
plugins:
  - projects:
      cache_dir: my/custom/dir
```

### 登录中

以下设置可用于日志记录：

---

#### `setting config.log`

`sponsors`
`version insiders-4.47.0`
`default _true_`

使用此设置控制插件是否应显示来自的日志消息
在构建网站时进行项目。虽然不被推荐，但您可以禁用
使用以下方式登录：

``` yaml
plugins:
  - projects:
      log: false
```

---

#### `setting config.log_level`

`sponsors`
`version insiders-4.47.0`
`default _info_`

使用此设置控制插件在以下情况下应采用的日志级别
遇到错误，这要求[`log`][config.log]设置为
启用。以下日志级别可用：

=== "`error`"

    ``` yaml
    plugins:
      - projects:
          log_level: error
    ```

    只报告错误。

=== "`warn`"

    ``` yaml
    plugins:
      - projects:
          log_level: warn
    ```

    报告错误和警告，终止内置程序
    [严格][mkdocs.strict]模式。

=== "`info`"

    ``` yaml
    plugins:
      - projects:
          log_level: info
    ```

    报告错误、警告和信息性消息。

=== "`debug`"

    ``` yaml
    plugins:
      - projects:
          log_level: debug
    ```

    报告所有消息，包括调试消息。

### 工程

以下设置可用于项目：

---

#### `setting config.projects`

`sponsors`
`version insiders-4.38.0`
`default _true_`

使用此设置启用或禁用项目生成。目前
插件的唯一目的是构建项目，因此它相当于
[`enabled'][config.enabled]设置，但将来可能会有其他功能
补充。如果要禁用项目构建，请使用：

``` yaml
plugins:
  - projects:
      projects: false
```

---

#### `setting config.projects_dir`

`sponsors`
`version insiders-4.38.0`
`default _projects_`

使用此设置可以更改项目所在的文件夹。它是
通常不需要更改此设置，但如果要重命名
文件夹或更改其文件系统位置，使用：

``` yaml
plugins:
  - projects:
      projects_dir: projects
```

请注意，[`projects`目录][config.projects_dir]仅用于
项目组织-它不包含在项目URL中，因为项目是
由插件自动提升。

提供的路径是从根目录解析的。

---

#### `setting config.projects_config_files`

`sponsors`
`version insiders-4.42.0`
`default _*/mkdocs.yml_`

使用此设置更改配置文件的位置或名称
插件将在扫描[项目目录]时查找
[配置项目目录]。当出现以下情况时，可能需要调整此设置
配置文件位于项目的子目录中，例如。
`docs/mkdocs.yml`：

``` yaml
plugins:
  - projects:
      projects_config_files: "**/mkdocs.yml" # (1)!
```

1.  如果所有项目共享其配置文件的相同位置。，
    `docs/mkdocs.yml`，建议完全限定路径，因为它更快
    要解决比“**”glob模式更复杂的问题。

    ``` yaml
    plugins:
      - projects:
          projects_config_files: "*/docs/mkdocs.yml"
    ```

    此配置符合以下目录结构
    使用git子模块的项目常见：

    ``` { .sh .no-copy }
    .
    ├─ docs/
    ├─ projects/
    │  ├─ git-submodule-a/
    │  │  └─ docs/
    │  │     └─ mkdocs.yml
    │  └─ git-submodule-b/
    │     └─ docs/
    │        └─ mkdocs.yml
    └─ mkdocs.yml
    ```

提供的路径是从[“projects”目录]解析的
[配置项目目录]。

---

#### `setting config.projects_config_transform`

`sponsors`
`version insiders-4.42.0`
`default none`

使用此设置转换从读取的每个项目的配置
`mkdocs.yml`在构建之前，允许调整配置
在将它们构建在一起时，每个项目都是完整的，但在构建它们时，请保持不变
单独构建它们：

``` yaml
plugins:
  - projects:
      projects_config_transform: !!python/name:projects.transform
```

在Python的[modulesearch中查找提供的模块和函数名
路径]。构建时，您需要将根目录添加到搜索路径中
你的网站，所以Python可以解决它。最简单的方法是添加工作
[`PYTHONPATH`][PYTHONPATH]环境变量的目录：

``` .sh
export PYTHONPATH=.
```

!!! tip "如何定义配置转换函数"

    [`python/name`][python name]标签由[PyYAML]提供，必须指向
    在Python的[模块搜索路径]中找到一个有效的模块和函数名。
    插件将“project”和顶级“config”对象传递给
    功能。

    例如，我们可以继承[`use_directory_urls`]
    从顶层开始为所有项目设置[mkdocs.use_directory_urls]
    配置：

    ``` py title="projects/__init__.py"
    from mkdocs.config.defaults import MkDocsConfig

    # Transform project configuration
    def transform(project: MkDocsConfig, config: MkDocsConfig):
        project.use_directory_urls = config.use_directory_urls
    ```

  [module search path]: https://docs.python.org/3/library/sys_path_init.html
  [PYTHONPATH]: https://docs.python.org/3/using/cmdline.html#envvar-PYTHONPATH
  [python-name]: https://pyyaml.org/wiki/PyYAMLDocumentation#yaml-tags-and-python-types
  [PyYAML]: https://pyyaml.org/

### 变量提升

以下设置可用于吊装：

---

#### `setting config.hoisting`

`sponsors`
`version insiders-4.39.0`
`default _true_`

使用此设置启用或禁用将主题文件提升到主目录
项目。如果禁用此设置，每个项目都会收到
主题的文件，可以认为是多余的：

``` yaml
plugins:
  - projects:
      hoisting: false
```

通常建议启用吊装，因为它可以更快地部署
更快地加载项目的网站，因为文件与
所有项目都可以进行重复数据删除。

### 局限性

该插件是MkDocs Material的最新补充之一，这意味着它
它相当年轻，有一些局限性。我们正在努力移除它们，并且
我们很高兴收到反馈，了解您的要求？5800.
目前的限制是：

- __仅支持基本多语言__: 我们将调查如何提供
  更好地支持多语言项目，使互联更容易
  项目并在它们之间切换。

- __单独的搜索索引和站点地图__: 目前，这些项目完全
  分开，这意味着它们将有单独的搜索索引和站点地图。

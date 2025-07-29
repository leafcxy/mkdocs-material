---
title: 内置群组插件
icon: material/format-list-group
---

# 内置群组插件

组插件允许将插件有条件地分组到逻辑单元中
使用以下命令为特定环境启用或禁用它们
[环境变量][mkdocs.env]，例如，仅启用
在持续集成（CI）期间[构建项目]时使用插件。

  [building your project]: ../creating-your-site.md#building-your-site

## Objective

### 工作原理

该插件有条件地延迟加载属于某个组的所有插件
if and only if组已启用，这意味着插件不会添加任何
禁用组时的开销。这也意味着分组插件
仅在启用组时才需要安装。

属于该组的插件以相同的顺序执行，就像
它们是在[`plugins][mkdocs.plugins]列表的顶层定义的。
因此，秩序得以保留和确定。

### 何时使用

每当您使用仅在特定情况下需要的多个插件时
环境，例如在持续集成期间构建项目时
（CI），该插件是使配置更简单的完美工具，因为它
消除了将配置拆分为多个文件的需要。

它可以与任何内置或第三方插件一起使用。

## 配置

`version 9.3.0`
`plugin [group] – built-in`
`flag multiple`
`flag experimental`

与所有[内置插件]一样，开始使用组插件是
直截了当。只需将以下行添加到`mkdocs.yml`中，然后开始
将插件拆分为逻辑单元：

``` yaml
plugins:
  - group
```

组插件内置于MkDocs的Material中，不需要
安装。

  [group]: group.md
  [built-in plugins]: index.md

### 一般的

以下设置可用：

---

#### `setting config.enabled`

`version 9.3.0`
`default _false_`

使用此设置可在[构建项目]时启用或禁用插件。
该插件的行为与所有其他内置插件不同——它是
默认禁用__。要启用组，请使用：

``` yaml
plugins:
  - group:
      enabled: !ENV CI # (1)!
```

1.  如果你只想使用组插件来更好地组织和
    总是想启用其中的插件，请使用：

    ``` yaml
    plugins:
      - group:
          enabled: true
    ```

默认情况下禁用插件的决定是为了简化使用
环境变量，因为它消除了为提供默认值的需要
环境变量。

现在，在[构建项目]时，您可以通过设置
[环境变量][mkdocs.env]：

``` sh
CI=true mkdocs build
```

  [building your project]: ../creating-your-site.md#building-your-site

---

#### `setting config.plugins`

`version 9.3.0`
`default none`

使用此设置列出属于该组的插件。语法是
与[`plugins][mkdocs.plugins]设置完全相同，因此您可以
只需复制您要分组的插件列表，例如：

``` yaml
plugins:
  - group:
      plugins:
        - optimize
        - minify
```

这里提到的插件仅用于说明目的。

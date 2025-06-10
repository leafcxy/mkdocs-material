---
title: Built-in typeset plugin
icon: material/format-title
---

# 内置排版插件

排版插件允许保留丰富的标题和
导航和目录中的标题。这意味着代码
块、图标、表情符号和任何其他内联格式都可以精确呈现
如页面内容中所定义。

---

<!-- md:sponsors --> __Sponsors only__ – 此插件当前保留给
[our awesome sponsors].

  [our awesome sponsors]: ../insiders/index.md

## 客观的

### 工作原理

在[构建项目]时，MkDocs从标题和
删除原始格式。这通常是有用的，也是一个好主意，因为
此信息可供可能有问题的其他插件使用
当传递HTML而不是纯文本时。

但是，这也意味着整个格式丢失。

该插件连接到渲染过程中，提取原始标题，
并使其可用于模板和插件中。模板
MkDocs的材料使用此信息来呈现
导航和目录。

  [building your project]: ../creating-your-site.md#building-your-site

### 何时使用

通常建议使用插件，因为它是一个即插即用的解决方案
这不需要任何配置，并且设计为开箱即用。
由于它不会覆盖，只会添加信息，因此预计不会
干扰其他插件。

## 配置

<!-- md:sponsors -->
<!-- md:version insiders-4.27.0 -->
<!-- md:plugin [typeset] – built-in -->
<!-- md:flag experimental -->

与所有[内置插件]一样，开始使用排版插件是
直截了当。只需将以下行添加到`mkdocs.yml`中，并观察
丰富的导航和目录：

``` yaml
plugins:
  - typeset
```

排版插件内置于MkDocs的Material中，不需要
安装。

  [typeset]: typeset.md
  [built-in plugins]: index.md

### 一般的

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:sponsors -->
<!-- md:version insiders-4.27.0 -->
<!-- md:default `true` -->

使用此设置可在[构建项目]时启用或禁用插件。
通常不需要指定此设置，但如果要禁用
插件，使用：

``` yaml
plugins:
  - typeset:
      enabled: false
```

  [building your project]: ../creating-your-site.md#building-your-site

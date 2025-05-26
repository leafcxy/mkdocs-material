---
title: 内置排版插件
icon: material/format-title
---

# 内置排版插件

排版插件允许在导航和目录中保留标题和标题的丰富呈现。这意味着代码块、图标、表情符号和任何其他内联格式都可以按照页面内容中定义的方式精确渲染。

---

<!-- md:sponsors --> __仅限赞助者__ – 此插件目前仅提供给[我们优秀的赞助者]。

  [our awesome sponsors]: ../insiders/index.md

## 目标

### 工作原理

当[构建项目]时，MkDocs 从标题中提取纯文本并丢弃原始格式。这通常是有用的，也是一个好主意，因为这些信息可供其他插件使用，这些插件在传递 HTML 而不是纯文本时可能会遇到问题。

然而，这也意味着所有格式都会丢失。

该插件钩入渲染过程，提取原始标题，并使它们可用于模板和插件。Material for MkDocs 的模板使用这些信息来渲染导航和目录的丰富版本。

  [building your project]: ../creating-your-site.md#building-your-site

### 何时使用

通常建议使用该插件，因为它是一个即插即用的解决方案，不需要任何配置，设计为开箱即用。由于它不会覆盖而只是添加信息，因此预计不会干扰其他插件。

## 配置

<!-- md:sponsors -->
<!-- md:version insiders-4.27.0 -->
<!-- md:plugin [typeset] – built-in -->
<!-- md:flag experimental -->

与所有[内置插件]一样，开始使用排版插件非常简单。只需在 `mkdocs.yml` 中添加以下行，并观察丰富的导航和目录：

``` yaml
plugins:
  - typeset
```

排版插件已内置到 Material for MkDocs 中，无需安装。

  [typeset]: typeset.md
  [built-in plugins]: index.md

### 常规设置

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:sponsors -->
<!-- md:version insiders-4.27.0 -->
<!-- md:default `true` -->

使用此设置在[构建项目]时启用或禁用插件。通常不需要指定此设置，但如果您想禁用插件，请使用：

``` yaml
plugins:
  - typeset:
      enabled: false
```

  [building your project]: ../creating-your-site.md#building-your-site

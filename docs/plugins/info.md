---
title: 内置信息插件
icon: material/information
---

# 内置信息插件

info插件是一个专门用于创建自包含的实用程序
[报告错误]或提出建议时，将[最小复制]作为“.zip”文件
[变更请求]，使我们维护人员和您之间的沟通更加紧密
更容易，因为我们有共同点要努力。

  [minimal reproductions]: ../guides/creating-a-reproduction.md
  [reporting bugs]: ../contributing/reporting-a-bug.md
  [change requests]: ../contributing/requesting-a-change.md

## Objective

### 工作原理

该插件通过收集
有关项目环境和配置的必要信息。
这使我们更容易修复错误，因为它需要您
[升级到最新版本]和[删除您的自定义设置]。

遵循这些原则时，您可以确信您不会报告
已在后续版本中修复的错误，或由以下原因引起的错误
您的自定义项之一。更重要的是，你积极帮助
我们尽快修复这个bug。

插件的输出是一个“.zip”文件，您可以与我们的维护人员共享。

  [Upgrade to the latest version]: ../contributing/reporting-a-bug.md#upgrade-to-latest-version
  [Remove your customizations]: ../contributing/reporting-a-bug.md#remove-customizations


### 何时使用

每当你[报告bug][报告bug]或有什么要讨论的时候，
如问题或[变更请求][变更请求]，您应附上
一种小型、自给自足的小型繁殖体。可运行的示例有助于
沟通更加高效，让我们的维护人员有更多时间受益
通过推进项目来吸引更多用户。最低限度的复制是强制性的
用于错误报告。

## 配置

`version 9.0.0`
`plugin [info] – built-in`

为了开始使用内置的信息插件，只需添加以下内容
行到“mkdocs.yml”，并快速[创建最小复制]进行共享
与我们的维护人员：

``` yaml
plugins:
  - info
```

信息插件内置于MkDocs的Material中，不需要
安装。

  [info]: info.md
  [create a minimal reproduction]: ../guides/creating-a-reproduction.md

### 一般的

以下设置可用：

---

#### `setting config.enabled`

`version 9.0.0`
`default _true_`

使用此设置可在[构建项目]时启用或禁用插件。
通常不需要指定此设置，但如果要禁用
插件，使用：

``` yaml
plugins:
  - info:
      enabled: false
```

  [building your project]: ../creating-your-site.md#building-your-site

---

#### `setting config.enabled_on_serve`

`version 9.0.6`
`default _false_`

使用此设置控制在以下情况下是否应启用插件
[预览您的网站]。通常不需要指定此设置，
但如果你想改变这种行为，请使用：

``` yaml
plugins:
  - info:
      enabled_on_serve: true
```

此设置简化了创建和检查最小值的过程
复制，因为它允许快速迭代复制，而无需
必须先禁用插件。

  [previewing your site]: ../creating-your-site.md#previewing-as-you-write

### Archive

---

#### `setting config.archive`

`version 9.0.0`
`default _true_`

使用此设置控制插件是否应创建“.zip”文件
从项目中退出或在版本检查后退出。此设置仅用于
用于调试插件本身：

``` yaml
plugins:
  - info:
      archive: false
```

---

#### `setting config.archive_stop_on_violation`

`version 9.0.0`
`default _true_`

使用此设置控制插件是否应停止创建`.zip`
当其中一个[要求]未得到满足时。此设置必须仅为
用于与自定义相关的[报告错误][报告错误]
[在我们的文档中明确提及]。您可以通过以下方式进行更改：

``` yaml
plugins:
  - info:
      archive_stop_on_violation: false
```

如果您在[报告错误][报告错误]时使用此设置，请
解释为什么你认为有必要包括定制。如果你是
不确定，请先通过[创建讨论]向我们提问。

  [requirements]: #how-it-works
  [explicitly mentioned in our documentation]: ?q=%22extends+base%22
  [creating a discussion]: https://github.com/squidfunk/mkdocs-material/discussions

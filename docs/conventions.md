# 约定

本节解释了本文档中使用的几个约定。

## 符号

本文档使用一些符号进行说明。在阅读之前
请确保您已熟悉以下列表
习俗：

### `sponsors` – 仅限赞助商 { data-toc-label="仅限赞助商" }

跳动的心脏符号表示特定的特征或行为只是
赞助商可以通过[Insiders]获得。确保您有权访问
[Insiders]如果你想使用该功能。

### `version` – 版本 { data-toc-label="版本" }

标签符号与版本号一起表示特定的
添加了特征或行为。确保您至少使用此版本
如果你想使用它。

### `version insiders` – 版本 (Insiders)  { data-toc-label="版本 (Insiders)" }

带有心形和版本号的标签符号表示
特定功能或行为已添加到[Insiders]版本的Material中
MkDocs。

### `default` – 默认值 { #default data-toc-label="默认值" }

`mkdocs.yml`中的某些属性在作者不使用时具有默认值
明确地定义它们。属性的默认值始终包含在内。

#### `default computed` – 计算默认值 { #default data-toc-label="计算默认值" }

一些默认值不是设置为静态值，而是根据其他值计算的，
如网站语言、存储库提供商或其他设置。

#### `default none` – 默认值为空 { #default data-toc-label="默认值为空" }

某些属性不包含默认值。这意味着功能
除非明确启用，否则与它们关联的内容不可用。

### `flag metadata` – 元数据属性 { #metadata data-toc-label="元数据属性" }

此符号表示所描述的内容是元数据属性，它可以
可以在Markdown文档中用作前台定义的一部分。

### `flag multiple` – 多个实例 { #multiple-instances data-toc-label="多个实例" }

此符号表示插件支持多个实例，即
可以在`mkdocs.yml`的`plugins`设置中多次使用。

### `feature` – 可选功能 { #feature data-toc-label="可选功能" }

大多数功能都隐藏在功能标志后面，这意味着它们必须
可以通过`mkdocs.yml`显式启用。这允许存在
潜在的正交特征。

### `flag experimental` – 实验的 { data-toc-label="实验的" }

一些新功能仍被认为是实验性的，这意味着它们可能
（尽管很少）随时变化，包括完全移除（
尚未发生）。

### `plugin` – 插件 { data-toc-label="插件" }

通过MkDocs优秀的插件架构实现了几个功能，
其中一些是内置的，并与Material for MkDocs一起分发，所以没有
需要安装。

### `extension` – Markdown扩展名 { data-toc-label="Markdown扩展名" #extension }

此符号表示所描述的内容是Markdown扩展，它可以
在`mkdocs.yml`中启用，并为Markdown添加额外功能
解析器。

### `flag required` – 要求的值 { #required data-toc-label="要求的值" }

需要一些（实际上很少）属性或设置，这意味着
作者必须明确地定义它们。

### `flag customization` – 自定义 { #customization data-toc-label="自定义" }

此符号表示所描述的内容是一种定制，必须
由作者补充。

### `utility` – 实用 { data-toc-label="实用" }

除了插件，还有一些基于MkDocs构建的实用程序
提供扩展功能，例如支持版本控制。

  [Insiders]: insiders/index.md


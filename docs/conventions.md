# 约定

本节解释了本文档中使用的几个约定。

## 符号

本文档使用一些符号进行说明。在阅读之前，请确保您已熟悉以下约定：

### <!-- md:sponsors --> – 仅限赞助商 { data-toc-label="Sponsors only" }

跳动的心脏符号表示特定的功能或行为仅对[内部人士]赞助商可用。如果您想使用该功能，请确保您有权访问[内部人士]。

### <!-- md:version --> – 版本 { data-toc-label="Version" }

标签符号与版本号一起表示特定的功能或行为是在该版本中添加的。如果您想使用它，请确保您至少使用此版本。

### <!-- md:version insiders- --> – 版本 (内部人士)  { data-toc-label="Version (Insiders)" }

带有心形和版本号的标签符号表示特定功能或行为已添加到 Material for MkDocs 的[内部人士]版本中。

### <!-- md:default --> – 默认值 { #default data-toc-label="Default value" }

`mkdocs.yml` 中的某些属性在作者未明确定义时具有默认值。属性的默认值始终包含在内。

#### <!-- md:default computed --> – 计算默认值 { #default data-toc-label="is computed" }

一些默认值不是设置为静态值，而是根据其他值计算的，如网站语言、仓库提供商或其他设置。

#### <!-- md:default none --> – 默认值为空 { #default data-toc-label="is empty" }

某些属性不包含默认值。这意味着除非明确启用，否则与它们关联的功能不可用。

### <!-- md:flag metadata --> – 元数据属性 { #metadata data-toc-label="Metadata property" }

此符号表示所描述的内容是元数据属性，它可以在 Markdown 文档中用作前置定义的一部分。

### <!-- md:flag multiple --> – 多个实例 { #multiple-instances data-toc-label="Multiple instances" }

此符号表示插件支持多个实例，即可以在 `mkdocs.yml` 的 `plugins` 设置中多次使用。

### <!-- md:feature --> – 可选功能 { #feature data-toc-label="Optional feature" }

大多数功能都隐藏在功能标志后面，这意味着它们必须通过 `mkdocs.yml` 显式启用。这允许存在潜在的正交功能。

### <!-- md:flag experimental --> – 实验性 { data-toc-label="Experimental" }

一些新功能仍被认为是实验性的，这意味着它们可能（尽管很少）随时变化，包括完全移除（尚未发生）。

### <!-- md:plugin --> – 插件 { data-toc-label="Plugin" }

通过 MkDocs 优秀的插件架构实现了几个功能，其中一些是内置的，并与 Material for MkDocs 一起分发，所以不需要安装。

### <!-- md:extension --> – Markdown 扩展 { data-toc-label="Markdown extension" #extension }

此符号表示所描述的内容是 Markdown 扩展，它可以在 `mkdocs.yml` 中启用，并为 Markdown 解析器添加额外功能。

### <!-- md:flag required --> – 必需值 { #required data-toc-label="Required value" }

需要一些（实际上很少）属性或设置，这意味着作者必须明确定义它们。

### <!-- md:flag customization --> – 自定义 { #customization data-toc-label="Customization" }

此符号表示所描述的内容是一种自定义，必须由作者补充。

### <!-- md:utility --> – 实用工具 { data-toc-label="Utility" }

除了插件，还有一些基于 MkDocs 构建的实用工具，提供扩展功能，例如支持版本控制。

  [内部人士]: insiders/index.md


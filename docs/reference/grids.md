---
icon: material/view-grid-plus
---

# 网格

Material for MkDocs 让你可以轻松地将内容分区排列为网格，将传达相似含义或同等重要性的区块分组。网格非常适合用于构建索引页，能够简要展示文档某一大部分的概览。

## 配置

此配置启用网格功能，允许将相同或不同类型的区块排列为矩形。将以下内容添加到 `mkdocs.yml`：

``` yaml
markdown_extensions: # (1)!
  - attr_list
  - md_in_html
```

1.  请注意，下面部分示例使用了[图标和表情]，需要[单独配置]。

查看更多配置选项：

- [Attribute Lists]
- [Markdown in HTML]

  [icons and emojis]: icons-emojis.md
  [configured separately]: icons-emojis.md#configuration
  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists
  [Markdown in HTML]: ../setup/extensions/python-markdown.md#markdown-in-html

## 使用方法

网格有两种类型：[卡片网格]，每个元素都包裹在悬浮时会浮起的卡片中；[通用网格]，可以将任意区块元素排列为矩形。

  [card grids]: #using-card-grids
  [generic grids]: #using-generic-grids

### 使用卡片网格

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->

卡片网格会用漂亮的悬浮卡片包裹每个网格项，鼠标悬停时会浮起。它们有两种略有不同的语法：[列表语法]和[区块语法]，以适应不同的使用场景。

  [list]: #list-syntax
  [block syntax]: #block-syntax

#### 列表语法

列表语法本质上是[卡片网格]的快捷方式，由一个带有 `grid` 和 `cards` 类的 `div` 包裹的无序（或有序）列表组成：

``` html title="卡片网格"
<div class="grid cards" markdown>

- :fontawesome-brands-html5: __HTML__ 用于内容和结构
- :fontawesome-brands-js: __JavaScript__ 用于交互
- :fontawesome-brands-css3: __CSS__ 用于文本溢出盒子
- :fontawesome-brands-internet-explorer: __Internet Explorer__ ... 啊？

</div>
```

<div class="result" markdown>
  <div class="grid cards" markdown>

- :fontawesome-brands-html5: __HTML__ 用于内容和结构
- :fontawesome-brands-js: __JavaScript__ 用于交互
- :fontawesome-brands-css3: __CSS__ 用于文本溢出盒子
- :fontawesome-brands-internet-explorer: __Internet Explorer__ ... 啊？

  </div>
</div>

列表元素可以包含任意 Markdown，只要外层 `div` 定义了 `markdown` 属性。下面是一个更复杂的示例，包含图标和链接：

``` html title="卡片网格，复杂示例"
<div class="grid cards" markdown>

-   :material-clock-fast:{ .lg .middle } __5 分钟快速上手__

    ---

    使用 [`mkdocs-material`](#) 和 [`pip`](#) 安装，几分钟即可开始使用

    [:octicons-arrow-right-24: 快速开始](#)

-   :fontawesome-brands-markdown:{ .lg .middle } __就是 Markdown__

    ---

    专注于内容，生成响应式且可搜索的静态站点

    [:octicons-arrow-right-24: 参考文档](#)

-   :material-format-font:{ .lg .middle } __量身定制__

    ---

    只需几行代码即可更改颜色、字体、语言、图标、Logo 等

    [:octicons-arrow-right-24: 个性化定制](#)

-   :material-scale-balance:{ .lg .middle } __开源 MIT__

    ---

    Material for MkDocs 采用 MIT 许可协议，并在 [GitHub] 上开源

    [:octicons-arrow-right-24: 许可证](#)

</div>
```

<div class="result" markdown>
  <div class="grid cards" markdown>

-   :material-clock-fast:{ .lg .middle } __5 分钟快速上手__

    ---

    使用 [`mkdocs-material`][mkdocs-material] 和 [`pip`][pip] 安装，几分钟即可开始使用

    [:octicons-arrow-right-24: 快速开始][getting started]

-   :fontawesome-brands-markdown:{ .lg .middle } __就是 Markdown__

    ---

    专注于内容，生成响应式且可搜索的静态站点

    [:octicons-arrow-right-24: 参考文档][reference]

-   :material-format-font:{ .lg .middle } __量身定制__

    ---

    只需几行代码即可更改颜色、字体、语言、图标、Logo 等

    [:octicons-arrow-right-24: 个性化定制][customization]

-   :material-scale-balance:{ .lg .middle } __开源 MIT__

    ---

    Material for MkDocs 采用 MIT 许可协议，并在 [GitHub] 上开源

    [:octicons-arrow-right-24: 许可证][license]

  </div>
</div>

如果空间不足以并排显示网格项，项目会拉伸至视口的全部宽度，例如在移动端视口下。如果空间充足，网格会以 3 项及以上的形式排列，例如[隐藏两侧边栏]时。

  [mkdocs-material]: https://pypistats.org/packages/mkdocs-material
  [pip]: ../getting-started.md#with-pip
  [getting started]: ../getting-started.md
  [reference]: ../reference/index.md
  [customization]: ../customization.md
  [license]: ../license.md
  [GitHub]: https://github.com/squidfunk/mkdocs-material
  [hiding both sidebars]: ../setup/setting-up-navigation.md#hiding-the-sidebars

#### 区块语法

区块语法允许将卡片与其他元素__一起__排列为网格，如[通用网格]一节所述。只需在 `grid` 内的任意区块元素上添加 `card` 类即可：

``` html title="卡片网格，区块"
<div class="grid" markdown>

:fontawesome-brands-html5: __HTML__ 用于内容和结构
{ .card }

:fontawesome-brands-js: __JavaScript__ 用于交互
{ .card }

:fontawesome-brands-css3: __CSS__ 用于文本溢出盒子
{ .card }

> :fontawesome-brands-internet-explorer: __Internet Explorer__ ... 啊？

</div>
```

<div class="result" markdown>
  <div class="grid" markdown>

:fontawesome-brands-html5: __HTML__ 用于内容和结构
{ .card }

:fontawesome-brands-js: __JavaScript__ 用于交互
{ .card }

:fontawesome-brands-css3: __CSS__ 用于文本溢出盒子
{ .card }

> :fontawesome-brands-internet-explorer: __Internet Explorer__ ... 啊？

  </div>
</div>

虽然这种语法一开始看起来有些冗长，但上面的例子展示了卡片网格现在可以与其他元素混合，并且这些元素也会拉伸到网格中。

### 使用通用网格

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->

通用网格允许将任意区块元素排列为网格，包括[警告块]、[代码块]、[内容标签页]等。只需用带有 `grid` 类的 `div` 包裹一组区块即可：

``` html title="通用网格"
<div class="grid" markdown>

=== "无序列表"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "有序列表"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci

``` title="内容标签页"
=== "无序列表"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "有序列表"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci
```

</div>
```

<div class="result" markdown>
  <div class="grid" markdown>

=== "无序列表"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "有序列表"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci

``` title="内容标签页"
=== "无序列表"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "有序列表"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci
```

  </div>
</div>

通用网格会自动调整其布局以适应可用空间，就像[卡片网格]一样。如果空间不足，网格项会垂直堆叠；如果空间充足，它们会水平排列。网格项的数量和大小会自动调整，以充分利用可用空间。

  [admonitions]: admonitions.md
  [code blocks]: code-blocks.md
  [content tabs]: content-tabs.md

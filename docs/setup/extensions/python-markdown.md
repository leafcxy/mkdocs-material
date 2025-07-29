# Python Markdown

MkDocs的材料支持大量的[Python Markdown]扩展，
这也是它对技术写作如此有吸引力的部分原因。下列的
是所有支持的扩展的列表，链接到
参考需要启用哪些功能。

  [Python Markdown]: https://python-markdown.github.io/

## 支持的扩展

### 缩写

`version 1.0.0`
`extension [abbr][Abbreviations]`

[缩写]扩展增加了向
元素，通过用`abbr`标签包裹它。只有纯文本（无标记）
支持。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - abbr
```

没有可用的配置选项。使用方法见参考：

- [Adding abbreviations]
- [Adding a glossary]

  [Abbreviations]: https://python-markdown.github.io/extensions/abbreviations/
  [Adding abbreviations]: ../../reference/tooltips.md#adding-abbreviations
  [Adding a glossary]: ../../reference/tooltips.md#adding-a-glossary

### 告诫

`version 0.1.0`
`extension [admonition][Admonition]`

[Admonition]扩展增加了对警告的支持，通常称为
_call-outs_，可以使用简单的语法在Markdown中定义。使能够
通过`mkdocs.yml`：

``` yaml
markdown_extensions:
  - admonition
```

没有可用的配置选项。使用方法见参考：

- [Adding admonitions]
- [Changing the title]
- [Removing the title]
- [Supported types]

  [Admonition]: https://python-markdown.github.io/extensions/admonition/
  [Adding admonitions]: ../../reference/admonitions.md#usage
  [Changing the title]: ../../reference/admonitions.md#changing-the-title
  [Removing the title]: ../../reference/admonitions.md#removing-the-title
  [Supported types]: ../../reference/admonitions.md#supported-types

### 属性列表

`version 0.1.0`
`extension [attr_list][Attribute Lists]`

[Attribute Lists]扩展允许添加HTML属性和CSS类
到[几乎所有][属性列表限制]Markdown内联和块级别
具有特殊语法的元素。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - attr_list
```

没有可用的配置选项。使用方法见参考：

- [Using annotations]
- [Using grids]
- [Adding buttons]
- [Adding tooltips]
- [Using icons with colors]
- [Using icons with animations]
- [Image alignment]
- [Image lazy-loading]

  [Attribute Lists]: https://python-markdown.github.io/extensions/attr_list/
  [Attribute Lists limitations]: https://python-markdown.github.io/extensions/attr_list/#limitations
  [Using grids]: ../../reference/grids.md#using-grids
  [Adding buttons]: ../../reference/buttons.md#adding-buttons
  [Adding tooltips]: ../../reference/tooltips.md#adding-tooltips
  [Using icons with colors]: ../../reference/icons-emojis.md#with-colors
  [Using icons with animations]: ../../reference/icons-emojis.md#with-animations
  [Image alignment]: ../../reference/images.md#image-alignment
  [Image lazy-loading]: ../../reference/images.md#image-lazy-loading

### 定义列表

`version 1.1.0`
`extension [def_list][Definition Lists]`

[Definition Lists]扩展增加了添加定义列表的能力（更多
通常称为[描述列表]-HTML中的“dl”）通过Markdown转换为
文件。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - def_list
```

没有可用的配置选项。使用方法见参考：

- [Using definition lists]

  [Definition Lists]: https://python-markdown.github.io/extensions/definition_lists/
  [description lists]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dl
  [Using definition lists]: ../../reference/lists.md#using-definition-lists

### 脚注

`version 1.0.0`
`extension [footnotes][Footnotes]`

[Footnotes]扩展允许定义内联脚注，然后
在文档的所有Markdown内容下方呈现。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - footnotes
```

不支持任何配置选项。使用方法见参考：

- [Adding footnote references]
- [Adding footnote content]

  [Footnotes]: https://python-markdown.github.io/extensions/footnotes/
  [Adding footnote references]: ../../reference/footnotes.md#adding-footnote-references
  [Adding footnote content]: ../../reference/footnotes.md#adding-footnote-content

### HTML中的Markdown

`version 0.1.0`
`extension [md_in_html][Markdown in HTML]`

[Markdown in HTML]扩展允许在HTML中编写Markdown，
这对于用自定义元素包装Markdown内容非常有用。启用它
通过`mkdocs.yml`：

``` yaml
markdown_extensions:
  - md_in_html
```

> 默认情况下，Markdown忽略原始HTML块级别内的任何内容
> 元素。启用“md_in_html”扩展后，原始html的内容
> 通过包含“Markdown”，块级元素可以被解析为Markdown`
> 开始标记上的属性。`markdown`属性将被删除
> 输出，而所有其他属性将被保留。

没有可用的配置选项。使用方法见参考：

- [Using annotations]
- [Using grids]
- [Image captions]

  [Markdown in HTML]: https://python-markdown.github.io/extensions/md_in_html/
  [Using annotations]: ../../reference/annotations.md#usage
  [Using grids]: ../../reference/grids.md#usage
  [Image captions]: ../../reference/images.md#image-captions

### 目录

`version 0.1.0`
`extension [toc][Table of Contents]`

[目录]扩展会自动生成目录
从文档中，MkDocs的材料将作为结果的一部分呈现
页面。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - toc:
      permalink: true
```

支持以下配置选项：

`option toc.title`

:   `version 7.3.5` `default computed` –
    此选项在右侧导航中设置目录的标题
    侧边栏，通常自动来源于以下内容的翻译
    在`mkdocs.yml`中设置的[站点语言]：

    ``` yaml
    markdown_extensions:
      - toc:
          title: On this page
    ```

`option toc.permalink`

:   `default _false_` 此选项添加锚链接
    在末尾包含段落符号“¶”或其他自定义符号
    每个标题，与您当前查看的页面完全相同
    MkDocs的材料将在鼠标悬停时显示：

    === "¶"

        ``` yaml
        markdown_extensions:
          - toc:
              permalink: true
        ```

    === "⚓︎"

        ``` yaml
        markdown_extensions:
          - toc:
              permalink: ⚓︎
        ```

`option toc.permalink_title`

:   `default _Permanent link_` 此选项设置
    悬停时显示并由屏幕阅读器读取的锚链接的标题。
    出于可访问性的原因，将其更改为更易于访问的版本可能是有益的
    可辨别的名称，说明锚点链接到该部分本身：

    ``` yaml
    markdown_extensions:
      - toc:
          permalink_title: Anchor link to this section for reference
    ```

`option toc.slugify`

:   `default _toc.slugify_` 此选项允许
    slug功能的定制。对于某些语言，默认值可能不是
    生成良好且可读的标识符——考虑使用另一个slug函数
    例如[Python Markdown扩展][Slugs]中的那些：

    === "Unicode"

        ``` yaml
        markdown_extensions:
          - toc:
              slugify: !!python/object/apply:pymdownx.slugs.slugify
                kwds:
                  case: lower
        ```

    === "Unicode, case-sensitive"

        ``` yaml
        markdown_extensions:
          - toc:
              slugify: !!python/object/apply:pymdownx.slugs.slugify {}
        ```

`option toc.toc_depth`

:   `default _6_` 定义要设置的级别范围
    包括在目录中。这可能对项目有用
    具有深度结构化标题的文档，以缩短文档的长度
    目录，或完全删除目录：

    === "Hide levels 4-6"

        ``` yaml
        markdown_extensions:
          - toc:
              toc_depth: 3
        ```

    === "Hide table of contents"

        ``` yaml
        markdown_extensions:
          - toc:
              toc_depth: 0
        ```

此扩展的其他配置选项不受官方支持
MkDocs的材料，这就是为什么它们可能会产生意想不到的结果。使用
他们的风险由你自己承担。

  [Table of Contents]: https://python-markdown.github.io/extensions/toc/
  [site language]: ../changing-the-language.md#site-language
  [Slugs]: https://facelessuser.github.io/pymdown-extensions/extras/slugs/

### Tables

`version 0.1.0`
`extension [tables][Tables]`

[Tables]扩展通过使用
简单的语法。通过`mkdocs.yml`启用它（尽管它应该通过以下方式启用
默认值）：

``` yaml
markdown_extensions:
  - tables
```

没有可用的配置选项。使用方法见参考：

- [Using data tables]
- [Column alignment]

  [Tables]: https://python-markdown.github.io/extensions/tables/
  [Using data tables]: ../../reference/data-tables.md#usage
  [Column alignment]: ../../reference/data-tables.md#column-alignment

## 被取代的扩展

不支持（或可能不支持）以下[Python Markdown]扩展
不再推荐使用。相反，替代方案
应当予以考虑。

### Fenced Code Blocks

`version 0.1.0`
`extension [fenced_code_blocks][Fenced Code Blocks]`

被[超级围栏]取代。这个扩展可能仍然有效，但
[SuperFences]扩展在许多方面都是优越的，因为它允许任意
嵌套，因此建议。

  [Fenced Code Blocks]: https://python-markdown.github.io/extensions/fenced_code_blocks/
  [SuperFences]: https://facelessuser.github.io/pymdown-extensions/extensions/superfences/

### CodeHilite

`version 0.1.0`
`extension [codehilite][CodeHilite]`

被[突出显示]取代。对CodeHilite的支持已于年终止
<！--md:version6.0.0-->，因为[Highlight]与其他工具有更好的集成
基本扩展，如[超级围栏]和[内联Hilite]。

  [CodeHilite]: https://python-markdown.github.io/extensions/code_hilite/
  [CodeHilite support]: https://github.com/squidfunk/mkdocs-material/releases/tag/0.1.0
  [Highlight]: https://facelessuser.github.io/pymdown-extensions/extensions/highlight/
  [InlineHilite]: https://facelessuser.github.io/pymdown-extensions/extensions/inlinehilite/

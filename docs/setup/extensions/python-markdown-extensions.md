# Python Markdown扩展

[Python Markdown Extensions]包是一个出色的集合
额外的扩展非常适合高级技术写作。材料
对于MkDocs，它将此包列为显式依赖项，因此它会自动
已安装受支持的版本。

  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/

## 支持的扩展

一般来说，所有属于[Python Markdown extensions]的扩展都应该
使用MkDocs的材料。以下列表包括所有扩展
是原生支持的，这意味着它们无需任何进一步调整即可工作。

### Arithmatex

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.arithmatex][Arithmatex] -->

[Athmetex]扩展允许渲染块和内联块
方程式，并与[MathJax][^1]无缝集成——一个用于
数学排版。通过`mkdocs.yml`启用它：

  [^1]:
    其他库（如[KaTeX]）也受支持，可以与
    一些额外的努力。请参阅[KaTeX上的Arithmatex文档]
    进一步的指导，因为这超出了MkDocs材料的范围。

``` yaml
markdown_extensions:
  - pymdownx.arithmatex:
      generic: true
```

除了在`mkdocs.yml`中启用扩展之外，还有MathJax配置和
需要包含JavaScript运行时，这可以用几行代码完成
[附加JavaScript]：

=== ":octicons-file-code-16: `docs/javascripts/mathjax.js`"

    ``` js
    window.MathJax = {
      tex: {
        inlineMath: [["\\(", "\\)"]],
        displayMath: [["\\[", "\\]"]],
        processEscapes: true,
        processEnvironments: true
      },
      options: {
        ignoreHtmlClass: ".*|",
        processHtmlClass: "arithmatex"
      }
    };

    document$.subscribe(() => { // (1)!
      MathJax.startup.output.clearCache()
      MathJax.typesetClear()
      MathJax.texReset()
      MathJax.typesetPromise()
    })
    ```

    1. 这将MathJax与[即时加载]集成在一起


=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_javascript:
      - javascripts/mathjax.js
      - https://unpkg.com/mathjax@3/es5/tex-mml-chtml.js
    ```

此扩展的其他配置选项不受官方支持
MkDocs的材料，这就是为什么它们可能会产生意想不到的结果。使用
他们的风险由你自己承担。

使用方法见参考：

- [Using block syntax]
- [Using inline block syntax]

  [Arithmatex]: https://facelessuser.github.io/pymdown-extensions/extensions/arithmatex/
  [Arithmatex documentation on KaTeX]: https://facelessuser.github.io/pymdown-extensions/extensions/arithmatex/#loading-katex
  [MathJax]: https://www.mathjax.org/
  [KaTeX]: https://github.com/Khan/KaTeX
  [additional JavaScript]: ../../customization.md#additional-javascript
  [instant loading]: ../setting-up-navigation.md#instant-loading
  [Using block syntax]: ../../reference/math.md#using-block-syntax
  [Using inline block syntax]: ../../reference/math.md#using-inline-block-syntax

### BetterEm

<!-- md:version 0.1.0 -->
<!-- md:extension [pymdownx.betterem][BetterEm] -->

[BetterEm]扩展改进了标记的检测，以强调文本
在Markdown中使用特殊字符，即“**bold**”和“_italic”_`
格式化。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - pymdownx.betterem
```

此扩展的配置选项并不特定于材质
MkDocs，因为它们只影响Markdown解析阶段。请参阅[BetterEm
文档][BetterEm]了解更多信息。

  [BetterEm]: https://facelessuser.github.io/pymdown-extensions/extensions/betterem/

### Caption

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.blocks.caption][Caption] -->

[Caption]扩展增加了向任何Markdown块添加标题的能力，
包括图像、表格和代码块。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - pymdownx.blocks.caption
```

此扩展的配置选项并不特定于材质
MkDocs，因为它们只影响Markdown解析阶段。请参阅[标题
文档][标题]了解更多信息。

  [Caption]: https://facelessuser.github.io/pymdown-extensions/extensions/blocks/plugins/caption/

### Caret, Mark & Tilde

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.caret][Caret] -->

[Caret]、[Mark]和[Tilde]扩展增加了突出显示文本的功能
并使用简单的语法定义子和上标。让他们在一起
通过`mkdocs.yml`：

``` yaml
markdown_extensions:
  - pymdownx.caret
  - pymdownx.mark
  - pymdownx.tilde
```

此扩展的配置选项并不特定于材质
MkDocs，因为它们只影响Markdown解析阶段。参见[注意事项]，[标记]
以及[Tilde文档][Tilde]以获取指导。

使用方法见参考：

- [Highlighting text]
- [Sub- and superscripts]

  [Caret]: https://facelessuser.github.io/pymdown-extensions/extensions/caret/
  [Mark]: https://facelessuser.github.io/pymdown-extensions/extensions/mark/
  [Tilde]: https://facelessuser.github.io/pymdown-extensions/extensions/tilde/
  [Highlighting text]: ../../reference/formatting.md#highlighting-text
  [Sub- and superscripts]: ../../reference/formatting.md#sub-and-superscripts

### Critic

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.critic][Critic] -->

[Critic]扩展允许使用[Critic Markup]来突出显示
在文档中添加、删除或更新部分，即用于跟踪
Markdown语法。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - pymdownx.critic
```

支持以下配置选项：

<!-- md:option pymdownx.critic.mode -->

:   <!-- md:default `view` --> 此选项定义标记的方式
    应该被解析，即是否只“查看”所有建议的更改，或者
    或者“接受”或“拒绝”它们：

    === "View changes"

        ``` yaml
        markdown_extensions:
          - pymdownx.critic:
              mode: view
        ```

    === "Accept changes"

        ``` yaml
        markdown_extensions:
          - pymdownx.critic:
              mode: accept
        ```

    === "Reject changes"

        ``` yaml
        markdown_extensions:
          - pymdownx.critic:
              mode: reject
        ```

使用方法见参考：

- [Highlighting changes]

  [Critic]: https://facelessuser.github.io/pymdown-extensions/extensions/critic/
  [Critic Markup]: https://github.com/CriticMarkup/CriticMarkup-toolkit
  [Highlighting changes]: ../../reference/formatting.md#highlighting-changes

### Details

<!-- md:version 1.9.0 -->
<!-- md:extension [pymdownx.details][Details] -->

[详细信息]扩展增强了[警告]扩展，使
由此产生的全面折叠，允许它们被打开和关闭
用户。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - pymdownx.details
```

没有可用的配置选项。使用方法见参考：

- [Collapsible blocks]

  [Details]: https://facelessuser.github.io/pymdown-extensions/extensions/details/
  [Admonition]: python-markdown.md#admonition
  [Collapsible blocks]: ../../reference/admonitions.md#collapsible-blocks

### Emoji

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.emoji][Emoji] -->

表情符号扩展自动内联捆绑的和自定义的图标和表情
将`*.svg`文件格式转换为生成的HTML页面。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji # (1)!
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
```

1.  [Python Markdown扩展]使用“pymdownx”命名空间，但为了
    支持图标内联，必须使用`materialx`命名空间，因为它
    扩展了pymdownx的功能。

支持以下配置选项：

<!-- md:option pymdownx.emoji.emoji_index -->

:   <!-- md:default `emojione` --> 此选项定义了哪个集合
    emojis用于渲染。请注意，使用“emojione”不是
    由于[许可限制][表情符号索引]而推荐：

    ``` yaml
    markdown_extensions:
      - pymdownx.emoji:
          emoji_index: !!python/name:material.extensions.emoji.twemoji
    ```

<!-- md:option pymdownx.emoji.emoji_generator -->

:   <!-- md:default `to_png` --> 此选项定义了如何
    解析的表情符号或图标快捷代码被渲染。请注意，图标只能
    与`to_svg`配置一起使用：

    ``` yaml
    markdown_extensions:
      - pymdownx.emoji:
          emoji_generator: !!python/name:material.extensions.emoji.to_svg
    ```

<!-- md:option pymdownx.emoji.options.custom_icons -->

:   <!-- md:default none --> 此选项允许列出文件夹
    在Markdown或`mkdocs.yml`中使用额外的图标集，即
    在[图标定制指南]中有更详细的解释：

    ``` yaml
    markdown_extensions:
      - pymdownx.emoji:
          emoji_index: !!python/name:material.extensions.emoji.twemoji
          emoji_generator: !!python/name:material.extensions.emoji.to_svg
          options:
            custom_icons:
              - overrides/.icons
    ```

此扩展的其他配置选项不受官方支持
MkDocs的材料，这就是为什么它们可能会产生意想不到的结果。使用
他们的风险由你自己承担。

使用方法见参考：

- [Using emojis]
- [Using icons]
- [Using icons in templates]

  [Emoji]: https://facelessuser.github.io/pymdown-extensions/extensions/emoji/
  [Emoji index]: https://facelessuser.github.io/pymdown-extensions/extensions/emoji/#default-emoji-indexes
  [icon customization guide]: ../changing-the-logo-and-icons.md#additional-icons
  [Using emojis]: ../../reference/icons-emojis.md#using-emojis
  [Using icons]: ../../reference/icons-emojis.md#using-icons
  [Using icons in templates]: ../../reference/icons-emojis.md#using-icons-in-templates

### Highlight

<!-- md:version 5.0.0 -->
<!-- md:extension [pymdownx.highlight][Highlight] -->

[Highlight]扩展增加了对代码块语法高亮显示的支持
（借助[SuperFence][pymdownx.superfaces]）和内联代码块
（借助[InlineHilite][pymdownx.InlineHilite]）。通过启用它
`mkdocs.yml`：

``` yaml
markdown_extensions:
  - pymdownx.highlight:
      anchor_linenums: true
  - pymdownx.superfences # (1)!
```

1.  [Highlight]由[SuperFences][pymdownx.superfaces]扩展用于
    对代码块执行语法高亮显示，而不是相反，这
    这就是为什么还需要启用此扩展。

支持以下配置选项：

<!-- md:option pymdownx.highlight.use_pygments -->

:   <!-- md:default `true` --> 此选项允许控制
    是否应在构建时使用高亮显示
    [Pygages]或在浏览器中使用JavaScript语法高亮显示：

    === "Pygments"

        ``` yaml
        markdown_extensions:
          - pymdownx.highlight:
              use_pygments: true
          - pymdownx.superfences
        ```

    === "JavaScript"

        ``` yaml
        markdown_extensions:
          - pymdownx.highlight:
              use_pygments: false
        ```

        例如，[Highlight.js]是一个JavaScript语法高亮显示工具，可以
        与一些[额外的JavaScript]和[额外的样式]集成
        `mkdocs.yml`中的表格]：

        === ":octicons-file-code-16: `docs/javascripts/highlight.js`"

            ``` js
            document$.subscribe(() => {
              hljs.highlightAll()
            })
            ```

        === ":octicons-file-code-16: `mkdocs.yml`"

            ``` yaml
            extra_javascript:
              - https://cdnjs.cloudflare.com/ajax/libs/highlight.js/10.7.2/highlight.min.js
              - javascripts/highlight.js
            extra_css:
              - https://cdnjs.cloudflare.com/ajax/libs/highlight.js/10.7.2/styles/default.min.css
            ```

        请注意，[Highlight.js]与
        [Highlight][pymdownx.Highlight]扩展名。

    以下所有配置选项仅与构建时兼容
    使用[Pygges]突出显示语法，因此如果`use_Pygments，则不适用`
    设置为“false”。

<!-- md:option pymdownx.highlight.pygments_lang_class -->

:   <!-- md:default `false` --> 此选项指示[Pygages]
    添加一个CSS类来标识代码块的语言，即
    自定义注释标记正常工作所必需的：

``` yaml
markdown_extensions:
  - pymdownx.highlight:
      pygments_lang_class: true
```

<!-- md:option pymdownx.highlight.auto_title -->

:   <!-- md:default `false` --> 此选项将自动
    在所有代码块中添加一个[title]，显示所使用语言的名称
    例如，`Python`是为`py`块打印的：

    ``` yaml
    markdown_extensions:
      - pymdownx.highlight:
          auto_title: true
    ```

<!-- md:option pymdownx.highlight.linenums -->

:   <!-- md:default `false` --> 此选项将添加行号
    到所有代码块。如果你想在_some_中添加行号，但不是全部
    代码块，请参阅[添加行号][添加行]一节
    代码块参考中的数字]，其中还包含一些提示
    使用行号：

    ``` yaml
    markdown_extensions:
      - pymdownx.highlight:
          linenums: true
    ```

<!-- md:option pymdownx.highlight.linenums_style -->

:   <!-- md:default `table` --> [Highlight]扩展
    提供了三种添加行号的方法，其中两种方法由支持
    MkDocs的材料。而`table`将代码块包装在`<table>中`
    元素“pymdownx inline”将行号呈现为行本身的一部分：

    ``` yaml
    markdown_extensions:
      - pymdownx.highlight:
          linenums_style: pymdownx-inline
    ```

    请注意，`inline`将把行号放在实际代码旁边，这
    意味着在用光标选择文本时，它们将被包括在内，或者
    将代码块复制到剪贴板。因此，无论是“表”的使用`
    或者建议使用“pymdownx内联”。

<!-- md:option pymdownx.highlight.anchor_linenums -->

:   <!-- md:version 8.1.0 --> :octicons-milestone-24:
    默认值：“false”-如果代码块包含行号，则启用此选项
    设置将用锚链接包裹它们，这样它们就可以被超链接
    更容易分享：

    ``` yaml
    markdown_extensions:
      - pymdownx.highlight:
          anchor_linenums: true
    ```

<!-- md:option pymdownx.highlight.line_spans -->

:   <!-- md:default none --> 设置此选项后，每个
    代码块的行被包裹在“span”中，这对功能至关重要
    如线条高亮显示以正确工作：

    ``` yaml
    markdown_extensions:
      - pymdownx.highlight:
          line_spans: __span
    ```

此扩展的其他配置选项不受官方支持
MkDocs的材料，这就是为什么它们可能会产生意想不到的结果。使用
他们的风险由你自己承担。

使用方法见参考：

- [Using code blocks]
- [Adding a title]
- [Adding line numbers]
- [Highlighting specific lines]
- [Custom syntax theme]

  [Highlight]: https://facelessuser.github.io/pymdown-extensions/extensions/highlight/
  [CodeHilite]: python-markdown.md#codehilite
  [pymdownx.superfences]: #superfences
  [pymdownx.inlinehilite]: #inlinehilite
  [Pygments]: https://pygments.org
  [additional style sheet]: ../../customization.md#additional-css
  [Highlight.js]: https://highlightjs.org/
  [title]: ../../reference/code-blocks.md#adding-a-title
  [Adding line numbers]: ../../reference/code-blocks.md#adding-line-numbers
  [Using code blocks]: ../../reference/code-blocks.md#usage
  [Adding a title]: ../../reference/code-blocks.md#adding-a-title
  [Highlighting specific lines]: ../../reference/code-blocks.md#highlighting-specific-lines
  [Custom syntax theme]: ../../reference/code-blocks.md#custom-syntax-theme

### InlineHilite

<!-- md:version 5.0.0 -->
<!-- md:extension [pymdownx.inlinehilite][InlineHilite] -->

[InlineHilite]扩展增加了对内联代码语法高亮显示的支持
阻碍。它建立在[Highlight][pymdownx.Highlight]扩展之上，从
其来源于其配置。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - pymdownx.highlight
  - pymdownx.inlinehilite
```

此扩展的配置选项并不特定于材质
MkDocs，因为它们只影响Markdown解析阶段。唯一的例外是
[`css_class`][InlineHilite options]选项，不得更改。请参阅
[内联Hilite文档][内联Hilite]以获取指导。

使用方法见参考：

- [Highlighting inline code blocks]

  [InlineHilite]: https://facelessuser.github.io/pymdown-extensions/extensions/inlinehilite/
  [InlineHilite options]: https://facelessuser.github.io/pymdown-extensions/extensions/inlinehilite/#options
  [pymdownx.highlight]: #highlight
  [Highlighting inline code blocks]: ../../reference/code-blocks.md#highlighting-inline-code-blocks

### Keys

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.keys][Keys] -->

[Keys]扩展添加了一个简单的语法，允许渲染键盘
例如++ctrl+alt+del++。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - pymdownx.keys
```

此扩展的配置选项并不特定于材质
MkDocs，因为它们只影响Markdown解析阶段。唯一的例外是
[`class`][Keys-options]选项，不得更改。请参阅
[密钥文档][密钥]了解更多信息。

使用方法见参考：

- [Adding keyboard keys]

  [Keys]: https://facelessuser.github.io/pymdown-extensions/extensions/keys/
  [Keys options]: https://facelessuser.github.io/pymdown-extensions/extensions/keys/#options
  [Adding keyboard keys]: ../../reference/formatting.md#adding-keyboard-keys

### SmartSymbols

<!-- md:version 0.1.0 -->
<!-- md:extension [pymdownx.smartsymbols][SmartSymbols] -->

[SmartSymbols]扩展将某些字符序列转换为
例如版权符号或分数。通过启用它
`mkdocs.yml`：

``` yaml
markdown_extensions:
  - pymdownx.smartsymbols
```

此扩展的配置选项并不特定于材质
MkDocs，因为它们只影响Markdown解析阶段。请参阅[SmartSymbols
文档][SmartSymbols]以获取指导。

  [SmartSymbols]: https://facelessuser.github.io/pymdown-extensions/extensions/smartsymbols/

### Snippets

<!-- md:version 0.1.0 -->
<!-- md:extension [pymdownx.snippets][Snippets] -->

[Snippets]扩展增加了从任意文件嵌入内容的能力
通过使用简单的
语法。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - pymdownx.snippets
```

此扩展的配置选项并不特定于材质
MkDocs，因为它们只影响Markdown解析阶段。请参阅[片段
文档][片段]了解更多信息。

使用方法见参考：

- [Adding a glossary]
- [Embedding external files]

  [Snippets]: https://facelessuser.github.io/pymdown-extensions/extensions/snippets/
  [Adding a glossary]: ../../reference/tooltips.md#adding-a-glossary
  [Embedding external files]: ../../reference/code-blocks.md#embedding-external-files

### SuperFences

<!-- md:version 0.1.0 -->
<!-- md:extension [pymdownx.superfences][SuperFences] -->

[SuperFences]扩展允许任意嵌套代码和内容
相互之间的块，包括警告、标签、列表和所有其他
元素。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - pymdownx.superfences
```

支持以下配置选项：

<!-- md:option pymdownx.superfences.custom_fences -->

:   <!-- md:default none --> 此选项允许定义
    自定义围栏的处理程序，例如保留[Meamaid.js]的定义
    要在浏览器中解释的图表：

    ``` yaml
    markdown_extensions:
      - pymdownx.superfences:
          custom_fences:
            - name: mermaid
              class: mermaid
              format: !!python/name:pymdownx.superfences.fence_code_format
    ```

    请注意，这将主要防止语法高亮显示
    应用。请参阅[图表]上的参考，了解Mermaid.js是如何工作的
    与MkDocs材料集成。

此扩展的其他配置选项不受官方支持
MkDocs的材料，这就是为什么它们可能会产生意想不到的结果。使用
他们的风险由你自己承担。

使用方法见参考：

- [Using annotations]
- [Using code blocks]
- [Using content tabs]
- [Using flowcharts]
- [Using sequence diagrams]
- [Using state diagrams]
- [Using class diagrams]
- [Using entity-relationship diagrams]

  [SuperFences]: https://facelessuser.github.io/pymdown-extensions/extensions/superfences/
  [Fenced Code Blocks]: python-markdown.md#fenced-code-blocks
  [Mermaid.js]: https://mermaid-js.github.io/mermaid/
  [diagrams]: ../../reference/diagrams.md
  [Using annotations]: ../../reference/annotations.md#usage
  [Using content tabs]: ../../reference/content-tabs.md#usage
  [Using flowcharts]: ../../reference/diagrams.md#using-flowcharts
  [Using sequence diagrams]: ../../reference/diagrams.md#using-sequence-diagrams
  [Using state diagrams]: ../../reference/diagrams.md#using-state-diagrams
  [Using class diagrams]: ../../reference/diagrams.md#using-class-diagrams
  [Using entity-relationship diagrams]: ../../reference/diagrams.md#using-entity-relationship-diagrams

### Tabbed

<!-- md:version 5.0.0 -->
<!-- md:extension [pymdownx.tabbed][Tabbed] -->

[Tabbed]扩展允许使用内容选项卡，这是一种简单的分组方式
可访问选项卡下的相关内容和代码块。通过启用它
`mkdocs.yml`：

``` yaml
markdown_extensions:
  - pymdownx.tabbed:
      alternate_style: true
```

支持以下配置选项：

<!-- md:option pymdownx.tabbed.alternate_style -->

:   <!-- md:version 7.3.1 --> <!-- md:default `false` -->
    <!-- md:flag required -->  此选项启用内容选项卡
    [替代样式]，它在移动视口上具有更好的行为，并且
    唯一支持的样式：

    ``` yaml
    markdown_extensions:
      - pymdownx.tabbed:
          alternate_style: true
    ```

<!-- md:option pymdownx.tabbed.combine_header_slug -->

:   <!-- md:default `false` --> 此选项启用内容选项卡'
    [`combine_header_slug`style]标志，它将标头的id添加到
    选项卡的id：

    ``` yaml
    markdown_extensions:
      - pymdownx.tabbed:
          combine_header_slug: true
    ```

<!-- md:option pymdownx.tabbed.slugify -->

:   <!-- md:default `None` --> 此选项允许
    slug功能的定制。对于某些语言，默认值可能不是
    生成良好且可读的标识符——考虑使用另一个slug函数
    例如[Python Markdown扩展][Slugs]中的那些：

    === "Unicode"

        ``` yaml
        markdown_extensions:
          - pymdownx.tabbed:
              slugify: !!python/object/apply:pymdownx.slugs.slugify
                kwds:
                  case: lower
        ```

    === "Unicode, case-sensitive"

        ``` yaml
        markdown_extensions:
          - pymdownx.tabbed:
              slugify: !!python/object/apply:pymdownx.slugs.slugify {}
        ```

此扩展的其他配置选项不受官方支持
MkDocs的材料，这就是为什么它们可能会产生意想不到的结果。使用
他们的风险由你自己承担。

使用方法见参考：

- [Grouping code blocks]
- [Grouping other content]
- [Embedded content]

  [Tabbed]: https://facelessuser.github.io/pymdown-extensions/extensions/tabbed/
  [alternate style]: https://facelessuser.github.io/pymdown-extensions/extensions/tabbed/#alternate-style
  [combine_header_slug style]: https://facelessuser.github.io/pymdown-extensions/extensions/tabbed/#tab-ids
  [better behavior on mobile viewports]: https://x.com/squidfunk/status/1424740370596958214
  [Grouping code blocks]: ../../reference/content-tabs.md#grouping-code-blocks
  [Grouping other content]: ../../reference/content-tabs.md#grouping-other-content
  [Embedded content]: ../../reference/content-tabs.md#embedded-content
  [Slugs]: https://facelessuser.github.io/pymdown-extensions/extras/slugs/

### Tasklist

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.tasklist][Tasklist] -->

[Tasklist]扩展允许使用[GitHub风味Markdown]
受启发的[任务列表][任务列表规范]，遵循相同的语法
习俗。通过`mkdocs.yml`启用它：

``` yaml
markdown_extensions:
  - pymdownx.tasklist:
      custom_checkbox: true
```

支持以下配置选项：

<!-- md:option pymdownx.tasklist.custom_checkbox -->

:   <!-- md:default `false` --> 此选项可切换渲染
    复选框的样式，用漂亮的图标替换原生复选框样式，
    因此建议：

    ``` yaml
    markdown_extensions:
      - pymdownx.tasklist:
          custom_checkbox: true
    ```

<!-- md:option pymdownx.tasklist.clickable_checkbox -->

:   <!-- md:default `false` --> 此选项切换是否
    复选框是可点击的。由于状态不持久，因此使用此
    从用户体验的角度来看，选项是_rather discused_：

    ``` yaml
    markdown_extensions:
      - pymdownx.tasklist:
          clickable_checkbox: true
    ```

此扩展的其他配置选项不受官方支持
MkDocs的材料，这就是为什么它们可能会产生意想不到的结果。使用
他们的风险由你自己承担。

使用方法见参考：

- [Using task lists]

  [Tasklist]: https://facelessuser.github.io/pymdown-extensions/extensions/tasklist/
  [GitHub Flavored Markdown]: https://github.github.com/gfm/
  [Tasklist specification]: https://github.github.com/gfm/#task-list-items-extension-
  [Using task lists]: ../../reference/lists.md#using-task-lists

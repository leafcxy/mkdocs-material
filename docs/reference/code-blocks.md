---
icon: material/code-json
---

# 代码块

代码块和示例是技术项目文档的重要组成部分。Material for MkDocs 提供了不同的方式来设置代码块的语法高亮，可以在构建时使用 [Pygments] 或在运行时使用 JavaScript 语法高亮器。

  [Pygments]: https://pygments.org

## 配置

此配置启用了代码块和内联代码块的语法高亮，并允许直接从其他文件包含源代码。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite
  - pymdownx.snippets
  - pymdownx.superfences
```

以下部分讨论如何将不同的语法高亮功能与推荐的 [Pygments] 一起使用，因此这些功能在使用 JavaScript 语法高亮器时不适用。

查看更多配置选项：

- [Highlight]
- [InlineHilite]
- [SuperFences]
- [Snippets]

  [Highlight]: ../setup/extensions/python-markdown-extensions.md#highlight
  [InlineHilite]: ../setup/extensions/python-markdown-extensions.md#inlinehilite
  [SuperFences]: ../setup/extensions/python-markdown-extensions.md#superfences
  [Snippets]: ../setup/extensions/python-markdown-extensions.md#snippets

### 代码复制按钮

<!-- md:version 9.0.0 -->
<!-- md:feature -->

代码块可以自动在右侧渲染一个按钮，允许用户将代码块的内容复制到剪贴板。将以下内容添加到 `mkdocs.yml` 以全局启用它们：

``` yaml
theme:
  features:
    - content.code.copy
```

??? info "为特定代码块启用或禁用代码复制按钮"

    如果您不想全局启用代码复制按钮，可以使用基于 [Attribute Lists] 扩展的略微不同的语法为特定代码块启用它们：

    ```` yaml
    ``` { .yaml .copy }
    # 代码块内容
    ```
    ````

    请注意，必须有一个语言短代码，它必须放在第一位，并且必须以 `.` 为前缀。同样，也可以为特定代码块禁用复制按钮：

    ```` { .yaml .no-copy }
    ``` { .yaml .no-copy }
    # 代码块内容
    ```
    ````

    要在不使用语法高亮的情况下启用或禁用复制按钮，您可以使用 `.text` 语言短代码，它不会高亮任何内容。

### 代码选择按钮

<!-- md:sponsors -->
<!-- md:version insiders-4.32.0 -->
<!-- md:flag experimental -->

代码块可以包含一个按钮，允许用户选择行范围，这对于链接到代码块的特定子部分非常完美。这允许用户动态应用[行高亮]。将以下内容添加到 `mkdocs.yml` 以全局启用它：

``` yaml
theme:
  features:
    - content.code.select
```

??? info "为特定代码块启用或禁用代码选择按钮"

    如果您不想全局启用代码选择按钮，可以使用基于 [Attribute Lists] 扩展的略微不同的语法为特定代码块启用它们：

    ```` yaml
    ``` { .yaml .select }
    # 代码块内容
    ```
    ````

    请注意，必须放在第一位的语言短代码现在也必须以 `.` 为前缀。同样，也可以为特定代码块禁用选择按钮：

    ```` { .yaml .no-select }
    ``` { .yaml .no-select }
    # 代码块内容
    ```
    ````

  [line highlighting]: #highlighting-specific-lines

### 代码注释

<!-- md:version 8.0.0 -->
<!-- md:feature -->

代码注释提供了一种舒适和友好的方式，通过在代码块的语言中添加数字标记和行内注释，将任意内容附加到代码块的特定部分。将以下内容添加到 `mkdocs.yml` 以全局启用它们：

``` yaml
theme:
  features:
    - content.code.annotate # (1)!
```

1.  :man_raising_hand: 我是一个代码注释！我可以包含 `code`、__格式化文本__、图片，...基本上任何可以用 Markdown 编写的内容。

??? info "为特定代码块启用代码注释"

    如果您不想全局启用代码注释，因为您不喜欢自动内联行为，可以使用基于 [Attribute Lists] 扩展的略微不同的语法为特定代码块启用它们：

    ```` yaml
    ``` { .yaml .annotate }
    # 代码块内容
    ```
    ````

    请注意，必须放在第一位的语言短代码现在也必须以 `.` 为前缀。

  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists

#### 自定义选择器

<!-- md:sponsors -->
<!-- md:version insiders-4.32.0 -->
<!-- md:flag experimental -->

通常，代码注释只能[放在注释中]，因为注释可以被认为是安全的放置位置。但是，有时可能需要在不允许注释的代码块部分放置注释，例如在字符串中。

可以按语言设置额外的选择器：

``` yaml
extra:
  annotate:
    json: [.s2] # (1)!
```

1.  [`.s2`][s2] 是 [Pygments] 为双引号字符串生成的词法单元的名称。如果您想在注释以外的词法单元中使用代码注释，请检查代码块并确定需要添加到额外选择器列表中的词法单元。

    __重要__：代码注释不能在词法单元之间分割。

现在，可以在 JSON 的字符串中使用代码注释：

``` json
{
  "key": "value (1)"
}
```

1.  :man_raising_hand: 我是一个代码注释！我可以包含 `code`、__格式化文本__、图片，...基本上任何可以用 Markdown 编写的内容。

  [placed in comments]: #adding-annotations
  [s2]: https://github.com/squidfunk/mkdocs-material/blob/87d5ca487b9d9ab95c41ee72813149d214048693/src/assets/stylesheets/main/extensions/pymdownx/_highlight.scss#L45

## 使用方法

代码块必须用包含三个反引号的两个单独行括起来。要为这些块添加语法高亮，请在开始块后直接添加语言短代码。查看[可用词法分析器列表]以找到给定语言的短代码：

```` markdown title="代码块"
``` py
import tensorflow as tf
```
````

<div class="result" markdown>

``` py
import tensorflow as tf
```

</div>

  [list of available lexers]: https://pygments.org/docs/lexers/

### 添加标题

为了提供额外的上下文，可以通过在短代码后直接使用 `title="<custom title>"` 选项为代码块添加自定义标题，例如显示文件名：

```` markdown title="带标题的代码块"
``` py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
````

<div class="result" markdown>

``` py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

</div>

### Adding annotations

Code annotations can be placed anywhere in a code block where a comment for the
language of the block can be placed, e.g. for JavaScript in `#!js // ...` and
`#!js /* ... */`, for YAML in `#!yaml # ...`, etc.[^1]:

  [^1]:
    Code annotations require syntax highlighting with [Pygments] – they're
    currently not compatible with JavaScript syntax highlighters, or languages
    that do not have comments in their grammar. However, we're actively working
    on supporting alternate ways of defining code annotations, allowing to
    always place code annotations at the end of lines.

```` markdown title="Code block with annotation"
``` yaml
theme:
  features:
    - content.code.annotate # (1)
```

1.  :man_raising_hand: I'm a code annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be written in Markdown.
````

<div class="result" markdown>

``` yaml
theme:
  features:
    - content.code.annotate # (1)
```

1.  :man_raising_hand: I'm a code annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be written in Markdown.

</div>

#### Stripping comments

<!-- md:version 8.5.0 -->
<!-- md:flag experimental -->

如果您希望去除代码注释周围的注释字符，只需在代码注释的右括号后添加一个 `!`：

```` markdown title="带注释的代码块，已去除注释"
``` yaml
# (1)!
```

1.  看，减少了行噪声！
````

<div class="result" markdown>

``` yaml
# (1)!
```

1.  看，减少了行噪声！

</div>

请注意，这只允许每个注释渲染一个代码注释。如果您想添加多个代码注释，由于技术原因，注释不能被去除。

### Adding line numbers

可以通过在短代码后直接使用 `linenums="<start>"` 选项为代码块添加行号，其中 `<start>` 表示起始行号。代码块可以从 `1` 以外的行号开始，这允许为了可读性而分割大型代码块：

```` markdown title="带行号的代码块"
``` py linenums="1"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
````

<div class="result" markdown>

``` py linenums="1"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

</div>

### Highlighting specific lines

可以通过将行号传递给放在语言短代码后面的 `hl_lines` 参数来高亮特定行。请注意，无论作为 [`linenums`][添加行号] 的一部分指定的起始行号如何，行计数都从 `1` 开始：

=== "行"

    ```` markdown title="带高亮行的代码块"
    ``` py hl_lines="2 3"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```
    ````

    <div class="result" markdown>

    ``` py linenums="1" hl_lines="2 3"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```

    </div>

=== "行范围"

    ```` markdown title="带高亮行范围的代码块"
    ``` py hl_lines="3-5"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```
    ````

    <div class="result" markdown>

    ``` py linenums="1" hl_lines="3-5"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```

    </div>

  [Adding line numbers]: #adding-line-numbers

### Highlighting inline code blocks

启用 [InlineHilite] 后，可以通过在它们前面加上 shebang（即 `#!`）并直接跟随相应的[语言短代码][可用词法分析器列表]来对内联代码块应用语法高亮。

``` markdown title="内联代码块"
`#!python range()` 函数用于生成数字序列。
```

<div class="result" markdown>

`#!python range()` 函数用于生成数字序列。

</div>

### Embedding external files

启用 [Snippets] 后，可以通过在代码块内直接使用 [`--8<--` 表示法][Snippets notation] 来嵌入其他文件（包括源文件）的内容：

```` markdown title="带外部内容的代码块"
``` title=".browserslistrc"
;--8<-- ".browserslistrc"
```
````

<div class="result" markdown>

``` title=".browserslistrc"
last 4 years
```

</div>

  [Snippets notation]: https://facelessuser.github.io/pymdown-extensions/extensions/snippets/#snippets-notation

## Customization

### Custom syntax theme

如果使用 [Pygments]，Material for MkDocs 提供了[代码块样式][colors]，这些样式使用自定义且平衡的调色板构建，同样适用于两种[配色方案]：

- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-number-color) " } `--md-code-hl-number-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-special-color) " } `--md-code-hl-special-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-function-color) " } `--md-code-hl-function-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-constant-color) " } `--md-code-hl-constant-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-keyword-color) " } `--md-code-hl-keyword-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-string-color) " } `--md-code-hl-string-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-name-color) " } `--md-code-hl-name-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-operator-color) " } `--md-code-hl-operator-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-punctuation-color) " } `--md-code-hl-punctuation-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-comment-color) " } `--md-code-hl-comment-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-generic-color) " } `--md-code-hl-generic-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-variable-color) " } `--md-code-hl-variable-color`

代码块前景色、背景色和行高亮颜色通过以下方式定义：

- :material-checkbox-blank-circle:{ style="color: var(--md-code-fg-color) " } `--md-code-fg-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-bg-color) " } `--md-code-bg-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-color) " } `--md-code-hl-color`

假设您想更改 `#!js "strings"` 的颜色。虽然有几种[字符串标记类型]，但它们使用相同的颜色。您可以通过使用[额外的样式表]分配新颜色：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    :root > * {
      --md-code-hl-string-color: #0FF1CE;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

如果您想调整特定类型的字符串，例如 ``#!js `backticks` ``，您可以在[语法主题定义]中查找特定的 CSS 类名，并作为[额外的样式表]的一部分覆盖它：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    .highlight .sb {
      color: #0FF1CE;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

  [colors]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/assets/stylesheets/main/_colors.scss
  [color schemes]: ../setup/changing-the-colors.md#color-scheme
  [types of string tokens]: https://pygments.org/docs/tokens/#literals
  [additional style sheet]: ../customization.md#additional-css
  [syntax theme definition]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/assets/stylesheets/main/extensions/pymdownx/_highlight.scss

### Annotation tooltip width

如果您的代码注释中托管了大量内容，可以通过在[额外的样式表]中添加以下内容来增加提示框的宽度：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    :root {
      --md-tooltip-width: 600px;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

这将使用更大的宽度渲染注释：

<div style="--md-tooltip-width: 600px;" markdown>

``` yaml
# (1)!
```

1. Muuuuuuuuuuuuuuuch more space for content

</div>

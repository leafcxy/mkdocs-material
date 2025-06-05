---
icon: material/code-json
---

# 代码块

代码块和示例是技术项目的重要组成部分
文档。MkDocs的材料提供了不同的语法设置方法
在构建时使用[Pygges]或
在运行时使用JavaScript语法高亮显示。

  [Pygments]: https://pygments.org

## 配置

此配置允许在代码块和内联代码上突出显示语法
块，并允许直接包含来自其他文件的源代码。添加
将以下行转换为`mkdocs.yml`：

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

以下部分讨论了如何使用不同的语法突出显示功能
使用[Pygges]，推荐的高亮显示，因此在使用时不适用
JavaScript语法高亮显示。

请参阅其他配置选项：

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

代码块可以自动在右侧呈现一个按钮，以允许
用户将代码块的内容复制到剪贴板。添加以下内容
`mkdocs.yml`以全局启用它们：

``` yaml
theme:
  features:
    - content.code.copy
```

??? info "启用或禁用特定代码块的代码复制按钮"

    如果您不想全局启用代码复制按钮，可以启用它们
    对于特定的代码块，使用基于
    [属性列表]扩展名：

    ```` yaml
    ``` { .yaml .copy }
    # Code block content
    ```
    ````

    请注意，必须有一个语言简码，它必须放在第一位
    还必须以“”作为前缀。`.同样，复制按钮也可以
    针对特定代码块禁用：

    ```` { .yaml .no-copy }
    ``` { .yaml .no-copy }
    # Code block content
    ```
    ````

    要启用或禁用复制按钮而不突出显示语法，您可以
    使用“.text”语言短代码，它不会突出显示任何内容。

### 代码选择按钮

<!-- md:sponsors -->
<!-- md:version insiders-4.32.0 -->
<!-- md:flag experimental -->

代码块可以包括一个按钮，允许通过以下方式选择行范围
用户，这非常适合链接到代码块的特定子部分。这允许用户动态应用[行突出显示]。添加以下内容
要全局启用`mkdocs.yml`：

``` yaml
theme:
  features:
    - content.code.select
```

??? info "启用或禁用特定代码块的代码选择按钮"

    如果不想全局启用代码选择按钮，可以启用
    通过使用基于以下内容的略有不同的语法，将它们用于特定的代码块
    [属性列表]扩展：

    ```` yaml
    ``` { .yaml .select }
    # Code block content
    ```
    ````

    请注意，必须先出现的语言简码现在也必须是
    前缀为`。`.同样，也可以禁用选择按钮
    特定代码块：

    ```` { .yaml .no-select }
    ``` { .yaml .no-select }
    # Code block content
    ```
    ````

  [line highlighting]: #highlighting-specific-lines

### 代码注释

<!-- md:version 8.0.0 -->
<!-- md:feature -->

代码注释提供了一种舒适友好的方式来附加任意
通过在代码块中添加数字标记，将内容添加到代码块的特定部分
以及代码块语言的内联注释。添加以下内容
`mkdocs.yml`以全局启用它们：

``` yaml
theme:
  features:
    - content.code.annotate # (1)!
```

1.  :man_raising_hand：我是一个代码注释！我可以包含__格式的“代码”
    text__、图像、。..基本上任何可以用Markdown写的东西。

??? info "为特定代码块启用代码注释"

    如果你不想全局启用代码注释，因为你不想
    与自动内联行为一样，您可以为特定对象启用它们
    基于
    [属性列表]扩展名：

    ```` yaml
    ``` { .yaml .annotate }
    # Code block content
    ```
    ````

    请注意，必须先出现的语言简码现在也必须是
    前缀为`。`.

  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists

#### 定制选择器

<!-- md:sponsors -->
<!-- md:version insiders-4.32.0 -->
<!-- md:flag experimental -->

通常，代码注释只能[放置在注释中]，因为注释可以
被认为可以安全放置。然而，有时可能需要放置
代码块中不允许注释的部分的注释，例如
串。

可以为每种语言设置其他选择器：

``` yaml
extra:
  annotate:
    json: [.s2] # (1)!
```

1.  [`.s2`][s2]是[Pygges]为双引号生成的词素名称
    串。如果你想在另一个词位中使用代码注释，而不是
    注释、检查代码块并确定需要添加哪个词素
    添加到附加选择器列表中。

    __重要__：代码注释不能在词法之间拆分。

现在，可以在JSON的字符串中使用代码注释：

``` json
{
  "key": "value (1)"
}
```

1.  :man_raising_hand：我是一个代码注释！我可以包含__格式的“代码”
    text__、图像、。..基本上任何可以用Markdown写的东西。

  [placed in comments]: #adding-annotations
  [s2]: https://github.com/squidfunk/mkdocs-material/blob/87d5ca487b9d9ab95c41ee72813149d214048693/src/assets/stylesheets/main/extensions/pymdownx/_highlight.scss#L45

## 使用

代码块必须用两个单独的行括起来，其中包含三个回溯符。
要为这些块添加语法高亮显示，请直接添加语言简码
在开放块之后。请参阅[可用词法分析器列表]以查找
给定语言的简码：

```` markdown title="Code block"
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

为了提供额外的上下文，可以在代码中添加自定义标题
直接在短代码后使用`title=“<custom-title>”`选项进行阻止，
例如，显示文件的名称：

```` markdown title="Code block with title"
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

### 添加注释

代码注释可以放置在代码块中的任何位置
可以放置块的语言，例如JavaScript的“#！js//。..以及
`#！js/*。..*/`，用于`#！yaml#。..等[^1]：

  [^1]:
    代码注释需要用[Pyggments]突出显示语法——它们是
    目前与JavaScript语法高亮显示或语言不兼容
    他们的语法中没有注释。然而，我们正在积极工作
    关于支持定义代码注释的替代方法，允许
    始终将代码注释放在行尾。

```` markdown title="Code block with annotation"
``` yaml
theme:
  features:
    - content.code.annotate # (1)
```

1.  :man_raising_hand：我是一个代码注释！我可以包含__格式的“代码”
    text__、图像、。..基本上任何可以用Markdown写的东西。
````

<div class="result" markdown>

``` yaml
theme:
  features:
    - content.code.annotate # (1)
```

1.  :man_raising_hand：我是一个代码注释！我可以包含__格式的“代码”
    text__、图像、。..基本上任何可以用Markdown写的东西。

</div>

#### 删除评论

<!-- md:version 8.5.0 -->
<!-- md:flag experimental -->

如果你想去掉代码注释周围的注释字符，
只需添加一个`！`在代码注释的右括号之后：

```` markdown title="Code block with annotation, stripped"
``` yaml
# (1)!
```

1.  Look ma, less line noise!
````

<div class="result" markdown>

``` yaml
# (1)!
```

1.  Look ma, less line noise!

</div>

请注意，这只允许按以下方式呈现单个代码注释
评论。如果要添加多个代码注释，则不能添加注释
由于技术原因被剥离。

### 添加行号

可以使用`linenums=“<start>”将行号添加到代码块中`
选项直接位于短代码之后，而“<start>”表示开始
行号。代码块可以从除“1”之外的行号开始
允许拆分大代码块以提高可读性：

```` markdown title="Code block with line numbers"
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

### 突出显示特定线条

通过将行号传递给`hl_lines，可以突出显示特定行`
参数放在语言简码之后。请注意，行计数开始
在“1”处，无论作为部分指定的起始行号如何
[`linenums`][添加行号]：

=== "Lines"

    ```` markdown title="Code block with highlighted lines"
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

=== "Line ranges"

    ```` markdown title="Code block with highlighted line range"
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

### 突出显示内联代码块

启用[InlineHilite]后，可以对内联应用语法高亮显示
通过在代码块前加上shebang（即“#！`，紧接着
相应的[语言简码][可用词法分析器列表]。

``` markdown title="Inline code block"
The `#!python range()` function is used to generate a sequence of numbers.
```

<div class="result" markdown>

The `#!python range()` function is used to generate a sequence of numbers.

</div>

### 嵌入外部文件

启用[Snippets]时，来自其他文件（包括源文件）的内容
可以直接使用[`--8<--`符号][Snippets符号]嵌入
在代码块内：

```` markdown title="Code block with external content"
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

## 自定义

### 自定义语法主题

如果使用[Pyggments]，MkDocs的材料提供了[代码块样式]
[颜色]，采用定制且均衡的调色板构建，效果良好
两种[配色方案]都同样好：

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

Code block foreground, background and line highlight colors are defined via:

- :material-checkbox-blank-circle:{ style="color: var(--md-code-fg-color) " } `--md-code-fg-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-bg-color) " } `--md-code-bg-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-color) " } `--md-code-hl-color`

假设您想更改“#”的颜色！js“字符串”`。虽然有
有几种[类型的字符串标记]，它们使用相同的颜色。您可以分配
使用[附加样式表]添加新颜色：

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

如果你想调整特定类型的字符串，例如“#！js的backticks，你
可以在[语法主题定义]中查找特定的CSS类名，以及
将其作为[附加样式表]的一部分覆盖：

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

### 注释工具提示宽度

如果你的代码注释中托管了大量内容，它可以是
通过添加以下内容来增加工具提示的宽度是个好主意
[附加样式表]：

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

这将以更大的宽度呈现注释：

<div style="--md-tooltip-width: 600px;" markdown>

``` yaml
# (1)!
```

1. 更多内容空间

</div>

---
icon: material/format-align-bottom
---

# 脚注

脚注是向文档添加补充或附加信息的好方法
特定的单词、短语或句子，而不会中断文档的流程。
MkDocs的材料提供了定义、参考和呈现的能力
脚注。

## 配置

此配置增加了定义内联脚注的能力，然后
在文档的所有Markdown内容下方呈现。将以下行添加到
`mkdocs.yml`：

``` yaml
markdown_extensions:
  - footnotes
```

请参阅其他配置选项：

- [Footnotes]

  [Footnotes]: ../setup/extensions/python-markdown.md#footnotes

### 脚注工具提示

`sponsors`
`version insiders-4.51.0`
`flag experimental`

[Insiders]允许将脚注呈现为内联工具提示，以便用户可以阅读
脚注没有脱离文档的上下文。脚注工具提示可以
在`mkdocs.yml`中启用：

``` yaml
theme:
  features:
    - content.footnote.tooltips
```

__我们的文档__上启用了脚注工具提示，所以要尝试一下，你
可以将任何脚注悬停或聚焦在本页或我们的任何其他页面上
文档。

  [Insiders]: ../insiders/index.md

## 使用

### 添加脚注引用

脚注引用必须括在方括号内，并且必须以
插入符号“^”，后面紧跟一个任意标识符，类似于
标准Markdown链接语法。

``` title="Text with footnote references"
Lorem ipsum[^1] dolor sit amet, consectetur adipiscing elit.[^2]
```

<div class="result" markdown>

Lorem ipsum[^1] dolor sit amet, consectetur adipiscing elit.[^2]

</div>

### 添加脚注内容

脚注内容必须使用与引用相同的标识符声明。
它可以插入文档中的任意位置，并且始终
呈现在页面底部。此外，脚注的反向链接
引用会自动添加。

#### 在一条线上

简短的脚注可以写在同一行上：

``` title="Footnote"
[^1]: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

<div class="result" markdown>

[:octicons-arrow-down-24: Jump to footnote](#fn:1)

</div>

  [^1]: Lorem ipsum dolor sit amet, consectetur adipiscing elit.

#### 在多条线上

段落可以写在下一行，并且必须缩进四个空格：

``` title="Footnote"
[^2]:
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
```

<div class="result" markdown>

[:octicons-arrow-down-24: Jump to footnote](#fn:2)

</div>

[^2]:
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus
    auctor massa, nec semper lorem quam in massa.

---
icon: material/format-align-bottom
---

# 脚注

脚注是一种很好的方式，可以在不中断文档流程的情况下，为特定单词、短语或句子添加补充或附加信息。Material for MkDocs 提供了定义、引用和渲染脚注的功能。

## 配置

此配置添加了定义内联脚注的功能，这些脚注会在文档的所有 Markdown 内容下方渲染。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - footnotes
```

查看更多配置选项：

- [Footnotes]

  [Footnotes]: ../setup/extensions/python-markdown.md#footnotes

### 脚注工具提示

<!-- md:sponsors -->
<!-- md:version insiders-4.51.0 -->
<!-- md:flag experimental -->

[Insiders] 允许将脚注渲染为内联工具提示，这样用户无需离开文档上下文即可阅读脚注。可以在 `mkdocs.yml` 中启用脚注工具提示：

``` yaml
theme:
  features:
    - content.footnote.tooltips
```

__我们的文档已启用脚注工具提示__，所以您可以尝试将鼠标悬停或聚焦在此页面或我们文档的任何其他页面上的任何脚注上。

  [Insiders]: ../insiders/index.md

## 使用方法

### 添加脚注引用

脚注引用必须用方括号括起来，并且必须以脱字符 `^` 开头，后跟一个任意标识符，这与标准 Markdown 链接语法类似。

``` title="带脚注引用的文本"
Lorem ipsum[^1] dolor sit amet, consectetur adipiscing elit.[^2]
```

<div class="result" markdown>

Lorem ipsum[^1] dolor sit amet, consectetur adipiscing elit.[^2]

</div>

### 添加脚注内容

脚注内容必须使用与引用相同的标识符声明。它可以插入到文档中的任意位置，并且始终在页面底部渲染。此外，会自动添加一个返回脚注引用的链接。

#### 单行脚注

简短的脚注可以写在同一行：

``` title="脚注"
[^1]: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

<div class="result" markdown>

[:octicons-arrow-down-24: 跳转到脚注](#fn:1)

</div>

  [^1]: Lorem ipsum dolor sit amet, consectetur adipiscing elit.

#### 多行脚注

段落可以写在下一行，并且必须缩进四个空格：

``` title="脚注"
[^2]:
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
```

<div class="result" markdown>

[:octicons-arrow-down-24: 跳转到脚注](#fn:2)

</div>

[^2]:
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus
    auctor massa, nec semper lorem quam in massa.

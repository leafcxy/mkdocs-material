---
icon: material/tooltip-plus
---

# 工具提示

技术文档中经常使用许多缩写词，这可能
需要额外的解释，特别是对于项目的新用户。对于这些
重要的是，MkDocs的Material使用Markdown扩展的组合来
启用全站术语表。

## 配置

此配置支持缩写，并允许构建一个简单的
项目范围内的术语表，从中心位置获取定义。添加
以下行指向`mkdocs.yml`：

``` yaml
markdown_extensions:
  - abbr
  - attr_list
  - pymdownx.snippets
```

请参阅其他配置选项：

- [Abbreviations]
- [Attribute Lists]
- [Snippets]

  [Abbreviations]: ../setup/extensions/python-markdown.md#abbreviations
  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists
  [Snippets]: ../setup/extensions/python-markdown-extensions.md#snippets

### 改进的工具提示

`version 9.5.0`
`flag experimental`

启用改进的工具提示后，MkDocs材质将取代浏览器的
使用漂亮的小工具提示渲染“title”属性的逻辑。
将以下行添加到`mkdocs.yml`中：

``` yaml
theme:
  features:
    - content.tooltips
```

现在，将为以下元素呈现工具提示：

- __Content__ – 带有“标题”、永久链接和代码复制按钮的元素
- __Header__ – 主页按钮、标题标题、调色板开关和存储库链接
- __Navigation__ – 用省略号缩短的链接，即“”。..`

## 使用

### 添加工具提示

Markdown语法允许为每个链接指定一个“标题”，这将
启用[改进的工具提示]时，渲染为漂亮的工具提示。添加a
工具提示指向包含以下行的链接：

``` markdown title="Link with tooltip, inline syntax"
[Hover me](https://example.com "I'm a tooltip!")
```

<div class="result" markdown>

[Hover me](https://example.com "I'm a tooltip!")

</div>

Tooltips can also be added to link references:

``` markdown title="Link with tooltip, reference syntax"
[Hover me][example]

  [example]: https://example.com "I'm a tooltip!"
```

<div class="result" markdown>

[Hover me](https://example.com "I'm a tooltip!")

</div>

For all other elements, a `title` can be added by using the [Attribute Lists]
extension:

``` markdown title="Icon with tooltip"
:material-information-outline:{ title="Important information" }
```

<div class="result" markdown>

:material-information-outline:{ title="Important information" }

</div>

  [Markdown syntax]: https://daringfireball.net/projects/markdown/syntax#link
  [improved tooltips]: #improved-tooltips

### 添加缩写

缩写可以通过使用类似于URL和
[脚注]，以“*”开头，紧随其后的是术语或
首字母缩略词应放在方括号内：

``` markdown title="Text with abbreviations"
The HTML specification is maintained by the W3C.

*[HTML]: Hyper Text Markup Language
*[W3C]: World Wide Web Consortium
```

<div class="result" markdown>

The HTML specification is maintained by the W3C.

*[HTML]: Hyper Text Markup Language
*[W3C]: World Wide Web Consortium

</div>

  [footnotes]: footnotes.md

### 添加术语表

[Snippets]扩展可用于通过移动来实现简单的术语表
专用文件[^1]中的所有缩写，以及[自动附加]此文件到所有
具有以下配置的页面：

  [^1]:
    强烈建议将包含
    “docs”文件夹外的缩写（这里是一个名为的文件夹
    `includes被使用），否则MkDocs可能会抱怨
    未引用的文件。

=== ":octicons-file-code-16: `includes/abbreviations.md`"

    ```` markdown
    *[HTML]: Hyper Text Markup Language
    *[W3C]: World Wide Web Consortium
    ````

=== ":octicons-file-code-16: `mkdocs.yml`"

    ```` yaml
    markdown_extensions:
      - pymdownx.snippets:
          auto_append:
            - includes/abbreviations.md
    ````

  [auto-append]: https://facelessuser.github.io/pymdown-extensions/extensions/snippets/#auto-append-snippets

!!! tip

    当使用“docs”文件夹之外的专用文件时，将父目录添加到列表中
    “watch”文件夹，以便在更新术语表文件时，项目会自动
    运行`mkdocs-serve`时重新加载。

    ```` yaml
    watch:
      - includes
    ````

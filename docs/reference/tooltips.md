---
icon: material/tooltip-plus
---

# 工具提示

技术文档经常使用许多缩写词，这些缩写词可能需要额外的解释，特别是对于项目的新用户。为此，Material for MkDocs 使用了一系列 Markdown 扩展来启用全站范围的术语表。

## 配置

此配置启用了缩写功能，并允许构建一个简单的项目范围术语表，从中央位置获取定义。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - abbr
  - attr_list
  - pymdownx.snippets
```

查看其他配置选项：

- [Abbreviations]
- [Attribute Lists]
- [Snippets]

  [Abbreviations]: ../setup/extensions/python-markdown.md#abbreviations
  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists
  [Snippets]: ../setup/extensions/python-markdown-extensions.md#snippets

### 改进的工具提示

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->

当启用改进的工具提示时，Material for MkDocs 会用漂亮的小工具提示替换浏览器对 `title` 属性的渲染逻辑。
将以下行添加到 `mkdocs.yml`：

``` yaml
theme:
  features:
    - content.tooltips
```

现在，以下元素将显示工具提示：

- __内容__ – 带有 `title` 的元素、永久链接和代码复制按钮
- __页眉__ – 主页按钮、页眉标题、调色板开关和仓库链接
- __导航__ – 被省略号缩短的链接，即 `...`

## 使用方法

### 添加工具提示

[Markdown 语法]允许为每个链接指定一个 `title`，当启用[改进的工具提示]时，这将渲染为一个漂亮的工具提示。使用以下行向链接添加工具提示：

``` markdown title="带工具提示的链接，内联语法"
[悬停在我上面](https://example.com "我是一个工具提示！")
```

<div class="result" markdown>

[悬停在我上面](https://example.com "我是一个工具提示！")

</div>

工具提示也可以添加到链接引用中：

``` markdown title="带工具提示的链接，引用语法"
[悬停在我上面][example]

  [example]: https://example.com "我是一个工具提示！"
```

<div class="result" markdown>

[悬停在我上面](https://example.com "我是一个工具提示！")

</div>

对于所有其他元素，可以使用[属性列表]扩展添加 `title`：

``` markdown title="带工具提示的图标"
:material-information-outline:{ title="重要信息" }
```

<div class="result" markdown>

:material-information-outline:{ title="重要信息" }

</div>

  [Markdown syntax]: https://daringfireball.net/projects/markdown/syntax#link
  [improved tooltips]: #improved-tooltips

### 添加缩写

可以使用类似于 URL 和[脚注]的特殊语法定义缩写，以 `*` 开头，后跟方括号中的术语或缩写：

``` markdown title="带缩写的文本"
HTML 规范由 W3C 维护。

*[HTML]: 超文本标记语言
*[W3C]: 万维网联盟
```

<div class="result" markdown>

HTML 规范由 W3C 维护。

*[HTML]: 超文本标记语言
*[W3C]: 万维网联盟

</div>

  [footnotes]: footnotes.md

### 添加术语表

可以使用[Snippets]扩展通过将所有缩写移动到专用文件[^1]来实现简单的术语表，并使用以下配置[自动附加]此文件到所有页面：

  [^1]:
    强烈建议将包含缩写的 Markdown 文件放在 `docs` 文件夹之外（这里使用了一个名为 `includes` 的文件夹），否则 MkDocs 可能会抱怨未引用的文件。

=== ":octicons-file-code-16: `includes/abbreviations.md`"

    ``` markdown
    *[HTML]: 超文本标记语言
    *[W3C]: 万维网联盟
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    markdown_extensions:
      - pymdownx.snippets:
          auto_append:
            - includes/abbreviations.md
    ```

  [auto-append]: https://facelessuser.github.io/pymdown-extensions/extensions/snippets/#auto-append-snippets

!!! tip

    当在 `docs` 文件夹之外使用专用文件时，将父目录添加到 `watch` 文件夹列表中，这样当术语表文件更新时，运行 `mkdocs serve` 时会自动重新加载项目。

    ``` yaml
    watch:
      - includes
    ```

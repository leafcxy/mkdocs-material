---
search:
  boost: 1.05
---

# 设置站内搜索

Material for MkDocs 提供了优秀的客户端搜索实现，无需集成可能不符合隐私法规的第三方服务。此外，搜索甚至支持[离线]，允许用户下载您的文档。

  [离线]: building-for-offline-usage.md

## 配置

### 内置搜索插件

<!-- md:version 0.1.0 -->
<!-- md:plugin -->

内置搜索插件与 Material for MkDocs 无缝集成，添加了基于 [lunr] 和 [lunr-languages] 的多语言客户端搜索。它默认启用，但当使用其他插件时，必须在 `mkdocs.yml` 中重新添加：

``` yaml
plugins:
  - search
```

所有设置请参阅[插件文档]。

  [插件文档]: ../plugins/search.md
  [lunr]: https://lunrjs.com
  [lunr-languages]: https://github.com/MihaiValentin/lunr-languages

### 搜索建议

<!-- md:version 7.2.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

启用搜索建议后，搜索会为最后一个单词显示最可能的补全，按 ++arrow-right++ 键可接受。将以下内容添加到 `mkdocs.yml`：

``` yaml
theme:
  features:
    - search.suggest
```

搜索 [:octicons-search-24: search su][搜索建议示例] 会建议 ^^search suggestions^^。

  [搜索建议示例]: ?q=search+su

### 搜索高亮

<!-- md:version 7.2.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

启用搜索高亮后，用户点击搜索结果后，Material for MkDocs 会高亮所有出现的内容。将以下内容添加到 `mkdocs.yml`：

``` yaml
theme:
  features:
    - search.highlight
```

搜索 [:octicons-search-24: code blocks][搜索高亮示例] 会高亮所有相关词。

  [搜索高亮示例]: ../reference/code-blocks.md?h=code+blocks

### 搜索分享

<!-- md:version 7.2.0 -->
<!-- md:feature -->

启用搜索分享后，重置按钮旁会显示 :material-share-variant: 分享按钮，可深度链接到当前搜索查询和结果。将以下内容添加到 `mkdocs.yml`：

``` yaml
theme:
  features:
    - search.share
```

用户点击分享按钮后，URL 会自动复制到剪贴板。

## 使用

### 搜索权重提升

<!-- md:version 8.3.0 -->
<!-- md:flag metadata -->

页面可通过 front matter 的 `search.boost` 属性提升在搜索中的排名。在 Markdown 文件顶部添加如下内容：

=== ":material-arrow-up-circle: 提升排名"

    ``` yaml
    ---
    search:
      boost: 2 # (1)!
    ---

    # 页面标题
    ...
    ```

    1.  :woman_in_lotus_position: 提升页面时请温和，__建议使用较低的值__。

=== ":material-arrow-down-circle: 降低排名"

    ``` yaml
    ---
    search:
      boost: 0.5
    ---

    # 页面标题
    ...
    ```

### 搜索排除

<!-- md:version 9.0.0 -->
<!-- md:flag metadata -->
<!-- md:flag experimental -->

页面可通过 front matter 的 `search.exclude` 属性从搜索中排除。在 Markdown 文件顶部添加如下内容：

``` yaml
---
search:
  exclude: true
---

# 页面标题
...
```

#### 排除章节

启用 [Attribute Lists] 后，可通过在 Markdown 标题后添加 `data-search-exclude` 标记来排除页面的特定章节：

=== ":octicons-file-code-16: `docs/page.md`"

    ``` markdown
    # 页面标题

    ## Section 1

    本节内容会被包含

    ## Section 2 { data-search-exclude }

    本节内容会被排除
    ```

=== ":octicons-codescan-16: `search_index.json`"

    ``` json
    {
      ...
      "docs": [
        {
          "location":"page/",
          "text":"",
          "title":"Document title"
        },
        {
          "location":"page/#section-1",
          "text":"<p>The content of this section is included</p>",
          "title":"Section 1"
        }
      ]
    }
    ```

  [Attribute Lists]: extensions/python-markdown.md#attribute-lists

#### 排除块

启用 [Attribute Lists] 后，可通过在 Markdown 行内或块级元素后添加 `data-search-exclude` 标记来排除页面的特定内容块：

=== ":octicons-file-code-16: `docs/page.md`"

    ``` markdown
    # 页面标题

    本块内容会被包含

    本块内容会被排除
    { data-search-exclude }
    ```

=== ":octicons-codescan-16: `search_index.json`"

    ``` json
    {
      ...
      "docs": [
        {
          "location":"page/",
          "text":"<p>The content of this block is included</p>",
          "title":"Document title"
        }
      ]
    }
    ```

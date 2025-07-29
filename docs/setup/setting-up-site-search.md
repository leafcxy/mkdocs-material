---
search:
  boost: 1.05
---

# 设置网站搜索

Material for MkDocs提供了一个出色的客户端搜索实现，
省略了集成第三方服务的需要，这可能
不符合隐私法规。此外，搜索甚至有效
[offline]，允许用户下载您的文档。

  [offline]: building-for-offline-usage.md

## 配置

### 内置搜索插件

`version 0.1.0`
`plugin`

内置的搜索插件与Material for MkDocs无缝集成，
使用[lunr]和[lunr语言]添加多语言客户端搜索。it is 的常用口语形式
默认情况下启用，但当其他插件出现时，必须重新添加到“mkdocs.yml”中
使用：

``` yaml
plugins:
  - search
```

有关所有设置的列表，请参阅[plugin documentation]。

  [plugin documentation]: ../plugins/search.md

  [lunr]: https://lunrjs.com
  [lunr-languages]: https://github.com/MihaiValentin/lunr-languages

### 搜索建议

`version 7.2.0`
`feature`
`flag experimental`

启用搜索建议后，搜索将显示最有可能的
最后一个单词的完成，可以用++右箭头++键接受。
将以下行添加到`mkdocs.yml`中：

``` yaml
theme:
  features:
    - search.suggest
```

正在搜索[：octicons-search-24:search-su][Search suggestions example]
生成^^搜索建议^^作为建议。

  [Search suggestions example]: ?q=search+su

### 搜索突出显示

`version 7.2.0`
`feature`
`flag experimental`

当启用搜索突出显示并且用户点击搜索结果时，
点击链接后，Material for MkDocs将突出显示所有事件。
将以下行添加到`mkdocs.yml`中：

``` yaml
theme:
  features:
    - search.highlight
```

搜索 [:octicons-search-24: code blocks][Search highlighting example]
突出显示这两个术语的所有出现。

  [Search highlighting example]: ../reference/code-blocks.md?h=code+blocks

### 搜索共享

`version 7.2.0`
`feature`

当搜索共享被激活时，一个：material share变体：共享按钮是
在重置按钮旁边呈现，允许深度链接到当前
搜索查询和结果。将以下行添加到`mkdocs.yml`中：

``` yaml
theme:
  features:
    - search.share
```

当用户单击共享按钮时，URL会自动复制到
剪贴板。

## 使用

### 搜索增强

`version 8.3.0`
`flag metadata`

页面可以在搜索中使用“search.boost”属性进行增强，
这将使他们排名更高。在a的顶部添加以下行
Markdown文件：

=== ":material-arrow-up-circle: Rank up"

    ``` yaml
    ---
    search:
      boost: 2 # (1)!
    ---

    # Page title
    ...
    ```

    1.  :woman_in_lotus_position: When boosting pages, be gentle and start with
        __low values__.

=== ":material-arrow-down-circle: Rank down"

    ``` yaml
    ---
    search:
      boost: 0.5
    ---

    # Page title
    ...
    ```

### 搜索排除

`version 9.0.0`
`flag metadata`
`flag experimental`

可以使用“search.exclude”作为标题将页面排除在搜索之外`
属性，将其从索引中删除。在a的顶部添加以下行
Markdown文件：

``` yaml
---
search:
  exclude: true
---

# Page title
...
```

#### 不包括章节

启用[Attribute Lists]时，可以排除页面的特定部分
通过在Markdown后添加“数据搜索排除”语法来进行搜索
标题：

=== ":octicons-file-code-16: `docs/page.md`"

    ``` markdown
    # Page title

    ## Section 1

    The content of this section is included

    ## Section 2 { data-search-exclude }

    The content of this section is excluded
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

#### 不包括区块

启用[Attribute Lists]时，可以排除页面的特定部分
通过在Markdown后添加“数据搜索排除”语法来进行搜索
内联或块级元素：

=== ":octicons-file-code-16: `docs/page.md`"

    ``` markdown
    # Page title

    The content of this block is included

    The content of this block is excluded
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

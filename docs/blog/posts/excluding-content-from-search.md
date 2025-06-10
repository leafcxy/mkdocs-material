---
date: 2021-09-26
authors: [squidfunk]
description: >
  Three new simple ways to exclude dedicated parts of a document from the search
  index, allowing for more fine-grained control
categories:
  - Search
links:
  - blog/posts/search-better-faster-smaller.md
  - setup/setting-up-site-search.md#search-exclusion
  - insiders/how-to-sponsor.md
---

# 从搜索中排除内容

__最新的Insiders版本带来了三种新的简单排除方法
从搜索索引中提取文档的专用部分，允许更多
精细控制。__

两周前，Material for MkDocs Insiders发布了一个全新的搜索
插件]，带来了[可用性的巨大改进]，但也提高了[速度
以及搜索索引的大小。有趣的是，如前所述
在博客文章中，我们只是触及了现在可能实现的表面。这
发布带来了一些有用的功能，增强了写作体验，
允许对页面、部分和块进行更细粒度的控制
Markdown文件应该通过内置的搜索功能进行索引。

<!-- more -->

_以下部分讨论了排除页面和
搜索索引中的部分。如果你想立即了解什么是新的，
跳到[紧接着的部分][新增内容]。_

  [brand new search plugin]: search-better-faster-smaller.md
  [massive improvements in usability]: search-better-faster-smaller.md#whats-new
  [speed and size]: search-better-faster-smaller.md#benchmarks
  [what's new]: #whats-new

## 现有技术

MkDocs拥有丰富而蓬勃发展的[插件]生态系统，而且它没有
令人惊讶的是，@chrieke已经有了一个很棒的插件来排除特定的
Markdown文件的部分–[mkdocs excluded search]插件。这可能是
安装有：

```
pip install mkdocs-exclude-search
```

__工作原理_: 插件post处理`searchindex.json`文件
由内置搜索插件生成，使作者能够
通过添加几行配置来排除某些页面和部分
`mkdocs.yml`。举个例子：

``` yaml
plugins:
  - search
  - exclude-search:
      exclude:
        - page.md
        - page.md#section
        - directory/*
        - /*/page.md
```

很容易看出，该插件遵循以配置为中心的方法
添加了对中缀和后缀过滤等高级过滤技术的支持
使用通配符。虽然这是一个非常强大的想法，但它也有一些
缺点：

1.  __排除模式和内容不在同一位置__: 排除模式
    需要在`mkdocs.yml`中定义，而不是作为各自的一部分
    文件或部分被排除在外。这可能会导致过时的排除
    模式，导致意外行为：

    - 当标题改变时，它的slug（永久链接）也会改变，这可能
      突然匹配（或取消匹配）模式，例如，当作者修复拼写错误时
      在标题中。

    - 由于排除模式支持使用通配符，因此不同的作者
      可能会在没有任何即时反馈的情况下覆盖彼此的模式，因为
      该插件只报告排除的文档数量，而不是what_
      已被排除在外。1.

  [^1]:
    当日志级别设置为“DEBUG”时，插件将准确报告
    页面和部分已从搜索索引中排除，但MkDocs将
    现在，用其核心和其他插件的调试输出淹没终端。

2.  __排除控制可能太粗糙__: The [mkdocs-exclude-search]
    插件只允许排除页面和部分。不是
    可以排除部分内容，例如不相关的内容
    搜索，但必须作为文档的一部分。

  [plugins]: https://github.com/mkdocs/mkdocs/wiki/MkDocs-Plugins
  [mkdocs-exclude-search]: https://github.com/chrieke/mkdocs-exclude-search

## 有什么新鲜事吗？

最新的Insiders版本为[__排除页面，
实现了从搜索索引中删除部分和块
通过前面的内容以及[属性列表]。请注意，它没有
替换[mkdocs excluded search]插件，但对其进行补充。

  [search exclusion]: ../../setup/setting-up-site-search.md#search-exclusion
  [Attribute Lists]: ../../setup/extensions/python-markdown.md#attribute-lists

### 不包括页面

通过添加一个简单的
指向相应Markdown文件的前端内容的指令。好东西
作者现在只需查看文档顶部即可学习
无论是否被排除在外：

``` yaml
---
search:
  exclude: true
---

# Page title
...
```

### 不包括章节

如果要排除某个部分，作者可以使用[属性列表]
在a末尾添加一个名为“数据搜索排除”的__pragma__的扩展
标题。该语法不包含在最终的HTML中，因为搜索语法是
在页面呈现之前由搜索插件过滤：

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

### 不包括区块

如果需要更细粒度的控制，可以添加__pragma__
任何正式的[块级元素]或[内联级元素]
由[Attribute Lists]扩展支持：

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
        },
      ]
    }
    ```

  [block-level element]: https://python-markdown.github.io/extensions/attr_list/#block-level
  [inline-level element]: https://python-markdown.github.io/extensions/attr_list/#inline

## 结论

最新版本提供了三种简单的方法来更精确地控制发生了什么
它补充了已经非常强大的搜索索引
[mkdocs excluded search]插件，允许采用新的方法来塑造
搜索索引的类型、结构、大小和内容。

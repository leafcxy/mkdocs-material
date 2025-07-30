---
title: Extensions
---

# 扩展

Markdown是一种非常小的语言，有一种参考实现，称为
[约翰·格鲁伯的Markdown]。[Python Markdown]和[Python Markdown扩展]
是两个增强Markdown写作体验的包，增加了有用的
技术写作的语法扩展。

  [John Gruber's Markdown]: https://daringfireball.net/projects/markdown/
  [Python Markdown]: python-markdown.md
  [Python Markdown Extensions]: python-markdown-extensions.md

## 支持的扩展

以下扩展都由Material for MkDocs支持，因此
强烈推荐。点击每个扩展以了解其目的和
配置：

<div class="mdx-columns" markdown>

- [Abbreviations]
- [Admonition]
- [Arithmatex]
- [Attribute Lists]
- [BetterEm]
- [Caret, Mark & Tilde]
- [Critic]
- [Definition Lists]
- [Details]
- [Emoji]
- [Footnotes]
- [Highlight]
- [Keys]
- [Markdown in HTML]
- [SmartSymbols]
- [Snippets]
- [SuperFences]
- [Tabbed]
- [Table of Contents]
- [Tables]
- [Tasklist]

</div>

  [Abbreviations]: python-markdown.md
  [Admonition]: python-markdown.md
  [Arithmatex]: python-markdown-extensions.md#arithmatex
  [Attribute Lists]: python-markdown.md
  [BetterEm]: python-markdown-extensions.md#betterem
  [Caret, Mark & Tilde]: python-markdown-extensions.md#caret-mark-tilde
  [Critic]: python-markdown-extensions.md#critic
  [Definition Lists]: python-markdown.md
  [Details]: python-markdown-extensions.md#details
  [Emoji]: python-markdown-extensions.md#emoji
  [Footnotes]: python-markdown.md
  [Highlight]: python-markdown-extensions.md#highlight
  [Keys]: python-markdown-extensions.md#keys
  [Markdown in HTML]: python-markdown.md
  [SmartSymbols]: python-markdown-extensions.md#smartsymbols
  [Snippets]: python-markdown-extensions.md#snippets
  [SuperFences]: python-markdown-extensions.md#superfences
  [Tabbed]: python-markdown-extensions.md#tabbed
  [Table of Contents]: python-markdown.md
  [Tables]: python-markdown.md#tables
  [Tasklist]: python-markdown-extensions.md#tasklist

## 配置

扩展配置为“mkdocs.yml”的一部分，即mkdocs配置
文件。以下部分包含引导的两个示例配置
您的文档项目。

  [overview]: #advanced-configuration

### 最小配置

当您使用Material时，此配置是一个很好的起点
首次使用MkDocs。最好的办法是探索[参考]，以及
逐步添加您想要使用的内容：

``` yaml
markdown_extensions:

  # Python Markdown
  - toc:
      permalink: true

  # Python Markdown Extensions
  - pymdownx.highlight
  - pymdownx.superfences
```

  [reference]: ../../reference/index.md

### 推荐配置

此配置启用了MkDocs Material的所有Markdown相关功能
对于有经验的用户来说，引导一个新的文档项目非常有用：

``` yaml
markdown_extensions:

  # Python Markdown
  - abbr
  - admonition
  - attr_list
  - def_list
  - footnotes
  - md_in_html
  - toc:
      permalink: true

  # Python Markdown Extensions
  - pymdownx.arithmatex:
      generic: true
  - pymdownx.betterem:
      smart_enable: all
  - pymdownx.caret
  - pymdownx.details
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
  - pymdownx.highlight
  - pymdownx.inlinehilite
  - pymdownx.keys
  - pymdownx.mark
  - pymdownx.smartsymbols
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true
  - pymdownx.tasklist:
      custom_checkbox: true
  - pymdownx.tilde
```

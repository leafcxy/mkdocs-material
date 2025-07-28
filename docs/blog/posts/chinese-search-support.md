---
date: 2022-05-05
authors: [squidfunk]
title: Chinese search support
description: >
  Insiders adds Chinese language support for the built-in search plugin – a
  feature that has been requested many times
categories:
  - Search
links:
  - blog/posts/search-better-faster-smaller.md
  - plugins/search.md#_12
  - insiders/how-to-sponsor.md
---

# Chinese search support – 中文搜索​支持

__内部人士为[内置搜索]添加了实验性的中文支持
插件]–一个长期以来被要求的功能
中国用户数量。__

仅次于美国和德国的第三大原产国
MkDocs用户的材料是中国。长期以来，[内置搜索插件]
不允许对汉字进行适当的分割，主要是因为
[lunr语言]中缺少用于搜索标记化和
堵塞。Insiders最新版本增加了期待已久的中文支持
对于内置的搜索插件，这是许多用户所要求的。

<!-- more -->

_Material for MkDocs終於​支持​中文​了！文本​被​正確​分割​並且​更​容易​找到。_
{ style="display: inline" }

_本文解释了如何为内置的
搜索插件在几分钟内。_
{ style="display: inline" }

  [built-in search plugin]: ../../plugins/search.md
  [lunr-languages]: https://github.com/MihaiValentin/lunr-languages

## 配置

MkDocs材料的中文支持由[jieba]提供
优秀的中文分词库。如果安装了[jieba]
内置的搜索插件会自动检测并运行中文字符
通过分割器。您可以通过以下方式安装[jieba]：

```
pip install jieba
```

仅当您指定了[`separator][separator]时，才需要执行下一步
在`mkdocs.yml`中配置。文本用[零宽度空白]分割
字符，因此它在搜索模式中呈现完全相同的结果。调整
`mkdocs.yml`使得[分隔符][分隔符]包括`\u200b`
字符：

``` yaml
plugins:
  - search:
      separator: '[\s\u200b\-]'
```

这就是所需要的。

## 使用

如果您按照配置指南中的说明进行操作，中文单词将
现在使用[jieba]进行标记。尝试搜索
[：八字搜索-24:支持][q=支持] 看看它是如何与
内置搜索插件。

---

请注意，这是一个实验性功能，而我@squidfunk不是
精通中文（还吗？）。如果你发现一个bug或认为有什么可以
已改进，请[打开一个问题]。

  [jieba]: https://pypi.org/project/jieba/
  [zero-width whitespace]: https://en.wikipedia.org/wiki/Zero-width_space
  [separator]: ../../plugins/search.md#config.separator
  [q=支持]: ?q=支持
  [open an issue]: https://github.com/squidfunk/mkdocs-material/issues/new/choose

---
date: 2021-12-27
authors: [squidfunk]
description: >
  2021 was a fantastic year for this project as we shipped many new awesome
  features and made this project sustainable
categories:
  - General
---

# 过去、现在和未来

__2021年对这个项目来说是美好的一年，因为我们推出了许多新的、令人惊叹的产品
功能，用户增长显著，并利用GitHub赞助商使
项目可持续。__

今天，[MkDocs]和MkDocs材料是最受欢迎的
为您的网站选择静态站点生成器和主题时的选项
技术文档项目。MkDocs的材料确保您
无论屏幕如何，内容总是完美地呈现给观众
分辨率或设备性能。它已经发展成为一个技术框架
写作，提供许多功能，其中一些功能在其他网站上尚未发现
静态站点生成器。然而，我们还远未结束，因为2022年即将到来
带来一些有趣的新功能。

<!-- more -->

_本文展示了2021年添加的所有功能，并给出了
对2022年下降趋势的展望。此外，它还提供了一些上下文
关于该项目的历史。_

  [MkDocs]: https://www.mkdocs.org

## 一点历史

2015年，尽管我在这个行业工作了10年，但我在开源方面还是相当新手。
我想发布我最新的开源项目[protobluff]，一个零拷贝
C的Protocol Buffers实现，这是我之前创建的一部分
启动。由于该项目非常复杂，我很快
意识到我需要好的用户文档。

在评估了静态站点生成器以及Hugo、Sphinx和MkDocs之后
特别是，我很快决定MkDocs似乎是一个不错的选择
专门针对技术项目文档，易于使用。
不幸的是，所有可用的主题看起来都过时了，而且考虑到我是一个
我是一个非常善于视觉的人，我就是无法说服自己结束这一天。

我想建立一个主题。

几个月后，在2016年2月，我发布了Material for
MkDocs（以及随之而来的[protobluff]，我想在第一个版本中发布的项目
地点），看起来像这样：

![Material for MkDocs 0.1.0][Material for MkDocs 0.1.0]

它已经完全响应了，总体来说，还可以，但勉强
可定制，因为只有徽标可以更改。除此之外，它别无选择：
没有颜色或导航选项，没有即时加载等。搜索非常
基本且仅支持的章节标题：

![Material for MkDocs 0.1.0 Search][Material for MkDocs 0.1.0 Search]

重要的是要知道，在这个时间点上，我已经为
MkDocs for[protobluff]，这是我真正关心的项目。近6年
后来，没有人知道protobluff，但这个小的副项目已经开始了
在那些日子里，你会告诉我像AWS这样的大型组织，
微软和欧洲核子研究中心，以及非常受欢迎的开源项目，如
FastAPI和Kubernetes将来会使用这个项目——我会
宣布你疯了。

我仍然觉得这个项目的成功非常令人惊讶，因为我认为
主题丰富，是一个已解决的问题。没有荣耀
在主题方面，没有明星可赚（记住我是开源新手，所以这是
我正在优化的指标），因为有成千上万的
选项。然而，随着时间的推移，我了解到执行很重要：
尽管MkDocs的Material解决了一个有数千种解决方案的问题
存在，它擅长于特定的利基市场，这个利基市场被称为
_技术项目文件。

如今，这个项目不仅很受欢迎，而且得到了近300名个人的资助
每年预算超过50000美元。这
允许我留出足够的时间来开发新功能，
bug修复、稳定性改进、问题分类和一般支持
对我来说，这就像一场梦，因为开源有很多失败的故事
资金和人们告诉你：不要做开源，你会为之工作
免费_

毕竟，在2021年实现开源的可持续性是可能的。

  [the first version]: https://github.com/squidfunk/mkdocs-material/releases/tag/0.1.0
  [Material for MkDocs 0.1.0]: the-past-present-and-future/mkdocs-material-0.1.0.png
  [Material for MkDocs 0.1.0 Search]: the-past-present-and-future/mkdocs-material-0.1.0-search.png
  [protobluff]: https://github.com/squidfunk/protobluff

## 2021年数字

2021年是激动人心的一年，因为该项目取得了显著增长。

__16.6万人__ 2021年访问了官方文件，总计160万
页面浏览量_与2020年相比增长了83%。平均值
访问者在网站上花费1.5分钟。虽然手机占12%
访问量中，平板电脑仅占0.6%。游客来自多达213个国家
国家，几乎覆盖了整个世界。

### 特征

Material中添加了38个新功能，这绝对令人兴奋
对于整个2021年的MkDocs来说——这是每9.6天一次的新功能——
这之所以成为可能，是因为资金状况不断改善。
以下是按字母顺序列出的所有功能，其中一些
作为[内部人士]的一部分，仍然仅供赞助商使用：

<div class="mdx-columns" markdown>

- [Admonition inline blocks]
- [Advanced search highlighting]
- [Anchor tracking]
- [Back-to-top button]
- [Boosting pages in search]
- [Brand new search plugin]
- [Code annotations]
- Code annotations: anchor links
- [Code annotations: strip comments]
- [Code block titles]
- [Code block line anchors]
- [Color palette toggle]
- [Content tabs: improved support]
- [Content tabs: auto-linking]
- Content tabs: animated indicator
- [Cookie consent]
- [Custom admonition icons]
- [Dark mode support for images]
- [Dismissable announcement bar]
- [Excluding content from search]
- Latest release tag
- [Mermaid.js integration]
- [Navigation icons]
- [Remove generator notice]
- [Rich search previews]
- Stay on page when switching versions
- [Search highlighting]
- [Search sharing]
- [Search suggestions]
- [Section index pages]
- [Site language selection]
- [Social cards]
- [Sticky navigation tabs]
- [Tags with search integration]
- [Tokenizer with lookahead]
- [Versioning]
- [Version warning]
- [Was this page helpful?]

</div>

此外，在推送的__1000个commit__中修复了很多错误
今年进入存储库。[changelog]包括所有修复程序的列表。
此外，在重构代码库上投入了大量时间
保持它的良好状态。当“mkdocs材料”包发布时
__55次，“mkdocs材料内幕人士”被运送了72次。

  [Insiders]: ../../insiders/index.md
  [Admonition inline blocks]: ../../reference/admonitions.md
  [Advanced search highlighting]: search-better-faster-smaller.md
  [Anchor tracking]: ../../setup/setting-up-navigation.md
  [Back-to-top button]: ../../setup/setting-up-navigation.md
  [Boosting pages in search]: ../../setup/setting-up-site-search.md
  [Brand new search plugin]: search-better-faster-smaller.md
  [Code annotations]: ../../reference/code-blocks.md
  [Code annotations: strip comments]: ../../reference/code-blocks.md
  [Code block titles]: ../../reference/code-blocks.md
  [Code block line anchors]: ../../setup/extensions/python-markdown-extensions.md
  [Color palette toggle]: ../../setup/changing-the-colors.md
  [Content tabs: improved support]: ../../reference/content-tabs.md
  [Content tabs: auto-linking]: ../../reference/content-tabs.md
  [Cookie consent]: ../../setup/ensuring-data-privacy.md
  [Custom admonition icons]: ../../reference/admonitions.md
  [Dark mode support for images]: ../../reference/images.md
  [Dismissable announcement bar]: ../../setup/setting-up-the-header.md
  [Excluding content from search]: ../../setup/setting-up-site-search.md
  [Mermaid.js integration]: ../../reference/diagrams.md
  [Navigation icons]: ../../reference/index.md
  [Remove generator notice]: ../../setup/setting-up-the-footer.md
  [Rich search previews]: search-better-faster-smaller.md
  [Search highlighting]: ../../setup/setting-up-site-search.md
  [Search sharing]: ../../setup/setting-up-site-search.md
  [Search suggestions]: ../../setup/setting-up-site-search.md
  [Section index pages]: ../../setup/setting-up-navigation.md
  [Site language selection]: ../../setup/changing-the-language.md
  [Social cards]: ../../setup/setting-up-social-cards.md
  [Sticky navigation tabs]: ../../setup/setting-up-navigation.md
  [Tags with search integration]: ../../setup/setting-up-tags.md
  [Tokenizer with lookahead]: search-better-faster-smaller.md
  [Versioning]: ../../setup/setting-up-versioning.md
  [Version warning]: ../../setup/setting-up-versioning.md
  [Was this page helpful?]: ../../setup/setting-up-site-analytics.md
  [changelog]: ../../changelog/index.md

### 基金

2021年，每月资金从1月初的1050美元增加到
超过4300美元（2021年12月27日），年度预算总额超过
$50,000.与去年相比，__资金收入增长了617%__
这绝对令人难以置信：

![Funding]

  [Funding]: the-past-present-and-future/funding.png

我提供这些数字只是为了履行我做出的透明度承诺
感谢我的[出色的赞助商]，并表明有可能使现有的公开赛
通过遵循精心设计的发布策略，源项目是可持续的。

您可以在[Insiders]指南中了解该策略。

  [awesome sponsors]: ../../insiders/how-to-sponsor.md

## 2022

站在明年的边缘，可以肯定地说，该项目将
继续繁荣和发展，产生许多令人惊叹的功能，使
技术写作更加舒适灵活。以下是摘录
2022年将出现的功能：

- __Instant previews__: [即时预览]将呈现特定的页面部分
  当鼠标悬停在内部链接上时，在工具提示内，这将允许实现
  比如词汇表。进一步支持改进术语表功能
  也将进行调查。

- __Text annotations__: 作为[代码注释]的逻辑进程
  如果在2021年添加，作者将能够为纯文本添加注释，
  为副业内容提供了绝佳的机会。当然，文本注释
  将与代码注释一样易于使用。

- __Navigation pruning__: 优化大型文档项目，材料
  MkDocs将引入一个名为“navigation.preeme”的新功能标志
  将导致文档项目的HTML文件明显更小
  巨大的导航层次结构。

- __Navigation status badge__: 作为最近添加的
  [导航图标][导航图标]支持，状态将归因于
  每个页面，允许在导航树中用图标标记一个页面
  ：材料警报decagram：__new__或：材料垃圾桶：__deprecated__。
  还将支持自定义状态类型。

- __Card grids__: 作为技术写作工具包中的另一个组件，
  [卡片网格]将允许在网格中排列内容，这尤其是
  对于概述页面很有用。它们将允许排列任意内容，
  包括代码块、警告等。

- __Blog support__: 博客支持仍在调查中，预计
  将成为2022年的主要新增项目之一。博客将完美整合
  通过编写文档，允许使用中可用的所有组件
  MkDocs的材料。

此列表不完整。此外，还将添加许多新的较小功能
明年，就像2021年一样。你可以关注[@squidfunk on X]留下来
更新。

__Happy new year!__ :tada:

  [Instant previews]: https://x.com/squidfunk/status/1466794654213492743
  [card grids]: https://github.com/squidfunk/mkdocs-material/issues/3018
  [under investigation]: https://github.com/squidfunk/mkdocs-material/issues/3353
  [@squidfunk on X]: https://x.com/squidfunk

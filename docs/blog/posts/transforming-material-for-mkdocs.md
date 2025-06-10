---
date: 2024-08-19
authors:
  - squidfunk
  - alexvoss
  - katharinalisalin
categories:
  - General
description: >
  We are transforming Material for MkDocs to ensure its community continues to thrive and doubling down on our commitment to Open Source.
title: How we're transforming Material for MkDocs
---

# 为MkDocs转换材料

__我们正在开发一套令人惊叹的功能，这需要一些幕后工作，我们现在准备在一系列帖子中分享。在这里，我们概述了我们的目标、正在开发的功能、让我们彻夜难眠的事情以及我们对开源的承诺。__

我们知道，自上次更新以来已经有一段时间了，这就是为什么我们渴望与您分享Material for MkDocs内部和周围发生的事情。在2024年的大部分时间里，我们一直专注于改造MkDocs材料的核心，为最常被要求的新的、相互关联的功能奠定基础。

本文是系列文章中的第一篇，我们将探讨如何通过改进信息检索来支持用户，为多语言网站和版本控制提供更好的支持，以及改善整体创作体验。我们概述了我们对项目发展的愿景，并描述了我们一直在做的工作。在这篇和接下来的博客文章中，我们将与您分享我们的进展，我们很高兴听到您的想法。

<!-- more -->

_请注意，这篇文章在脚注中包含了几个技术细节，特别是关于挑战的部分。如果你对细节不感兴趣，可以跳过它们_

## 一个成功的故事

2024年，Material for MkDocs已经牢固地确立了自己作为文档框架领域领先工具的地位，截至本文撰写之时，每月下载量超过500万次。@squidfunk最初的个人项目已经发展成为一个多功能的资源，用于创建全面的文档网站、个人网站、博客，特别是用于管理组织内外的知识。

由于近[50000]个公共GitHub项目依赖于Material for MkDocs，很明显该框架已经产生了重大影响。数以万计的作者依靠我们每月向数百万用户提供文档。[^1]除了被[许多流行的开源项目]采用外，Material for MkDocs还得到了[AWS]、[微软]和[西门子]等大公司以及许多其他公司和个人的信任和财务支持。我们非常感谢我们得到的持续支持，这使我们能够将时间投入到这个项目中，使编写文档变得愉快。

  [^1]:
    我们从企业和其他开源维护者那里收集了宝贵的反馈，这些反馈表明实际数字甚至更高。许多组织在私有基础设施（如GitLab等自托管平台）中利用该框架进行内部知识管理。这表明，MkDocs材料的真正范围远远超出了公开可见的范围。

  [50,000]: https://github.com/squidfunk/mkdocs-material/network/dependents
  [many popular Open Source projects]: https://github.com/squidfunk/mkdocs-material?tab=readme-ov-file#trusted-by-
  [AWS]: https://x.com/squidfunk/status/1740389441284579767
  [Microsoft]: https://x.com/squidfunk/status/1801909506391105840
  [Siemens]: https://x.com/squidfunk/status/1699799988069646761

我们的用户特别欣赏Material for MkDocs的易用性和简单的设置。它通过为您处理web技术的复杂性简化了流程，因此您可以在几分钟内构建一个生产就绪的静态网站，而无需花费数年时间掌握前端开发或JavaScript。这使得它可以被广泛的用户访问，无论他们的技术背景如何。此外，MkDocs的材料是麻省理工学院许可的，可以免费使用，这有助于它的广泛采用，并允许每个人免费构建复杂的文档网站。

我们的愿景是为您提供工具，让您拥有自己的文档，使您能够开发自己的流程来制作出色的文档，并避免被锁定在昂贵的订阅服务中，即使是做简单的事情。我们认为，这些工具应该易于设置和配置以满足您的需求，这一点很重要，但如果需要，还应该给您进一步调整它们的自由。这就是为什么我们一直在努力确保我们的架构是模块化的，面向未来。2.

  [^2]:
    Material for MkDocs附带的[内置插件]完美地概述了这一原则，因为它们相互补充，可以结合使用来构建复杂的管道。这种模块化设计允许用户挑选他们需要的功能，确保框架保持轻量级和灵活性。

    例如，[privacy plugin]可以与[optimize plugin]协同工作，以便外部资产可以通过与文档其余部分相同的优化管道传递。这意味着您可以在存储库之外存储和编辑未优化的文件，并让这两个插件自动为您构建一个优化的网站。

  [built-in plugins]: ../../plugins/index.md
  [privacy plugin]: ../../plugins/privacy.md
  [optimize plugin]: ../../plugins/optimize.md

## 挑战

现在，让我们谈谈我们的旅程以及我们正在应对的特殊挑战。“我们”指的是@squidfunk有幸围绕他的原创作品建立的令人难以置信的团队，这要归功于他从[赞助商]那里获得的财政支持。这个卓越的团队包括@alexvoss和@katharinalisalin，他们在研究、开发和社区支持方面的宝贵贡献对该项目的持续成功至关重要。

我们一起开始探索新技术，整合我们从用户那里收到的反馈，并从第一原则重新思考关键组件，为我们不断发展的社区服务，这是创建文档的最佳框架之一。

  [sponsors]: https://github.com/sponsors/squidfunk

本节重点介绍我们一直关注的关键领域。

### 搜索和发现

在我们看来，搜索是任何有效文档网站的基石，使用户能够快速找到所需的信息。从一开始，我们就依赖于[Lunr.js]，这是一个流行的客户端搜索库，它简化了文档站点的部署，而不需要外部服务。多年来，Lunr.js在用Material for MkDocs构建的网站上回答了数百万个查询，为我们提供了很好的服务。然而，随着用户需求的演变，我们遇到了难以克服的局限性。

  [Lunr.js]: https://github.com/olivernn/lunr.js

我们了解到，Lunr.js核心的[BM25排名算法]（与许多其他搜索实现一样）并不适合有效和稳定的类型先行。添加新文档可能会影响现有的排名，需要手动调整[^3]，这既繁琐又难以扩展。此外，Lunr.js的性能问题源于其设计没有充分利用现代JavaScript引擎和优化，使其速度较慢且内存密集。4.

  [^3]:
    在[BM25][BM25排名算法]中增强文档可能会带来挑战，特别是在文档语料库不断变化的情况下。相关性是根据术语频率和术语在整个语料库中的重要性来计算的。增强文档包括调整其权重，使其在搜索结果中更突出。

    随着新文档的添加或现有文档的修改，术语频率的整体分布及其重要性可能会发生变化。这种重新校准可能会降低提升的有效性，使在不断变化的数据集中保持一致的排名变得更加困难。从本质上讲，增强的文档可能不会像预期的那样突出或相关，从而导致搜索结果中的不平衡和可扩展性问题。

  [^4]:
    Lunr.js使用JavaScript对象来索引和管理搜索数据，由于JavaScript引擎处理对象操作的方式，这会导致效率低下。JavaScript引擎使用内联缓存和对象形状优化等技术优化性能。然而，这些优化依赖于可预测和一致的对象结构。

    Lunr.js索引的动态特性——文档可以有不同的结构——阻碍了引擎有效地应用这些优化。这意味着，虽然JavaScript引擎可以针对固定、可预测的对象结构进行优化，但它们难以应对Lunr.js索引的多态性和流动性，从而导致随着数据量的增长而出现性能问题。

  [BM25 ranking algorithm]: https://en.wikipedia.org/wiki/Okapi_BM25

在过去的几年里，我们在[改善搜索体验]方面投入了大量资金。例如，扩展Lunr.js的功能以添加对[丰富搜索预览]和[标记器前瞻]的支持需要大量的工程工作。Lunr.js允许使用[管道函数]自定义词干、停用词过滤和修剪等任务，但这使得添加术语突出显示或替代排名方法等扩展变得特别困难。再加上Lunr.js自2020年以来一直未得到维护，很明显我们需要找到一个更强大的解决方案。我们已经研究了其他基于JavaScript的库来保持我们的客户端搜索，但没有一个符合我们的要求或达到我们的期望。

  [improving the search experience]: search-better-faster-smaller.md
  [rich search previews]: search-better-faster-smaller.md#rich-search-previews
  [tokenizer lookahead]: search-better-faster-smaller.md#tokenizer-lookahead
  [pipeline functions]: https://lunrjs.com/guides/customising.html#pipeline-functions
  [unmaintained since 2020]: https://github.com/olivernn/lunr.js/releases/tag/

为了应对这些挑战，我们已经开始根据第一原则开发一个新的搜索系统，该系统不仅匹配，而且已经超过了Lunr.js的能力。该系统从头开始构建，速度更快，更紧凑，最重要的是：模块化。它基于一个不断发展的核心，围绕我们认为必不可少的两个核心概念——引擎和插件——发展，允许灵活配置和组装文本索引、向量嵌入、过滤、排名、突出显示等组件。它的每个部分都可以被替换或扩展，使用户能够根据自己的特定需求定制搜索系统。

我们的新搜索系统将作为一个单独的麻省理工学院许可的开源项目发布，旨在处理从小型博客到大型文档项目的各种场景。当然，它支持离线使用，并与客户端和服务器环境无缝集成。先进的排名系统提供了精细的控制，与第三方服务的集成现在更加简单。

__:octicons-goal-16: 目标——通过提供适应不同内容类型的搜索系统，使用户能够快速找到所需的信息，同时使作者无需管理外部服务。__

你可能会想知道为什么它还没有上市。从头开始开发该系统并发掘其潜力的过程使我们重新评估了MkDocs材料的核心概念。因此，我们决定推迟发布新的搜索系统，以便将其整合到我们开始进行的更广泛的更新中。如果你继续阅读，你会了解我们决定采用这种方法的更多原因。

我们很高兴在本系列的下一篇文章中分享有关此更新的更多细节。

### 翻译和版本控制

在MkDocs中支持多语言网站是[我们讨论板上最受欢迎的功能]和与用户的对话中，但它带来了重大挑战，因为MkDocs本身并不支持它。版本控制也是如此，它还涉及多项目构建的同步。虽然MkDocs生态系统已经开发了[各种插件和工具]来解决这些问题，但仍有大量未开发的潜力。我们开始探索这些领域，但很快遇到了阻碍我们进步的问题。

  [most requested feature on our discussion board]: https://github.com/squidfunk/mkdocs-material/discussions/2346
  [various plugins and tools]: https://github.com/mkdocs/catalog?tab=readme-ov-file#-site-building-site-management

如您所知，我们最初的工作涉及[项目插件]，旨在扩展MkDocs以添加对多项目环境的支持，作为支持多语言网站和版本控制的坚实基础。不幸的是，由于MkDocs的内部架构和设计限制，我们遇到了重大挑战，我们正在积极解决这些问题。5.

  [^5]:
    在开发[projects插件]时，我们最初取得了[良好的进展]，包括添加了对嵌套项目的支持，并允许子项目具有更多子项目的树形结构。然而，我们很快遇到了困难，特别是在跨项目导航方面。为了说明这一点，想象一下，每个项目都可以链接到任何其他项目，这使得处理这些互连变得复杂，特别是在处理循环依赖关系时，例如项目A链接到项目B，反之亦然。

    在MkDocs中实现多项目支持尤其具有挑战性，因为缺乏官方编程API，这使扩展其功能的工作变得复杂。此外，在建设项目之前解决导航问题对于确保适当的互联互通至关重要。这些挑战加在一起，使项目插件的开发成为一项复杂的工作。

  [projects plugin]: ../../plugins/projects.md
  [good progress]: https://github.com/squidfunk/mkdocs-material/discussions/5800

__:octicons-goal-16: 目标——通过提供无缝集成多个文档项目的方法，将文档扩展到任何规模或团队结构，无论它们涉及不同的语言、版本还是整个工作体系的不同部分。__

因此，我们正在开发一种新方法，为多语言支持和版本控制提供更全面、更稳健的解决方案。这种新方法也与搜索等相邻功能相交，因为我们的许多用户对将多个文档站点的结果组合到统一搜索界面中的[联合搜索]功能感兴趣。在发布新的搜索系统之前，克服这一挑战是我们需要解决的主要障碍之一。

  [federated search]: https://github.com/squidfunk/mkdocs-material/issues/5230

### 编辑和协作

我们曾考虑开发一个实时编辑器来应对MkDocs（大型项目的性能问题），在大多数情况下，这些问题源于不使用缓存的计算密集型插件。基于[Pyodide]（=在浏览器中运行Python）的[概念证明]在用户中引起了极大的兴趣，并促使许多组织和个人分享他们的协作工作流程以获得反馈。遗憾的是，实现这个实时编辑器被证明非常具有挑战性，因为它需要重建MkDocs的大部分内容。[^6]在停止这种方法的工作后，我们在多项目支持方面的进展再次让我们相信，我们最终可以解决过去几年中多次报道的编辑缓慢的问题。7.

  [performance issues with large projects]: https://github.com/mkdocs/mkdocs/issues/3695#issuecomment-2093299518
  [proof of concept]: https://x.com/squidfunk/status/1338252230265360391
  [Pyodide]: https://pyodide.org/
  [generated significant interest]: https://github.com/squidfunk/mkdocs-material/issues/2110

  [^6]:
    我们的[概念验证]支持MkDocs Material的一些功能，但并没有涵盖所有功能。例如，集成对图标的支持或文档之间的链接将需要重新实现MkDocs的部分内容，以绕过完全重建——这显然是我们想要避免的。此外，某些链接，例如从模式生成的博客文章的链接，不仅被翻译，而且是动态计算的，这意味着它们不能通过将“.md”扩展名替换为“.html”来推断。

  [^7]:
    在我们再次向MkDocs的维护人员提出这个问题[^8]，并在2024年中期[维护人员变更]之后，一项旨在通过[仅渲染当前正在构建的页面]来解决缓慢加载问题的[彻底重写]工作已经开始。目前尚不清楚这种重写将如何与现有插件的要求相结合。复杂的插件，如[mkdocstrings]，或我们的[内置博客]和[标签]插件，需要协调构建所有页面，以准确解析页面之间的链接和计算资源，如果不构建整个项目，就无法确定这些链接。

    __Update__{ title="August 21, 2024" }: 新的维护者现在公开表示，他正在开发一个新版本的MkDocs，该版本[不需要或不支持插件]，并提到它将通过模板、主题和样式提供定制功能，这也是他在[8月1日的团队电话会议]上向我们和其他几位用户提到的。在这次通话中，我们多次就这将如何影响生态系统提出异议，但无济于事。没有提供插件支持的意图或路线图。这一发展与我们的目标正交，即通过模块化的方式，使用户和组织能够使核心框架适应他们的需求。我们正在努力解决这种情况，并将为我们的社区提供一条前进的道路。

  [we raised this issue]: https://github.com/mkdocs/mkdocs/issues/3695
  [maintainership changed]: https://github.com/mkdocs/mkdocs/discussions/3677
  [ground-up rewrite]: https://github.com/mkdocs/sketch
  [rendering only the page currently being built]: https://github.com/mkdocs/mkdocs/issues/3695#issuecomment-2117939743
  [mkdocstrings]: https://mkdocstrings.github.io/
  [built-in blog]: ../../plugins/blog.md
  [tags]: ../../plugins/tags.md
  [does not require or support plugins]: https://github.com/mkdocs/mkdocs/discussions/3815#discussioncomment-10398312
  [a team call on August 1]: https://github.com/mkdocs/mkdocs/discussions/3671#discussioncomment-10164237
  [we raised objections multiple times]: https://github.com/mkdocs/mkdocs/discussions/3671#discussioncomment-10215445

  [^8]:
    Previously raised issues include [#2418], [#2384], and [#1900].

  [#1900]: https://github.com/mkdocs/mkdocs/issues/1900
  [#2384]: https://github.com/mkdocs/mkdocs/issues/2384
  [#2418]: https://github.com/mkdocs/mkdocs/issues/2418

这使我们开始合作，这最初不在我们的优先事项清单上。然而，在整个2024年，与各种组织和流行开源项目的维护者的对话强调了对增强协作功能的频繁要求。许多用户表示需要允许非技术团队成员建议和更改文档的功能。我们衷心感谢这一反馈，因为它是在一个关键时刻出现的。我们认识到，有必要简化对变化的跟踪和讨论，并促进按需捐款。

__:octicons-goal-16: 目标——无论技术水平如何，每个人都可以轻松地处理和改进文档，并为不断增长的知识库做出贡献。__[^9]

  [^9]:
    我们正在积极调整未来的发展努力，以解决这一问题，并认识到这是一个需要改进的关键领域。虽然这不是我们可以立即实现的，但我们致力于在我们的工作中实现这一愿景。

这种对协作的关注与企业管理知识的方式是一致的。在大型组织中，文档通常存在于[信息孤岛]中——分散但必不可少的信息存储库。我们理解，需要能够将这些不同的来源统一为一个连贯的知识体系，同时保持分散的所有权。这也与我们之前概述的多项目支持工作以及在多个项目之间实现[联合搜索]的新搜索系统非常一致。

  [information silos]: https://en.wikipedia.org/wiki/Information_silo

### 大型语言模型（LLMs）

大约一年前，我们在文档网站上引入了一个[实验性聊天机器人]。它很快成为最受期待的功能之一，用户要求能够在自己的网站上部署类似的功能，这突显了对交互式文档工具日益增长的需求。然而，我们发现，在现有的无数聊天解决方案中添加内容，并在ChatGPT的基础上简单地构建另一个瘦包装是无稽之谈。

__:octicons-goal-16: 目标——我们设想创建一个统一的界面，无缝集成高级搜索、聊天和摘要功能，提供交互式文档体验。__

  [experimental chatbot]: https://github.com/squidfunk/mkdocs-material/discussions/6240

当我们深入研究这个雄心勃勃的项目时，我们从用户反馈中获得了宝贵的见解。用户开始用他们的母语与聊天机器人进行交互，这是我们没有预料到的结果，因为我们的文档是英文的。值得注意的是（或者很明显，对于那些常年从事法学硕士工作的人来说），聊天机器人用同样的语言做出了回应。LLM的这种能力是这些机器学习模型真正令人兴奋的特性之一，因为它有可能提高文档的可访问性。然而，尽管我们采用了最先进的RAG方法，但结果喜忧参半，偶尔还会出现幻觉。

这些经验使我们在集成基于LLM的功能之前，优先考虑增强我们的搜索能力。从头开始构建搜索引擎已经是一项艰巨的工作，如果没有坚实的搜索基础，增加更多的复杂性还为时过早。通过重新构建我们的搜索功能，我们的目标是创建一个强大的平台，无缝支持高级信息检索，并提供连贯的交互式文档体验。

## 团队、透明度和增长

在我们应对挑战和探索该项目机遇的同时，我们认为有必要展示我们如何为其持续增长和成功奠定坚实的基础。请将此视为概述，而不是正式的路线图——我们的详细计划正在制定中。我们强调的目标代表了我们旨在解决的最具影响力的领域。

感谢赞助商的慷慨支持，我们很幸运能够组建一支能够为此投入大量时间和专业知识的团队。这种新发现的能力使我们能够更深入地研究核心开发，同时也更全面地与我们的用户社区互动。特别值得一提的是@kamilkrzyskow，他是我们宝贵的[社区专家]之一，在支持用户和促进我们平台上的讨论方面发挥了至关重要的作用。

  [community experts]: ../../insiders/community-experts-program/index.md

在团队的支持下，@squidfunk可以专注于开发的核心，而我们已经开始投资用户研究。这项工作有助于我们了解组织和个人如何与我们的工具互动，根据与用户和公司的大量对话的真实反馈来指导项目的未来方向。

为了进一步扩大我们的团队，我们致力于提高透明度和沟通。由于时间限制，我们之前的工作经常发生在幕后，但我们现在专注于使我们的流程更加开放，并吸引新的贡献者。通过采用这种协作方法，我们的目标是增强我们的工具，并确保它们满足我们社区不断变化的需求。

## 我们面前有什么

当我们展望未来时，我们现在正在奠定的一些基础对于即将到来的激动人心的发展至关重要。我们讨论的许多举措都是基础性工作，将为更具雄心和创新性的功能奠定基础。一旦这些核心要素到位，我们将提供一系列与我们的愿景和目标相一致的令人兴奋的新功能。

在接下来的几个月里，我们将分享更多关于我们计划的细节，以及它们将如何为我们的总体目标做出贡献。虽然增长和创新是我们计划的首要任务，但我们想向您保证，我们的核心价值观保持不变。我们致力于维护迄今为止指导我们的原则，确保我们的增长既健康又一致：

- 针对最近公司偏离开源核心思想的行业趋势，我们正在加倍致力于开源，因为我们相信这是我们工作和[文档即代码]方法的价值主张的核心。

  [docs as code]: https://www.writethedocs.org/guide/docs-as-code/

- 我们的[有机增长方法]是这一战略的一部分，因为它使我们独立于个人资金来源和提供投资回报的压力，而这正是导致许多其他项目偏离开源原则的原因。

  [organic approach to growth]: https://star-history.com/#squidfunk/mkdocs-material

- 同样，我们也受到社区对核心框架适应丰富生态系统的需求的驱动。可扩展性和模块化是实现这一目标的关键，我们正在努力通过提供清晰的接口来改善开发人员体验。

请继续关注最新进展，我们将继续巩固我们的进展并探索新的可能性。我们对未来感到兴奋，并期待在我们前进的过程中与您分享更多。

_Martin, Alex and Kathi_ :octicons-heart-fill-24:{ .mdx-heart .mdx-insiders }

# 错误报告

MkDocs的材料是一个积极维护的项目，我们不断努力
改善。对于如此规模和复杂性的项目，可能会出现错误。如果你
如果您发现了一个错误，您可以通过在我们的
公共[问题跟踪器]，遵循本指南。

  [issue tracker]: https://github.com/squidfunk/mkdocs-material/issues

## 在创建问题之前

拥有20000多名用户，每隔一天就会产生一个问题。维护人员
该项目的负责人正努力通过以下方式减少未决问题的数量
尽快修复错误。通过遵循本指南，您将确切地知道
我们需要什么信息来快速帮助您。

__但首先，在创建问题之前，请执行以下操作。__

### U升级至最新版本

您发现的错误很可能已经在后续版本中得到修复
版本。因此，在报告问题之前，请确保您正在运行
MkDocs材料的[最新版本]。请参阅我们的[升级指南]
了解如何升级到最新版本。

!!! warning "Bug修复不是向后移植的"

    请理解，只有最新版本的
    MkDocs的材料将被处理。此外为了减少重复工作，
    修复程序不能向后移植到早期版本。

### 删除自定义项

如果您正在使用[自定义]，如[附加CSS]、[JavaScript]或
[主题扩展]，请在报告错误之前将其从`mkdocs.yml`中删除。
我们无法为可能隐藏在您的覆盖中的错误提供官方支持，因此
确保从`mkdocs.yml`中省略以下设置：

  - [`theme.custom_dir`][theme.custom_dir]
  - [`hooks`][hooks]
  - [`extra_css`][extra_css]
  - [`extra_javascript`][extra_javascript]

如果在删除这些设置后，错误消失了，则错误可能是由以下原因引起的
您的自定义设置。一个好主意是逐渐增加它们以缩小范围
问题的根本原因。如果您进行了重大版本升级，请确保
调整了您覆盖的所有部分。

!!! warning "我们文档中提到的定制"

    Material for MkDocs提供的一些功能只能实现
    定制。如果您在任何自定义设置中发现错误[
    我们的文档明确提到]，当然，我们鼓励您
    报告它。

__如果你遇到问题，不要羞于在我们的[讨论板]上寻求帮助
问题。__

  [latest version]: ../changelog/index.md
  [upgrade guide]: ../upgrade.md
  [Customizations]: ../customization.md
  [additional CSS]: ../customization.md#additional-css
  [JavaScript]: ../customization.md#additional-javascript
  [theme extension]: ../customization.md#extending-the-theme
  [theme.custom_dir]: https://www.mkdocs.org/user-guide/configuration/#custom_dir
  [hooks]: https://www.mkdocs.org/user-guide/configuration/#hooks
  [extra_css]: https://www.mkdocs.org/user-guide/configuration/#extra_css
  [extra_javascript]: https://www.mkdocs.org/user-guide/configuration/#extra_javascript
  [discussion board]: https://github.com/squidfunk/mkdocs-material/discussions
  [StackOverflow]: https://stackoverflow.com
  [that our documentation explicitly mentions]: ?q="extends+base"

### 搜索解决方案

在这个阶段，我们知道问题在最新版本中仍然存在
不是由您的任何自定义造成的。然而，问题可能源于
配置文件中的小拼写错误或语法错误，例如“mkdocs.yml”。

现在，在您完成创建已回答的错误报告的麻烦之前
并立即关闭，链接到相关文档部分或
另一个已报告或已结束的问题或讨论，您可以节省时间
我们和你自己做一些研究：

1.  [搜索我们的文档]并查找可能的相关章节
    与你的问题有关。如果找到，请确保已配置
    一切正常。1.

  [^1]:
    在向`mkdocs.yml`添加行时，请确保保留了
    正如文档中提到的缩进，因为YAML是一个
    空白敏感语言。许多报道的问题被证明是
    配置错误。

1.  [搜索我们的问题跟踪器][问题跟踪器]，因为其他用户可能已经
    已经报告了同样的问题，甚至可能有已知的解决方法
    或者修复它。因此，不需要创建新问题。

2.  [搜索我们的讨论板][讨论板]了解其他用户
    我们正在努力解决类似的问题，并与我们的伟大团队合作
    社区寻求解决方案。这里解决了很多问题。

__Keep track of all <u>search terms</u> and <u>relevant links</u>, you'll need
them in the bug report.__[^2]

  [^2]:
    我们的文档中可能使用了与您不同的术语，
    但我们的意思是一样的。当您包含搜索词和相关链接时
    在您的错误报告中，您帮助我们调整和改进文档。

---

此时，当你还没有找到解决问题的办法时，我们
鼓励你制造一个问题，因为现在你很可能
被我们还不知道的东西绊倒了。阅读以下部分以学习
如何创建一个完整且有用的bug报告。

  [Search our documentation]: ?q=

## 问题模板

我们创建了一个新的问题模板，使错误报告过程变得简单
尽可能提高我们社区和我们的效率。这是
我们在回答和解决1600多个问题（而且还在增加）方面的经验
由以下部分组成：

- [Title]
- [Context] <small>optional</small>
- [Bug description]
- [Related links]
- [Reproduction]
- [Steps to reproduce]
- [Browser] <small>optional</small>
- [Checklist]

  [Title]: #title
  [Context]: #context
  [Bug description]: #bug-description
  [Related links]: #related-links
  [Reproduction]: #reproduction
  [Steps to reproduce]: #steps-to-reproduce
  [Browser]: #browser
  [Checklist]: #checklist

### 名称

一个好的标题应当简短且富有描述性。它应该是一句话的执行
问题摘要，即您要报告的错误的影响和严重程度
可以从标题中推断出来。

| <!-- --> | Example  |
| -------- | -------- |
| :material-check:{ style="color: #4DB6AC" } __Clear__ | Built-in `typeset` plugin changes precedence of nav title over `h1`
| :material-close:{ style="color: #EF5350" } __Wordy__ | The built-in `typeset` plugin changes the precedence of the nav title over the document headline
| :material-close:{ style="color: #EF5350" } __Unclear__ | Title does not work
| :material-close:{ style="color: #EF5350" } __Useless__ | Help

### Context <small>optional</small> { #context }

在描述错误之前，您可以为我们提供额外的上下文
了解你想要实现什么。解释情况
您在其中使用MkDocs的Material，以及您的想法可能是什么
相关。不要在这里写bug。

> __为什么这可能有帮助__: 一些错误仅在特定设置中表现出来，
> 例如，当您的文档包含
> 数千份文件。

### Bug描述

现在，针对您要报告的错误。提供清晰、专注、具体和
您遇到的错误的简明摘要。解释为什么你认为这是一个bug
应向MkDocs的材料部门报告，而不是向其任何一个部门报告
依赖性。[^3]坚持以下原则：

  [^3]:
    有时，用户会在我们的[问题跟踪器]上报告由以下原因引起的错误
    我们的上游依赖项，包括[MkDocs]、[Python Markdown]，
    [Python Markdown扩展]或第三方插件。一个好的经验法则是
    将[`theme.name][theme.name]更改为`mkdocs`或`readthedocs`，然后
    检查问题是否仍然存在。如果是这样，问题可能不是
    与MkDocs材料相关，应向上游报告。当在
    如有疑问，请使用我们的[讨论板]寻求帮助。

-   __Explain the <u>what</u>, not the <u>how</u>__ – 不要解释
    [如何重现错误][重现步骤]在这里，我们到了那里。
    集中精力尽可能清楚地阐明问题及其影响。

-   __Keep it short and concise__ – 如果这个bug可以用一个词来精确解释
    或者两句话，太好了。不要夸大它——维护者和未来的用户
    如果能少读书，我会很感激的。

-   __One bug at a time__ – 如果你遇到几个无关的bug，请
    为他们创建单独的问题。不要在同一个问题中报告它们，因为
    这使得归因变得困难。

---

:material-run-fast: __Stretch goal__ – 如果您找到了解决方法或修复方法
这个bug，你可以在之前帮助其他用户暂时缓解这个问题
我们维护人员可以修复代码库中的错误。

> __Why we need this__: 为了让我们理解这个问题，我们
> 需要对其进行清晰的描述并量化其影响，这一点至关重要
> 用于分类和优先级排序。

  [MkDocs]: https://www.mkdocs.org
  [Python Markdown]: https://python-markdown.github.io/extensions/
  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/
  [theme.name]: https://www.mkdocs.org/user-guide/configuration/#theme

### 相关链接

当然，在报告错误之前，您已经阅读了我们的文档和
[找不到有效的解决方案][搜索解决方案]。请分享链接
我们文档中可能与该错误相关的所有部分，因为它
帮助我们逐步改进它。

此外，由于您搜索了我们的[问题跟踪器]和[讨论板]
在报告问题之前，可能已经发现了几个问题或
讨论，也包括这些。每个问题或讨论的链接都会创建
反向链接，为我们的维护人员和其他用户提供未来的指导。

---

:material-run-fast: __Stretch goal__ – 如果你也包括搜索词，你
当你为你的问题[寻找解决方案][寻找解决方案]时，你
使我们的维护人员更容易改进文档。

> __Why we need this__: 相关链接帮助我们更好地了解您的身份
> 试图实现以及我们的文档部分是否需要
> 调整、扩展或大修。

  [search for solutions]: #search-for-solutions

### 生殖

最小限度的复制是每一份写得很好的bug报告的核心，因为
它允许我们的维护人员立即重新创建必要的条件
检查错误以快速找到其根本原因。事实证明，问题
简洁的小复制品可以更快地修复。

[:material-bug: Create reproduction][Create reproduction]{ .md-button .md-button--primary }

---

创建复制品后，最好有一个.zip文件
不大于1MB。只需将“.zip”文件拖放到此字段中
将自动上传到GitHub。

> __为什么我们需要这个__: 如果一个问题没有最低限度的复制或只是
> 一个包含数千个文件的存储库的链接，维护人员需要
> 投入大量时间试图重新创造合适的条件，以实现收支平衡
> 检查这个bug，更不用说修复它了。

!!! warning "不共享指向存储库的链接"

    虽然我们知道在开发人员中包含链接是一种很好的做法
    对于带有错误报告的存储库，我们目前不支持
    过程。原因是复制，这是自动的
    由[内置信息插件]生成的包含所有必要的
    经常被遗忘的环境信息。

    此外，还有许多MkDocs材料的非技术用户
    创建存储库时遇到问题。

  [Create reproduction]: ../guides/creating-a-reproduction.md
  [built-in info plugin]: ../plugins/info.md

### 重现步骤

此时，您为我们提供了足够的信息来了解该错误
并为我们提供了一个可以运行和检查的复制品。然而，当
我们运行你的复制，我们可能无法立即看到
bug在行动。

因此，请列出我们在运行您的
繁殖以观察虫子。保持步骤简短明了，并确保
不要遗漏任何东西。使用简单的语言，就像你向别人解释的那样
五岁，注重连续性。

> __为什么我们需要这个__: 我们必须知道如何引导你的繁殖
> 观察bug，因为有些bug只发生在某些视口或
> 具体条件。

### Browser <small>optional</small> { #browser }

如果你报告的bug只发生在一个或多个特定浏览器中，
我们需要知道哪些浏览器受到了影响。此字段是可选的，因为它是
仅当您报告的错误不涉及崩溃时才相关
[预览]或[构建]您的网站。

---

:material-incognito: __无痕模式__ – 请验证错误是否存在
不是由浏览器扩展引起的。切换到隐身模式并尝试复制
bug。如果它消失了，那是由于延期造成的。

> __为什么我们需要这个__: 有些bug只出现在特定的浏览器或版本中。
> 从现在开始，几乎所有的浏览器都是常青的，我们通常不需要知道
> 它发生的版本，但我们以后可能会要求提供。如有疑问，请添加
> 浏览器版本作为上述字段的第一步。

  [previewing]: http://localhost:8000/mkdocs-material/creating-your-site/#previewing-as-you-write
  [building]: http://localhost:8000/mkdocs-material/creating-your-site/#building-your-site

### 清单

感谢您遵循指南并创建了一个高质量和完整的bug
报告——你快完成了。检查表确保您已阅读本指南
并尽最大努力为我们提供所需的一切
知道帮助你。

__我们从这里开始。__

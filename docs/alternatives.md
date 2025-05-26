# 选择

有很多静态网站生成器和主题，可以选择
为你的技术栈选择一个合适的是一个艰难的决定。如果你不确定材料
因为MkDocs是适合您的解决方案，本节应该帮助您评估
替代解决方案。

## Docusaurus

Facebook的[Docusaurus]是一个非常受欢迎的文档生成器，也是一个很好的
如果您或您的公司已经在使用[React]构建您的网站，请选择。
它将生成一个从根本上不同的[单页应用程序]
从为您生成的Material for MkDocs网站。

__优势__

- 非常强大、可定制和可扩展
- 提供许多有助于技术写作的组件
- 庞大而丰富的生态系统，由Facebook支持

__挑战__

- 学习曲线高，必须具备JavaScript知识
- JavaScript生态系统非常不稳定，维护成本很高
- 需要更多的时间来起床和跑步

当涉及到文档时，[Docusaurus]是最佳选择之一
输出单个页面应用程序的网站，还有更多的解决方案，
包括[Docz]、[Gatsby]、[Vuepress]和[Docsify]这种方法
这个问题类似。

  [Docusaurus]: https://docusaurus.io/
  [React]: https://reactjs.org/
  [single page application]: https://en.wikipedia.org/wiki/Single-page_application
  [Docz]: https://www.docz.site/
  [Gatsby]: https://www.gatsbyjs.com/
  [VuePress]: https://vuepress.vuejs.org/
  [Docsify]: https://docsify.js.org/

## Jekyll

[Jekyll]可能是最成熟和最广泛的静态网站之一
生成器，用[Ruby]编写。它不是专门针对
技术项目文档，有许多主题可供选择，其中
可能具有挑战性。

__优势__

- 久经考验，丰富的生态系统，许多主题可供选择
- 为博客带来强大的功能（永久链接、标签等）
- 生成一个SEO友好的网站，类似于Material for MkDocs

__挑战__

- 不专门针对技术项目文档
- Markdown功能有限，不如Python Markdown高级
- 需要更多的时间来起床和跑步

  [Jekyll]: https://jekyllrb.com/
  [Ruby]: https://www.ruby-lang.org/de/

## Sphinx

[Shinx]是一个专门针对以下对象的替代静态站点生成器
生成参考文档，提供以下强大功能
缺少MkDocs。它使用[reStructured text]，一种类似于Markdown的格式，
一些用户发现更难使用。

__优势__

- 非常强大、可定制和可扩展
- 从[Python docstrings]生成参考文档
- 庞大而丰富的生态系统，被许多Python项目使用

__挑战__

- 学习曲线高，[reStructured text]语法可能具有挑战性
- 搜索功能不如MkDocs提供的强大
- 需要更多的时间来起床和跑步

如果您正在考虑使用Sphinx，因为您需要生成引用
文档，你应该试试[mkdocstrings]——一个积极维护的
基于MkDocs构建的流行框架，实现了类似Sphinx的
功能。

  [Sphinx]: https://www.sphinx-doc.org/
  [reStructured text]: https://en.wikipedia.org/wiki/ReStructuredText
  [Python docstrings]: https://www.python.org/dev/peps/pep-0257/
  [mkdocstrings]: https://github.com/mkdocstrings/mkdocstrings

## GitBook

[GitBook]提供了一个托管文档解决方案，可以生成美观且
GitHub存储库中Markdown文件的功能站点。然而，事实的确如此
曾经是开源的，但不久前变成了闭源解决方案。

__优势__

- 托管解决方案，所需技术知识最少
- 自定义域、身份验证和其他企业功能
- 团队协作功能强大

__挑战__

- 闭源代码，专有项目不免费
- Markdown功能有限，不如Python Markdown高级
- 许多开源项目从GitBook转移

许多用户从[GitBook]切换到Material for MkDocs，因为他们想保留
控制和拥有他们的文档，支持开源解决方案。

  [GitBook]: https://www.gitbook.com/

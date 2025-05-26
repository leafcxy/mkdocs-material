# 选择

有很多静态网站生成器和主题可供选择，为您的技术栈选择一个合适的解决方案是一个艰难的决定。如果您不确定 Material for MkDocs 是否适合您的需求，本节应该帮助您评估替代解决方案。

## Docusaurus

Facebook 的 [Docusaurus] 是一个非常受欢迎的文档生成器，如果您或您的公司已经在使用 [React] 构建网站，这是一个很好的选择。它将生成一个从根本上不同的[单页应用程序]，与 Material for MkDocs 生成的网站不同。

__优势__

- 非常强大、可定制和可扩展
- 提供许多有助于技术写作的组件
- 庞大而丰富的生态系统，由 Facebook 支持

__挑战__

- 学习曲线高，必须具备 JavaScript 知识
- JavaScript 生态系统非常不稳定，维护成本很高
- 需要更多的时间来启动和运行

当涉及到文档时，[Docusaurus] 是输出单页应用程序网站的最佳选择之一，还有其他类似的解决方案，包括 [Docz]、[Gatsby]、[Vuepress] 和 [Docsify]。

  [Docusaurus]: https://docusaurus.io/
  [React]: https://reactjs.org/
  [single page application]: https://en.wikipedia.org/wiki/Single-page_application
  [Docz]: https://www.docz.site/
  [Gatsby]: https://www.gatsbyjs.com/
  [VuePress]: https://vuepress.vuejs.org/
  [Docsify]: https://docsify.js.org/

## Jekyll

[Jekyll] 可能是最成熟和最广泛使用的静态网站生成器之一，使用 [Ruby] 编写。它不是专门针对技术项目文档设计的，有许多主题可供选择，这可能具有挑战性。

__优势__

- 久经考验，丰富的生态系统，许多主题可供选择
- 为博客带来强大的功能（永久链接、标签等）
- 生成一个 SEO 友好的网站，类似于 Material for MkDocs

__挑战__

- 不专门针对技术项目文档
- Markdown 功能有限，不如 Python Markdown 高级
- 需要更多的时间来启动和运行

  [Jekyll]: https://jekyllrb.com/
  [Ruby]: https://www.ruby-lang.org/de/

## Sphinx

[Sphinx] 是一个专门针对生成参考文档的替代静态站点生成器，提供了一些 Material for MkDocs 所缺少的强大功能。它使用 [reStructured text]，一种类似于 Markdown 的格式，一些用户发现更难使用。

__优势__

- 非常强大、可定制和可扩展
- 从 [Python docstrings] 生成参考文档
- 庞大而丰富的生态系统，被许多 Python 项目使用

__挑战__

- 学习曲线高，[reStructured text] 语法可能具有挑战性
- 搜索功能不如 MkDocs 提供的强大
- 需要更多的时间来启动和运行

如果您正在考虑使用 Sphinx 来生成参考文档，您应该试试 [mkdocstrings] —— 一个积极维护的基于 MkDocs 构建的流行框架，实现了类似 Sphinx 的功能。

  [Sphinx]: https://www.sphinx-doc.org/
  [reStructured text]: https://en.wikipedia.org/wiki/ReStructuredText
  [Python docstrings]: https://www.python.org/dev/peps/pep-0257/
  [mkdocstrings]: https://github.com/mkdocstrings/mkdocstrings

## GitBook

[GitBook] 提供了一个托管文档解决方案，可以从 GitHub 仓库中的 Markdown 文件生成美观且功能强大的站点。然而，它曾经是开源的，但不久前变成了闭源解决方案。

__优势__

- 托管解决方案，所需技术知识最少
- 自定义域、身份验证和其他企业功能
- 团队协作功能强大

__挑战__

- 闭源代码，专有项目不免费
- Markdown 功能有限，不如 Python Markdown 高级
- 许多开源项目从 GitBook 转移

许多用户从 [GitBook] 切换到 Material for MkDocs，因为他们想要保留对文档的控制权，并支持开源解决方案。

  [GitBook]: https://www.gitbook.com/

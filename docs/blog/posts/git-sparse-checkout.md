---
date: 2023-09-22
authors: [squidfunk]
categories:
  - Build
  - Performance
links:
  - publishing-your-site.md#with-github-actions
  - creating-your-site.md#building-your-site
---

# 使用`git sparse checkout`实现更快的文档构建

__利用GitHub Actions中的“git sparse checkout”使我们能够加快速度
文档构建在我们的存储库中，将结账时间从20缩短到30
秒到2秒。__

开发一种在CI工作流中构建文档的有效方法
至关重要，尤其是在拥有数千个存储库的大型存储库中工作时
承诺，就像我们一样。当然，我们希望快速构建文档
高效，确保快速高效的工作流程。当同时使用时
很棒的[git提交者][git提交者]和[git修订日期本地化]
[git修订日期本地化]插件，用于显示[文档贡献者]和
在每页底部的[日期]处，我们需要设置“获取深度：0”，
这导致我们的存储库的结账时间为20到30秒。By
在[GitHub Actions]中利用[git sparse checkout][git sparse checkout]，
退房时间缩短到2秒。

  [git sparse-checkout]: https://git-scm.com/docs/git-sparse-checkout
  [GitHub Actions]: ../../publishing-your-site.md#with-github-actions
  [git-revision-date-localized]: https://github.com/timvink/mkdocs-git-revision-date-localized-plugin
  [git-committers]: https://github.com/ojacques/mkdocs-git-committers-plugin-2
  [document contributors]: ../../setup/adding-a-git-repository.md#document-contributors
  [dates]: ../../setup/adding-a-git-repository.md#document-dates

<!-- more -->

## 底漆

[`git sparse checkout`][git sparse checkout]只允许您签出一个
存储库中文件的子集，使其对大型应用程序非常有用
完整签出需要很长时间，并且包含许多文件的存储库
在构建文档时不相关。

## GitHub操作

在[GitHub Actions]中启用[`git sparse checkout][git sparse checkout]
并确保您只构建所需的文档，添加
将以下行添加到工作流文件中：

``` yaml
- uses: actions/checkout@v4
  with:
    fetch-depth: 0
    sparse-checkout: |
      docs
      includes
```

[`git sparse checkout`][git sparse checkout]始终检出所有文件
位于存储库的根目录中。这意味着，无论指定了什么
稀疏签出的路径或目录，位于根目录中的文件
存储库将始终包含在签出过程中。

因此，您只需指定构建所需的目录
文档。在我们的例子中，我们只需要“docs”和“includes”文件夹，
但如果你需要额外的目录，你可以把它们添加到
列表。[GitHub Actions]的完整示例工作流：

``` yaml hl_lines="13-18"
name: documentation
on:
  push:
    branches:
      - master
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
          sparse-checkout: |
            docs
            includes
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - run: pip install mkdocs-material
      - run: mkdocs gh-deploy --force
```

## 结论

就这些！我们对结果非常满意，并希望这将
帮助您加快[GitHub Actions]中的文档构建速度。As
请随时在下面的评论中分享您的想法和经验。

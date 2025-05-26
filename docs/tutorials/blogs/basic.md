# 基础博客

博客是与你的受众互动的好方法。软件开发人员可以使用
一个博客，宣布新功能，演示其使用方法并提供背景
信息。您可以通过评论以下状态来展示自己的能力
将自己的作品作为最佳实践进行艺术创作或记录。关于当前主题的帖子可以提供帮助
为你的主网站吸引访客，可以让你的观众保持参与度。属于的
当然，你可以在博客上写任何你感兴趣的话题。

[blog plugin]使博客与其他内容一起运行变得容易，但你
如果帖子是唯一的类型，还可以将其配置为运行独立博客
你需要的内容。

在简要概述博客的基本概念后，本教程将指导您
通过配置[blog plugin]、设置博客的过程，
创建帖子和定义帖子元数据。

[blog plugin]: ../../plugins/blog.md

__所需时间:__ 通常为20分钟

## 关键概念

**帖子、摘录**: 博客由许多自包含的posts（通常称为
文章）和一个按时间倒序显示帖子的索引页面，其中
最新的帖子在顶部。索引页通常只显示一个简短的_excerpt_和一个
用户可以单击链接导航到完整帖子。

**元数据**: 索引页面和帖子本身都列出了以下信息
当你发布这篇文章时，当你更新它时，作者是谁，以及
预计阅读时间为。

**蛞蝓**: 由于博客文章主要按时间排列，而不是按层次结构排列，
它们的URL不反映这种结构。相反，每个帖子的URL
包含一个简短的描述，即_slug_，通常来源于
帖子中的第一个标题。

**导航**: 主导航结构是时间线，您可以
细分为_类_。主索引页面显示了最近的帖子
而archive_部分允许访问按年份组织的旧版本。
此外，帖子可以标记为_tagged_，_tag索引页提供了额外的
基于内容的导航结构。

你可以在[Material for MkDocs blog]上看到所有这些元素。

[Material for MkDocs blog]: https://squidfunk.github.io/mkdocs-material/blog/

## 设置你的博客

博客插件是MkDocs材料的一部分，但你需要对其进行配置
在`mkdocs.yml`中。

!!! example "建立博客"

    如果你还没有这样做，为你的博客创建一个项目，
    然后编辑`mkdocs.yml`文件，确保其包含以下内容：

    ```yaml
    site_name: Blog Tutorial
    site_description: an example blog set up following the tutorial
    site_url: http://www.example.com

    theme:
      name: material

    plugins:
      - search
      - blog
    ```

    博客插件将为您的博客文章创建一个目录结构，如果
    不存在，因此只需运行`mkdocs-serve`即可获取：

    ```
    docs
    ├── blog
    │   ├── index.md
    │   └── posts
    └── index.md
    ```

现在，在`docs/blog/posts`中创建您的第一篇博客文章。您可以使用任何
您喜欢的帖子命名约定和目录结构，只要
它们位于`docs/blog/posts`中。

每篇帖子_must_都有一个页眉，出现在Markdown的顶部
用三个破折号分隔行之间的代码。在这个标题中，你需要有
至少是一个“日期”条目，但您可以添加其他数据，如下所示。
标题后面是页面内容。请注意，这很重要
当插件使用它来生成splug时，要有一个一级标题。也，
通过添加“<！--more-->`到页面，您可以定义摘录的结束位置
索引页面显示的内容。

!!! example "写你的第一篇文章"

    创建一个文件`docs/blog/posts/myfirst.md`，其中包含以下内容：

    ```
    ---
    date:
      created: 2023-12-31
    ---

    # Happy new years eve!

    We hope you are all having fun and wish you all the best for the new year!
    <!-- more -->

    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua.
    ```

    然后，运行`mkdocs-serve`并将您的web浏览器指向
    `http://localhost:8000/blog`.

    博客插件会自动为以下内容创建导航元素
    博客。索引页面仅显示摘录。当您选择
    “继续阅读”链接，您将看到完整的博客文章。注意它是如何
    具有从第一级标题生成的URL。

!!! tip "导航"

    我们还有一个[tutorial on navigation]，向您展示如何更改
    自动创建导航，并将博客集成到现有的
    导航结构。它展示了如何创建辅助导航，生成
    作者页面和控制分页。

[tutorial on navigation]: navigation.md

## 发布元数据

除了日期，您还可以提供其他元数据并提供插件
指示，例如将帖子视为草稿或将其固定。

### 草稿

你可能想制作一篇博客文章的草稿，并在当地使用它，但
将其从发布的版本中排除。只需在页面中添加一个字段
标题，表示帖子仍处于草稿状态。

!!! example "创建草稿"

    在`docs/blogs/posts/draft.md`中创建第二篇博客文章，内容如下
    内容：

    ```hl_lines="4"
    ---
    date:
      created: 2024-01-01
    draft: true
    ---

    # Happy new year!

    Happy 2024 to everyone. Wishing you all the best!
    <!-- more -->

    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua.
    ```

    现在，请注意草稿如何显示在索引页上，但带有标签
    表示这是一份草稿。当你运行`mkdocs-build`时，草稿将
    _输出中未显示：

    ```
    $ mkdocs build
    $ ls site/blog
    site/blog
    ├── 2023
    │   └── 12
    │       └── 31
    │           └── happy-new-years-eve
    │               └── index.html
    ...
    ```

    2024年的第一篇博客文章尚未发布，因为它仍在起草中
    舞台。记得在需要时删除标题中的“草稿”设置
    出版它。

如果您正在使用[Insiders Edition]，您还可以创建
一个用于保存草稿的文件夹，并使用[Meta-plugin]添加
将`draft`标题设置为该文件夹中的所有帖子。这有好处
更容易看出哪些帖子仍处于草稿状态。我们将介绍
稍后的元插件。

[Meta plugin]: ../../plugins/meta.md

### 编辑

有时，博客作者需要更新帖子。这可能会发生在你做
当你需要在帖子中反映的错误或事情发生变化时。向
表示您已经编辑了一篇帖子，您可以在页面中包含一个“更新”日期
头球

!!! example "编辑帖子"

    更改您的第一篇博客文章，然后在标题中添加编辑日期：

    ```hl_lines="3 4"
    ---
    date:
      created: 2023-12-31
      updated: 2024-01-02
    ---
    ```

博客文章本身的元数据部分将包含编辑日期，
尽管默认情况下索引页面省略了此细节。

### 读取时间

为了让读者了解他们阅读一篇帖子可能需要多长时间，
自动计算读取时间。如果你想覆盖它，你可以
在页眉中指定您估计的分钟数
你的读者会阅读这篇文章。

!!! example "超越阅读时间"

    在你的第一篇博客文章中添加阅读时间覆盖：

    ```hl_lines="5"
    ---
    date:
      created: 2023-12-31
      updated: 2024-01-02
    readtime: 15
    ---
    ```

### 固定

有时，博客作者想“固定”一篇特定的帖子，这样它就永远
出现在索引页面的顶部，无论发布了什么。如果你
正在使用[Insiders Edition]，您可以通过添加“pin”来实现`
页眉中的属性：

!!! example "钉一根柱子 <!-- md:sponsors -->"

    将“pin”属性添加到您的第一篇博客文章中：

    ```hl_lines="6"
    ---
    date:
      created: 2023-12-31
      updated: 2024-01-02
    readtime: 15
    pin: true
    ---
    ```

    观察这如何使帖子出现在索引页面的顶部，即使
    它的发布日期早于其他帖子。一个小的pin图标显示
    帖子已被固定。

### 相关链接

当你的博客是技术文档等更广泛网站的一部分时，你
将希望提供从博客文章到其他内容的链接。一种方式你
可以这样做的是有一个相关的链接部分。博客插件可以创建一个
如果您在页眉中提供链接目标：

!!! example "添加相关链接部分 <!-- md:sponsors -->"

    将以下内容添加到博客文章中：

    ``` hl_lines="5-7"
    ---
    date:
      created: 2023-12-31
    ...
    links:
      - index.md
      - blog/index.md
    ---
    ```

    相关链接显示在元数据部分下方。

这里的好处是你不需要提供页面标题。插件
将通过应用MkDocs用于
主导航。事实上，语法与`nav`部分相同
在`mkdocs.yml`中，您可以根据需要覆盖标题，甚至可以定义
子章节：

!!! example "覆盖页面标题"

    更改链接部分以覆盖页面标题：

    ```hl_lines="6-9"
    ---
    date:
      created: 2023-12-31
    ...
    links:
      - Homepage: index.md
      - Blog index: blog/index.md
      - External links:
        - Material documentation: https://squidfunk.github.io/mkdocs-material
    ---
    ```

该插件在宽屏幕的左侧边栏中呈现相关链接
足够了，在窄屏幕上的柱子底部。更改您的尺寸
浏览器窗口查看此操作。

## 元插件

Meta插件有助于简化元数据的管理
同一子目录中的一组文件。而不必重复同样的事情
在许多文件的页眉中添加元数据，您可以添加`.meta.yml`
目录中的文件，Meta插件会将其内容合并到
包含的所有页面的标题。页面标题中的设置
优先级，因此您始终可以通过将设置添加到帖子中来覆盖它们
头球

例如，您可能希望通过将草稿保存在目录中来管理它们
这样它们不仅被标记为草稿，而且更容易找到。
（否则，您需要检查页眉或从
输出到文件中，以找出哪些帖子是草稿。）

!!! example "使用Meta插件起草 <!-- md:sponsors -->"

    您首先需要在`mkdocs.yaml`中激活插件：

    ```yaml hl_lines="4"
    plugins:
      - search
      - blog
      - meta
    ```

    现在为草稿创建文件夹：

    === "MacOS/Linux"

        ```bash
        $ mkdir docs/blog/posts/drafts
        ```

    === "Windows"
        ```powershell
        $ mkdir docs\blog\posts\drafts
        ```

    现在，在这个文件夹中，创建一个文件`.meta.yml`，其中包含：

    ```yaml
    draft: true
    ```

    添加另一篇博客文章并将其存储在“docs/blog/posts/drafts”中。当你
    在本地查看，您将看到将其标识为草稿的标签，
    而在为发布而构建的版本中，它不会出现。要移动a
    从草稿状态发布到已发布，只需将其移出“草稿/”。

[meta]: ../../plugins/meta.md
[Insiders Edition]: ../../insiders/index.md

## 接下来是什么？

你现在应该有一个工作博客。然而，随着内容的积累，你
可能想确保人们能找到他们感兴趣的帖子，所以
您可能希望添加带有标签和类别的辅助导航。你可以
拥有多个作者，并希望将帖子也归因于他们
为他们生成作者页面。我们有一个关于导航、分页、，
以及涵盖这些主题的作者。

[tutorial on navigation, pagination, and authors]: navigation.md

你可能想通过允许人们
订阅RSS提要或设置评论系统。[约定
《传播教程》将引导您完成这些设置。

[engagement and dissemination tutorial]: engage.md

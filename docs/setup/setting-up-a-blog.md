# 建立博客

MkDocs的材料使构建博客变得非常容易，无论是作为sidecar还是
您的文档或独立文件。在引擎运行时专注于你的内容
所有繁重的工作，自动生成[档案]和[类别]
索引、[post-slugs]、可配置[分页]等。

---

__查看我们的[blog]，它是用新的[内置博客插件]创建的！__

  [archive]: ../plugins/blog.md#archive
  [category]: ../plugins/blog.md#categories
  [post slugs]: ../plugins/blog.md#config.post_url_format
  [pagination]: ../plugins/blog.md#pagination
  [blog]: ../blog/index.md

## 配置

### 内置博客插件

`version 9.2.0`
`plugin`
`flag experimental`
`demo create-blog`

内置的博客插件增加了从以下文件夹构建博客的支持
帖子，用日期和其他结构化数据注释。首先，添加
将以下行转换为`mkdocs.yml`：

``` yaml
plugins:
  - blog
```

如果你的`mkdocs.yml`中没有导航（`nav`）定义，那么
由于博客插件将添加导航，因此没有其他事情可做
自动。如果您确实定义了导航，则需要添加*
博客索引页面仅为*。您不需要也不应该添加个人
博客文章。例如：

```yaml
nav:
  - index.md
  - Blog:
    - blog/index.md
```

有关所有设置的列表，请参阅[插件文档]。

  [plugin documentation]: ../plugins/blog.md

#### 高级设置

`sponsors`
`version insiders-4.44.0`

以下高级设置目前保留给我们的[赞助商]
[内部人士]。它们完全是可选的，不会影响
博客，但可能有助于自定义：

- [`archive_pagination`][config.archive_pagination]
- [`archive_pagination_per_page`][config.archive_pagination_per_page]
- [`categories_sort_by`][config.categories_sort_by]
- [`categories_sort_reverse`][config.categories_sort_reverse]
- [`categories_pagination`][config.categories_pagination]
- [`categories_pagination_per_page`][config.categories_pagination_per_page]
- [`authors_profiles_pagination`][config.authors_profiles_pagination]
- [`authors_profiles_pagination_per_page`][config.authors_profiles_pagination_per_page]

随着我们发现新的用例，我们将在此处添加更多设置。

  [Insiders]: ../insiders/index.md
  [built-in blog plugin]: ../plugins/blog.md
  [built-in plugins]: ../insiders/getting-started.md#built-in-plugins
  [start writing your first post]: #writing-your-first-post

  [config.archive_pagination]: ../plugins/blog.md#config.archive_pagination
  [config.archive_pagination_per_page]: ../plugins/blog.md#config.archive_pagination_per_page
  [config.categories_sort_by]: ../plugins/blog.md#config.categories_sort_by
  [config.categories_sort_reverse]: ../plugins/blog.md#config.categories_sort_reverse
  [config.categories_pagination]: ../plugins/blog.md#config.categories_pagination
  [config.categories_pagination_per_page]: ../plugins/blog.md#config.categories_pagination_per_page
  [config.authors_profiles_pagination]: ../plugins/blog.md#config.authors_profiles_pagination
  [config.authors_profiles_pagination_per_page]: ../plugins/blog.md#config.authors_profiles_pagination_per_page

### RSS

`version 9.2.0`
`plugin [rss]`

[内置博客插件]与[RSS插件][RSS]无缝集成，
它提供了一种简单的方法，可以将RSS提要添加到您的博客（或整个博客）中
文件）。使用`pip `进行安装：

```
pip install mkdocs-rss-plugin
```

然后，在`mkdocs.yml`中添加以下行：

``` yaml
plugins:
  - rss:
      match_path: blog/posts/.* # (1)!
      date_from_meta:
        as_creation: date
      categories:
        - categories
        - tags # (2)!
```

1.  RSS插件允许过滤提要中包含的URL。在……里面
    在这个例子中，只有博客文章才会成为提要的一部分。

2.  如果你想在提要中包含帖子的类别及其标签，
    在此处添加“类别”和“标签”。

支持以下配置选项：

`option rss.enabled`

:   `default _true_` 此选项指定是否
    在构建项目时启用该插件。如果你想加快速度
    在本地构建中，您可以使用[环境变量][mkdocs.env]：

    ``` yaml
    plugins:
      - rss:
          enabled: !ENV [CI, false]
    ```

`option rss.match_path`

:   `default _.*_` 此选项指定了
    页面应该包含在提要中。例如，只包括博客
    在提要中的帖子中，使用以下正则表达式：

    ``` yaml
    plugins:
      - rss:
          match_path: blog/posts/.*
    ```

`option rss.date_from_meta`

:   `default none` 此选项指定了
    front matter属性应用作页面的创建日期
    饲料。建议使用`date`属性：

    ``` yaml
    plugins:
      - rss:
          date_from_meta:
            as_creation: date
    ```

`option rss.categories`

:   `default none` 此选项指定了
    前体属性作为提要的一部分用作类别。如果你
    使用[categories]和[tags]，用以下行添加它们：

    ``` yaml
    plugins:
      - rss:
          categories:
            - categories
            - tags
    ```

`option rss.comments_path`

:   `default none` 此选项指定锚点
    在那里可以找到帖子或页面的评论。如果你已经整合了
    [评论系统]，添加以下行：

    ``` yaml
    plugins:
      - rss:
          comments_path: "#__comments"
    ```

MkDocs的材料将自动向您的网站添加[必要的元数据]
这将使RSS提要可被浏览器和提要阅读器发现。

此扩展的其他配置选项不受官方支持
MkDocs的材料，这就是为什么它们可能会产生意想不到的结果。使用它们
自行承担风险。

  [rss]: https://guts.github.io/mkdocs-rss-plugin/
  [categories]: ../plugins/blog.md#categories
  [tags]: setting-up-tags.md#built-in-tags-plugin
  [comment system]: adding-a-comment-system.md
  [necessary metadata]: https://guts.github.io/mkdocs-rss-plugin/configuration/#integration
  [theme extension]: ../customization.md

### 仅博客

你可能需要构建一个没有任何文档的纯博客。
在这种情况下，您可以创建这样的文件夹树：

``` { .sh .no-copy }
.
├─ docs/
│  ├─ posts/ # (1)!
│  ├─ .authors.yml
│  └─ index.md
└─ mkdocs.yml
```

1.  请注意，`posts`目录位于`docs`的根目录中，没有
    中间的“博客”目录。

并将以下行添加到`mkdocs.yml`中：

``` yaml
plugins:
  - blog:
      blog_dir: . # (1)!
```

1.  有关插件的更多信息，请参阅[插件文档]
    [blog_dir][blog_dir]设置。

采用此配置，博客文章的url将为“/<post_slug>”`
而不是“/blog/<post_slug>”。

## 使用

### 写你的第一篇文章

成功设置[内置博客插件]后，是时候写了
你的第一篇帖子。该插件不采用任何特定的目录结构，因此
你完全可以自由地组织你的帖子，只要它们都是
位于“posts”目录内：

``` { .sh .no-copy }
.
├─ docs/
│  └─ blog/
│     ├─ posts/
│     │  └─ hello-world.md # (1)!
│     └─ index.md
└─ mkdocs.yml
```

1.  如果你想以不同的方式安排帖子，你可以自由地这样做。网址
    根据[post_url_format][post-slugs]中指定的格式构建，以及
    帖子的标题和日期，无论它们是如何组织的
    在“posts”目录中。

创建一个名为“hello world.md”的新文件，并添加以下行：

``` yaml
---
draft: true # (1)!
date: 2024-01-31 # (2)!
categories:
  - Hello
  - World
---

# Hello world!
...
```

1.  如果将帖子标记为[草稿]，则帖子日期旁边会出现一个红色标记
    在索引页上。网站建成后，草稿不包括在
    输出。[此行为可以更改]，例如在以下情况下渲染草稿
    构建部署预览。

2.  如果您希望提供多个日期，可以使用以下语法：，
    允许您定义上次更新博客文章的日期+
    您可以在模板中添加更多自定义日期：

    ``` yaml
    ---
    date:
      created: 2022-01-31
      updated: 2022-02-02
    ---

    # Hello world!
    ```

    请注意，创建日期必须设置在“date.created”下，因为每个
    博客文章必须设置创建日期。

当你启动[实时预览服务器]时，你应该会收到第一个
帖子！你也会意识到，[归档]和[类别]索引已经
自动为您生成。

  [draft]: ../plugins/blog.md#drafts
  [This behavior can be changed]: ../plugins/blog.md#config.draft
  [live preview server]: ../creating-your-site.md#previewing-as-you-write

#### 添加摘录

博客索引以及[存档]和[类别]索引可以列出
每个帖子的全部内容或帖子的摘录。摘录可以通过以下方式创建
添加一个`<！--more-->`分隔符位于帖子的前几段之后：

``` py
# Hello world!

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
massa, nec semper lorem quam in massa.

<!-- more -->
...
```

当[内置博客插件]生成所有索引时
[摘录分隔符]会自动提取，允许用户开始
在决定加入之前先阅读一篇帖子。

  [excerpt separator]: ../plugins/blog.md#config.post_excerpt_separator

#### 添加作者

为了给你的帖子增添更多个性，你可以将每个帖子关联起来
与一个或多个[作者]一起发布。首先，创建
在您的博客目录中添加一个[`.orges.yml`][authors_file]文件，并添加一个作者：

``` yaml
authors:
  squidfunk:
    name: Martin Donath
    description: Creator
    avatar: https://github.com/squidfunk.png
```

[`.orges.yml`][authors_file]文件将每个作者与一个
标识符（在本例中为“squidfunk”），然后可以在帖子中使用。
可以配置不同的属性。对于所有可能属性的列表，
请查阅[`authors_file][authors_file]文档。

现在，您可以通过引用一个或多个作者的文章来为其分配作者
Markdown文件前面“authors”下的标识符`
财产。对于每位作者，在左侧边栏中都会呈现一个小简介
每篇帖子，以及索引页面上的帖子摘录：

``` yaml
---
date: 2024-01-31
authors:
  - squidfunk
    ...
---

# Hello world!
...
```

  [authors]: ../plugins/blog.md#authors
  [authors_file]: ../plugins/blog.md#config.authors_file

#### 添加作者资料

`sponsors`
`version insiders-4.46.0`
`flag experimental`

如果你想为每个作者添加一个专用页面，你可以启用作者
通过设置[`authors_profiles][authors_profiles]配置来配置配置文件
选择“true”。只需在`mkdocs.yml`中添加以下行：

``` yaml
plugins:
  - blog:
      authors_profiles: true
```

如果将其与[自定义索引页]结合使用，则可以创建一个专用页面
为每位作者提供简短描述、社交媒体链接等。-基本上
任何你可以用Markdown写的东西。帖子列表随后附加在
页面的内容。

  [authors_profiles]: ../plugins/blog.md#config.authors_profiles
  [custom index pages]: #custom-index-pages

#### 添加类别

分类是按主题对帖子进行分组的好方法
专用索引页。这样，对特定主题感兴趣的用户可以
探索你关于这个话题的所有帖子。确保启用了[类别]
将它们添加到前面的“类别”属性中：

``` yaml
---
date: 2024-01-31
categories:
  - Hello
  - World
---

# Hello world!
...
```

如果你想在输入类别时避免拼写错误，你可以
在`mkdocs.yml`中定义所需的类别，作为
[`categories_allowed][categories_alowed]配置选项。这个
如果在[内置博客插件]中找不到类别，则将停止构建
名单。

  [categories_allowed]: ../plugins/blog.md#config.categories_allowed

#### 添加标签

除了[类别]，[内置博客插件]还与
[内置标签插件]。如果你在前面的`tags`属性中添加标签
作为帖子的一部分，帖子从[tags索引]链接：

``` yaml
---
date: 2024-01-31
tags:
  - Foo
  - Bar
---

# Hello world!
...
```

像往常一样，标签显示在主标题上方，帖子被链接
在标签索引页面上（如果已配置）。请注意，帖子仅作为页面
与他们的头衔相关联。

  [built-in tags plugin]: ../plugins/tags.md
  [tags index]: setting-up-tags.md#adding-a-tags-index

#### 更换蛞蝓

slug是URL中使用的帖子的简短描述。它们是自动生成的，但您可以为页面指定自定义slug：

``` yaml
---
slug: hello-world
---

# Hello there world!
...
```

#### 添加相关链接

`version 9.6.0`
`flag experimental`

相关链接提供了突出添加更多阅读内容的完美方式_
左侧边栏中包含的帖子部分，指导用户
文档的其他目的地。使用front matter的“links”属性
为帖子添加相关链接：

``` yaml
---
date: 2024-01-31
links:
  - plugins/search.md
  - insiders/how-to-sponsor.md
---

# Hello world!
...
```

您可以使用与中[`nav`][mkdocs.nav]部分完全相同的语法
`mkdocs.yml`，这意味着您可以为链接设置明确的标题，添加外部
链接，甚至使用嵌套：

``` yaml
---
date: 2024-01-31
links:
  - plugins/search.md
  - insiders/how-to-sponsor.md
  - Nested section:
    - External link: https://example.com
    - setup/setting-up-site-search.md
---

# Hello world!
...
```

如果你仔细观察，你会发现你甚至可以使用锚点链接到
文档的特定部分，扩展了
`mkdocs.yml`中的[`nav`][mkdocs.nav]语法。[内置博客插件]解析
并将锚点的标题设置为相关链接的[字幕]。

请注意，所有链接都必须与[`docs_dir`][mkdocs.docs_dir]相关，如下所示
[nav][mkdocs.nav]设置也是如此。

  [subtitle]: ../reference/index.md#setting-the-page-subtitle

#### 链接到帖子

虽然[post URL][post slugs]是动态计算的，但[内置博客
plugin]确保所有帖子和帖子资产之间的链接
对的。如果你想链接到一篇帖子，只需使用Markdown文件的路径
作为链接引用（链接必须是相对的）：

``` markdown
[Hello World!](blog/posts/hello-world.md)
```

从帖子链接到页面，例如索引，遵循相同的方法：

``` markdown
[Blog](../index.md)
```

“posts”目录中的所有资产都被复制到“blog/assets”文件夹中
当网站正在建设时。当然，您还可以参考以下资产
“posts”目录之外的帖子。[内置博客插件]确保
所有链接都是正确的。

#### 固定帖子

`sponsors`
`version insiders-4.53.0`
`flag experimental`

如果你想把一篇文章固定在索引页的顶部，以及存档
以及它所属的类别索引，您可以使用front matter的`pin`属性：

``` yaml
---
date: 2024-01-31
pin: true
---

# Hello world!
...
```

如果固定了多个帖子，则按其创建日期进行排序
首先显示最新的固定帖子，然后显示其他固定帖子
降序。

#### 设置阅读时间

当[启用]时，计算每个帖子的预期阅读时间，
其被呈现为帖子和帖子摘录的一部分。如今，许多博客
显示阅读时间，这就是[内置博客插件]提供此功能的原因
能力也是。

然而，有时计算出的阅读时间可能感觉不准确，或者
导致奇数和令人不快的数字。因此，阅读时间可以
重写并显式设置a的front matter“readtime”属性
职位：

``` yaml
---
date: 2024-01-31
readtime: 15
---

# Hello world!
...
```

这将禁用自动读取时间计算。

!!! warning "汉字、日文和韩文"

    阅读时间计算目前不采用中文分词，
    考虑到日文和韩文字符。这意味着阅读
    用这些语言发帖的时间可能不准确。我们正在计划
    在未来增加支持。与此同时，请使用“阅读时间”`
    front matter属性用于设置读取时间。

  [enabled]: ../plugins/blog.md#config.post_readtime

#### 设置默认值

`version 9.6.0`
`plugin [meta][built-in meta plugin] – built-in`
`flag experimental`

如果你有很多帖子，那么定义上述所有内容可能会觉得多余
对于每个帖子。幸运的是，[内置元插件]允许设置默认前端
每个文件夹的内容属性。您可以按类别对帖子进行分组，或
authors，并添加一个`.meta.yml`文件来设置公共属性：

``` { .sh .no-copy }
.
├─ docs/
│  └─ blog/
│     ├─ posts/
│     ├─ .meta.yml # (1)!
│     └─ index.md
└─ mkdocs.yml
```

1.  如前所述，您还可以将`.meta.yml`文件放置在嵌套文件夹中
    在“posts”目录中。然后，此文件可以定义所有前沿内容
    在帖子中有效的属性，例如：

    ``` yaml
    authors:
      - squidfunk
    categories:
      - Hello
      - World
    ```

请注意，顺序很重要——必须在
mkdocs.yml中的blog插件，以便正确获取所有设置的默认值
通过[内置博客插件]：

``` yaml
plugins:
  - meta
  - blog
```

“.meta.yml”文件中的列表和字典将与
为帖子定义的值，这意味着您可以在
`.meta.yml，然后为每个帖子添加特定的属性或覆盖。

  [built-in meta plugin]: ../plugins/meta.md

### 添加页面

除了帖子，还可以通过以下方式在博客中添加静态页面
mkdocs.yml的[nav][mkdocs.nav]部分中的页面。全部生成
索引包含在最后一个指定页面之后。例如，添加页面
在博客的作者中，将以下内容添加到`mkdocs.yml`中：

``` yaml
nav:
  - Blog:
    - blog/index.md
    - blog/authors.md
      ...
```

## 自定义

### 自定义索引页

`version 9.6.0`
`flag experimental`

如果您想将自定义内容添加到自动生成的[存档]和
[类别]索引，例如在列表之前添加类别描述
帖子，您可以在同一位置手动创建类别页面
[内置博客插件]将创建它：

``` { .sh .no-copy }
.
├─ docs/
│  └─ blog/
│     ├─ category/
│     │  └─ hello.md # (1)!
│     ├─ posts/
│     └─ index.md
└─ mkdocs.yml
```

1.  最简单的方法是首先[添加类别]到博客文章中，然后采取
    由[内置博客插件]生成的URL，并在
    [blog_dir][blog_dir]文件夹中的相应位置。

    请注意，所示的目录列表基于默认配置。
    如果为以下选项指定了不同的值，请务必进行调整
    相应地，路径：

    - [`blog_dir`][blog_dir]
    - [`categories_url_format`][categories_url_format]
    - [`categories_slugify`][categories_slugify]

现在，您可以将任意内容添加到新创建的文件中，或设置特定的
此页面的首页属性，例如更改[页面描述]：

``` yaml
---
description: Nullam urna elit, malesuada eget finibus ut, ac tortor.
---

# Hello
...
```

属于该类别的所有帖子摘录都会自动附加。

  [add the category]: #adding-categories
  [page description]: ../reference/index.md#setting-the-page-description
  [categories_url_format]: ../plugins/blog.md#config.categories_url_format
  [categories_slugify]: ../plugins/blog.md#config.categories_slugify
  [blog_dir]: ../plugins/blog.md#config.blog_dir

### 覆盖模板

[内置博客插件]是在与MkDocs的Material相同的基础上构建的，
这意味着您可以使用以下命令覆盖博客使用的所有模板
[主题扩展]像往常一样。

[内置博客插件]添加了以下模板：

- [`blog.html`][blog.html] – Template for blog, archive and category index
- [`blog-post.html`][blog-post.html] – Template for blog post

  [theme extension]: ../customization.md#extending-the-theme

  [blog.html]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/blog.html
  [blog-post.html]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/blog-post.html

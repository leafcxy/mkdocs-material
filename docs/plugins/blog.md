---
title: 内置博客插件
icon: material/newspaper-variant-outline
---

# 内置博客插件

博客插件使构建博客变得非常容易，无论是作为sidecar还是
您的文档或作为主要内容。在插件运行期间，专注于您的内容
完成所有繁重的工作，生成所有最新帖子的视图，[存档]和
[类别]页面，可配置[分页]等等。

  [archive]: #archive
  [category]: #categories
  [pagination]: #pagination

## 客观的

### 工作原理

该插件扫描已配置的[“posts”目录][config.post_dir]以查找
`.md文件，从中自动生成分页视图[^1]。如果没有
否则，插件会要求您的项目具有以下内容
目录布局，并将为您创建任何缺失的目录或文件：

  [^1]:
    视图是自动生成的页面，即
    您的博客列出了所有最新帖子，以及[存档]和[类别]
    通过[元数据]列出与其关联的所有帖子的页面
    时间顺序。

``` { .sh .no-copy }
.
├─ docs/
│  └─ blog/
│     ├─ posts/
│     └─ index.md
└─ mkdocs.yml
```

[`blog`目录][config.blog_dir]中的`index.md`文件是条目
指向你的博客——一个按时间倒序列出所有帖子的分页视图
订单。除此之外，该插件还支持自动创建[存档]和
[category]页面列出了某个时间间隔或类别的帖子子集。

[Post url][config.Post_url_format]是完全可配置的，无论是否
您是否希望您的URL包含帖子的日期。始终呈现日期
以项目的[站点语言]的区域设置显示。就像在其他
静态博客框架、帖子可以用各种[元数据]进行注释，
允许与其他[内置插件]轻松集成，例如
[社交]和[标签]插件。

帖子可以组织在嵌套文件夹中，目录布局适合您的
根据特定需求，可以使用该材料的所有组件和语法
MkDocs提供，包括[警告]、[注释]、[代码块]，
[内容选项卡]、[图表]、[图标]、[数学]等。

  [metadata]: #metadata
  [built-in plugins]: index.md
  [social]: social.md
  [tags]: tags.md
  [admonitions]: ../reference/admonitions.md
  [annotations]: ../reference/annotations.md
  [code blocks]: ../reference/code-blocks.md
  [content tabs]: ../reference/content-tabs.md
  [diagrams]: ../reference/diagrams.md
  [icons]: ../reference/icons-emojis.md
  [math]: ../reference/math.md

### 何时使用

如果你想在项目中添加一个博客，或者从另一个博客迁移
MkDocs的Material框架，因为它具有出色的技术写作能力
功能，这个插件是一个不错的选择，因为它与
许多其他内置插件：

<div class="grid cards" markdown>

-   :material-file-tree: &nbsp; __[Built-in meta plugin][meta]__

    ---

    元插件使将[元数据]应用于帖子子集变得容易，
    包括作者、标签、类别、草稿状态以及社交卡
    布局。

    ---

    __Simpler organization, categorization and management of post metadata__

-   :material-share-circle: &nbsp; __[Built-in social plugin][social]__

    ---

    社交插件会自动生成美观且可定制的内容
    每个帖子和页面的社交卡片，在社交媒体上作为预览显示。

    ---

    __Links to your blog render beautiful social cards when shared on social
    media__

-   :material-rabbit: &nbsp; __[Built-in optimize plugin][optimize]__

    ---

    优化插件自动识别并优化所有媒体文件
    通过使用压缩和转换在项目中引用
    技术。

    ---

    __Your blog loads faster as smaller images are served to your users__

-   :material-tag-text: &nbsp; __[Built-in tags plugin][tags]__

    ---

    标签插件允许将帖子与页面一起分类
    项目，以提高其可发现性，并将帖子连接到您的
    文档。

    ---

    __Your documentation's tag system integrates with your blog__

</div>

  [meta]: meta.md
  [social]: social.md
  [optimize]: optimize.md
  [tags]: tags.md

## 配置

`version 9.2.0`
`plugin [blog] – built-in`
`flag multiple`
`flag experimental`

与所有[内置插件]一样，开始使用博客插件是
直截了当。只需将以下行添加到`mkdocs.yml`中，您就可以
开始写你的第一篇文章：

``` yaml
plugins:
  - blog
```

博客插件内置于MkDocs的Material中，不需要
安装。

  [blog]: blog.md
  [built-in plugins]: index.md

### 导航

如果您的`mkdocs.yml`中没有配置站点导航，那么有
无需更多操作。博客[存档]和[类别]页面将自动
显示在自动生成的导航下方。

如果您确实定义了导航结构，则需要指定
博客应该出现在哪里。创建一个带有索引的导航部分
博客的页面]：

```yaml
theme:
  name: material
  features:
    - navigation.indexes
nav:
  - ...
  - Blog:
    - blog/index.md
```

[存档]和[类别]页面将显示在该部分中
博客部分页面下方的子部分。在这种情况下，他们会出现
在`index.md`之后。“index.md”文件的路径必须匹配
[blog_dir][config.blog_dir]。这意味着您可以命名博客导航
输入任何你喜欢的东西：“博客”或“新闻”，或者“提示”。

[navigation section with an index page]: ../setup/setting-up-navigation.md#section-index-pages

### 一般的

以下设置可用：

---

#### `setting config.enabled`

`version 9.2.0`
`default _true_`

使用此设置可在[构建项目]时启用或禁用插件。
通常不需要指定此设置，但如果要禁用
插件，使用：

``` yaml
plugins:
  - blog:
      enabled: false
```

  [building your project]: ../creating-your-site.md#building-your-site

---

#### `setting config.blog_dir`

`version 9.2.0`
`md:default _blog_`

使用此设置更改您的博客在
[文档目录][mkdocs.docs_dir]。路径包含在生成的
URL作为所有帖子和视图的前缀。您可以通过以下方式进行更改：

=== "Documentation + Blog"

    ``` yaml
    plugins:
      - blog:
          blog_dir: blog
    ```

=== "Blog only"

    ``` yaml
    plugins:
      - blog:
          blog_dir: .
    ```

提供的路径是从[`docs`目录][mkdocs.docs_dir]解析的。

---

#### <!-- md:setting config.blog_toc -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

使用此设置可利用目录在中显示帖子标题
意见。如果你的帖子摘录很长，这可能会很有用。如果你想要我
要启用它，请使用：

``` yaml
plugins:
  - blog:
      blog_toc: true
```

### 贴子

以下设置可用于帖子：

---

#### <!-- md:setting config.post_dir -->

<!-- md:version 9.2.0 -->
<!-- md:default `{blog}/posts` -->

使用此设置更改帖子所在的文件夹。它是
通常不需要更改此设置，但如果要重命名
文件夹或更改其文件系统位置，使用：

``` yaml
plugins:
  - blog:
      post_dir: "{blog}/articles"
```

请注意，[`posts`目录][config.post_dir]仅用于post
组织-它不包含在帖子URL中，因为它们是自动的
并且由该插件轻松生成。

以下占位符可用：

- `blog` – [`blog` directory][config.blog_dir]

提供的路径是从[`docs`目录][mkdocs.docs_dir]解析的。

---

#### <!-- md:setting config.post_date_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `long` -->

使用此设置可更改帖子的日期格式。此插件使用[babel]
以配置的[站点语言]呈现日期。你可以用babel
[模式语法]或以下简码：

=== "Monday, January 31, 2024"

    ``` yaml
    plugins:
      - blog:
          post_date_format: full
    ```

=== "January 31, 2024"

    ``` yaml
    plugins:
      - blog:
          post_date_format: long
    ```

=== "Jan 31, 2024"

    ``` yaml
    plugins:
      - blog:
          post_date_format: medium
    ```

=== "1/31/24"

    ``` yaml
    plugins:
      - blog:
          post_date_format: short
    ```

请注意，根据[网站语言]的不同，结果可能会有所不同
其他语言。

  [babel]: https://pypi.org/project/Babel/
  [site language]: ../setup/changing-the-language.md#site-language
  [pattern syntax]: https://babel.pocoo.org/en/latest/dates.html#pattern-syntax

---

#### <!-- md:setting config.post_url_date_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `yyyy/MM/dd` -->

使用此设置可更改帖子URL中使用的日期格式。格式字符串
必须遵循[babel]的[pattern语法]，并且不应包含空格。
一些流行的选择：

=== ":material-link: blog/2024/01/31/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          post_url_date_format: yyyy/MM/dd
    ```

=== ":material-link: blog/2024/01/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          post_url_date_format: yyyy/MM
    ```

=== ":material-link: blog/2024/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          post_url_date_format: yyyy
    ```

如果你想从帖子URL中删除日期，例如，当你的博客功能
主要是常青内容，您可以从
[`post_url_format`][config.post_url_fformat]格式字符串。

---

#### <!-- md:setting config.post_url_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `{date}/{slug}` -->

使用此设置更改生成帖子时使用的格式字符串
URL。您可以自由组合占位符，并用斜线或其他符号将其连接起来
字符：

=== ":material-link: blog/2024/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          post_url_format: "{date}/{slug}"
    ```

=== ":material-link: blog/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          post_url_format: "{slug}"
    ```

以下占位符可用：

- `categories` – Post categories, slugified with [`categories_slugify`][config.categories_slugify]
- `date` – Post date, formatted with [`post_url_date_format`][config.post_url_date_format]
- `slug` – Post title, slugified with [`post_slugify`][config.post_slugify], or explicitly set via [`slug`][meta.slug] metadata property
- `file` – Post filename without `.md` file extension

如果删除“日期”占位符，请确保帖子URL不会冲突
其中其他页面的URL托管在[“blog”目录][config.blog_dir]下，
因为这会导致未定义的行为。

---

#### <!-- md:setting config.post_url_max_categories -->

<!-- md:version 9.2.0 -->
<!-- md:default `1` -->

使用此设置为中包含的类别数量设置上限
如果“类别”占位符是[“post_url_format”]的一部分，则发布url
[config.post_url_format]，帖子定义了类别：

``` yaml
plugins:
  - blog:
      post_url_format: "{categories}/{slug}"
      post_url_max_categories: 2
```

如果给出了多个类别，则在行贿后用“/”连接。

---

#### <!-- md:setting config.post_slugify -->

<!-- md:version 9.2.0 -->
<!-- md:default [`pymdownx.slugs.slugify`][pymdownx.slugs.slugify] -->

使用此设置更改生成与URL兼容的slug的功能
从帖子标题。默认情况下，['slugify][pymdownx.slugs.slugify]函数
[Python Markdown扩展]的用法如下：

``` yaml
plugins:
  - blog:
      post_slugify: !!python/object/apply:pymdownx.slugs.slugify
        kwds:
          case: lower
```

默认配置支持Unicode，应该能为所有人生成良好的slug
语言。当然，您还可以为以下对象提供自定义的slugif功能
更精细的控制。

  [pymdownx.slugs.slugify]: https://github.com/facelessuser/pymdown-extensions/blob/01c91ce79c91304c22b4e3d7a9261accc931d707/pymdownx/slugs.py#L59-L65
  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/extras/slugs/

---

#### <!-- md:setting config.post_slugify_separator -->

<!-- md:version 9.2.0 -->
<!-- md:default `-` -->

使用此设置更改传递给slugif的分隔符
函数集为[`post_slugify`]的一部分[config.post_slugify]。虽然默认
是连字符，可以设置为任何字符串，例如“_”：

``` yaml
plugins:
  - blog:
      post_slugify_separator: _
```

---

#### <!-- md:setting config.post_excerpt -->

<!-- md:version 9.2.0 -->
<!-- md:default `optional` -->

默认情况下，插件会制作[帖子摘录]（../setup/setup-a-blog.md#添加摘录）
可选。当一篇帖子没有定义摘录时，视图包括整个帖子。
此设置可用于制作所需的帖子摘录：

=== "Optional"

    ``` yaml
    plugins:
      - blog:
          post_excerpt: optional
    ```

=== "Required"

    ``` yaml
    plugins:
      - blog:
          post_excerpt: required
    ```

当需要帖子摘录时，没有摘录分隔符的帖子会引发
错误。因此，当您想确保所有帖子
已定义摘录。

---

#### <!-- md:setting config.post_excerpt_max_authors -->

<!-- md:version 9.2.0 -->
<!-- md:default `1` -->

使用此设置为中呈现的作者数量设置上限
发布摘录。虽然每篇文章可能由多位作者撰写，但这种设置
允许将显示限制为少数甚至单个作者，或禁用
文章摘录中的作者：

=== "Render up to 2 authors"

    ``` yaml
    plugins:
      - blog:
          post_excerpt_max_authors: 2
    ```

=== "Disable authors"

    ``` yaml
    plugins:
      - blog:
          post_excerpt_max_authors: 0
    ```

这仅适用于观点中的帖子摘录。帖子总是呈现所有作者。

---

#### <!-- md:setting config.post_excerpt_max_categories -->

<!-- md:version 9.2.0 -->
<!-- md:default `5` -->

使用此设置为中呈现的类别数量设置上限
发布摘录。虽然每个帖子可能被分配到多个类别，但这
设置允许将显示限制为几个甚至单个类别，或
禁用帖子摘录中的类别：

=== "Render up to 2 categories"

    ``` yaml
    plugins:
      - blog:
          post_excerpt_max_categories: 2
    ```

=== "Disable categories"

    ``` yaml
    plugins:
      - blog:
          post_excerpt_max_categories: 0
    ```

这仅适用于观点中的帖子摘录。帖子总是呈现所有类别。

---

#### <!-- md:setting config.post_excerpt_separator -->

<!-- md:version 9.2.0 -->
<!-- md:default <code>&lt;!-- more --&gt;</code> -->

使用此设置设置插件将在帖子中查找的分隔符
生成帖子摘录时的内容。所有内容__before _分隔符为
被认为是摘录的一部分：

``` yaml
plugins:
  - blog:
      post_excerpt_separator: <!-- more -->
```

通常的做法是使用HTML注释作为分隔符。

---

#### <!-- md:setting config.post_readtime -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否应自动计算
帖子的阅读时间，然后以帖子摘录的形式呈现，以及
发布自己：

``` yaml
plugins:
  - blog:
      post_readtime: false
```

!!! warning "汉字、日文和韩文"

    阅读时间计算目前不采用中文分词，
    考虑到日文和韩文字符。这意味着阅读
    用这些语言发帖的时间可能不准确。我们正在计划
    在未来增加支持。与此同时，请使用“阅读时间”`
    front matter属性用于设置读取时间。

---

#### <!-- md:setting config.post_readtime_words_per_minute -->

<!-- md:version 9.2.0 -->
<!-- md:default `265` -->

使用此设置更改读者应阅读的字数
在计算帖子的阅读时间时，每分钟。如果你想微调
它，使用：

``` yaml
plugins:
  - blog:
      post_readtime_words_per_minute: 300
```

每分钟265个单词的阅读时间被认为是
[成年人的平均阅读时间]。

  [average reading time of an adult]: https://help.medium.com/hc/en-us/articles/214991667-Read-time

### 档案

以下设置可用于存档页面：

---

#### <!-- md:setting config.archive -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用存档页面。存档页面显示所有
按相反顺序发布特定时间间隔（例如年、月等）的帖子。如果你
要禁用存档页面，请使用：

``` yaml
plugins:
  - blog:
      archive: false
```

---

#### <!-- md:setting config.archive_name -->

<!-- md:version 9.2.0 -->
<!-- md:default computed -->

使用此设置更改插件添加到的存档部分的标题
导航。如果省略此设置，则其来源于翻译。
如果你想更改它，请使用：

``` yaml
plugins:
  - blog:
      archive_name: Archive
```

---

#### <!-- md:setting config.archive_date_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `yyyy` -->

使用此设置可更改用于存档页面标题的日期格式。这个
格式字符串必须遵循[babel]的[模式语法]。一些流行的选择：

=== "2024"

    ``` yaml
    plugins:
      - blog:
          archive_date_format: yyyy
    ```

=== "January 2024"

    ``` yaml
    plugins:
      - blog:
          archive_date_format: MMMM yyyy
    ```

请注意，根据[网站语言]的不同，结果可能会有所不同
其他语言。

---

#### <!-- md:setting config.archive_url_date_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `yyyy` -->

使用此设置可更改用于存档页面URL的日期格式
格式字符串必须遵循[babel]的[pattern语法]，并且不应包含
空白。一些流行的选择：

=== ":material-link: blog/archive/2024/"

    ``` yaml
    plugins:
      - blog:
          archive_url_date_format: yyyy
    ```

=== ":material-link: blog/archive/2024/01/"

    ``` yaml
    plugins:
      - blog:
          archive_url_date_format: yyyy/MM
    ```

---

#### <!-- md:setting config.archive_url_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `archive/{date}` -->

使用此设置更改生成时使用的格式字符串
存档页面URL。您可以自由组合占位符，并将其与
斜线或其他字符：

=== ":material-link: blog/archive/2024/"

    ``` yaml
    plugins:
      - blog:
          archive_url_format: "archive/{date}"
    ```

=== ":material-link: blog/2024/"

    ``` yaml
    plugins:
      - blog:
          archive_url_format: "{date}"
    ```

以下占位符可用：

- `date` – Archive date, formatted with [`archive_url_date_format`][config.archive_url_date_format]

---

#### <!-- md:setting config.archive_pagination -->

<!-- md:sponsors -->
<!-- md:version insiders-4.44.0 -->
<!-- md:default `true` -->

使用此设置可启用或禁用存档页面的分页。价值
此设置的值继承自[`pagination][config.pagination]，除非它是
明确设置。要禁用分页，请使用：

``` yaml
plugins:
  - blog:
      archive_pagination: false
```

---

#### <!-- md:setting config.archive_pagination_per_page -->

<!-- md:sponsors -->
<!-- md:version insiders-4.44.0 -->
<!-- md:default `10` -->

使用此设置可更改每个存档页面呈现的帖子数量。这个
此设置的值继承自[“pagination_per_page”]
[config.pagion_per_page]，除非明确设置。要更改它，请使用：

``` yaml
plugins:
  - blog:
      archive_pagination_per_page: 5
```

---

#### <!-- md:setting config.archive_toc -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

使用此设置可利用目录显示所有帖子的标题
存档页面。此设置的值继承自[`blog_toc`]
[config.blog_toc]，除非明确设置。要更改它，请使用

``` yaml
plugins:
  - blog:
      archive_toc: true
```

### 类别

以下设置可用于类别页面：

---

#### <!-- md:setting config.categories -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用类别页面。类别页面显示所有
按时间倒序排列特定类别的帖子。如果你想
禁用类别页面，使用：

``` yaml
plugins:
  - blog:
      categories: false
```

---

#### <!-- md:setting config.categories_name -->

<!-- md:version 9.2.0 -->
<!-- md:default computed -->

使用此设置更改插件添加到的类别部分的标题
导航。如果省略此设置，则其来源于翻译。
如果你想更改它，请使用：

``` yaml
plugins:
  - blog:
      categories_name: Categories
```

---

#### <!-- md:setting config.categories_url_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `category/{slug}` -->

使用此设置更改生成时使用的格式字符串
类别页面URL。您可以自由组合占位符，并将其与
斜线或其他字符：

=== ":material-link: blog/category/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          categories_url_format: "category/{slug}"
    ```

=== ":material-link: blog/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          categories_url_format: "{slug}"
    ```

以下占位符可用：

- `slug `–类别，用[`categories_slugify`][config.categories_shugify]分隔

---

#### <!-- md:setting config.categories_slugify -->

<!-- md:version 9.2.0 -->
<!-- md:default [`pymdownx.slugs.slugify`][pymdownx.slugs.slugify] -->

使用此设置更改生成与URL兼容的slug的功能
从类别。默认情况下，['slugify][pymdownx.slugs.slugify]函数
[Python Markdown扩展]的用法如下：

``` yaml
plugins:
  - blog:
      categories_slugify: !!python/object/apply:pymdownx.slugs.slugify
        kwds:
          case: lower
```

默认配置支持Unicode，应该能为所有人生成良好的slug
语言。当然，您还可以为以下对象提供自定义的slugif功能
更精细的控制。

---

#### <!-- md:setting config.categories_slugify_separator -->

<!-- md:version 9.2.0 -->
<!-- md:default `-` -->

使用此设置更改传递给slugif的分隔符
函数集为[类别_插件]的一部分[配置.类别_插件]。与…同时
默认值是连字符，可以设置为任何字符串，例如“_”：

``` yaml
plugins:
  - blog:
      categories_slugify_separator: _
```

---

#### <!-- md:setting config.categories_sort_by -->

<!-- md:sponsors -->
<!-- md:version insiders-4.45.0 -->
<!-- md:default `material.plugins.blog.view_name` -->

使用此设置可指定用于排序类别的自定义函数。给
例如，如果你想按类别包含的帖子数量对类别进行排序，
使用以下配置：

``` yaml
plugins:
  - blog:
      categories_sort_by: !!python/name:material.plugins.blog.view_post_count
```

别忘了启用[`categories_sort_reverse][config.categories_sort _reverse]。
您可以定义自己的比较函数，该函数必须返回一些值
可以在排序时进行比较，即字符串或数字。

---

#### <!-- md:setting config.categories_sort_reverse -->

<!-- md:sponsors -->
<!-- md:version insiders-4.45.0 -->
<!-- md:default `false` -->

使用此设置可颠倒类别的排序顺序。By
默认情况下，类别按升序排序，但您可以颠倒顺序
如下：

``` yaml
plugins:
  - blog:
      categories_sort_reverse: true
```

---

#### <!-- md:setting config.categories_allowed -->

<!-- md:version 9.2.0 -->
<!-- md:default none -->

该插件允许根据预定义列表检查类别，以便
捕捉拼写错误或确保类别不是任意添加的。指定
您希望允许的类别：

``` yaml
plugins:
  - blog:
      categories_allowed:
        - Search
        - Performance
```

如果帖子引用的类别不属于
这个列表。可以使用[“类别”]将帖子分配到类别中
[meta.classes]元数据属性。

---

#### <!-- md:setting config.categories_pagination -->

<!-- md:sponsors -->
<!-- md:version insiders-4.44.0 -->
<!-- md:default `true` -->

使用此设置可启用或禁用类别页面的分页。价值
此设置的值继承自[`pagination][config.pagination]，除非它是
明确设置。要禁用分页，请使用：

``` yaml
plugins:
  - blog:
      categories_pagination: false
```

---

#### <!-- md:setting config.categories_pagination_per_page -->

<!-- md:sponsors -->
<!-- md:version insiders-4.44.0 -->
<!-- md:default `10` -->

使用此设置可更改每个类别页面呈现的帖子数量。这个
此设置的值继承自[“pagination_per_page”]
[config.pagion_per_page]，除非明确设置。要更改它，请使用：

``` yaml
plugins:
  - blog:
      categories_pagination_per_page: 5
```

---

#### <!-- md:setting config.categories_toc -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

使用此设置可利用目录显示所有帖子的标题
类别页面。此设置的值继承自[`blog_toc`]
[config.blog_toc]，除非明确设置。要更改它，请使用：

``` yaml
plugins:
  - blog:
      categories_toc: true
```

### 作者

作者可以使用以下设置：

---

#### <!-- md:setting config.authors -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用文章作者。如果启用了该设置，
该插件将查找一个名为[`.orges.yml`][config.authors_file]的文件
在帖子和视图中呈现作者。通过以下方式禁用此行为：

``` yaml
plugins:
  - blog:
      authors: false
```

---

#### <!-- md:setting config.authors_file -->

<!-- md:version 9.2.0 -->
<!-- md:default `{blog}/.authors.yml` -->

使用此设置可更改其中包含作者信息的文件的路径
你的帖子驻留。通常不需要更改此设置，但如果
您需要使用：

``` yaml
plugins:
  - blog:
      authors_file: "{blog}/.authors.yml"
```

以下占位符可用：

- `blog`–[blog`目录][config.blog_dir]

提供的路径是从[`docs`目录][mkdocs.docs_dir]解析的。

!!! info "Format of author information"

    The `.authors.yml` file must adhere to the following format:

    ``` yaml title=".authors.yml"
    authors:
      <author>:
        name: string        # Author name
        description: string # Author description
        avatar: url         # Author avatar
        slug: url           # Author profile slug
        url: url            # Author website URL
    ```

    请注意，“<author>”必须设置为用于关联作者的标识符
    带有帖子，例如GitHub用户名“squidfunk”。此标识符可以
    然后在[作者][元作者]元数据属性中使用
    一篇帖子。支持多个作者。例如，请参见
    [我们博客使用的`.orges.yml`文件][.orges.ymml]。

  [.authors.yml]: https://github.com/squidfunk/mkdocs-material/blob/master/docs/blog/.authors.yml

---

#### <!-- md:setting config.authors_profiles -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default `false` -->

使用此设置启用或禁用自动生成的作者配置文件。
作者简介按时间倒序显示作者的所有帖子。
您可以通过以下方式启用作者配置文件：

``` yaml
plugins:
  - blog:
      authors_profiles: true
```

---

#### <!-- md:setting config.authors_profiles_name -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default computed -->

使用此设置更改插件添加到的作者部分的标题
导航。如果省略此设置，则其来源于翻译。
如果你想更改它，请使用：

``` yaml
plugins:
  - blog:
      authors_profiles_name: Authors
```

---

#### <!-- md:setting config.authors_profiles_url_format -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default `author/{slug}` -->

使用此设置更改生成时使用的格式字符串
作者配置文件URL。您可以自由组合占位符，并将其与
斜线或其他字符：

=== ":material-link: blog/author/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          authors_profiles_url_format: "author/{slug}"
    ```

=== ":material-link: blog/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          authors_profiles_url_format: "{slug}"
    ```

The following placeholders are available:

- `slug` – 来自[`authors_file][config.authors_file]的作者段符或标识符
- `name` – 来自[`authors_file][config.authors_file]的作者名称

---

#### <!-- md:setting config.authors_profiles_pagination -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default `true` -->

使用此设置可启用或禁用作者配置文件的分页。价值
此设置的值继承自[`pagination][config.pagination]，除非它是
明确设置。要禁用分页，请使用：

``` yaml
plugins:
  - blog:
      authors_profiles_pagination: false
```

---

#### <!-- md:setting config.authors_profiles_pagination_per_page -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default `10` -->

使用此设置可更改每个存档页面呈现的帖子数量。这个
此设置的值继承自[“pagination_per_page”]
[config.pagion_per_page]，除非明确设置。要更改它，请使用：

``` yaml
plugins:
  - blog:
      authors_profiles_pagination_per_page: 5
```

---

#### <!-- md:setting config.authors_profiles_toc -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default `false` -->

使用此设置可利用目录显示所有帖子的标题
作者简介。此设置的值继承自[`blog_toc`]
[config.blog_toc]，除非明确设置。要更改它，请使用：

``` yaml
plugins:
  - blog:
      authors_profiles_toc: true
```

### 分页

以下设置可用于分页：

---

#### <!-- md:setting config.pagination -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置在视图生成的页面中启用或禁用分页
按逆时间顺序显示帖子或帖子子集。如果你想要我
要禁用分页，请使用：

``` yaml
plugins:
  - blog:
      pagination: false
```

---

#### <!-- md:setting config.pagination_per_page -->

<!-- md:version 9.2.0 -->
<!-- md:default `10` -->

使用此设置可更改每页呈现的帖子数量。如果你有
相当长的帖子摘录，减少帖子数量可能是个好主意
每页：

``` yaml
plugins:
  - blog:
      pagination_per_page: 5
```

---

#### <!-- md:setting config.pagination_url_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `page/{page}` -->

使用此设置更改生成时使用的格式字符串
分页视图URL。您可以自由组合占位符，并用
斜线或其他字符：

=== ":material-link: blog/page/n/"

    ``` yaml
    plugins:
      - blog:
          pagination_url_format: "page/{page}"
    ```

=== ":material-link: blog/n/"

    ``` yaml
    plugins:
      - blog:
          pagination_url_format: "{page}"
    ```

The following placeholders are available:

- `page` – Page number

---

#### <!-- md:setting config.pagination_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `~2~` -->

使用此设置更改生成时使用的格式字符串
分页视图URL。您可以自由组合占位符，并用
斜线或其他字符：

=== "1 2 3 .. n"

    ``` yaml
    plugins:
      - blog:
          pagination_format: "~2~"
    ```

=== "1 2 3 .. n :material-chevron-right: :material-chevron-double-right:"

    ``` yaml
    plugins:
      - blog:
          pagination_format: "$link_first $link_previous ~2~ $link_next $link_last"
    ```

=== "1 :material-chevron-right:"

    ``` yaml
    plugins:
      - blog:
          pagination_format: "$link_previous $page $link_next"
    ```

The following placeholders are supported by [paginate]:

- `#!css $first_page` – Number of first reachable page
- `#!css $last_page` – Number of last reachable page
- `#!css $page` – Number of currently selected page
- `#!css $page_count` – Number of reachable pages
- `#!css $items_per_page` – Maximal number of items per page
- `#!css $first_item` – Index of first item on the current page
- `#!css $last_item` – Index of last item on the current page
- `#!css $item_count` – Total number of items
- `#!css $link_first` – Link to first page (unless on first page)
- `#!css $link_last` – Link to last page (unless on last page)
- `#!css $link_previous` – Link to previous page (unless on first page)
- `#!css $link_next` – Link to next page (unless on last page)

  [paginate]: https://pypi.org/project/paginate/

---

#### <!-- md:setting config.pagination_if_single_page -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

使用此设置可控制是否应自动禁用分页
当视图仅由单个页面组成时。如果你想一直渲染
分页，使用：

``` yaml
plugins:
  - blog:
      pagination_if_single_page: true
```

---

#### <!-- md:setting config.pagination_keep_content -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

使用此设置启用或禁用内容的持久性，即如果分页
视图还应显示其包含的视图的内容。如果你愿意
启用此行为，请使用：

``` yaml
plugins:
  - blog:
      pagination_keep_content: true
```

### Drafts

以下设置可用于草稿：

---

#### <!-- md:setting config.draft -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

渲染[草稿帖子][元草稿]在部署预览中很有用。使用这个
设置以指定插件在以下情况下是否应包含标记为草稿的帖子
[构建您的项目]：

=== "Render drafts"

    ``` yaml
    plugins:
      - blog:
          draft: true
    ```

=== "Don't render drafts"

    ``` yaml
    plugins:
      - blog:
          draft: false
    ```

---

#### <!-- md:setting config.draft_on_serve -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否应包含标记为的帖子
[预览网站]时的草稿。如果你不想包括草稿帖子
预览时，使用：

``` yaml
plugins:
  - blog:
      draft_on_serve: false
```

  [previewing your site]: ../creating-your-site.md#previewing-as-you-write

---

#### <!-- md:setting config.draft_if_future_date -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

该插件可以自动将带有未来日期的帖子标记为草稿。当
日期已过今天，当
[构建你的项目]，除非明确标记为草稿：

``` yaml
plugins:
  - blog:
      draft_if_future_date: true
```

## 使用

### 元数据

帖子可以定义一些元数据属性，指定插件的方式
呈现它们，在哪些视图中集成它们，以及它们如何链接到
彼此。每个帖子的元数据都会根据模式进行验证，以允许
更快地发现语法错误。

以下属性可用：

---

#### <!-- md:setting meta.authors -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性通过提供以下列表将帖子与[作者]相关联
标识符如[`authors_file][config.authors_file]中所定义。如果A
无法解析作者，插件将终止并显示错误：

``` yaml
---
authors:
  - squidfunk # (1)!
---

# Post title
...
```

1.  Authors are linked by using their identifiers. As an example, see
    [the `.authors.yml` file][.authors.yml] we're using for our blog.

  [authors]: #authors

---

#### <!-- md:setting meta.categories -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性将帖子与一个或多个[类别][类别]相关联，
使帖子成为生成的类别页面的一部分。类别已定义
作为字符串列表（允许使用空格）：

``` yaml
---
categories:
  - Search
  - Performance
---

# Post title
...
```

如果你想防止为帖子分配类别时出现意外拼写错误，你
可以使用以下命令在“mkdocs.yml”中设置预定义的允许类别列表
[`categories_allowed][config.categories_alowed]设置。

---

#### <!-- md:setting meta.date -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:flag required -->

使用此属性指定帖子的日期。注意，该属性是必需的，
这意味着构建在未设置时失败。其他日期可以通过以下方式设置
使用稍微不同的语法：

=== "Date"

    ``` yaml
    ---
    date: 2024-01-31
    ---

    # Post title
    ...
    ```

=== "Update date"

    ``` yaml
    ---
    date:
      created: 2024-01-31 # (1)!
      updated: 2024-02-01
    ---

    # Post title
    ...
    ```

    1.  Each post must have a creation date set.

=== "Custom date"

    ``` yaml
    ---
    date:
      created: 2024-01-31
      my_custom_date: 2024-02-01 # (1)!
    ---

    # Post title
    ...
    ```

    1.  博客插件验证所有日期，并允许使用
        模板中的[babel]的[模式语法]。当使用主题扩展时，
        作者可以将自定义日期添加到模板中。

        这是在#5733中首次提出的要求。

支持以下日期格式：

- `2024-01-31`
- `2024-01-31T12:00:00`

---

#### <!-- md:setting meta.draft -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性将帖子标记为草稿。该插件允许包含或
使用[构建项目]时排除标记为草稿的帖子
[草稿][配置草稿]设置。将帖子标记为草稿：

``` yaml
---
draft: true
---

# Post title
...
```

---

#### <!-- md:setting meta.pin -->

<!-- md:sponsors -->
<!-- md:version insiders-4.53.0 -->
<!-- md:flag metadata -->
<!-- md:default `false` -->
<!-- md:flag experimental -->

使用此属性将柱子固定到视图的顶部。如果有多个帖子
固定后，固定的帖子按降序排列，出现在所有帖子之前
其他帖子。在柱子上钉上：

``` yaml
---
pin: true
---

# Post title
...
```

---

#### <!-- md:setting meta.links -->

<!-- md:sponsors -->
<!-- md:version insiders-4.23.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->
<!-- md:flag experimental -->

使用此属性定义在侧边栏中呈现的链接列表
一篇帖子。该属性遵循与中的[`nav`][mkdocs.nav]相同的语法
`mkdocs.yml`，支持部分甚至锚点：

=== "Links"

    ``` yaml
    ---
    links:
      - setup/setting-up-site-search.md
      - insiders/index.md
    ---

    # Post title
    ...
    ```

=== "Links with sections"

    ``` yaml
    ---
    links:
      - setup/setting-up-site-search.md
      - Insiders:
        - insiders/index.md
        - insiders/getting-started.md
    ---

    # Post title
    ...
    ```

=== "Links with anchors"

    ``` yaml
    ---
    links:
      - plugins/search.md # (1)!
      - Insiders:
        - insiders/how-to-sponsor.md
        - insiders/getting-started.md#_1
    ---

    # Post title
    ...
    ```

    1.  如果链接定义了锚点，则插件会从以下位置解析锚点
        链接页面，并将锚点标题设置为[字幕]。

所有相关链接都是从[`docs`目录][mkdocs.docs_dir]解析的。

  [subtitle]: ../reference/index.md#setting-the-page-subtitle

---

#### <!-- md:setting meta.readtime -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:default computed -->

使用此属性显式设置帖子的阅读时间（分钟）。什么时候？
启用[`post_readtime`][config.post_readtime]后，插件将计算
帖子的阅读时间，可以用以下命令覆盖：

``` yaml
---
readtime: 15
---

# Post title
...
```

---

#### <!-- md:setting meta.slug -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:default computed -->

使用此属性可以显式设置帖子的slug。默认情况下，slug
帖子由[`post_slugify][config.post_sluglify]自动计算
可以用以下命令覆盖帖子标题中的函数：

``` yaml
---
slug: help-im-trapped-in-a-universe-factory
---

# Post title
...
```

Slugs are passed to [`post_url_format`][config.post_url_format].

---

!!! question "缺少什么？"

    在设置博客或从其他博客框架迁移时，您
    可能会发现您缺少特定功能–我们很乐意
    考虑将其添加到插件中！你可以[展开讨论]
    在我们的[问题跟踪器]上提出问题或创建[更改请求]，因此我们
    可以找出它是否适合该插件。

  [open a discussion]: https://github.com/squidfunk/mkdocs-material/discussions
  [change request]: ../contributing/requesting-a-change.md
  [issue tracker]: https://github.com/squidfunk/mkdocs-material/issues

# 导航、作者和分页

博客插件提供博客风格的导航，具有逆时间顺序
默认情况下，索引页和按年份组织的存档。本教程显示
如何配置默认导航的详细信息、配置作者以及
使用类别和[Tags plugin]添加更多导航选项。

[Tags plugin]: ../../plugins/tags.md

__所需时间:__ 通常为30分钟

## Integrating navigation

到目前为止，您已经让博客插件和MkDocs担心导航问题。对于一些
用例，这可能就足够了，不声明一个
`mkdocs.yml`中的`nav`部分。

但是，您可能希望将博客与其他内容和导航集成在一起
您在配置的`nav`部分定义的结构。
在这种情况下，你需要提供一个博客插件应该放置的地方
将博客导航附加到导航结构的其余部分。

!!! example "与网站导航集成"

    将以下内容添加到您的`mkdocs.yml`中，以了解博客插件如何
    将博客导航与整体导航结构整合。
    请注意，此时您需要指定的唯一内容是
    博客的索引页及其路径必须与`blog_dir`设置匹配，
    默认情况下为`blog`：

    ```yaml hl_lines="5 6"
    nav:
      - Home: index.md
      - Install: install.md
      - Usage: usage.md
      - Blog:
         - blog/index.md
    ```

    您会注意到"Blog"在导航结构中是重复的。向
    为了避免这种情况，您可以使用`navigation.indexes`功能来创建博客
    为博客的部分索引页面建立索引：

    ```yaml hl_lines="3 4"
    theme:
      name: material
      features:
        - navigation.indexes
    ```

!!! tip "独立博客"

    如果你需要的是一个独立的博客，而不是一个与
    对于更大的网站，这可以通过使用`blog_dir`配置选项来完成。
    要了解如何做到这一点，请参阅[setting up a blog]。
    本教程的其余部分假设您正在将博客与
    更宽的网站。

[Setting up a blog]: ../../setup/setting-up-a-blog.md#blog-only

!!! tip "添加页面"

    您可以将其他页面添加到博客部分，方法是将它们放入
    `docs/blog`（并将其添加到导航中）。博客档案将
    添加到这些页面之后的导航中。

## 配置存档

默认情况下，博客存档仅按年份列出帖子。如果你想添加
按月列出，您可以配置存档的日期格式。

!!! example "按月组织岗位"

    将以下内容添加到您的`mkdocs.yml`中，以获取月份列表
    名称（使用主题选项中选择的语言）：

    ```yaml hl_lines="2"
    - blog:
        archive_date_format: MMMM yyyy
    ```

    如果你不想要完整的月份名称，你可以指定日期
    例如，配置“MM/yyyy”。

    如果你想添加日期，你可以为它们添加一个占位符。
    例如，要获得美式输出，请将其设置为`MM/dd/yyyy`。
    对于按完整日期对博客文章进行排序的插件，您将
    还需要设置`archive_url_date_format`以包含月份
    还有日期，所以也把它改为`MM/dd/yyyy`。

## 使用类别

分类是一种让博客文章按主题访问的方式，同时保留
导航结构基于每个类别列表中的时间顺序。
当存在一组有限的非重叠类别时使用它们
你可以把你的帖子分类。

类别显示在主导航中，因此可以从那里直接访问。
这意味着类别相对较少，否则
主导航中的`categories`部分将变得过于拥挤。


!!! example "添加类别"

    通过将类别添加到页眉，将其添加到您的第一篇博客文章中：

    ``` hl_lines="4 5""
    ---
    date: 2023-12-31
    updated: 2024-01-02
    categories:
      - Holidays
    ---
    ```

    现在博客文章已经分类，`Holidays`出现在
    主导航中的`Categories`和博客文章出现在
    此类别的索引页。


!!! tip "单一类别还是多个类别？"

    虽然传统上一篇博客文章只属于
    一个类别，Material for MkDocs实际上允许您分配更多
    不止一个。虽然这给了你一定程度的自由，但你应该
    可能不要过多使用它，尤其是因为你可以使用标签
    处理多种分类。我们将在下一步介绍它们。

材料允许您控制博客作者可以使用的类别。你
在`mkdocs.yml`中声明它们。这样你就可以确保每个人都坚持下去
根据商定的类别，插件可以检测拼写错误。

!!! example "控制你的类别"

    在博客插件的配置中添加一个`categories_allowed`条目
    条目"Holidays"和"News"：

    ```yaml hl_lines="5-7"
    plugins:
      - search
      - blog:
          archive_date_format: MMMM yyyy
          categories_allowed:
            - Holidays
            - News
    ```

    现在，当你在博客文章中添加一个与以下内容不匹配的类别时
    第二，你应该得到一个构建错误。

## 使用标签

[Tags plugin]提供了另一种对博客文章进行分类和制作的方法
它们可以独立于主导航结构访问。标签很有用
使相关内容即使在不同部分也易于发现
导航层次结构。

[Tags plugin]: https://squidfunk.github.io/mkdocs-material/plugins/tags/

您可能有这样的教程以及更全面的设置指南
以及参考文件。向所有三个添加相同的标签表明它们
是相关的。正如您将看到的，可以从标记的页面导航到
标签索引，并从那里指向携带相同标签的其他页面。

!!! example "启用插件并添加标签"

    首先，您需要将插件添加到您的`mkdocs.yml`中：

    ```yaml hl_lines="8"
    plugins:
      - search
      - blog:
          archive_date_format: MMMM yyyy
          categories_allowed:
            - Holidays
            - News
      - tags
    ```

    完成此操作后，您可以在页眉中为帖子添加标签：

    ``` hl_lines="9-12""
    ---
    date:
      created: 2023-12-31
      updated: 2024-01-02
    authors:
      - material
    categories:
      - Holidays
    tags:
      - new year
      - hogmanay
      - festive season
    ---
    ```

您应该在帖子顶部看到您定义的标签。然而，在
就这样。而博客插件会自动为
类别，标签插件对标签不做同样的事情。这是因为
tags插件不是博客专用的。您可以将其用于任何网站内容，因此
标签索引是否应该删除尚不清楚。

您可以使用Material的公共版本为配置基本标记索引
MkDocs。当然，Insider Edition也支持这一点，但也提供
一种允许任意数量标签的替代索引机制
索引、作用域列表、阴影标签、嵌套标签等等。

!!! example "添加标签索引"
    === "Basic tag index"

        要使用公共版本配置标记索引，请添加`tags_file`条目
        转到标签插件的配置，并在nav中进行配置`
        部分。记住在现有的“标签”条目末尾添加一个冒号。

        ```yaml hl_lines="8-9 17"
        plugins:
            - search
            - blog:
                archive_date_format: MMMM yyyy
                categories_allowed:
                    - Holidays
                    - News
            - tags:
                tags_file: blog/tags.md

        nav:
            - Home: index.md
            - Install: install.md
            - Usage: usage.md
            - Blog:
                - blog/index.md
                - Tags: blog/tags.md
        ```

        标签索引将附加到配置的页面上，您应该
        现在在指定位置创建。

        请注意，您可以将标记索引页放在主目录中的任何位置
        导航，所以如果你在其他地方使用标签，而不仅仅是在你的
        blog，那么您可能希望在blog部分之外有标签索引
        导航。


    === "内幕版"

        要添加标签索引，您需要在Markdown文件中添加一个占位符来告诉
        在该点插入索引的插件。这意味着你
        可以在索引前后添加内容。至关重要的是，您可以添加
        多个页面中的占位符，每个页面都有一个配置
        标签的子集应显示在索引中。

        最简单的索引页看起来像这样。在`docs/tags.md`下创建它。

        ```markdown
        # Tag index
        <!-- material/tags -->
        ```

        现在，您可能希望将博客的标签与标签分开
        您可以在页面的其余部分使用。您可以通过分配来实现这一点
        标签索引一个作用域。将以下内容放在`docs/blog/tags.md`下：

        ```markdown
        # Tag index  for the blog
        <!-- material/tags { scope: true } -->
        ```

        您现在有两个索引页面：一个覆盖整个网站，另一个
        只覆盖博客。将两者添加到导航中：

        ```yaml
        nav:
            - Home: index.md
            - Tags: tags.md
            - Blog:
                - blog/index.md
                - blog/tags.md
        ```

        Insider Edition中的标签插件是一个非常强大的工具
        我们只能触及它可能的表面。如果你
        在完成本教程的这一部分后，您想探索更多内容，
        请查看[tags plugin reference]。

[tags plugin reference]: ../../plugins/tags.md

## 定义作者

如果你的博客有不止一个作者，那么你可能想确定作者
对于每一篇博客文章。博客插件允许您创建一个包含以下内容的文件
作者信息，然后参考特定帖子的作者
页面标题。

!!! example "创建作者信息"

    创建一个文件`docs/blog/.orges.yml`，其中包含以下内容：

    ```yaml
    authors:
      team:
        name: Team
        description: Creator
        avatar: https://simpleicons.org/icons/materialformkdocs.svg
      squidfunk:
        name: Martin Donath
        description: Creator
        avatar: https://github.com/squidfunk.png
    ```

    然后在第一篇帖子的标题中添加一行：


    ```hl_lines="5-6"
    ---
    date:
      created: 2023-12-31
      updated: 2024-01-02
    authors:
      - team
    ---
    ```

    请注意，`authors`是一个列表，因此您可以指定多个作者。

使用Insiders版本，您可以创建自定义作者索引页面
可以突出作者的贡献，并提供额外的
关于他们的信息。

!!! example "添加作者页面 <!-- md:sponsors -->"

    首先，您需要在`mkdocs.yml`中启用作者配置文件：

    ```yaml hl_lines="8"
    plugins:
      - search
      - blog:
          archive_date_format: MMMM yyyy
          categories_allowed:
              - Holidays
              - News
          authors_profiles: true
    ```

    检查你的博客，看看主目录中现在有一个额外的条目
    `archive`和`categories`旁边的导航，列出作者和
    他们的贡献。

    要自定义作者页面，您可以创建一个覆盖该页面的页面
    默认生成。首先，创建配置文件所在的`author`目录
    页面将位于：

    ```hl_lines="3"
    docs
    ├── blog
    │   ├── author
    │   ├── index.md
    │   └── posts
    │       ├── draft.md
    │       └── myfirst.md
    └── index.md
    ```

    然后创建一个页面`docs/blog/owner/team.md`：

    ```
    # The Material Team

    A small group of people dedicated to making writing documentation easy, if
    not outright fun! Here are some of the things we have blogged about:
    ```

    如您所见，作者索引将附加到您所拥有的内容上
    写在Markdown文件中。

## 分页

一旦你的博客开始增长，你可能不想关注这个数字
每页显示的帖子数量。默认情况下，该插件在上最多显示10个帖子
索引页面。您可以单独更改主索引的此数字，
归档索引页面和类别索引页面。

!!! example "更改分页"

    再添加五篇博客文章，然后将分页设置为每篇显示五篇
    仅限页面：

    ```yaml hl_lines="7"
    - blog:
        archive_date_format: MMMM yyyy
        categories_allowed:
            - Holidays
            - News
        authors_profiles: true
        pagination_per_page: 5
    ```

    您将看到存档和类别页面的分页设置
    继承自您添加的设置。如果你想有不同的
    不同索引页的设置，您可以指定每个设置
    单独：

    ```yaml
    - blog:
        archive_date_format: MMMM yyyy
        categories_allowed:
            - Holidays
            - News
        authors_profiles: true
        pagination_per_page: 5
        archive_pagination_per_page: 10
        categories_pagination_per_page: 10
    ```

## 博客目录

一旦你有足够多的帖子，你可能想做的另一件事
是打开为博客生成目录的功能
索引页面，让读者有机会快速浏览内容
无需滚动，即可在每页上找到他们感兴趣的内容
（假设每页的帖子数量不太大）。

!!! example "打开目录功能"

    要为博客索引页生成目录，请添加以下内容
    博客插件的配置：

    ```yaml hl_lines="2"
    - blog:
        blog_toc: true
        archive_date_format: MMMM yyyy
        # ...
    ```

## 定制蛞蝓

如果出于某种原因，您对Material for MkDocs方式不满意
将标题转换为slugs，您可以创建自己的slugify函数，或者
可以手动为特定帖子定义一个slug。

!!! example "Slugify功能"

    要定义自己的slugify函数，您需要编写一个Python函数
    在给定来自的额外参数的情况下，将文本转换为slug
    配置。你还需要编写一个函数来返回
    功能。

    假设你想定义两个可以切换的slugify函数。
    第一个函数返回一个类似于默认slugify函数的slug
    生产。第二个将结果切割成文字并返回
    基于最多五个的蛞蝓：

    ```python
    import re, functools, unicodedata

    RE_HTML_TAGS = re.compile(r'</?[^>]*>', re.UNICODE)
    RE_INVALID_SLUG_CHAR = re.compile(r'[^\w\- ]', re.UNICODE)
    RE_WHITESPACE = re.compile(r'\s', re.UNICODE)

    def _make_slug(text, sep, **kwargs):
        slug = unicodedata.normalize('NFC', text)
        slug = RE_HTML_TAGS.sub('', slug)
        slug = RE_INVALID_SLUG_CHAR.sub('', slug)
        slug = slug.strip().lower()
        slug = RE_WHITESPACE.sub(sep, slug)
        return slug

    def _make_slug_short(text, sep, **kwargs):
        words = _make_slug(text, sep, **kwargs).split(sep)
        return sep.join(words[:5])

    def slugify(**kwargs):
        if 'short' in kwargs and kwargs['short']:
            return functools.partial(_make_slug_short, **kwargs)
        return functools.partial(_make_slug, **kwargs)
    ```
    将此代码保存在`ext/slugs.py `中，并添加一个（空）`__init__.py`
    文件，以指示该目录是一个模块。现在您可以配置
    您的自定义slugify代码如下：

    ```yaml hl_lines="4-6"
    plugins:
    - blog:
        # other entries omitted
        post_slugify: !!python/object/apply:ext.slugs.slugify
          kwds:
            short: true
    ```

    将博客文章的标题改为五个字以上，并观察
    slugify函数如何缩短URL。将“short”属性更改为
    `false，你可以再次关闭它。

如果你只想对一篇博客文章施加影响，你可以定义
通过在帖子的标题中手动指定它。请注意，这是指
作为最后的选择。为每个帖子手动指定一个自定义slug
乏味。

!!! example "手动定义slug"

    例如，如果你想让蛞蝓变成“ny-eve”而不是“something”
    漫长的“新年快乐夜”，你可以添加以下内容：

    ```hl_lines="7"
    ---
    date:
      created: 2023-12-31
      updated: 2024-01-02
    readtime: 15
    pin: true
    slug: ny-eve
    ---
    ```

    此帖子的URL现在应该是
    `http://localhost:8000/blog/2023/01/31/ny-eve/`.

## 接下来是什么？

你可能想通过允许人们
通过提供指向您的社交媒体个人资料的链接，订阅RSS提要
提供分享和点赞按钮或通过设置评论系统。
[engagement and dissemination tutorial]将引导您完成这些设置。

[engagement and dissemination tutorial]: engage.md

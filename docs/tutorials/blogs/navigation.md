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

## Using categories

Categories are a way to make blog posts accessible by topic while retaining
the navigation structure based on chronology within each category listing.
Use them when there is a limited set of non-overlapping categories that
you can sort your posts into.

Categories appear in the main navigation, so are directly accessible from there.
This implies that there are relatively few categories as otherwise the
`categories` section in your main navigation will become too crowded.


!!! example "Add a category"

    Add a category to your first blog post by adding it to the page header:

    ``` hl_lines="4 5""
    ---
    date: 2023-12-31
    updated: 2024-01-02
    categories:
      - Holidays
    ---
    ```

    Now that the blog post has been categorised, `Holidays` appears under
    `Categories` in the main navigation and the blog post appears in the
    index page for this category.


!!! tip "Single or multiple categories?"

    While it is traditionally the case that a blog post would belong to only
    one category, Material for MkDocs actually allows you to assign more
    than one. While this gives you a degree of freedom, you should
    probably not use this too much, not least because you can use tags to
    deal with multiple classifications. We will cover them in the next step.

Material allows you to control which categories blog authors can use. You
declare them in the `mkdocs.yml`. This way you can make sure everyone sticks
to agreed categories and that the plugin detects typos.

!!! example "Control your categories"

    Add a `categories_allowed` entry to the configuration of the Blog plugin
    with the entries "Holidays" and "News":

    ```yaml hl_lines="5-7"
    plugins:
      - search
      - blog:
          archive_date_format: MMMM yyyy
          categories_allowed:
            - Holidays
            - News
    ```

    Now, when you add a category to a blog post that does not match one of these
    two, you should get a build error.

## Using tags

The [Tags plugin] provides another way to classify blog posts and to make
them accessible independently of the main navigation structure. Tags are useful
for making related content easily discoverable even if it is in different parts
of the navigation hierarchy.

[Tags plugin]: https://squidfunk.github.io/mkdocs-material/plugins/tags/

You may have a tutorial like this one as well as a more comprehensive setup guide
and reference documentation. Adding the same tag to all three shows that they
are related. As you will see, it is possible to navigate from a tagged page to
the tag index and, from there, to other pages that carry the same tag.

!!! example "Enable the plugin and add tags"

    First, you need to add the plugin to your `mkdocs.yml`:

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

    Once this is done, you can add tags to posts in the page header:

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

You should see the tags that you defined at the top of the post. However, at the
moment that is it. While the blog plugin automatically creates an index page for
categories, the tags plugin does not do the same for tags. This is because the
tags plugin is not specific for blogs. You can use it for any site content, so
it is not obvious were the tag index should go.

You can configure a basic tag index using the public version of Material for
MkDocs. The Insider Edition supports this as well, of course, but also provides
an alternative index mechanism that allows for an arbitrary number of tag
indexes, scoped listings, shadow tags, nested tags, and much more.

!!! example "Adding a tags index"
    === "Basic tag index"

        To configure a tag index using the public version, add a `tags_file` entry
        to your configuration of the tags plugin and configure it in your `nav`
        section. Remember to add a colon at the end of the existing `tags` entry.

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

        The tag index will be appended to the configured page, which you should
        now create at the location specified.

        Note that you can put the tag index page anywhere in your primary
        navigation, so if you are using tags elsewhere instead of just in your
        blog then you may want to have the tag index outside the blog section
        of the navigation.


    === "Insider Edition"

        To add a tag index, you add a placeholder in a Markdown file to tell
        the plugin to insert an index at that point. This means that you
        can add content before and after the index. Crucially, you can add
        placeholders in multiple pages, each with a configuration of what
        subset of tags should be displayed in the index.

        The simplest index page looks like this. Create it under `docs/tags.md`.

        ```markdown
        # Tag index
        <!-- material/tags -->
        ```

        Now, you may want to keep the tags for your blog separate from tags
        you use in the rest of your page. You can achieve this by assigning
        the tag index a scope. Put the following under `docs/blog/tags.md`:

        ```markdown
        # Tag index  for the blog
        <!-- material/tags { scope: true } -->
        ```

        You now have two index pages: one covers the whole site and one
        covers only the blog. Add both to the navigation:

        ```yaml
        nav:
            - Home: index.md
            - Tags: tags.md
            - Blog:
                - blog/index.md
                - blog/tags.md
        ```

        The tags plugin in the Insider Edition is an incredibly powerful tool
        and we can only scratch the surface of what is possible with it. If you
        want to explore more after you have worked for this part of the tutorial,
        have a look at the [tags plugin reference].

[tags plugin reference]: ../../plugins/tags.md

## Defining authors

If your blog has more than one author then you may want to identify the author
for each blog post. The blog plugin allows you to create a file that contains
the author information and to then reference the authors of a particular post in
the page header.

!!! example "Create author info"

    Create a file `docs/blog/.authors.yml` with this content:

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

    and then add a line to the header of the first post:


    ```hl_lines="5-6"
    ---
    date:
      created: 2023-12-31
      updated: 2024-01-02
    authors:
      - team
    ---
    ```

    Note that `authors` is a list, so you can specify multiple authors.

With the Insiders edition, you can create custom author index pages that
can highlight the contributions of an author as well as provide additional
information about them.

!!! example "Add author page <!-- md:sponsors -->"

    First, you need to enable author profiles in the `mkdocs.yml`:

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

    Check your blog to see that there is now an extra entry in the main
    navigation next to `archive` and `categories` that lists the authors and
    their contributions.

    To customize the author page, you can create a page that overrides the one
    generated by default. First, create the `author` directory that the profile
    pages will live in:

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

    Then create a page `docs/blog/author/team.md`:

    ```
    # The Material Team

    A small group of people dedicated to making writing documentation easy, if
    not outright fun! Here are some of the things we have blogged about:
    ```

    As you can see, the author index gets appended to the content you have
    written in the Markdown file.

## Pagination

Once your blog starts growing, you may not want to pay attention to the number
of posts displayed per page. By default, the plugin displays up to 10 posts on
the index pages. You can change this number separately for the main index,
the archive index pages, and the category index pages.

!!! example "Changing pagination"

    Add five more blog posts, then set the pagination setting to show five per
    page only:

    ```yaml hl_lines="7"
    - blog:
        archive_date_format: MMMM yyyy
        categories_allowed:
            - Holidays
            - News
        authors_profiles: true
        pagination_per_page: 5
    ```

    You will see that the pagination setting for archive and category pages
    are inherited from the setting you added. If you want to have different
    settings for the different index pages, you can specify each setting
    separately:

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

## Blog table of contents

Another thing you may want to do once you have a large enough number of posts
is to turn on the function that produces a table of contents for the blog
index pages, giving your readers the opportunity to quickly scan the content
of each page for something that interests them without having to scroll
(assuming that the number of post per page is not too big).

!!! example "Turn on the table of contents feature"

    To produce a table of contents for the blog index pages, add the following
    to the configuration of the blog plugin:

    ```yaml hl_lines="2"
    - blog:
        blog_toc: true
        archive_date_format: MMMM yyyy
        # ...
    ```

## Custom slugs

If, for some reason, you are not happy with the way that Material for MkDocs
turns headings into slugs, you can create your own slugify function or you
can manually define a slug for a specific post.

!!! example "Slugify function"

    To define your own slugify function, you need to write a Python function
    that converts text into a slug given additional arguments from the
    configuration. You also need to write a function that returns that
    function.

    Say you want to define two slugify functions that you can switch between.
    The first one returns a slug similar to what the default slugify function
    produces. The second one cuts the result of that up into words and returns
    a slug based on a maximum of five of them:

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
    Save this code in `ext/slugs.py` and also add an (empty) `__init__.py`
    file to indicate that the directory is a module. Now you can configure
    your custom slugify code like this:

    ```yaml hl_lines="4-6"
    plugins:
    - blog:
        # other entries omitted
        post_slugify: !!python/object/apply:ext.slugs.slugify
          kwds:
            short: true
    ```

    Change the heading of a blog post to be longer than five words and observe
    how the slugify function shortens the URL. Change the `short` attribute to
    `false` and you can turn this off again.

If you want to influence the slug only for a single blog post, you can define
it manually by specifying it in the header of the post. Note that this is meant
as a last resort option. Specifying a custom slug manually for every post would
be tedious.

!!! example "Manually define slug"

    If, for example, you wanted the slug to be 'ny-eve'  instead of the somewhat
    lengthy 'happy-new-years-eve', you could add the following:

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

    The URL for this post should now be
    `http://localhost:8000/blog/2023/01/31/ny-eve/`.

## What's next?

You may want to increase engagement with your blog by allowing people to
subscribe to an RSS feed, by providing links to your social media profiles, by
providing share and like buttons, or by setting up a comment system.
The [engagement and dissemination tutorial] walks you through setting these up.

[engagement and dissemination tutorial]: engage.md

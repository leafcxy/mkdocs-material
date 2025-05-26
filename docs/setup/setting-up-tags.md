# 设置标签

MkDocs的材料增加了对带有标签的页面分类的一流支持，
这增加了与组相关的页面的可能性，并使其可被发现
通过搜索和专用的[tags index]。如果您的文档很大，请标记
可以帮助更快地发现相关信息。

  [tags index]: #adding-a-tags-index

## 配置

### 内置标签插件

<!-- md:version 8.2.0 -->
<!-- md:plugin -->

内置的标签插件增加了对任何带有标签的页面进行分类的能力
作为页面首页的一部分。为了添加对标签的支持，请添加
将以下行添加到`mkdocs.yml`：

``` yaml
plugins:
  - tags
```

有关所有设置的列表，请参阅[插件文档]。

  [plugin documentation]: ../plugins/tags.md

#### 高级设置

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

以下高级设置目前保留给我们的[赞助商]
[内部人士]。它们完全是可选的，只会添加额外的功能
标签插件：

<!-- - [`listings_layout`][config.listings_layout] -->
- [`listings_toc`][config.listings_toc]

我们将在不久的将来在此处添加更多设置。

  [Insiders]: ../insiders/index.md
  [config.listings_layout]: ../plugins/tags.md#config.listings_layout
  [config.listings_toc]: ../plugins/tags.md#config.listings_toc

### 标记图标和标识符

<!-- md:version 8.5.0 -->
<!-- md:flag experimental -->
<!-- md:example tags-with-icons -->

每个标签都可以与一个图标相关联，然后在标签内呈现。
在将图标分配给标签之前，将每个标签与唯一的标识符相关联，
在`mkdocs.yml`中添加以下内容：

``` yaml
extra:
  tags:
    <tag>: <identifier> # (1)!
```

1.  标识符只能包含字母数字字符以及破折号
    和下划线。例如，如果你有一个标签“兼容性”，你可以
    将“compat”设置为标识符：

    ``` yaml
    extra:
      tags:
        Compatibility: compat
    ```

    Identifiers can be reused between tags. Tags which are not explicitly
    associated will use the default tag icon which is :material-pound:

Next, each identifier can be associated with an icon, even a [custom icon], by
adding the following lines to `mkdocs.yml` under the `theme.icon` configuration
setting:

=== "Tag icon"

    ``` yaml
    theme:
      icon:
        tag:
          <identifier>: <icon> # (1)!
    ```

    1.  Enter a few keywords to find the perfect icon using our [icon search] and
        click on the shortcode to copy it to your clipboard:

        <div class="mdx-iconsearch" data-mdx-component="iconsearch">
          <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="tag" />
          <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
            <div class="mdx-iconsearch-result__meta"></div>
            <ol class="mdx-iconsearch-result__list"></ol>
          </div>
        </div>

=== "Tag default icon"

    ``` yaml
    theme:
      icon:
        tag:
          default: <icon>
    ```

??? example "Expand to inspect example"

    ``` yaml
    theme:
      icon:
        tag:
          html: fontawesome/brands/html5
          js: fontawesome/brands/js
          css:  fontawesome/brands/css3
    extra:
      tags:
        HTML5: html
        JavaScript: js
        CSS: css
    ```

  [custom icon]: changing-the-logo-and-icons.md#additional-icons
  [icon search]: ../reference/icons-emojis.md#search

## 使用

### 添加标签

<!-- md:version 8.2.0 -->
<!-- md:example tags -->

When the [built-in tags plugin] is enabled, tags can be added for a document
with the front matter `tags` property. Add the following lines at the top of a
Markdown file:

``` sh
---
tags:
  - HTML5
  - JavaScript
  - CSS
---

...
```

The page will now render with those tags above the main headline and within the
search preview, which now allows to __find pages by tags__.

??? question "How to set tags for an entire folder?"

    With the help of the [built-in meta plugin], you can ensure that tags are
    set for an entire section and all nested pages, by creating a `.meta.yml`
    file in the corresponding folder with the following content:

    ``` yaml
    tags:
      - HTML5
      - JavaScript
      - CSS
    ```

    The tags set in `.meta.yml` are merged and deduplicated with the tags
    defined for a page, which means you can define common tags in `.meta.yml`
    and then add specific tags for each page. The tags in `.meta.yml` are
    appended.

  [built-in tags plugin]: ../plugins/tags.md
  [built-in meta plugin]: ../plugins/meta.md

### 添加标签索引

<!-- md:version 8.2.0 -->
<!-- md:example tags -->

The [built-in tags plugin] allows to define a file to render a tags index,
which can be any page that is part of the `nav` section. To add a tags index,
create a page, e.g. `tags.md`:

``` markdown
# Tags

Following is a list of relevant tags:

<!-- material/tags -->
```

The tags marker specifies the position of the tags index, i.e. it is
replaced with the actual tags index when the page is rendered. You can include
arbitrary content before and after the marker:

[![Tags index][tags index enabled]][tags index enabled]

  [tags index enabled]: ../assets/screenshots/tags-index.png

### 高级功能

[Insiders] ships a __ground up rewrite of the tags plugin__ which is infinitely
more powerful than the current version in the community edition. It allows
for an arbitrary number of tags indexes (listings), [scoped listings],
[shadow tags], [nested tags], and much more.

  [scoped listings]: #scoped-listings
  [shadow tags]: #shadow-tags
  [nested tags]: #nested-tags

#### 可配置列表

<!-- md:version 9.6.0 -->
<!-- md:flag experimental -->

Listings can be configured in `mkdocs.yml` or directly at the location of the
marker that you position in a Markdown document. Some examples:

- __Use [scoped listings]__: limit the tags index to pages that are on the same
  level of the subsection of the documentation the page is in:

    ``` html
    <!-- material/tags { scope: true } -->
    ```

- __List only specific tags__: limit the tags index to a single or multiple
  selected tags, e.g., `Foo` and `Bar`, excluding all other tags:

    ``` html
    <!-- material/tags { include: [Foo, Bar] } -->
    ```

- __Exclude pages with specific tags__: don't include pages that are tagged
  with specific tags, e.g. `Internal`. This can be any tag, including a shadow
  tag:

    ``` html
    <!-- material/tags { exclude: [Internal] } -->
    ```

- __Enable or disable tags inside the table of contents__: specify whether the
  table of contents lists all tags under the nearest headline:

    ``` html
    <!-- material/tags { toc: false } -->
    ```

See the [listing configuration] for all options.

  [listing configuration]: ../plugins/tags.md#listing-configuration

#### 范围列表

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

If your documentation is large, you might want to consider using scoped listings
which will only include pages that are on the same level or below the page
containing the listing. Just use:

``` html
<!-- material/tags { scope: true } -->
```

If you plan to use multiple scoped indexes, it's a good idea to define a
listing configuration in `mkdocs.yml`, which you can then reference by its id:

``` yaml
plugins:
  - tags:
      listings_map:
        scoped:
          scope: true
```

You can now use:

``` html
<!-- material/tags scoped -->
```

#### 阴影标签

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

Shadow tags are tags that are solely meant to organization, which can be
included or excluded for rendering with a simple flag. They can be enumerated
in the [`shadow_tags`][config.shadow_tags] setting:

``` yaml
plugins:
  - tags:
      shadow_tags:
        - Draft
        - Internal
```

If a document is tagged with `Draft`, the tag will only be rendered if
[`shadow`][config.shadow] setting is enabled, and excluded when it is disabled.
This is an excellent opportunity for using tags for structuring.

  [config.shadow]: ../plugins/tags.md#config.shadow
  [config.shadow_tags]: ../plugins/tags.md#config.shadow_tags

#### 嵌套标签

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

[Insiders] ships support for nested tags. The
[`tags_hierarchy_separator`][config.tags_hierarchy_separator] allows to create
hierarchies of tags, e.g., `Foo/Bar`. Nested tags will be rendered as children
of the parent tag:

``` yaml
plugins:
  - tags:
      tags_hierarchy: true
```

  [config.tags_hierarchy_separator]: ../plugins/tags.md#config.tags_hierarchy_separator

### 隐藏页面上的标签

While the tags are rendered above the main headline, sometimes, it might be
desirable to hide them for a specific page, which can be achieved with the
front matter `hide` property:

``` yaml
---
hide:
  - tags
---

# Page title
...
```

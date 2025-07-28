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

    标识符可以在标签之间重复使用。未明确标注的标签
    关联将使用默认标记图标，即：材料磅：

接下来，每个标识符都可以通过以下方式与图标相关联，甚至是[自定义图标]
在`theme.icon`配置下的`mkdocs.yml`中添加以下行
设置：

=== "Tag icon"

    ``` yaml
    theme:
      icon:
        tag:
          <identifier>: <icon> # (1)!
    ```

    1.  输入几个关键字，使用我们的[图标搜索]找到完美的图标，然后
        单击短代码将其复制到剪贴板：

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

??? example "展开以检查示例"

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
  [icon search]: ../reference/icons-emojis.md#_2

## 使用

### 添加标签

<!-- md:version 8.2.0 -->
<!-- md:example tags -->

启用[内置标签插件]后，可以为文档添加标签
带有前体“标签”属性。在a的顶部添加以下行
Markdown文件：

``` sh
---
tags:
  - HTML5
  - JavaScript
  - CSS
---

...
```

现在，页面将在主标题上方和内部显示这些标签
搜索预览，现在允许按标签查找页面。

??? question "如何为整个文件夹设置标签？"

    借助[内置元插件]，您可以确保标签
    通过创建`.meta.yml为整个节和所有嵌套页面设置`
    相应文件夹中的文件，内容如下：

    ``` yaml
    tags:
      - HTML5
      - JavaScript
      - CSS
    ```

    在“.meta.yml”中设置的标签与标签合并并消除重复
    为页面定义，这意味着您可以在`.meta.yml中定义常用标记`
    然后为每个页面添加特定的标签。`.meta.yml`中的标签是
    附。

  [built-in tags plugin]: ../plugins/tags.md
  [built-in meta plugin]: ../plugins/meta.md

### 添加标签索引

<!-- md:version 8.2.0 -->
<!-- md:example tags -->

[内置标签插件]允许定义一个文件来呈现标签索引，
该页面可以是“导航”部分的任何页面。为了添加标签索引，
创建一个页面，例如`tags.md`：

``` markdown
# Tags

以下是相关标签列表：

<!-- material/tags -->
```

标签标记指定标签索引的位置，即
在页面呈现时，用实际的标签索引替换。您可以包括
标记前后的任意内容：

[![Tags index][tags index enabled]][tags index enabled]

  [tags index enabled]: ../assets/screenshots/tags-index.png

### 高级功能

[内部人士]对标签插件进行了彻底的重写，这是无限的
比社区版中的当前版本更强大。它允许
对于任意数量的标签索引（列表）、[范围列表]，
[阴影标签]、[嵌套标签]等等。

  [scoped listings]: #scoped-listings
  [shadow tags]: #shadow-tags
  [nested tags]: #nested-tags

#### 可配置列表

<!-- md:version 9.6.0 -->
<!-- md:flag experimental -->

列表可以在`mkdocs.yml`中配置，也可以直接在
您在Markdown文档中放置的标记。一些例子：

- __Use [scoped listings]__: 将标签索引限制在相同的页面上
  该页面所在文档的子章节级别：

    ``` html
    <!-- material/tags { scope: true } -->
    ```

- __List only specific tags__: 将标签索引限制为单个或多个
  选定的标签，例如“Foo”和“Bar”，不包括所有其他标签：

    ``` html
    <!-- material/tags { include: [Foo, Bar] } -->
    ```

- __Exclude pages with specific tags__: 不包括标记的页面
  带有特定标签，例如“内部”。这可以是任何标签，包括阴影
  标签：

    ``` html
    <!-- material/tags { exclude: [Internal] } -->
    ```

- __Enable or disable tags inside the table of contents__: 指定是否
  目录列出了最近标题下的所有标签：

    ``` html
    <!-- material/tags { toc: false } -->
    ```

有关所有选项，请参阅[列表配置]。

  [listing configuration]: ../plugins/tags.md#listing-configuration

#### 范围列表

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

如果您的文档很大，您可能需要考虑使用范围列表
其将仅包括处于同一级别或低于该页面的页面
包含列表。只需使用：

``` html
<!-- material/tags { scope: true } -->
```

如果你打算使用多个作用域索引，最好定义一个
在`mkdocs.yml`中列出配置，然后您可以通过其id引用它：

``` yaml
plugins:
  - tags:
      listings_map:
        scoped:
          scope: true
```

您现在可以使用：

``` html
<!-- material/tags scoped -->
```

#### 阴影标签

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

影子标签是专门用于组织的标签，可以
包含或排除使用简单标志进行渲染。它们可以列举出来
在[`shadow_tags`][config.shadow_tags]设置中：

``` yaml
plugins:
  - tags:
      shadow_tags:
        - Draft
        - Internal
```

如果文档被标记为“草稿”，则只有在以下情况下才会呈现该标记
[`shadow`][config.shadow]设置已启用，禁用时将被排除。
这是使用标签进行结构化的绝佳机会。

  [config.shadow]: ../plugins/tags.md#config.shadow
  [config.shadow_tags]: ../plugins/tags.md#config.shadow_tags

#### 嵌套标签

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

[Insiders]提供对嵌套标签的支持。这个
[标签层次分隔符][配置标签层次分隔器]允许创建
标签的层次结构，例如“Foo/Bar”。嵌套标签将呈现为子标签
父标签的：

``` yaml
plugins:
  - tags:
      tags_hierarchy: true
```

  [config.tags_hierarchy_separator]: ../plugins/tags.md#config.tags_hierarchy_separator

### 隐藏页面上的标签

虽然标签呈现在主标题上方，但有时它可能是
希望为特定页面隐藏它们，这可以通过以下方式实现
前体“隐藏”属性：

``` yaml
---
hide:
  - tags
---

# Page title
...
```

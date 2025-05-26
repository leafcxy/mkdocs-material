# 设置标签

Material for MkDocs 为页面分类提供了标签支持，增加了相关页面分组和通过搜索及专用[标签索引]发现的可能性。如果您的文档较大，标签可以帮助更快地发现相关信息。

  [标签索引]: #adding-a-tags-index

## 配置

### 内置标签插件

<!-- md:version 8.2.0 -->
<!-- md:plugin -->

内置标签插件增加了对任何带有标签的页面进行分类的能力。要添加标签支持，请在 `mkdocs.yml` 中添加以下行：

``` yaml
plugins:
  - tags
```

有关所有设置的列表，请参阅[插件文档]。

  [插件文档]: ../plugins/tags.md

#### 高级设置

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

以下高级设置目前保留给我们的[赞助商][内部人士]。它们完全是可选的，只会为标签插件添加额外功能：

<!-- - [`listings_layout`][config.listings_layout] -->
- [`listings_toc`][config.listings_toc]

我们将在不久的将来在此处添加更多设置。

  [内部人士]: ../insiders/index.md
  [config.listings_layout]: ../plugins/tags.md#config.listings_layout
  [config.listings_toc]: ../plugins/tags.md#config.listings_toc

### 标签图标和标识符

<!-- md:version 8.5.0 -->
<!-- md:flag experimental -->
<!-- md:example tags-with-icons -->

每个标签都可以与一个图标关联，然后在标签内呈现。在将图标分配给标签之前，将每个标签与唯一标识符关联，在 `mkdocs.yml` 中添加以下内容：

``` yaml
extra:
  tags:
    <tag>: <identifier> # (1)!
```

1.  标识符只能包含字母数字字符以及破折号和下划线。例如，如果您有一个标签"兼容性"，可以将"compat"设置为标识符：

    ``` yaml
    extra:
      tags:
        Compatibility: compat
    ```

    标识符可以在标签之间重复使用。未明确关联的标签将使用默认标签图标 :material-pound:。

接下来，每个标识符可以与一个图标关联，甚至可以是[自定义图标]，通过在 `theme.icon` 配置设置下添加以下行到 `mkdocs.yml`：

=== "标签图标"

    ``` yaml
    theme:
      icon:
        tag:
          <identifier>: <icon> # (1)!
    ```

    1.  输入几个关键字，使用我们的[图标搜索]找到合适的图标，然后点击短代码复制：

        <div class="mdx-iconsearch" data-mdx-component="iconsearch">
          <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="搜索图标" data-mdx-component="iconsearch-query" value="tag" />
          <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
            <div class="mdx-iconsearch-result__meta"></div>
            <ol class="mdx-iconsearch-result__list"></ol>
          </div>
        </div>

=== "标签默认图标"

    ``` yaml
    theme:
      icon:
        tag:
          default: <icon>
    ```

??? example "展开查看示例"

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

  [自定义图标]: changing-the-logo-and-icons.md#additional-icons
  [图标搜索]: ../reference/icons-emojis.md#search

## 使用

### 添加标签

<!-- md:version 8.2.0 -->
<!-- md:example tags -->

启用[内置标签插件]后，可以通过 front matter 的 `tags` 属性为文档添加标签。在 Markdown 文件顶部添加以下行：

``` sh
---
tags:
  - HTML5
  - JavaScript
  - CSS
---

...
```

页面现在会在主标题上方和搜索预览中显示这些标签，允许__通过标签查找页面__。

??? question "如何为整个文件夹设置标签？"

    借助[内置元数据插件]，您可以通过在相应文件夹中创建 `.meta.yml` 文件来确保为整个部分和所有嵌套页面设置标签，内容如下：

    ``` yaml
    tags:
      - HTML5
      - JavaScript
      - CSS
    ```

    `.meta.yml` 中设置的标签会与页面定义的标签合并并去重，这意味着您可以在 `.meta.yml` 中定义通用标签，然后为每个页面添加特定标签。`.meta.yml` 中的标签会被追加。

  [内置标签插件]: ../plugins/tags.md
  [内置元数据插件]: ../plugins/meta.md

### 添加标签索引

<!-- md:version 8.2.0 -->
<!-- md:example tags -->

[内置标签插件]允许定义文件来呈现标签索引，该文件可以是 `nav` 部分中的任何页面。要添加标签索引，创建一个页面，例如 `tags.md`：

``` markdown
# 标签

以下是相关标签列表：

<!-- material/tags -->
```

标签标记指定标签索引的位置，即在页面呈现时替换为实际标签索引。您可以在标记前后包含任意内容：

[![标签索引][标签索引已启用]][标签索引已启用]

  [标签索引已启用]: ../assets/screenshots/tags-index.png

### 高级功能

[内部人士]提供了__标签插件的完全重写版本__，比社区版当前版本功能更强大。它允许任意数量的标签索引（列表）、[作用域列表]、[影子标签]、[嵌套标签]等。

  [作用域列表]: #scoped-listings
  [影子标签]: #shadow-tags
  [嵌套标签]: #nested-tags

#### 可配置列表

<!-- md:version 9.6.0 -->
<!-- md:flag experimental -->

列表可以在 `mkdocs.yml` 中配置，或直接在您放置在 Markdown 文档中的标记位置配置。一些示例：

- __使用[作用域列表]__：将标签索引限制为与页面所在文档子部分同级别的页面：

    ``` html
    <!-- material/tags { scope: true } -->
    ```

- __仅列出特定标签__：将标签索引限制为单个或多个选定标签，例如 `Foo` 和 `Bar`，排除所有其他标签：

    ``` html
    <!-- material/tags { include: [Foo, Bar] } -->
    ```

- __排除带有特定标签的页面__：不包含带有特定标签的页面，例如 `Internal`。这可以是任何标签，包括影子标签：

    ``` html
    <!-- material/tags { exclude: [Internal] } -->
    ```

- __启用或禁用目录中的标签__：指定目录是否在最近标题下列出所有标签：

    ``` html
    <!-- material/tags { toc: false } -->
    ```

请参阅[列表配置]了解所有选项。

#### 范围列表

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

如果您的文档是大的，您可能想要考虑使用作用域列表，它将只包括与列表所在页面同级别的页面或以下页面。只需使用：

``` html
<!-- material/tags { scope: true } -->
```

如果您计划使用多个作用域索引，这是一个好主意，在 `mkdocs.yml` 中定义一个列表配置，然后通过其 id 引用它：

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

阴影标签是仅用于组织目的的标签，可以通过简单标志包括或排除渲染。它们可以在 [`shadow_tags`][config.shadow_tags] 设置中枚举：

``` yaml
plugins:
  - tags:
      shadow_tags:
        - Draft
        - Internal
```

如果文档被标记为 `Draft`，标签将仅在 [`shadow`][config.shadow] 设置启用时渲染，并在禁用时排除。这是一个很好的机会，可以使用标签进行结构化。

  [config.shadow]: ../plugins/tags.md#config.shadow
  [config.shadow_tags]: ../plugins/tags.md#config.shadow_tags

#### 嵌套标签

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

[内部人士]提供了对嵌套标签的支持。
[`tags_hierarchy_separator`][config.tags_hierarchy_separator] 允许创建标签层次结构，例如 `Foo/Bar`。嵌套标签将作为父标签的子标签呈现：

``` yaml
plugins:
  - tags:
      tags_hierarchy: true
```

  [config.tags_hierarchy_separator]: ../plugins/tags.md#config.tags_hierarchy_separator

### 隐藏页面上的标签

虽然标签在主标题上方呈现，有时，为特定页面隐藏它们可能是可取的，可以通过 front matter 的 `hide` 属性实现：

``` yaml
---
hide:
  - tags
---

# Page title
...
```

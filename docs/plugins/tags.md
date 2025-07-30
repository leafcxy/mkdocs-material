---
title: Built-in tags plugin
icon: material/tag-text
---

# 内置标签插件

标签插件添加了对页面分类的一流支持，使用
标签，增加了对相关页面进行分组和制作的可能性
可通过搜索和专用标签索引发现。如果您的文档是
大的标签可以帮助更快地发现相关信息。

## 客观的

### 工作原理

该插件扫描所有页面的[`tags][meta.tags]元数据属性
生成标签索引，这是标签及其所在页面的倒排列表
标签索引可以位于[`nav`][mkdocs.nav]中的任何位置，
允许在向项目添加标签时具有最大的灵活性。

### 何时使用

如果要向项目添加一个或多个标记索引
插件是一个完美的选择，因为它使这个过程变得简单得可笑。
此外，它与其他几个完美集成
[内置插件]Material for MkDocs提供：

<div class="grid cards" markdown>

-   :material-file-tree: &nbsp; __[Built-in meta plugin][meta]__

    ---

    元插件可以确保您的
    项目使用[specific tags][meta.tags]进行注释，因此它们不能
    添加页面时忘记了。

    ---

    __更简单地组织和管理不同子部分中的标签__

-   :material-newspaper-variant-outline: &nbsp; __[Built-in blog plugin][blog]__

    ---

    标签插件允许将帖子与页面一起分类
    项目，以提高其可发现性，并将帖子连接到您的
    文档。

    ---

    __您的文档标签系统与您的博客集成__

</div>

  [meta]: meta.md
  [blog]: blog.md
  [built-in plugins]: index.md

## 配置

`version 8.2.0`
`plugin [tags] – built-in`
`flag multiple`

与所有[内置插件]一样，开始使用标签插件是
直截了当。只需将以下行添加到`mkdocs.yml`中，然后开始使用
[tags][meta.tags]用于对页面进行分类：

``` yaml
plugins:
  - tags
```

标签插件内置于MkDocs的Material中，不需要
安装。

  [tags]: tags.md

### 一般的

以下设置可用：

---

#### `setting config.enabled`

`version 9.1.7`
`default _true_`

使用此设置可在[构建项目]时启用或禁用插件。
通常不需要指定此设置，但如果要禁用
插件，使用：

``` yaml
plugins:
  - tags:
      enabled: false
```

  [building your project]: ../creating-your-site.md#building-your-site

### 标签

以下设置可用于标记：

---

#### `setting config.tags`

`version 9.3.2`
`default _true_`

使用此设置启用或禁用标记的呈现。插件仍然
从所有页面中提取标签，例如，用于[导出标签]而不呈现它们。
可以通过以下方式禁用渲染：

``` yaml
plugins:
  - tags:
      tags: false
```

如果[`export_only][config.export_orly]，此设置将自动禁用
已启用。

  [exporting tags]: #export

---

#### `setting config.tags_file`

`version 8.2.0`
`default none`

!!! warning "此设置已弃用"

    版本<！--md:version 9.6.0-->，此设置已弃用，因为
    版本对标签插件进行了彻底的重写，这要多得多
    比以前的版本强大。标签[列表]可以在任何页面上使用
    现在。

<div style="opacity: 0.5" markdown>

使用此设置指定标记索引的位置，即页面
用于呈现所有标签及其相关页面的列表。如果此设置为
指定后，标签将变为可点击的，指向
标签索引：

``` yaml
plugins:
  - tags:
      tags_file: tags.md
```

包含标签索引的页面可以链接到[`nav`][mkdocs.nav]中的任何位置
mkdocs.yml的一节。此设置不是必需的，您应该只使用它
如果你想有一个标签索引。

提供的路径是从[`docs`目录][mkdocs.docs_dir]解析的。

</div>

  [listings]: ../setup/setting-up-tags.md

---

#### `setting config.tags_slugify`

`version 9.6.0`
`default [_pymdownx.slugs.slugify_][pymdownx.slugs.slugify]`

使用此设置更改生成与URL兼容的slug的功能
从帖子标题。默认情况下，['slugify][pymdownx.slugs.slugify]函数
[Python Markdown扩展]的用法如下：

``` yaml
plugins:
  - tags:
      tags_slugify: !!python/object/apply:pymdownx.slugs.slugify
        kwds:
          case: lower
```

默认配置支持Unicode，应该能为所有人生成良好的slug
语言。当然，您还可以为以下对象提供自定义的slugif功能
更精细的控制。

  [pymdownx.slugs.slugify]: https://github.com/facelessuser/pymdown-extensions/blob/01c91ce79c91304c22b4e3d7a9261accc931d707/pymdownx/slugs.py#L59-L65
  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/extras/slugs/

---

#### `setting config.tags_slugify_separator`

`version 9.6.0`
`default _-_ `

使用此设置更改传递给slugif的分隔符
函数设置为[tags_slugify][config.tags_slugif]的一部分。虽然默认
是连字符，可以设置为任何字符串，例如“_”：

``` yaml
plugins:
  - tags:
      tags_slugify_separator: _
```

---

#### `setting config.tags_slugify_format`

`version 9.6.0`
`default _tag:{slug}_`

使用此设置更改生成标记时使用的格式字符串
蛞蝓。最好在标签slug前加一个字符串，使它们
唯一，默认值为：

``` yaml
plugins:
  - tags:
      tags_slugify_format: "tag:{slug}"
```

以下占位符可用：

- `slug` – Tag slug, slugified with [`tags_slugify`][config.tags_slugify]

---

#### `setting config.tags_hierarchy`

`sponsors`
`version insiders-4.48.0`
`default _false_`
`flag experimental`

使用此设置启用对标签层次结构（嵌套标签。，
`foo/bar`）。如果您打算创建标签的分层列表，可以
在`mkdocs.yml`中启用此设置：

``` yaml
plugins:
  - tags:
      tags_hierarchy: true
```

---

#### `setting config.tags_hierarchy_separator`

`sponsors`
`version insiders-4.48.0`
`default _/_`
`flag experimental`

使用此设置更改创建标记时使用的分隔符
等级制度。默认情况下，标签之间用正斜杠“/”分隔，但
可以将其更改为任何字符串，例如“”。`:

``` yaml
plugins:
  - tags:
      tags_hierarchy_separator: .
```

---

#### `setting config.tags_sort_by`

`version 9.6.0`
`default _material.plugins.tags.tag_name_`

使用此设置可指定用于比较标记的自定义函数。默认情况下，
标签比较区分大小写，但您可以使用`tagname_casefold`
不区分大小写的比较：

``` yaml
plugins:
  - tags:
      tags_sort_by: !!python/name:material.plugins.tags.tag_name_casefold
```

您还可以定义自己的比较函数，该函数必须返回一个字符串
或表示标签的数字，用于排序，并在
[`tags_sort_by`][config.tags_sord_by]。

---

#### `setting config.tags_sort_reverse`

`version 9.6.0`
`default _false_`

使用此设置可反转比较时标签的排序顺序
他们。默认情况下，标签按升序排序，但您可以反转
订购如下：

``` yaml
plugins:
  - tags:
      tags_sort_reverse: true
```

---

#### `setting config.tags_name_property`

`version 9.6.0`
`default [_tags_][meta.tags]`

使用此设置可更改所使用的前端属性的名称
插件。通常不需要更改此设置，但如果你愿意
要更改它，您可以使用：

``` yaml
plugins:
  - tags:
      tags_name_property: tags
```

---

#### `setting config.tags_name_variable`

`version 9.6.0`
`default _tags_`

使用此设置可更改所使用的模板变量的名称
插件。通常不需要更改此设置，但如果你愿意
要更改它，您可以使用：

``` yaml
plugins:
  - tags:
      tags_name_variable: tags
```

---

#### `setting config.tags_allowed`

`version 9.6.0`
`default none`

该插件允许根据预定义的列表检查标签，以便捕获
拼写错误或确保标签不是随意添加的。指定您的标签
希望允许：

``` yaml
plugins:
  - tags:
      tags_allowed:
        - HTML5
        - JavaScript
        - CSS
```

如果页面引用的标签不是
这个列表。可以使用[`tags][meta.tags]将页面分配给标签
元数据属性。

### 列表

以下设置可用于列表：

---

#### `setting config.listings`

`version 9.6.0`
`default _true_`

使用此设置启用或禁用列表。通常不需要
更改此设置，因为列表完全由内联注释创建，但是
如有必要，您可以通过以下方式禁用它们：

``` yaml
plugins:
  - tags:
      listings: false
```

如果[`export_only][config.export_orly]，此设置将自动禁用
已启用。

  [exporting tags]: #export

---

#### `setting config.listings_map`

`version 9.6.0`
`default none`

使用此定义列表配置，然后可以在列表中引用
具有自定义标识符。共享配置是一个好主意，尤其是
当您有许多标签列表时：

``` yaml
plugins:
  - tags:
      listings_map:
        custom-id:
          scope: true
          exclude: Internal
```

然后，只需引用列表标识符：

``` html
<!-- material/tags custom-id -->
```

有关所有可用设置的列表，请参阅[列表部分]。

  [listings section]: #listing-configuration

---

#### `setting config.listings_sort_by`

`version 9.6.0`
`default _material.plugins.tags.item_title_`

使用此设置可指定用于比较列表项的自定义函数。By
默认情况下，项目按标题排序，但您可以更改排序
具有以下配置的标准：

=== "Sort by item title"

    ``` yaml
    plugins:
      - tags:
          listings_sort_by: !!python/name:material.plugins.tags.item_title
    ```

=== "Sort by item URL"

    ``` yaml
    plugins:
      - tags:
          listings_sort_by: !!python/name:material.plugins.tags.item_url
    ```

您还可以定义自己的比较函数，该函数必须返回一个字符串
或表示项目的数字，用于排序，并在
[`listings_sort_by][config.listings_sport_by]。

---

#### `setting config.listings_sort_reverse`

`version 9.6.0`
`default _false_`

使用此设置可反转比较时项目的排序顺序
他们。默认情况下，项目按升序排序，但您可以颠倒顺序
订购如下：

``` yaml
plugins:
  - tags:
      listings_sort_reverse: true
```

---

#### `setting config.listings_tags_sort_by`

`version 9.6.0`
`default _material.plugins.tags.tag_name_`

使用此设置可指定用于比较列表中标记的自定义函数。靠近
默认情况下，标记比较区分大小写，但您可以使用`tagname_casefold`
对于不区分大小写的情况：

``` yaml
plugins:
  - tags:
      tags_sort_by: !!python/name:material.plugins.tags.tag_name_casefold
```

您还可以定义自己的比较函数，该函数必须返回一个字符串
或表示标签的数字，用于排序，并在
[`tags_sort_by`][config.tags_sord_by]。

---

#### `setting config.listings_tags_sort_reverse`

`version 9.6.0`
`default _false_`

使用此设置可反转比较时标签的排序顺序
他们。默认情况下，标签按升序排序，但您可以反转
订购如下：

``` yaml
plugins:
  - tags:
      tags_sort_reverse: true
```

---

#### `setting config.listings_directive`

`version 9.6.0`
`default _material/tags_`

使用此设置更改插件将查找的指令的名称
在处理页面时。如果你想使用比以下指令更短的指令
`材料/标签，您可以使用：

``` yaml
plugins:
  - tags:
      listings_directive: $tags
```

使用此设置，现在必须按如下方式引用列表：

``` html
<!-- $tags { include: [foo, bar] } -->
```

---

#### `setting config.listings_toc`

`sponsors`
`version insiders-4.48.0`
`default _true_`

使用此设置启用或禁用目录中显示的标记。
如果您不希望标签显示在目录中，可以禁用此功能
行为：

``` yaml
plugins:
  - tags:
      listings_toc: false
```

### 阴影标签

以下设置可用于阴影标记：

---

#### `setting config.shadow`

`sponsors`
`version insiders-4.48.0`
`default _false_`

使用此设置指定插件是否应在
在[构建项目]时，在页面和列表中，这可能对
部署预览：

=== "Show shadow tags"

    ``` yaml
    plugins:
      - tags:
          shadow: true
    ```

=== "Hide shadow tags"

    ``` yaml
    plugins:
      - tags:
          shadow: false
    ```

---

#### `setting config.shadow_on_serve`

`sponsors`
`version insiders-4.48.0`
`default _true_`

使用此设置控制插件是否应在
在[预览您的网站]时，您可以在页面和列表中查看。如果你不想包括
预览时，请使用：

``` yaml
plugins:
  - tags:
      shadow_on_serve: false
```

  [previewing your site]: ../creating-your-site.md#previewing-as-you-write

---

#### `setting config.shadow_tags`

`sponsors`
`version insiders-4.48.0`
`default none`

该插件允许指定一个预定义的阴影标签列表，这些标签可以
通过使用['shadow][config.shadow]将其包含在构建中或从构建中排除
设置。阴影标记必须指定为列表：

``` yaml
plugins:
  - tags:
      shadow_tags:
        - Draft
        - Internal
```

---

#### `setting config.shadow_tags_prefix`

`sponsors`
`version insiders-4.48.0`
`default none`

使用此设置指定一个字符串作为每个标记的前缀。
如果标记以此字符串开头，则标记为影子标记。一个常见的
实践是使用“_”作为前缀：

``` yaml
plugins:
  - tags:
      shadow_tags_prefix: _
```

---

#### `setting config.shadow_tags_suffix`

`sponsors`
`version insiders-4.48.0`
`default none`

使用此设置指定一个字符串作为每个标记的后缀。
如果标记以此字符串结尾，则标记为影子标记。一种选择
可以使用“Internal”作为后缀：


``` yaml
plugins:
  - tags:
      shadow_tags_suffix: Internal
```

### 出口

以下设置可用于导出：

---

#### `setting config.export`

`sponsors`
`version insiders-4.49.0`
`default _true_`

使用此设置控制插件是否创建“tags.json”文件
在您的[`site`目录][mkdocs.site_dir]中，然后可以由以下用户使用
其他插件和项目：

``` yaml
plugins:
  - tags:
      export: true
```

---

#### `setting config.export_file`

`sponsors`
`version insiders-4.49.0`
`default _tags.json_`

使用此设置更改导出标记所在的文件路径
存储。通常不需要更改此设置，但如果需要，
使用：

``` yaml
plugins:
  - tags:
      export_file: tags.json
```

提供的路径是从[`site`目录][mkdocs.site_dir]解析的。

---

#### `setting config.export_only`

`sponsors`
`version insiders-4.49.0`
`default _false_`

提供此设置仅是为了方便禁用标签的呈现
以及具有单个设置的列表（例如通过使用环境变量），
同时保持导出功能：

``` yaml
plugins:
  - tags:
      export_only: true
```

这将自动禁用[标签][配置标签]和
[列表][配置列表]设置。

## 使用

### 元数据

以下属性可用：

---

#### `setting meta.tags`

`version 8.2.0`
`flag metadata`
`default none`

使用此属性将页面与一个或多个标记相关联，使页面
出现在生成的标签索引中。标签被定义为字符串列表
（允许使用空格）：

``` yaml
---
tags:
  - HTML5
  - JavaScript
  - CSS
---

# Page title
...
```

如果你想在为页面分配标签时防止意外拼写错误，你可以
使用以下命令在`mkdocs.yml`中设置预定义的允许标签列表
[标签允许][配置标签允许]设置。

### 列出配置

列表配置控制哪些标签包含在列表中或从列表中排除
列表以及列表是否仅包括当前范围内的页面。
此外，列表可以覆盖全局配置中的某些值。

以下设置可用：

---

#### `setting listing.scope`

`version 9.6.0`
`default _false_`

此设置指定列表是否应仅考虑以下页面
在页面文档的当前小节中，该列表是
嵌入：

=== "Inline usage"

    ``` html
    <!-- material/tags { scope: true } -->
    ```

=== "Usage in `mkdocs.yml`"

    ``` yaml
    plugins:
      - tags:
          listings_map:
            custom-id:
              scope: false
    ```

    然后，只需引用列表标识符：

    ``` html
    <!-- material/tags custom-id -->
    ```

---

#### `setting listing.shadow`

`sponsors`
`version insiders-4.49.0`
`default computed`

此设置指定列表是否应包含阴影标记
允许覆盖每个列表上的全局[“shadow”][config.shadow]设置
依据：

=== "Inline usage"

    ``` html
    <!-- material/tags { shadow: true } -->
    ```

=== "Usage in `mkdocs.yml`"

    ``` yaml
    plugins:
      - tags:
          listings_map:
            custom-id:
              shadow: true
    ```

    然后，只需引用列表标识符：

    ``` html
    <!-- material/tags custom-id -->
    ```

---

#### `setting listing.toc`

`sponsors`
`version insiders-4.48.0`
`default [_listings_toc_][config.listings_toc]`

此设置指定列表是否应呈现表内的标记
内容，允许覆盖全局[`listings_toc`][config.listings_to]
按每个列表设置：

=== "Inline usage"

    ``` html
    <!-- material/tags { toc: true } -->
    ```

=== "Usage in `mkdocs.yml`"

    ``` yaml
    plugins:
      - tags:
          listings_map:
            custom-id:
              toc: true
    ```

    然后，只需引用列表标识符：

    ``` html
    <!-- material/tags custom-id -->
    ```

---

#### `setting listing.include`

`version 9.6.0`
`default none`

使用此设置指定列表中应包含哪些标记。每个
包含此设置中的标记的页面列在
相应标签：

=== "Inline usage"

    ``` html
    <!-- material/tags { include: [foo, bar] } -->
    ```

=== "Usage in `mkdocs.yml`"

    ``` yaml
    plugins:
      - tags:
          listings_map:
            custom-id:
              include:
                - foo
                - bar
    ```

    然后，只需引用列表标识符：

    ``` html
    <!-- material/tags custom-id -->
    ```

如果此设置为空，则包括所有标签和页面。

---

#### `setting listing.exclude`

`version 9.6.0`
`default none`

使用此设置指定应从列表中排除哪些标记。每个
包含此设置中的标记的页面被排除在外
完整列出：

=== "Inline usage"

    ``` html
    <!-- material/tags { exclude: [foo, bar] } -->
    ```

=== "Usage in `mkdocs.yml`"

    ``` yaml
    plugins:
      - tags:
          listings_map:
            custom-id:
              exclude:
                - foo
                - bar
    ```

    然后，只需引用列表标识符：

    ``` html
    <!-- material/tags custom-id -->
    ```

如果此设置为空，则不排除任何标签或页面。

## 局限性

由于MkDocs架构，标签插件的实现很棘手。
值得注意的是，标记列表标记不能出现在代码块中。技术方面
详细信息，请参阅#8114。

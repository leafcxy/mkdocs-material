---
title: 内置标签插件
icon: material/tag-text
---

# 内置标签插件

标签插件为使用标签对页面进行分类提供了一流的支持，使相关页面可以分组并通过搜索和专用标签索引被发现。如果您的文档很大，标签可以帮助更快地发现相关信息。

## 目标

### 工作原理

该插件扫描所有页面的[`tags`][meta.tags]元数据属性，并生成标签索引，这是一个标签及其出现页面的倒排列表。标签索引可以位于[`nav`][mkdocs.nav]中的任何位置，为项目添加标签时提供最大的灵活性。

### 何时使用

如果您想为项目添加一个或多个标签索引，标签插件是一个完美的选择，因为它使这个过程变得非常简单。此外，它与 Material for MkDocs 提供的其他几个[内置插件]完美集成：

<div class="grid cards" markdown>

-   :material-file-tree: &nbsp; __[内置元数据插件][meta]__

    ---

    元数据插件可以确保项目的子部分使用[特定标签][meta.tags]进行注释，这样在添加页面时就不会忘记它们。

    ---

    __简化不同子部分中标签的组织和管理__

-   :material-newspaper-variant-outline: &nbsp; __[内置博客插件][blog]__

    ---

    标签插件允许在项目中同时为帖子和页面添加分类，以提高它们的可发现性并将帖子与文档连接起来。

    ---

    __您的文档标签系统与博客集成__

</div>

  [meta]: meta.md
  [blog]: blog.md
  [built-in plugins]: index.md

## 配置

<!-- md:version 8.2.0 -->
<!-- md:plugin [tags] – built-in -->
<!-- md:flag multiple -->

与所有[内置插件]一样，开始使用标签插件非常简单。只需在 `mkdocs.yml` 中添加以下行，然后开始使用[标签][meta.tags]对页面进行分类：

``` yaml
plugins:
  - tags
```

标签插件已内置到 Material for MkDocs 中，无需安装。

  [tags]: tags.md

### 常规设置

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:version 9.1.7 -->
<!-- md:default `true` -->

使用此设置在[构建项目]时启用或禁用插件。通常不需要指定此设置，但如果您想禁用插件，请使用：

``` yaml
plugins:
  - tags:
      enabled: false
```

  [building your project]: ../creating-your-site.md#building-your-site

### 标签

以下标签设置可用：

---

#### <!-- md:setting config.tags -->

<!-- md:version 9.3.2 -->
<!-- md:default `true` -->

使用此设置启用或禁用标签的渲染。插件仍然会从所有页面提取标签，例如，用于[导出标签]而不渲染它们。可以通过以下方式禁用渲染：

``` yaml
plugins:
  - tags:
      tags: false
```

如果启用了[`export_only`][config.export_only]，此设置会自动禁用。

  [exporting tags]: #export

---

#### <!-- md:setting config.tags_file -->

<!-- md:version 8.2.0 -->
<!-- md:default none -->

!!! warning "此设置已弃用"

    从版本 <!-- md:version 9.6.0 --> 开始，此设置已弃用，因为此版本包含__标签插件的完全重写__，比之前的版本更强大。现在可以在任何页面上使用标签[列表]。

<div style="opacity: 0.5" markdown>

使用此设置指定标签索引的位置，这是用于渲染所有标签及其关联页面列表的页面。如果指定了此设置，标签将变为可点击的，指向标签索引中的相应部分：

``` yaml
plugins:
  - tags:
      tags_file: tags.md
```

包含标签索引的页面可以在 `mkdocs.yml` 的[`nav`][mkdocs.nav]部分的任何位置链接。此设置不是必需的 - 只有在您想要有标签索引时才应使用它。

提供的路径从[`docs`目录][mkdocs.docs_dir]解析。

</div>

  [listings]: ../setup/setting-up-tags.md#adding-a-tags-index

---

#### <!-- md:setting config.tags_slugify -->

<!-- md:version 9.6.0 -->
<!-- md:default [`pymdownx.slugs.slugify`][pymdownx.slugs.slugify] -->

使用此设置更改从帖子标题生成 URL 兼容的 slug 的函数。默认情况下，使用[Python Markdown Extensions]的[`slugify`][pymdownx.slugs.slugify]函数，如下所示：

``` yaml
plugins:
  - tags:
      tags_slugify: !!python/object/apply:pymdownx.slugs.slugify
        kwds:
          case: lower
```

默认配置支持 Unicode，应该能为所有语言生成良好的 slug。当然，您也可以提供自定义的 slug 生成函数以获得更精细的控制。

  [pymdownx.slugs.slugify]: https://github.com/facelessuser/pymdown-extensions/blob/01c91ce79c91304c22b4e3d7a9261accc931d707/pymdownx/slugs.py#L59-L65
  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/extras/slugs/

---

#### <!-- md:setting config.tags_slugify_separator -->

<!-- md:version 9.6.0 -->
<!-- md:default `-` -->

使用此设置更改作为[`tags_slugify`][config.tags_slugify]一部分设置的 slug 生成函数的分隔符。虽然默认是连字符，但可以设置为任何字符串，例如 `_`：

``` yaml
plugins:
  - tags:
      tags_slugify_separator: _
```

---

#### <!-- md:setting config.tags_slugify_format -->

<!-- md:version 9.6.0 -->
<!-- md:default `tag:{slug}` -->

使用此设置更改生成标签 slug 时使用的格式字符串。最好用使它们唯一的字符串作为标签 slug 的前缀，默认为：

``` yaml
plugins:
  - tags:
      tags_slugify_format: "tag:{slug}"
```

以下占位符可用：

- `slug` – 标签 slug，使用[`tags_slugify`][config.tags_slugify]进行 slug 化

---

#### <!-- md:setting config.tags_hierarchy -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `false` -->
<!-- md:flag experimental -->

使用此设置启用标签层次结构支持（嵌套标签，例如 `foo/bar`）。如果您打算创建标签的层次结构列表，可以在 `mkdocs.yml` 中启用此设置：

``` yaml
plugins:
  - tags:
      tags_hierarchy: true
```

---

#### <!-- md:setting config.tags_hierarchy_separator -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `/` -->
<!-- md:flag experimental -->

使用此设置更改创建标签层次结构时使用的分隔符。默认情况下，标签用正斜杠 `/` 分隔，但可以将其更改为任何字符串，例如 `.：

``` yaml
plugins:
  - tags:
      tags_hierarchy_separator: .
```

---

#### <!-- md:setting config.tags_sort_by -->

<!-- md:version 9.6.0 -->
<!-- md:default `material.plugins.tags.tag_name` -->

使用此设置指定自定义函数以比较标签。默认情况下，标签比较是区分大小写的，但可以使用 `tag_name_casefold` 进行不区分大小写的比较：

``` yaml
plugins:
  - tags:
      tags_sort_by: !!python/name:material.plugins.tags.tag_name_casefold
```

您也可以定义自己的比较函数，该函数必须返回一个字符串或数字，表示用于排序的标签，并在[`tags_sort_by`][config.tags_sort_by]中引用它。

---

#### <!-- md:setting config.tags_sort_reverse -->

<!-- md:version 9.6.0 -->
<!-- md:default `false` -->

使用此设置反转标签比较时的顺序。默认情况下，标签按升序排序，但可以通过以下方式反转排序：

``` yaml
plugins:
  - tags:
      tags_sort_reverse: true
```

---

#### <!-- md:setting config.tags_name_property -->

<!-- md:version 9.6.0 -->
<!-- md:default [`tags`][meta.tags] -->

使用此设置更改插件使用的 front matter 属性名称。通常不需要更改此设置，但如果您想更改它，可以使用：

``` yaml
plugins:
  - tags:
      tags_name_property: tags
```

---

#### <!-- md:setting config.tags_name_variable -->

<!-- md:version 9.6.0 -->
<!-- md:default `tags` -->

使用此设置更改插件使用的模板变量名称。通常不需要更改此设置，但如果您想更改它，可以使用：

``` yaml
plugins:
  - tags:
      tags_name_variable: tags
```

---

#### <!-- md:setting config.tags_allowed -->

<!-- md:version 9.6.0 -->
<!-- md:default none -->

插件允许检查标签是否符合预定义列表，以防止拼写错误或确保标签不是任意添加的。使用以下方法指定要允许的标签：

``` yaml
plugins:
  - tags:
      tags_allowed:
        - HTML5
        - JavaScript
        - CSS
```

如果页面引用列表中不存在的标签，插件会停止构建。页面可以通过使用[`tags`][meta.tags]元数据属性分配标签。

### 列表配置

以下设置可用于列表：

---

#### <!-- md:setting config.listings -->

<!-- md:version 9.6.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用列表。通常不需要更改此设置，因为列表完全由内联注释生成，但可以通过以下方式禁用：

``` yaml
plugins:
  - tags:
      listings: false
```

此设置自动禁用，如果启用了[`export_only`][config.export_only]。

  [exporting tags]: #export

---

#### <!-- md:setting config.listings_map -->

<!-- md:version 9.6.0 -->
<!-- md:default none -->

使用此定义列表配置，然后可以在列表中使用自定义标识符引用列表：

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

请参阅[列表部分]以获取所有可用设置的列表。

  [listings section]: #listing-configuration

---

#### <!-- md:setting config.listings_sort_by -->

<!-- md:version 9.6.0 -->
<!-- md:default `material.plugins.tags.item_title` -->

使用此设置指定自定义函数以比较列表项。默认情况下，项目按其标题排序，但可以通过以下配置更改排序标准：

=== "按项目标题排序"

    ``` yaml
    plugins:
      - tags:
          listings_sort_by: !!python/name:material.plugins.tags.item_title
    ```

=== "按项目 URL 排序"

    ``` yaml
    plugins:
      - tags:
          listings_sort_by: !!python/name:material.plugins.tags.item_url
    ```

您也可以定义自己的比较函数，该函数必须返回一个字符串或数字，表示用于排序的项目，并在[`listings_sort_by`][config.listings_sort_by]中引用它。

---

#### <!-- md:setting config.listings_sort_reverse -->

<!-- md:version 9.6.0 -->
<!-- md:default `false` -->

使用此设置反转项目比较时的顺序。默认情况下，项目按升序排序，但可以通过以下方式反转排序：

``` yaml
plugins:
  - tags:
      listings_sort_reverse: true
```

---

#### <!-- md:setting config.listings_tags_sort_by -->

<!-- md:version 9.6.0 -->
<!-- md:default `material.plugins.tags.tag_name` -->

使用此设置指定自定义函数以比较列表中的标签。默认情况下，标签比较是区分大小写的，但可以使用 `tag_name_casefold` 进行不区分大小写的比较：

``` yaml
plugins:
  - tags:
      tags_sort_by: !!python/name:material.plugins.tags.tag_name_casefold
```

您也可以定义自己的比较函数，该函数必须返回一个字符串或数字，表示用于排序的标签，并在[`tags_sort_by`][config.tags_sort_by]中引用它。

---

#### <!-- md:setting config.listings_tags_sort_reverse -->

<!-- md:version 9.6.0 -->
<!-- md:default `false` -->

使用此设置反转标签比较时的顺序。默认情况下，标签按升序排序，但可以通过以下方式反转排序：

``` yaml
plugins:
  - tags:
      tags_sort_reverse: true
```

---

#### <!-- md:setting config.listings_directive -->

<!-- md:version 9.6.0 -->
<!-- md:default `material/tags` -->

使用此设置更改插件在处理页面时查找的指令名称。如果您想使用比 `material/tags` 更短的指令，可以使用：

``` yaml
plugins:
  - tags:
      listings_directive: $tags
```

使用此设置，列表必须像这样引用：

``` html
<!-- $tags { include: [foo, bar] } -->
```

---

#### <!-- md:setting config.listings_toc -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用标签在目录中显示。如果您不希望标签在目录中显示，可以通过以下方式禁用此行为：

``` yaml
plugins:
  - tags:
      listings_toc: false
```

### 阴影标签

以下设置可用于阴影标签：

---

#### <!-- md:setting config.shadow -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `false` -->

使用此设置指定插件是否应在页面和列表中包括阴影标签，这可能对部署预览很有用：

=== "显示阴影标签"

    ``` yaml
    plugins:
      - tags:
          shadow: true
    ```

=== "隐藏阴影标签"

    ``` yaml
    plugins:
      - tags:
          shadow: false
    ```

---

#### <!-- md:setting config.shadow_on_serve -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否应在页面和列表中包括阴影标签，当[预览您的网站]时。如果您不希望在预览时包括它们，请使用：

``` yaml
plugins:
  - tags:
      shadow_on_serve: false
```

  [previewing your site]: ../creating-your-site.md#previewing-as-you-write

---

#### <!-- md:setting config.shadow_tags -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default none -->

插件允许指定预定义的阴影标签列表，这些标签可以包括和排除使用[`shadow`][config.shadow]设置构建。阴影标签必须指定为列表：

``` yaml
plugins:
  - tags:
      shadow_tags:
        - Draft
        - Internal
```

---

#### <!-- md:setting config.shadow_tags_prefix -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default none -->

使用此设置指定一个字符串，该字符串将检查为每个标签的前缀。如果标签以该字符串开头，则标记为阴影标签。一个常见做法是使用 `_` 作为前缀：

``` yaml
plugins:
  - tags:
      shadow_tags_prefix: _
```

---

#### <!-- md:setting config.shadow_tags_suffix -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default none -->

使用此设置指定一个字符串，该字符串将检查为每个标签的后缀。如果标签以该字符串结尾，则标记为阴影标签。一个选项可以是使用 `Internal` 作为后缀：


``` yaml
plugins:
  - tags:
      shadow_tags_suffix: Internal
```

### 导出

以下设置可用于导出：

---

#### <!-- md:setting config.export -->

<!-- md:sponsors -->
<!-- md:version insiders-4.49.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否在您的[`site`目录][mkdocs.site_dir]中创建 `tags.json` 文件，该文件可以被其他插件和项目消耗：

``` yaml
plugins:
  - tags:
      export: true
```

---

#### <!-- md:setting config.export_file -->

<!-- md:sponsors -->
<!-- md:version insiders-4.49.0 -->
<!-- md:default `tags.json` -->

使用此设置更改导出标签存储的文件路径。通常不需要更改此设置，但如果需要，可以使用：

``` yaml
plugins:
  - tags:
      export_file: tags.json
```

提供的路径从[`site`目录][mkdocs.site_dir]解析。

---

#### <!-- md:setting config.export_only -->

<!-- md:sponsors -->
<!-- md:version insiders-4.49.0 -->
<!-- md:default `false` -->

此设置仅出于方便提供，以通过单个设置（例如使用环境变量）禁用标签和列表的渲染，同时保持导出功能：

``` yaml
plugins:
  - tags:
      export_only: true
```

这将自动禁用[`tags`][config.tags]和[`listings`][config.listings]设置。

## 用法

### 元数据

以下属性可用：

---

#### <!-- md:setting meta.tags -->

<!-- md:version 8.2.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性将页面与一个或多个标签关联，使页面出现在生成的标签索引中。标签定义为字符串列表（允许使用空格）：

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

如果您希望防止在分配标签时意外拼写页面，可以在 `mkdocs.yml` 中使用[`tags_allowed`][config.tags_allowed]设置设置预定义的允许标签列表。

### 列表配置

列表配置控制哪些标签包含在或排除在列表中，以及列表是否仅考虑当前范围中的页面。此外，列表可以覆盖一些全局配置值。

以下设置可用：

---

#### <!-- md:setting listing.scope -->

<!-- md:version 9.6.0 -->
<!-- md:default `false` -->

此设置指定列表是否应仅考虑页面，这些页面位于页面文档的当前子部分中：

=== "内联用法"

    ``` html
    <!-- material/tags { scope: true } -->
    ```

=== "在 `mkdocs.yml` 中用法"

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

#### <!-- md:setting listing.shadow -->

<!-- md:sponsors -->
<!-- md:version insiders-4.49.0 -->
<!-- md:default computed -->

此设置指定列表是否应包括阴影标签，这允许覆盖全局[`shadow`][config.shadow]设置，按列表基础：

=== "内联用法"

    ``` html
    <!-- material/tags { shadow: true } -->
    ```

=== "在 `mkdocs.yml` 中用法"

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

#### <!-- md:setting listing.toc -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default [`listings_toc`][config.listings_toc] -->

此设置指定列表是否应在目录中渲染标签，允许覆盖全局[`listings_toc`][config.listings_toc]设置，按列表基础：

=== "内联用法"

    ``` html
    <!-- material/tags { toc: true } -->
    ```

=== "在 `mkdocs.yml` 中用法"

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

#### <!-- md:setting listing.include -->

<!-- md:version 9.6.0 -->
<!-- md:default none -->

使用此设置指定哪些标签应包含在列表中。每个包含此设置中一个标签的页面，都会列在相应的标签下：

=== "内联用法"

    ``` html
    <!-- material/tags { include: [foo, bar] } -->
    ```

=== "在 `mkdocs.yml` 中用法"

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

#### <!-- md:setting listing.exclude -->

<!-- md:version 9.6.0 -->
<!-- md:default none -->

使用此设置指定哪些标签不应包含在列表中。每个包含此设置中一个标签的页面，都会从列表中完全排除：

=== "内联用法"

    ``` html
    <!-- material/tags { exclude: [foo, bar] } -->
    ```

=== "在 `mkdocs.yml` 中用法"

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

如果此设置为空，则不包括任何标签或页面。

## 限制

标签插件的实现由于 MkDocs 架构而复杂。特别地，标签列表标记不能出现在代码块中。有关技术细节，请参考 #8114。

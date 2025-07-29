# 构建优化的网站

Material for MkDocs, by default, allows to build optimized sites that rank great
on search engines, load fast (even on slow networks), and work perfectly without
JavaScript. Additionally, the [built-in optimize plugin] adds support for
further useful automatic optimization techniques.

  [built-in optimize plugin]: #built-in-optimize-plugin

## 配置

### 内置项目插件

`sponsors`
`version insiders-4.38.0`
`plugin [projects] – built-in`
`flag experimental`

内置的项目插件允许将文档拆分为多个
不同的MkDocs项目，__同时构建它们__和
__一起为他们服务。将以下内容添加到`mkdocs.yml`中：

``` yaml
plugins:
  - projects
```

有关所有设置的列表，请参阅[插件文档]。

  [projects]: ../plugins/projects.md
  [plugin documentation]: ../plugins/projects.md

??? info "项目插件的用例"

    项目插件的理想用例是：

    - 建立多语言网站
    - 在你的文档旁边建立一个博客
    - 拆分大型代码库以获得更好的性能

    请注意，该插件目前处于实验阶段。我们会提前发布，
    这样我们就可以与用户一起改进它，使其更加完善
    当我们发现新的用例时，它非常强大。

#### 范围

`version 8.0.0`
`default none`

可能有一个用例，你想共享用户级设置，比如
所选的[调色板]或所有项目的[cookie同意]。着手做
因此，在`mkdocs.yml`中添加以下行：

``` yaml
extra:
  scope: /
```

!!! example "工作原理"

    假设你有这样的网站结构：
    ```
    .
    └── /
        ├── subsite-a/
        ├── subsite-b/
        └── subsite-c/
    ```
    默认情况下，每个站点都有自己的作用域（“/subsite-a/”、“/subite-b/”、，
    `/子网站c/`）。要修改此行为，请添加以下行
    `mkdocs.yml`：

    ``` yaml
    extra:
      scope: /
    ```

    通过将其设置为“/”，它应该允许您共享以下首选项
    在主网站和所有子网站上：

    - [Cookie consent][cookie consent]
    - [Linking of content tabs, i.e. active tab]
    - [Color palette][color palette]

  [Scope support]: https://github.com/squidfunk/mkdocs-material/releases/tag/8.0.0
  [cookie consent]: ../setup/ensuring-data-privacy.md#cookie-consent
  [Linking of content tabs, i.e. active tab]: ../reference/content-tabs.md
  [color palette]: ../setup/changing-the-colors.md#color-palette

### 内置优化插件

`sponsors`
`version insiders-4.29.0`
`plugin [optimize] – built-in`
`flag experimental`

内置的优化插件会自动识别和优化所有媒体
使用压缩和转换技术将文件作为构建的一部分。添加
将以下行添加到`mkdocs.yml`：

``` yaml
plugins:
  - optimize
```

有关所有设置的列表，请参阅[插件文档][优化]。

  [optimize]: ../plugins/optimize.md

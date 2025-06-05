# 内置插件

MkDocs的材料最初是[MkDocs][MkDocs]的主题，但后来
发展成为一个用于构建和维护文档的成熟框架。
主题仍然是该项目的核心，但现在伴随着
越来越多的互补内置插件。

我们努力使这些插件尽可能模块化和通用化，以便它们
可用于各种各样的项目和用例。通过提供有用的
默认设置，我们还试图使它们尽可能易于使用，以便
你可以快速开始，稍后调整他们的设置
在开发内置插件时，我们始终坚持以下设计原则：

- **模块化：**内置插件设计为模块化，因此它们可以
  易于组合以实现复杂的管道。例如
  [离线]、[优化]和[隐私]插件可以一起使用来构建
  真正的[离线功能文档]。

- **互操作性：**内置插件的设计与
  可能，因此它们可以与其他插件结合使用，包括
  第三方插件。我们努力使其易于与庞大的
  围绕[MkDocs][MkDocs]发展起来的生态系统。

- **性能：**内置插件的设计速度和
  尽可能提高内存效率，这样它们就不会不必要地变慢
  建筑。这对于具有以下功能的大型文档项目尤为重要
  数千页。

  [mkdocs]: https://www.mkdocs.org/
  [design principles]: ../design-principles.md
  [offline-capable documentation]: ../setup/building-for-offline-usage.md

## Categories

### 管理

以下插件极大地改善了工作时的创作体验
通过提供更好的管理能力，从
管理插件、多个项目和元数据，以创建
错误报告的最小复制：

<div class="grid cards" markdown>

-   :material-format-list-group: &nbsp; __[Built-in group plugin][group]__

    ---

    组插件允许将插件有条件地分组到逻辑单元中
    使用以下命令为特定环境启用或禁用它们
    [环境变量][mkdocs.env]。

    ---

    __Optimal management of plugins when building in different environments__

-   :material-file-tree: &nbsp; __[Built-in meta plugin][meta]__

    ---

    元插件使管理所有人的元数据（前端内容）变得容易
    文件夹中的页面，因此某些页面子集使用特定的标签或
    自定义模板。

    ---

    __Simpler organization, categorization and management of metadata__

-   :material-folder-open: &nbsp; __[Built-in projects plugin][projects]__

    ---

    项目插件允许将您的主项目拆分为多个不同的
    项目，同时构建它们并将它们作为一个整体一起预览。

    ---

    __Connect multiple projects together, and build them separately or as one__

-   :material-information: &nbsp; __[Built-in info plugin][info]__

    ---

    info插件是一个小而有用的实用程序，有助于创建
    自包含的最小复制，因此我们维护人员可以修复报告
    bug更快。

    ---

    __您的错误报告质量最高，因此我们可以尽快修复它们
    可能的__


</div>

  [group]: group.md
  [info]: info.md
  [meta]: meta.md
  [projects]: projects.md

### 优化

以下插件旨在帮助您构建优化的文档，
通过更快的加载时间，更好地让用户更容易访问它
搜索引擎排名、社交媒体上精美的预览图片和GDPR
符合几行配置：

<div class="grid cards" markdown>

-   :material-share-circle: &nbsp; __[Built-in social plugin][social]__

    ---

    社交插件会自动生成美观且可定制的内容
    文档每一页的社交卡片，以预览形式显示在
    社会化媒体。

    ---

    __当在社交媒体上分享时，指向您网站的链接会呈现美丽的社交卡片
    媒体__

-   :material-rabbit: &nbsp; __[Built-in optimize plugin][optimize]__

    ---

    优化插件自动识别并优化所有媒体文件
    通过使用压缩和转换在项目中引用
    技术。

    ---

    __Your site loads faster as smaller images are served to your users__

-   :material-shield-account: &nbsp; __[Built-in privacy plugin][privacy]__

    ---

    隐私插件自动下载外部资产，方便
    自托管，允许符合GDPR的单行
    配置。

    ---

    __Your documentation can be made GDPR compliant with minimal effort__

-   :material-connection: &nbsp; __[Built-in offline plugin][offline]__

    ---

    离线插件增加了对构建[离线功能文档]的支持，
    因此，您可以将[`site`目录][mkdocs.site_dir]作为`.zip分发`
    可以下载的文件。

    ---

    __Your documentation can work without connectivity to the internet__

</div>

  [offline]: offline.md
  [optimize]: optimize.md
  [privacy]: privacy.md
  [social]: social.md

### 所容纳之物

以下插件旨在帮助您设置博客，提供搜索
为用户提供功能，为页面和帖子添加标签，并使用相同的功能
文档特定部分的排版功能与
主要内容：

<div class="grid cards" markdown>

-   :material-newspaper-variant-outline: &nbsp; __[Built-in blog plugin][blog]__

    ---

    博客插件为Material for添加了一流的博客支持
    MkDocs，既可以作为文档的侧车，也可以作为独立的
    安装。

    ---

    __Your blog is built with the same powerful engine as your documentation__

-   :material-magnify: &nbsp; __[Built-in search plugin][search]__

    ---

    搜索插件在标题中添加了一个搜索栏，允许用户搜索
    整个文档，这样他们更容易找到它们是什么
    寻找。

    ---

    __Your documentation is searchable without any external services, even
    offline__

-   :material-tag-text: &nbsp; __[Built-in tags plugin][tags]__

    ---

    标签插件添加了对带有标签的页面进行分类的一流支持，
    添加对相关页面进行分组的功能，以提高对
    相关内容。

    ---

    __Your pages are categorized with tags, yielding additional context__

-   :material-format-title: &nbsp; __[Built-in typeset plugin][typeset]__

    ---

    排版插件允许保留标题的丰富呈现
    以及导航和目录中的标题。

    ---

    __Sidebars preserve the same formatting as section titles in pages__

</div>

  [blog]: blog.md
  [search]: search.md
  [tags]: tags.md
  [typeset]: typeset.md

## 结构

### 多个实例

几个内置插件支持多个实例，这意味着
它们可以在同一配置文件中多次使用，从而允许
为项目的不同部分微调行为。目前
以下插件支持多个实例：

<div class="mdx-columns" markdown>

- [Built-in blog plugin][blog]
- [Built-in group plugin][group]
- [Built-in optimize plugin][optimize]
- [Built-in privacy plugin][privacy]
- [Built-in social plugin][social]

</div>

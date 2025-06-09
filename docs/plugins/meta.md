---
title: Built-in meta plugin
icon: material/file-tree
---

# 内置元插件

元插件解决了为所有人设置元数据（前台）的问题
文件夹中的页面，即项目的一个子部分，尤其是
有助于确保页面的某个子集具有特定的标签，并使用
或者归因于作者。

## Objective

### 工作原理

该插件扫描[`docs`目录][mkdocs.docs_dir]中的`.meta.yml`文件，
并递归地将这些文件的内容与元数据（front
内容）包含在同一文件夹和所有子文件夹中的所有页面。
例如，如果您想将标签<span class=“md tag”>示例</span>添加到
多个页面，使用：

``` yaml title=".meta.yml"
tags:
  - Example
```

现在，给定以下目录布局，如果将文件存储在文件夹中
名为“example”的文件夹中的所有页面都会收到标签，而所有页面
文件夹外部不受影响：

``` { .sh .no-copy hl_lines="4-8" }
.
├─ docs/
│  ├─ ...
│  ├─ example/
│  │  ├─ .meta.yml
│  │  ├─ a.md
│  │  ├─ ...
│  │  └─ z.md
│  └─ ...
└─ mkdocs.yml
```

当组合元数据时，列表和字典会递归合并
意味着您可以将值附加到列表中，并在列表中添加或设置特定属性
任意级别的词典。

### 何时使用

虽然插件本身除了添加和
合并元数据后，它是许多其他内置元数据的完美伴侣
Material for MkDocs提供的插件。一些最强大的组合
元插件和其他内置插件包括：

<div class="grid cards" markdown>

-   :material-share-circle: &nbsp; __[Built-in social plugin][social]__

    ---

    The meta plugin can be used to [change the layout] for social cards or
    [change specific layout options] like [background] or [color]
    for a subset of pages.

    ``` yaml title=".meta.yml"
    social:
      cards_layout: default/variant
    ```

-   :material-newspaper-variant-outline: &nbsp; __[Built-in blog plugin][blog]__

    ---

    The meta plugin allows to automatically associate blog posts with specific
    [authors] and [categories], ensuring that blog posts are always correctly
    annotated.

    ``` yaml title=".meta.yml"
    authors:
      - squidfunk
    ```

-   :material-tag-text: &nbsp; __[Built-in tags plugin][tags]__

    ---

    The meta plugin makes it possible to ensure that subsections of your
    project are annotated with [specific tags], so they can't be forgotten when
    adding pages.

    ``` yaml title=".meta.yml"
    tags:
      - Example
    ```

-   :material-magnify: &nbsp; __[Built-in search plugin][search]__

    ---

    The meta plugin makes it easy to [boost] specific sections in search results
    or to [exclude] them entirely from being indexed, giving more granular
    control over search.

    ``` yaml title=".meta.yml"
    search:
      exclude: true
    ```

</div>

  [social]: social.md
  [change the layout]: social.md#meta.social.cards_layout
  [change specific layout options]: social.md#meta.social.cards_layout_options
  [background]: social.md#option.background_color
  [color]: social.md#option.color
  [blog]: blog.md
  [authors]: blog.md#meta.authors
  [categories]: blog.md#meta.categories
  [tags]: tags.md
  [specific tags]: tags.md#meta.tags
  [search]: search.md
  [exclude]: search.md#meta.search.exclude
  [boost]: search.md#meta.search.boost

## 配置

<!-- md:version 9.6.0 -->
<!-- md:plugin [meta] – built-in -->
<!-- md:flag experimental -->

与所有[内置插件]一样，开始使用元插件是
直截了当。只需将以下行添加到`mkdocs.yml`中，然后开始
一次为多个页面应用元数据：

``` yaml
plugins:
  - meta
```

元插件包含在MkDocs的Material中，不需要
安装。

  [meta]: meta.md
  [built-in plugins]: index.md

### 一般的

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:version 9.6.0 -->
<!-- md:default `true` -->

使用此设置可在[构建项目]时启用或禁用插件。
通常不需要指定此设置，但如果要禁用
插件，使用：

``` yaml
plugins:
  - meta:
      enabled: false
```

  [building your project]: ../creating-your-site.md#building-your-site

### 元文件

以下设置可用于元文件：

---

#### <!-- md:setting config.meta_file -->

<!-- md:version 9.6.0 -->
<!-- md:default `.meta.yml` -->

使用此设置更改插件在以下情况下将查找的元文件名
扫描[文档目录][mkdocs.docs-dir]。通常没有必要
更改此设置，但如果要更改，请使用：

``` yaml
plugins:
  - meta:
      meta_file: .meta.yml
```

提供的路径是从[`docs`目录][mkdocs.docs_dir]解析的
递归。

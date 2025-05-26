# 参考

Material for MkDocs 包含许多出色的功能，使技术写作成为一种愉快的活动。本文档的这一部分解释了如何设置页面，并展示了可以直接在 Markdown 文件中使用的所有可用示例。

## 配置

## 使用方法

### 设置页面 `title`

每个页面都有一个指定的标题，用于导航侧边栏、[社交卡片]和其他地方。虽然 MkDocs 尝试通过[四步流程]自动确定页面的标题，但也可以通过前置元数据 `title` 属性显式设置标题：

``` yaml
---
title: Lorem ipsum dolor sit amet # (1)!
---

# 页面标题
...
```

1.  这一行将生成的页面的 HTML 文档 [`head`][head] 中的 [`title`][title] 设置为给定值。请注意，通过 [`site_name`][site_name] 设置的站点标题会附加一个破折号。

  [social cards]: ../setup/setting-up-social-cards.md
  [four step process]: https://www.mkdocs.org/user-guide/writing-your-docs/#meta-data
  [title]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/title
  [head]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head
  [site_name]: https://www.mkdocs.org/user-guide/configuration/#site_name

### 设置页面 `description`

Markdown 文件可以包含一个描述，该描述会添加到页面的 `meta` 标签中，也用于[社交卡片]。如果作者没有为 Markdown 文件明确定义描述，最好在 `mkdocs.yml` 中设置一个 [`site_description`][site_description] 作为后备值：

``` yaml
---
description: Nullam urna elit, malesuada eget finibus ut, ac tortor. # (1)!
---

# 页面标题
...
```

1.  这一行将当前页面的文档 `head` 中包含描述的 `meta` 标签设置为提供的值。

  [site_description]: https://www.mkdocs.org/user-guide/configuration/#site_description

### 设置页面 `icon`

<!-- md:version 9.2.0 -->
<!-- md:flag experimental -->

可以为每个页面分配一个图标，然后将其作为导航侧边栏的一部分渲染，如果启用的话，也可以作为[导航标签]的一部分。使用前置元数据 `icon` 属性引用图标，在 Markdown 文件顶部添加以下行：

``` yaml
---
icon: material/emoticon-happy # (1)!
---

# 页面标题
...
```

1.  输入几个关键词，使用我们的[图标搜索]找到完美的图标，然后点击短代码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="搜索图标" data-mdx-component="iconsearch-query" value="emoticon happy" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

  [Insiders]: ../insiders/index.md
  [icon search]: icons-emojis.md#search
  [navigation tabs]: ../setup/setting-up-navigation.md#navigation-tabs

### 设置页面 `status`

<!-- md:version 9.2.0 -->
<!-- md:flag experimental -->
<!-- md:example page-status -->

可以为每个页面分配一个状态，然后将其作为导航侧边栏的一部分显示。首先，通过将以下内容添加到 `mkdocs.yml` 来将状态标识符与描述关联：

``` yaml
extra:
  status:
    <identifier>: <description> # (1)!
```

1.  标识符只能包含字母数字字符，以及破折号和下划线。例如，如果您有一个状态 `Recently added`，您可以设置 `new` 作为标识符：

    ``` yaml
    extra:
      status:
        new: Recently added
    ```

现在可以通过前置元数据 `status` 属性设置页面状态。例如，您可以通过在 Markdown 文件顶部添加以下行来将页面标记为 `new`：

``` yaml
---
status: new
---

# 页面标题
...
```

以下状态标识符已经定义：

- :material-alert-decagram: – `new`
- :material-trash-can: – `deprecated`

您可以以这种方式定义自定义页面状态，但如果您希望它使用默认图标以外的图标，您还需要在 `extra.css` 中配置它。我们有一个[自定义页面状态示例]可以帮助您入门。

[example for a custom page status]: https://mkdocs-material.github.io/examples/page-status/

### 设置页面 `subtitle`

<!-- md:version 9.6.0 -->
<!-- md:flag experimental -->

每个页面都可以定义一个副标题，然后通过使用前置元数据 `subtitle` 属性将其作为导航侧边栏的一部分渲染在标题下方，添加以下行：

``` yaml
---
subtitle: Nullam urna elit, malesuada eget finibus ut, ac tortor
---

# 页面标题
...
```

### 设置页面 `template`

如果您使用[主题扩展]并在 `overrides` 目录中创建了新的页面模板，您可以为特定页面启用它。在 Markdown 文件顶部添加以下行：

``` yaml
---
template: custom.html
---

# 页面标题
...
```

??? question "如何为整个文件夹设置页面模板？"

    借助[内置元数据插件]，您可以通过在相应文件夹中创建 `.meta.yml` 文件来为整个部分和所有嵌套页面设置自定义模板，内容如下：

    ``` yaml
    template: custom.html
    ```

  [theme extension]: ../customization.md#extending-the-theme
  [built-in meta plugin]: ../plugins/meta.md

## 自定义

### 在模板中使用元数据

#### :material-check-all: 在所有页面上

为了向文档添加自定义 `meta` 标签，您可以[扩展主题][theme extension]并[覆盖 `extrahead` 块][overriding blocks]，例如，通过 `robots` 属性为搜索引擎添加索引策略：

``` html
{% extends "base.html" %}

{% block extrahead %}
  <meta name="robots" content="noindex, nofollow" />
{% endblock %}
```

  [overriding blocks]: ../customization.md#overriding-blocks

#### :material-check: 在单个页面上

如果您想在单个页面上设置 `meta` 标签，或者想为不同页面设置不同的值，您可以在模板覆盖中使用 `page.meta` 对象，例如：

``` html
{% extends "base.html" %}

{% block extrahead %}
  {% if page and page.meta and page.meta.robots %}
    <meta name="robots" content="{{ page.meta.robots }}" />
  {% else %}
    <meta name="robots" content="index, follow" />
  {% endif %}
{% endblock %}
```

您现在可以像 [`title`][title] 和 [`description`][description] 一样使用 `robots` 来设置值。请注意，在这种情况下，模板定义了一个 `else` 分支，如果没有给出值，它将设置一个默认值。

  [title]: #setting-the-page-title
  [description]: #setting-the-page-description

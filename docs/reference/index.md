# 参考

MkDocs的材料包含了许多强大的功能，使技术
写一个快乐的活动。本节文档解释了如何设置
一个页面，展示所有可以直接从
在Markdown文件中。

## 配置

## 使用

### 设置页面标题`

每个页面都有一个指定的标题，用于导航侧边栏，用于
[社交卡]和其他地方。而MkDocs试图自动
在[四步过程]中确定页面的标题，标题也可以是
用front matter的`title`属性显式设置：

``` yaml
---
title: Lorem ipsum dolor sit amet # (1)!
---

# Page title
...
```

1.  此行在HTML文档的内部设置[`title][title]
    将生成的页面的['head][head]设置为给定值。请注意
    站点标题通过[`site_name][site_name]设置，并附加一个
    冲撞

  [social cards]: ../setup/setting-up-social-cards.md
  [four step process]: https://www.mkdocs.org/user-guide/writing-your-docs/#meta-data
  [title]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/title
  [head]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head
  [site_name]: https://www.mkdocs.org/user-guide/configuration/#site_name

### 设置页面描述`

Markdown文件可以包含添加到以下“meta”标签中的描述
页面，也用于[社交卡]。设定一个好主意
如果满足以下条件，则将`mkdocs.yml`中的['site_description][site_description]作为回退值
作者没有明确定义Markdown文件的描述：

``` yaml
---
description: Nullam urna elit, malesuada eget finibus ut, ac tortor. # (1)!
---

# Page title
...
```

1.  此行设置包含描述的“meta”标签
    将当前页面的文档“head”设置为提供的值。

  [site_description]: https://www.mkdocs.org/user-guide/configuration/#site_description

### 设置页面图标`

<!-- md:version 9.2.0 -->
<!-- md:flag experimental -->

可以为每个页面分配一个图标，然后将其呈现为
导航侧边栏以及[导航选项卡]（如果启用）。使用正面
matter `icon`属性引用图标，在
Markdown文件的顶部：

``` yaml
---
icon: material/emoticon-happy # (1)!
---

# Page title
...
```

1.  输入几个关键字，使用我们的[图标搜索]找到完美的图标，然后
    单击短代码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="emoticon happy" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

  [Insiders]: ../insiders/index.md
  [icon search]: icons-emojis.md#_2
  [navigation tabs]: ../setup/setting-up-navigation.md#_9

### 设置页面状态`

<!-- md:version 9.2.0 -->
<!-- md:flag experimental -->
<!-- md:example page-status -->

可以为每个页面分配一个状态，然后将其显示为
导航侧边栏。首先，通过以下方式将状态标识符与描述相关联
将以下内容添加到`mkdocs.yml`中：

``` yaml
extra:
  status:
    <identifier>: <description> # (1)!
```

1.  标识符只能包含字母数字字符以及破折号
    和下划线。例如，如果您的状态为“最近添加”，则可以
    将“new”设置为标识符：

    ``` yaml
    extra:
      status:
        new: Recently added
    ```

现在可以使用front matter“status”属性设置页面状态。For
例如，您可以在页面顶部用以下行将页面标记为“新”
Markdown文件：

``` yaml
---
status: new
---

# Page title
...
```

已定义以下状态标识符：

- :material-alert-decagram: – `new`
- :material-trash-can: – `deprecated`

您可以通过这种方式定义自定义页面状态，但如果您想这样做
您还需要配置默认图标以外的图标
在你的`extra.css`中。我们有一个[自定义示例
页面状态]以帮助您开始。

[example for a custom page status]: https://mkdocs-material.github.io/examples/page-status/

### 设置页面的副标题`

<!-- md:version 9.6.0 -->
<!-- md:flag experimental -->

每页都可以定义一个副标题，然后将其作为标题的一部分呈现在标题下方
通过使用前体“字幕”属性，对导航侧边栏进行修改，以及
添加以下行：

``` yaml
---
subtitle: Nullam urna elit, malesuada eget finibus ut, ac tortor
---

# Page title
...
```

### 设置页面模板`

如果您使用[主题扩展]并在
`override目录，您可以为特定页面启用它。添加以下内容
Markdown文件顶部的行：

``` yaml
---
template: custom.html
---

# Page title
...
```

??? question "如何为整个文件夹设置页面模板？"

    借助[内置元插件]，您可以设置自定义模板
    对于整个部分和所有嵌套页面，通过创建一个`.meta.yml`文件
    在相应的文件夹中，包含以下内容：

    ``` yaml
    template: custom.html
    ```

  [theme extension]: ../customization.md#extending-the-theme
  [built-in meta plugin]: ../plugins/meta.md

## 自定义

### 在模板中使用元数据

#### :material-check-all: 在所有页面上

为了在文档中添加自定义的“meta”标签，您可以[扩展主题
][主题扩展]和[覆盖'extrahead'块][覆盖块]，
例如，通过“robots”属性为搜索引擎添加索引策略：

``` html
{% extends "base.html" %}

{% block extrahead %}
  <meta name="robots" content="noindex, nofollow" />
{% endblock %}
```

  [overriding blocks]: ../customization.md#overriding-blocks

#### :material-check: 在一个页面上

如果你想在一个页面上设置一个“meta”标签，或者想设置不同的
对于不同页面的值，您可以在您的
模板覆盖，例如：

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

你现在可以像[`title][title]一样使用`robots`
[`description][description]来设置值。请注意，在这种情况下
模板定义了一个“else”分支，如果没有给出，它将设置默认值。

  [title]: #setting-the-page-title
  [description]: #setting-the-page-description

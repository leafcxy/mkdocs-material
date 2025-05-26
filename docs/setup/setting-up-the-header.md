# 设置页眉

Material for MkDocs 的页眉可以自定义，支持显示公告栏、滚动时自动隐藏，并提供进一步的配置选项。它还包括[搜索栏]和显示项目[git 仓库]的位置，详见相关专门指南。

  [搜索栏]: setting-up-site-search.md
  [git 仓库]: adding-a-git-repository.md

## 配置

### 自动隐藏

<!-- md:version 6.2.0 -->
<!-- md:feature -->

启用自动隐藏后，当用户滚动超过某个阈值时，页眉会自动隐藏，为内容留出更多空间。在 `mkdocs.yml` 中添加如下内容：

``` yaml
theme:
  features:
    - header.autohide
```

### 公告栏

<!-- md:version 5.0.0 -->
<!-- md:flag customization -->

Material for MkDocs 包含一个公告栏，非常适合向用户显示项目新闻或其他重要信息。当用户滚动过页眉时，公告栏会自动消失。要添加公告栏，请[扩展主题]并[覆盖 `announce` 块][覆盖块]，默认内容为空：

``` html
{% extends "base.html" %}

{% block announce %}
  <!-- 在此处添加公告内容，可包含任意 HTML -->
{% endblock %}
```

  [扩展主题]: ../customization.md#extending-the-theme
  [覆盖块]: ../customization.md#overriding-blocks

#### 标记为已读

<!-- md:version 8.4.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

为临时公告栏添加"标记为已读"按钮，用户点击后可关闭当前公告。在 `mkdocs.yml` 中添加如下内容：

``` yaml
theme:
  features:
    - announce.dismiss
```

用户点击按钮后，当前公告会被关闭，直到公告内容发生变化才会再次显示。这一切都已自动处理。

[滚动到本页顶部][top]查看实际效果。

  [top]: #

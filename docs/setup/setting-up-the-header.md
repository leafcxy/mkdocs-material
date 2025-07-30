# 设置标题

Material for MkDocs标题可以定制，以显示公告栏
滚动时消失，并提供一些进一步配置的选项。
它还包括[search bar]和一个显示项目的位置
[git repository]，如这些专门指南中所解释的。

  [search bar]: setting-up-site-search.md
  [git repository]: adding-a-git-repository.md

## 配置

### 自动隐藏

`version 6.2.0`
`feature`

启用自动隐藏后，当
用户滚动超过某个阈值，为内容留下更多空间。添加
将以下行转换为`mkdocs.yml`：

``` yaml
theme:
  features:
    - header.autohide
```

### 公告栏

`version 5.0.0`
`flag customization`

MkDocs的材料包括一个公告栏，这是一个完美的地方
向用户显示项目新闻或其他重要信息。当用户
滚动过标题，栏将自动消失。为了添加
公告栏，[extend the theme]和[override the `announce`
block][overriding blocks]，默认为空：

``` html
{% extends "base.html" %}

{% block announce %}
  <!-- Add announcement here, including arbitrary HTML -->
{% endblock %}
```

  [extend the theme]: ../customization.md
  [overriding blocks]: ../customization.md#overriding-blocks

#### 标记为已读

`version 8.4.0`
`feature`
`flag experimental`

为了呈现可标记为已阅读的临时公告
用户，可以包括一个按钮来取消当前的公告。添加
将以下行转换为`mkdocs.yml`：

``` yaml
theme:
  features:
    - announce.dismiss
```

当用户点击按钮时，当前公告将被取消，不会
再次显示，直到公告的内容发生变化。这已经处理好了
自动。

[Scroll to the top of this page][top] to see it in action.

  [top]: #

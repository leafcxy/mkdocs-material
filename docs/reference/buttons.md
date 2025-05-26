---
icon: material/button-cursor
---

# 按钮

Material for MkDocs 为主要和次要按钮提供了专用样式，可以添加到任何链接、`label` 或 `button` 元素中。这对于带有专门_号召性用语_的文档或落地页特别有用。

## 配置

此配置允许使用简单的语法为所有内联和块级元素添加属性，将任何链接转换为按钮。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - attr_list
```

查看更多配置选项：

- [Attribute Lists]

  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists

## 使用方法

### 添加按钮

要将链接渲染为按钮，在其后添加花括号并添加 `.md-button` 类选择器。如果激活，按钮将接收选定的[主色]和[强调色]。

``` markdown title="按钮"
[订阅我们的新闻通讯](#){ .md-button }
```

<div class="result" markdown>

[订阅我们的新闻通讯][Demo]{ .md-button }

</div>

  [primary color]: ../setup/changing-the-colors.md#primary-color
  [accent color]: ../setup/changing-the-colors.md#accent-color
  [Demo]: javascript:alert$.next("Demo")

### 添加主要按钮

如果您想显示填充的主要按钮（如 Material for MkDocs 的[落地页]），请同时添加 `.md-button` 和 `.md-button--primary` CSS 类选择器。

``` markdown title="主要按钮"
[订阅我们的新闻通讯](#){ .md-button .md-button--primary }
```

<div class="result" markdown>

[订阅我们的新闻通讯][Demo]{ .md-button .md-button--primary }

</div>

  [landing page]: ../index.md

### 添加图标按钮

当然，可以通过使用[图标语法]和任何有效的图标短代码，为所有类型的按钮添加图标，这些图标可以通过我们的[图标搜索]轻松找到。

``` markdown title="带图标的按钮"
[发送 :fontawesome-solid-paper-plane:](#){ .md-button }
```

<div class="result" markdown>

[发送 :fontawesome-solid-paper-plane:][Demo]{ .md-button }

</div>

  [icon syntax]: icons-emojis.md#using-icons
  [icon search]: icons-emojis.md#search

# 设置版本控制

Material for MkDocs使部署项目的多个版本变得容易
通过与添加这些功能的外部实用程序集成来记录文档
MkDocs，即[mike]。部署新版本时，您的旧版本
文档保持不变。

  [mike]: https://github.com/jimporter/mike

## 配置

### 版本控制

<!-- md:version 7.0.0 -->
<!-- md:utility [mike] -->
<!-- md:demo example-versioning -->

[mike]使部署项目文档的多个版本变得容易。
它与Material for MkDocs原生集成，可以通过以下方式启用
`mkdocs.yml`：

``` yaml
extra:
  version:
    provider: mike
```

这将在标头中呈现一个版本选择器：

<figure markdown>

[![Version selector preview]][Version selector preview]

  <figcaption markdown>

查看版本控制示例以了解其实际应用情况——
[mkdocs-material.github.io/example-versioning][version example]

  </figcaption>
</figure>

!!! quote "[Why use mike?]"

    mike的核心思想是，一旦你为某个项目生成了文档
    特定版本，您永远不需要再次触摸该版本。这
    这意味着您永远不必担心破坏MkDocs中的更改，因为您的
    旧文档（使用旧版本的MkDocs构建）已经生成
    坐在你的gh-pages分店。

    虽然mike很灵活，但它是围绕将您的文档放在一个
    `<major>。<minor>`目录，带有可选别名（例如`latest`或`dev`）
    特别值得注意的版本。这使得创建永久链接变得容易
    无论你想引导人们访问哪个版本的文档。

  [Version selector preview]: ../assets/screenshots/versioning.png
  [version example]: https://mkdocs-material.github.io/example-versioning/
  [Why use mike?]: https://github.com/jimporter/mike#why-use-mike

### 切换版本时保持一致

当用户在版本选择器中选择一个版本时，他们通常希望
到与他们之前查看的页面对应的页面。材料Material for
MkDocs默认实现了这种行为，但有一些注意事项：

- 必须在`mkdocs.yml`中正确设置[`site_url][mkdocs.site_url]。
  请参阅[“发布新版本”]（#Publishing-a-new-version）部分
  举个例子。
- 重定向是通过JavaScript进行的，无法知道你在哪个页面
  将提前重定向到。

### 版本警告

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如果您正在使用版本控制，您可能希望在用户
访问除最新版本之外的任何其他版本。使用[主题扩展]，
你可以[覆盖过时的块][覆盖块]：

``` html
{% extends "base.html" %}

{% block outdated %}
  You're not viewing the latest version.
  <a href="{{ '../' ~ base_url }}"> <!-- (1)! -->
    <strong>Click here to go to latest.</strong>
  </a>
{% endblock %}
```

1.  给定`href`属性的此值，链接将始终重定向到
    您网站的根目录，然后将重定向到最新版本。这
    确保您网站的旧版本不依赖于特定的别名，
    例如“latest”，以便以后更改别名而不会中断
    早期版本。

这将在标题上方显示版本警告：

[![Version warning preview]][Version warning preview]

默认版本由“最新”别名标识。如果你想设置
另一个别名作为最新版本，例如“stable”，添加以下行
转到`mkdocs.yml`：

``` yaml
extra:
  version:
    default: stable # (1)!
```

1.  您还可以将多个别名定义为默认版本，例如`stable`
    以及“发展”。

    ``` yaml
    extra:
      version:
        default:
          - stable
          - development
    ```

    现在，每个具有“稳定”和“开发”别名的版本都不会
    显示版本警告。

确保一个别名与[默认版本]匹配，因为这是用户所在的位置
重定向到。

  [theme extension]: ../customization.md#extending-the-theme
  [overriding blocks]: ../customization.md#overriding-blocks
  [Version warning preview]: ../assets/screenshots/version-warning.png
  [default version]: #setting-a-default-version

### 版本别名

<!-- md:version 9.5.23 -->
<!-- md:default `false` -->

如果您正在使用别名进行版本控制，并希望显示版本别名
除了版本号，您还可以通过设置别名来启用此功能`
选择“true”：

``` yaml
extra:
  version:
    alias: true
```

## 使用

虽然本节概述了发布新版本的基本工作流程，
最好查阅 [mike's documentation][mike]，让自己熟悉一下
它的力学。

### 发布新版本

如果要发布项目文档的新版本，请选择
版本标识符，并使用以下命令将别名集更新为默认版本：

```
mike deploy --push --update-aliases 0.1 latest
```

请注意，每个版本都将部署为“site_url”的子目录，
您应该明确设置。例如，如果您的`mkdocs.yml`包含：

``` yaml
site_url: 'https://docs.example.com/'  # Trailing slash is recommended
```

文档将发布到以下网址：

- _docs.example.com/0.1/_
- _docs.example.com/0.2/_
- ...

### 设置默认版本

当从[mike]开始时，一个好主意是将别名设置为默认版本，
例如“最新”，发布新版本时，始终将别名更新为
指向最新版本：

```
mike set-default --push latest
```

发布新版本时，[mike]将在根目录中创建重定向
将项目文档转换为与别名关联的版本：

_docs.example.com_ :octicons-arrow-right-24: _docs.example.com/0.1_

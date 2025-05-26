# 设置版本控制

Material for MkDocs 为项目文档提供了版本控制支持，允许用户在不同版本之间切换。这对于维护多个版本的文档非常有用，特别是当您有多个版本的软件或服务时。

## 配置

### 版本选择器

<!-- md:version 7.0.0 -->
<!-- md:feature -->

版本选择器允许用户在文档的不同版本之间切换。要启用此功能，请在 `mkdocs.yml` 中添加以下内容：

``` yaml
theme:
  features:
    - navigation.version
```

### 版本配置

<!-- md:version 7.0.0 -->
<!-- md:default none -->

在 `mkdocs.yml` 中配置版本信息，以便在版本选择器中显示：

``` yaml
extra:
  version:
    provider: mike
```

### 版本提供者

<!-- md:version 7.0.0 -->
<!-- md:default none -->

Material for MkDocs 支持多种版本提供者，您可以根据需要选择：

- `mike`: 使用 [mike] 工具管理版本。
- `custom`: 自定义版本提供者，您需要手动管理版本。

  [mike]: https://github.com/jimporter/mike

### 版本选择器配置

<!-- md:version 7.0.0 -->
<!-- md:default none -->

您可以通过 `theme.version` 配置版本选择器的外观和行为：

``` yaml
theme:
  version:
    provider: mike
    default: latest
    selector: true
```

- `provider`: 版本提供者，可以是 `mike` 或 `custom`。
- `default`: 默认版本，例如 `latest`。
- `selector`: 是否显示版本选择器。

## 使用

### 添加版本

使用 [mike] 工具添加新版本：

``` sh
mike deploy <version> <alias>
```

例如，添加版本 `1.0.0` 并将其别名为 `latest`：

``` sh
mike deploy 1.0.0 latest
```

### 切换版本

用户可以通过版本选择器在不同版本之间切换。版本选择器会显示在导航栏中，用户可以选择所需的版本。

## 自定义

### 自定义版本选择器

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如需自定义和覆盖[版本选择器]，请[扩展主题]并[覆盖 `version.html` partial][覆盖 partials]，该 partial 通常包含 `mkdocs.yml` 中设置的 version 属性。

  [版本选择器]: #version-selector
  [扩展主题]: ../customization.md#extending-the-theme
  [覆盖 partials]: ../customization.md#overriding-partials

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
    例如"latest"，以便以后更改别名而不会中断
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

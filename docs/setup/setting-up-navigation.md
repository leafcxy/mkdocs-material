# 设置导航

Material for MkDocs 提供了灵活的导航功能，允许您自定义文档的导航结构。通过配置导航，您可以组织文档内容，使其更易于访问和浏览。

## 配置

### 导航结构

<!-- md:version 0.1.0 -->
<!-- md:default none -->

在 `mkdocs.yml` 中配置导航结构，以定义文档的层次结构：

``` yaml
nav:
  - Home: index.md
  - Getting Started:
    - Installation: getting-started/installation.md
    - Configuration: getting-started/configuration.md
  - User Guide:
    - Basic Usage: user-guide/basic-usage.md
    - Advanced Features: user-guide/advanced-features.md
```

- `nav`: 定义文档的导航结构，每个条目可以是一个页面或一个包含子页面的部分。

### 导航图标

<!-- md:version 0.1.0 -->
<!-- md:default none -->

您可以为导航项添加图标，以增强视觉效果。在 `mkdocs.yml` 中配置图标：

``` yaml
nav:
  - Home: index.md
    icon: material/home
  - Getting Started:
    icon: material/rocket
    - Installation: getting-started/installation.md
    - Configuration: getting-started/configuration.md
```

- `icon`: 为导航项指定图标，使用 Material Design 图标库中的图标名称。

## 使用

### 添加导航项

在 `mkdocs.yml` 中添加新的导航项，以扩展文档的导航结构。您可以根据需要添加页面和子页面。

### 查看导航

一旦配置了导航结构，您可以通过导航栏访问文档的不同部分。导航栏通常显示在页面的顶部或侧边，用户可以通过点击导航项快速跳转到相应的页面。

## 自定义

### 自定义导航

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如需自定义和覆盖[导航配置]，请[扩展主题]并[覆盖 `nav.html` partial][覆盖 partials]，该 partial 通常包含 `mkdocs.yml` 中设置的 nav 属性。

  [导航配置]: #navigation-configuration
  [扩展主题]: ../customization.md#extending-the-theme
  [覆盖 partials]: ../customization.md#overriding-partials

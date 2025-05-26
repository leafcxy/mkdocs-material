# 更改徽标和图标

Material for MkDocs 允许您自定义文档的徽标和图标，以增强品牌识别和用户体验。通过配置徽标和图标，您可以使文档更具个性化和吸引力。

## 配置

### 徽标

<!-- md:version 0.1.0 -->
<!-- md:default none -->

在 `mkdocs.yml` 中配置徽标，以替换默认的 Material for MkDocs 徽标：

``` yaml
theme:
  logo: assets/logo.svg
  icon: assets/icon.svg
```

- `logo`: 指定徽标的图像文件路径。
- `icon`: 指定网站图标的图像文件路径。

### 图标

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

### 添加徽标和图标

在 `mkdocs.yml` 中添加徽标和图标，以自定义文档的外观。您可以根据需要替换默认的徽标和图标。

### 查看徽标和图标

一旦配置了徽标和图标，您可以通过导航栏和页面标题查看自定义的徽标和图标。徽标通常显示在导航栏的顶部，图标则用于导航项。

## 自定义

### 自定义徽标和图标

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如需自定义和覆盖[徽标和图标配置]，请[扩展主题]并[覆盖 `logo.html` partial][覆盖 partials]，该 partial 通常包含 `mkdocs.yml` 中设置的 logo 和 icon 属性。

  [徽标和图标配置]: #logo-and-icon-configuration
  [扩展主题]: ../customization.md#extending-the-theme
  [覆盖 partials]: ../customization.md#overriding-partials

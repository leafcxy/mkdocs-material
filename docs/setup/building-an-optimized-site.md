# 构建优化站点

Material for MkDocs 提供了多种功能，以优化您的文档站点，提高加载速度和用户体验。通过配置优化设置，您可以确保文档的高效访问。

## 配置

### 优化设置

<!-- md:version 0.1.0 -->
<!-- md:default none -->

在 `mkdocs.yml` 中配置优化设置，以提高站点的性能：

``` yaml
theme:
  features:
    - optimize
```

- `optimize`: 启用优化功能，以提高站点的加载速度和性能。

### 自定义优化

<!-- md:version 0.1.0 -->
<!-- md:default none -->

您可以为优化设置自定义配置。在 `mkdocs.yml` 中配置优化设置：

``` yaml
theme:
  features:
    - optimize
  optimize:
    minify: true
    compress: true
```

- `optimize.minify`: 启用代码压缩功能，以减少文件大小。
- `optimize.compress`: 启用文件压缩功能，以提高加载速度。

## 使用

### 添加优化设置

在 `mkdocs.yml` 中添加优化设置，以提高站点的性能。您可以根据需要启用代码压缩和文件压缩功能。

### 查看优化设置

一旦配置了优化设置，您可以通过浏览器查看站点的加载速度和性能。优化后的站点将更快地加载，提供更好的用户体验。

## 自定义

### 自定义优化设置

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如需自定义和覆盖[优化配置]，请[扩展主题]并[覆盖 `optimize.html` partial][覆盖 partials]，该 partial 通常包含 `mkdocs.yml` 中设置的 optimize 属性。

  [优化配置]: #optimization-configuration
  [扩展主题]: ../customization.md#extending-the-theme
  [覆盖 partials]: ../customization.md#overriding-partials

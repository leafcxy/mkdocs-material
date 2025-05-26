# 设置站点分析

Material for MkDocs 支持多种分析工具，帮助您了解用户如何与您的文档交互。通过集成这些工具，您可以收集有关页面访问、用户行为和其他重要指标的数据。

## 配置

### Google Analytics

<!-- md:version 0.1.0 -->
<!-- md:default none -->

要启用 Google Analytics，请在 `mkdocs.yml` 中添加以下内容：

``` yaml
extra:
  analytics:
    provider: google
    property: !ENV GOOGLE_ANALYTICS_KEY
```

- `provider`: 分析提供者，例如 `google`。
- `property`: Google Analytics 的跟踪 ID。

### 其他分析工具

<!-- md:version 0.1.0 -->
<!-- md:default none -->

Material for MkDocs 还支持其他分析工具，您可以根据需要配置：

- `plausible`: 使用 [Plausible Analytics]。
- `matomo`: 使用 [Matomo Analytics]。

  [Plausible Analytics]: https://plausible.io/
  [Matomo Analytics]: https://matomo.org/

## 使用

### 查看分析数据

一旦配置了分析工具，您可以通过相应的分析平台查看数据。这些平台通常提供详细的报告，帮助您了解用户行为和改进文档。

## 自定义

### 自定义分析配置

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如需自定义和覆盖[分析配置]，请[扩展主题]并[覆盖 `analytics.html` partial][覆盖 partials]，该 partial 通常包含 `mkdocs.yml` 中设置的 analytics 属性。

  [分析配置]: #analytics-configuration
  [扩展主题]: ../customization.md#extending-the-theme
  [覆盖 partials]: ../customization.md#overriding-partials

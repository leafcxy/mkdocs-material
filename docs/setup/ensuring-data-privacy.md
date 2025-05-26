# 确保数据隐私

Material for MkDocs 提供了多种功能，以确保您的文档符合数据隐私法规，如 GDPR。通过配置数据隐私设置，您可以保护用户数据并增强文档的安全性。

## 配置

### 数据隐私设置

<!-- md:version 0.1.0 -->
<!-- md:default none -->

在 `mkdocs.yml` 中配置数据隐私设置，以保护用户数据：

``` yaml
theme:
  features:
    - privacy.cookie
    - privacy.analytics
```

- `privacy.cookie`: 启用 cookie 通知，以告知用户网站使用 cookie。
- `privacy.analytics`: 启用分析通知，以告知用户网站使用分析工具。

### 自定义通知

<!-- md:version 0.1.0 -->
<!-- md:default none -->

您可以为 cookie 和分析通知自定义文本。在 `mkdocs.yml` 中配置通知文本：

``` yaml
theme:
  features:
    - privacy.cookie
    - privacy.analytics
  privacy:
    cookie:
      text: 我们使用 cookie 来改善您的体验。
    analytics:
      text: 我们使用分析工具来了解您如何使用我们的网站。
```

- `privacy.cookie.text`: 自定义 cookie 通知的文本。
- `privacy.analytics.text`: 自定义分析通知的文本。

## 使用

### 添加数据隐私设置

在 `mkdocs.yml` 中添加数据隐私设置，以保护用户数据。您可以根据需要启用 cookie 和分析通知。

### 查看数据隐私设置

一旦配置了数据隐私设置，您可以通过网站的通知查看 cookie 和分析通知。通知通常显示在页面的底部，用户可以通过点击接受或拒绝。

## 自定义

### 自定义数据隐私设置

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如需自定义和覆盖[数据隐私配置]，请[扩展主题]并[覆盖 `privacy.html` partial][覆盖 partials]，该 partial 通常包含 `mkdocs.yml` 中设置的 privacy 属性。

  [数据隐私配置]: #data-privacy-configuration
  [扩展主题]: ../customization.md#extending-the-theme
  [覆盖 partials]: ../customization.md#overriding-partials

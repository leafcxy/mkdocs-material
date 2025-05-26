# 添加评论系统

Material for MkDocs 支持集成评论系统，以增强用户互动和反馈。通过配置评论系统，您可以允许用户在文档页面发表评论和讨论。

## 配置

### 评论系统设置

<!-- md:version 0.1.0 -->
<!-- md:default none -->

在 `mkdocs.yml` 中配置评论系统设置，以集成评论功能：

``` yaml
theme:
  features:
    - comments
```

- `comments`: 启用评论系统功能，以支持用户互动和反馈。

### 自定义评论系统

<!-- md:version 0.1.0 -->
<!-- md:default none -->

您可以为评论系统设置自定义配置。在 `mkdocs.yml` 中配置评论系统设置：

``` yaml
theme:
  features:
    - comments
  comments:
    provider: giscus
    repo: username/repo
    category: General
```

- `comments.provider`: 指定评论系统的提供商，如 Giscus。
- `comments.repo`: 指定用于存储评论的仓库。
- `comments.category`: 指定评论的分类。

## 使用

### 添加评论系统设置

在 `mkdocs.yml` 中添加评论系统设置，以集成评论功能。您可以根据需要指定评论系统的提供商和配置。

### 查看评论系统设置

一旦配置了评论系统设置，您可以通过文档页面查看评论功能。用户可以在页面底部发表评论，参与讨论。

## 自定义

### 自定义评论系统设置

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如需自定义和覆盖[评论系统配置]，请[扩展主题]并[覆盖 `comments.html` partial][覆盖 partials]，该 partial 通常包含 `mkdocs.yml` 中设置的 comments 属性。

  [评论系统配置]: #comment-system-configuration
  [扩展主题]: ../customization.md#extending-the-theme
  [覆盖 partials]: ../customization.md#overriding-partials

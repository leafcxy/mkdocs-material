# 添加 Git 仓库

Material for MkDocs 支持将文档与 Git 仓库集成，以便于版本控制和协作。通过配置 Git 仓库设置，您可以轻松管理文档的变更和更新。

## 配置

### Git 仓库设置

<!-- md:version 0.1.0 -->
<!-- md:default none -->

在 `mkdocs.yml` 中配置 Git 仓库设置，以集成文档与 Git 仓库：

``` yaml
theme:
  features:
    - git
```

- `git`: 启用 Git 仓库集成功能，以支持版本控制和协作。

### 自定义 Git 仓库

<!-- md:version 0.1.0 -->
<!-- md:default none -->

您可以为 Git 仓库设置自定义配置。在 `mkdocs.yml` 中配置 Git 仓库设置：

``` yaml
theme:
  features:
    - git
  git:
    repository: https://github.com/username/repo.git
    branch: main
```

- `git.repository`: 指定 Git 仓库的 URL。
- `git.branch`: 指定要使用的分支名称。

## 使用

### 添加 Git 仓库设置

在 `mkdocs.yml` 中添加 Git 仓库设置，以集成文档与 Git 仓库。您可以根据需要指定仓库 URL 和分支名称。

### 查看 Git 仓库设置

一旦配置了 Git 仓库设置，您可以通过文档页面查看 Git 仓库的集成。用户可以通过点击链接访问 Git 仓库，查看文档的版本历史和变更。

## 自定义

### 自定义 Git 仓库设置

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如需自定义和覆盖[Git 仓库配置]，请[扩展主题]并[覆盖 `git.html` partial][覆盖 partials]，该 partial 通常包含 `mkdocs.yml` 中设置的 git 属性。

  [Git 仓库配置]: #git-repository-configuration
  [扩展主题]: ../customization.md#extending-the-theme
  [覆盖 partials]: ../customization.md#overriding-partials

# 设置社交卡片

Material for MkDocs 支持为您的文档页面生成社交卡片，以便在社交媒体平台上分享时提供更好的预览。社交卡片通常包含页面标题、描述和图像，以吸引用户点击。

## 配置

### 社交卡片生成器

<!-- md:version 8.0.0 -->
<!-- md:feature -->

要启用社交卡片生成，请在 `mkdocs.yml` 中添加以下内容：

``` yaml
plugins:
  - social
```

### 社交卡片配置

<!-- md:version 8.0.0 -->
<!-- md:default none -->

在 `mkdocs.yml` 中配置社交卡片的外观和行为：

``` yaml
plugins:
  - social:
      cards_layout_options:
        background_color: "#FFFFFF"
        text_color: "#000000"
        font: "Roboto"
```

- `background_color`: 社交卡片的背景颜色。
- `text_color`: 社交卡片上的文本颜色。
- `font`: 社交卡片上使用的字体。

## 使用

### 生成社交卡片

一旦配置了社交卡片生成器，您可以通过以下命令生成社交卡片：

``` sh
mkdocs build
```

生成的社交卡片将保存在 `site` 目录中，您可以在社交媒体平台上使用它们。

## 自定义

### 自定义社交卡片

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如需自定义和覆盖[社交卡片配置]，请[扩展主题]并[覆盖 `social.html` partial][覆盖 partials]，该 partial 通常包含 `mkdocs.yml` 中设置的 social 属性。

  [社交卡片配置]: #social-cards-configuration
  [扩展主题]: ../customization.md#extending-the-theme
  [覆盖 partials]: ../customization.md#overriding-partials

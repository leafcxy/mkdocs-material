---
icon: material/emoticon-happy-outline
---

# 图标与表情

Material for MkDocs 最棒的功能之一，就是可以在项目文档中几乎零成本地使用[超过 10,000 个图标][icon search]和数千个表情。此外，还可以[添加自定义图标]，并在 `mkdocs.yml`、文档和模板中使用。

  [icon search]: #search
  [custom icons can be added]: ../setup/changing-the-logo-and-icons.md#additional-icons

## 搜索

<div class="mdx-iconsearch" data-mdx-component="iconsearch">
  <input
    class="md-input md-input--stretch mdx-iconsearch__input"
    placeholder="搜索图标和表情数据库"
    data-mdx-component="iconsearch-query"
  />
  <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result">
    <select
      class="mdx-iconsearch-result__select"
      data-mdx-component="iconsearch-select"
    >
      <option value="all" selected>全部</option>
      <option value="icons">图标</option>
      <option value="emojis">表情</option>
    </select>
    <div class="mdx-iconsearch-result__meta"></div>
    <ol class="mdx-iconsearch-result__list"></ol>
  </div>
</div>
<small>
  :octicons-light-bulb-16:
  **提示：** 输入关键词查找图标和表情，点击短代码即可复制到剪贴板。
</small>

## 配置

此配置启用图标和表情的使用，只需简单的短代码即可调用，通过[图标搜索]可发现所有可用短代码。将以下内容添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - attr_list
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
```

Material for MkDocs 内置了以下图标集：

- :material-material-design: – [Material Design]
- :fontawesome-brands-font-awesome: – [FontAwesome]
- :octicons-mark-github-16: – [Octicons]
- :simple-simpleicons: – [Simple Icons]

查看更多配置选项：

- [Attribute Lists]
- [Emoji]
- [带自定义图标的 Emoji]

  [Material Design]: https://pictogrammers.com/library/mdi/
  [FontAwesome]: https://fontawesome.com/search?m=free
  [Octicons]: https://octicons.github.com/
  [Simple Icons]: https://simpleicons.org/
  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists
  [Emoji]: ../setup/extensions/python-markdown-extensions.md#emoji
  [Emoji with custom icons]: ../setup/extensions/python-markdown-extensions.md#+pymdownx.emoji.options.custom_icons

## 使用方法

### 使用表情

只需将表情的短代码放在两个冒号之间即可在 Markdown 中插入表情。如果你使用的是 [Twemoji]（推荐），可以在 [Emojipedia] 查找所有短代码：

``` title="表情"
:smile:
```

<div class="result" markdown>

:smile:

</div>
  [Twemoji]: https://github.com/jdecked/twemoji
  [Emojipedia]: https://emojipedia.org/twitter/

### 使用图标

启用 [Emoji] 后，可以像使用表情一样使用图标，只需引用主题内置图标的有效路径（位于[`.icons`][custom icons] 目录），并将 `/` 替换为 `-`：

``` title="图标"
:fontawesome-regular-face-laugh-wink:
```

<div class="result" markdown>

:fontawesome-regular-face-laugh-wink:

</div>

  [custom icons]: https://github.com/squidfunk/mkdocs-material/tree/master/material/templates/.icons

#### 带颜色

启用 [Attribute Lists] 后，可以通过特殊语法为图标添加自定义 CSS 类。虽然 HTML 允许使用[内联样式]，但更推荐添加[额外样式表]，将样式声明放入专用 CSS 类：

<style>
  .youtube {
    color: #EE0F0F;
  }
</style>

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    .youtube {
      color: #EE0F0F;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

自定义后，在图标短代码中添加 CSS 类即可：

``` markdown title="带颜色的图标"
:fontawesome-brands-youtube:{ .youtube }
```

<div class="result" markdown>

:fontawesome-brands-youtube:{ .youtube }

</div>

  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists
  [inline styles]: https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/style
  [additional style sheet]: ../customization.md#additional-css

#### 带动画

和[颜色]一样，也可以通过[额外样式表]为图标添加[动画]，只需定义 `@keyframes` 规则并为图标添加专用 CSS 类：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    @keyframes heart {
      0%, 40%, 80%, 100% {
        transform: scale(1);
      }
      20%, 60% {
        transform: scale(1.15);
      }
    }
    .heart {
      animation: heart 1000ms infinite;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

自定义后，在图标短代码中添加 CSS 类即可：

``` markdown title="带动画的图标"
:octicons-heart-fill-24:{ .heart }
```

<div class="result" markdown>

:octicons-heart-fill-24:{ .mdx-heart }

</div>

  [colors]: #with-colors
  [animations]: https://developer.mozilla.org/en-US/docs/Web/CSS/animation

### 侧边栏中的图标与表情 :smile:

借助[内置 typeset 插件]，你可以在标题中使用图标和表情，这些内容会被渲染到侧边栏。该插件会保留 Markdown 和 HTML 格式。

  [built-in typeset plugin]: ../plugins/typeset.md

## 个性化定制

### 在模板中使用图标

当你通过 partial 或 block [扩展主题] 时，可以直接用 Jinja 的 [`include`][include] 函数引用任何[主题内置图标][icon search]，并用 `.twemoji` CSS 类包裹：

``` html
<span class="twemoji">
  {% include ".icons/fontawesome/brands/youtube.svg" %} <!-- (1)! -->
</span>
```

1.  输入关键词，使用我们的[图标搜索]找到完美的图标，然后点击短代码复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="搜索图标" data-mdx-component="iconsearch-query" value="brands youtube" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

Material for MkDocs 的模板就是这样做的。

  [extending the theme]: ../customization.md#extending-the-theme
  [include]: https://jinja.palletsprojects.com/en/2.11.x/templates/#include

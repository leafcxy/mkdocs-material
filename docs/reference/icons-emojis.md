---
icon: material/emoticon-happy-outline
---

# 图标， 表情符号

Material for MkDocs的最佳功能之一是可以使用[更多
项目中有10000多个图标[图标搜索]和数千个表情符号
文档几乎不需要额外的工作。此外，[自定义图标
可以添加]并在“mkdocs.yml”、文档和模板中使用。

  [icon search]: #search
  [custom icons can be added]: ../setup/changing-the-logo-and-icons.md#additional-icons

## 搜索

<div class="mdx-iconsearch" data-mdx-component="iconsearch">
  <input
    class="md-input md-input--stretch mdx-iconsearch__input"
    placeholder="Search the icon and emoji database"
    data-mdx-component="iconsearch-query"
  />
  <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result">
    <select
      class="mdx-iconsearch-result__select"
      data-mdx-component="iconsearch-select"
    >
      <option value="all" selected>All</option>
      <option value="icons">Icons</option>
      <option value="emojis">Emojis</option>
    </select>
    <div class="mdx-iconsearch-result__meta"></div>
    <ol class="mdx-iconsearch-result__list"></ol>
  </div>
</div>
<small>
  :octicons-light-bulb-16:
  **Tip:** Enter some keywords to find icons and emojis and click on the
  shortcode to copy it to your clipboard.
</small>

## 配置

此配置允许使用简单的图标和表情符号
可以通过[图标搜索]发现的短代码。添加以下内容
指向`mkdocs.yml`的行：

``` yaml
markdown_extensions:
  - attr_list
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
```

以下图标集与MkDocs的Material捆绑在一起：

- :material-material-design: – [Material Design]
- :fontawesome-brands-font-awesome: – [FontAwesome]
- :octicons-mark-github-16: – [Octicons]
- :simple-simpleicons: – [Simple Icons]

请参阅其他配置选项：

- [Attribute Lists]
- [Emoji]
- [Emoji with custom icons]

  [Material Design]: https://pictogrammers.com/library/mdi/
  [FontAwesome]: https://fontawesome.com/search?m=free
  [Octicons]: https://octicons.github.com/
  [Simple Icons]: https://simpleicons.org/
  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists
  [Emoji]: ../setup/extensions/python-markdown-extensions.md#emoji
  [Emoji with custom icons]: ../setup/extensions/python-markdown-extensions.md#+pymdownx.emoji.options.custom_icons

## 使用

### 使用表情符号

通过添加表情符号的短代码，可以将表情符号集成到Markdown中
在两个冒号之间。如果你正在使用[Twemoji]（推荐），你可以查找
[Emojipedia]上的简码：

``` title="Emoji"
:smile:
```

<div class="result" markdown>

:smile:

</div>
  [Twemoji]: https://github.com/jdecked/twemoji
  [Emojipedia]: https://emojipedia.org/twitter/

### 使用图标

启用[Emoji]后，可以通过引用使用类似于表情符号的图标
指向与主题捆绑在一起的任何图标的有效路径，这些图标位于
[图标][自定义图标]目录，并将“/”替换为“-”：

``` title="Icon"
:fontawesome-regular-face-laugh-wink:
```

<div class="result" markdown>

:fontawesome-regular-face-laugh-wink:

</div>

  [custom icons]: https://github.com/squidfunk/mkdocs-material/tree/master/material/templates/.icons

#### 有颜色

启用[属性列表]后，可以通过以下方式将自定义CSS类添加到图标中
在图标后添加特殊语法。HTML允许使用[inline
样式]，始终建议添加[附加样式表]并移动
声明到专用CSS类中：

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

应用自定义后，将CSS类添加到图标短代码中：

``` markdown title="Icon with color"
:fontawesome-brands-youtube:{ .youtube }
```

<div class="result" markdown>

:fontawesome-brands-youtube:{ .youtube }

</div>

  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists
  [inline styles]: https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/style
  [additional style sheet]: ../customization.md#additional-css

#### 带动画

与添加[颜色]类似，通过以下方式为图标添加[动画]也很容易
使用[附加样式表]，定义“@keyframes”规则并添加
图标专用CSS类：

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

应用自定义后，将CSS类添加到图标短代码中：

``` markdown title="Icon with animation"
:octicons-heart-fill-24:{ .heart }
```

<div class="result" markdown>

:octicons-heart-fill-24:{ .mdx-heart }

</div>

  [colors]: #with-colors
  [animations]: https://developer.mozilla.org/en-US/docs/Web/CSS/animation

### 侧边栏中的图标和表情符号：微笑：smile:

借助[内置排版插件]，您可以使用图标和表情符号
在标题中，这些标题将在侧栏中呈现。插件保留
Markdown和HTML格式。

  [built-in typeset plugin]: ../plugins/typeset.md

## 自定义

### 在模板中使用图标

当你用片段或块来[扩展主题]时，你可以简单地
使用Jinja的[与主题捆绑的][图标搜索]引用任何图标
[include][include]函数，并用.tweemoji CSS类包裹它：

``` html
<span class="twemoji">
  {% include ".icons/fontawesome/brands/youtube.svg" %} <!-- (1)! -->
</span>
```

1.  输入几个关键字，使用我们的[图标搜索]找到完美的图标，然后
    单击短代码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="brands youtube" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

这正是Material for MkDocs在其模板中所做的。

  [extending the theme]: ../customization.md#extending-the-theme
  [include]: https://jinja.palletsprojects.com/en/2.11.x/templates/#include

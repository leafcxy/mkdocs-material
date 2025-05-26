# 更改颜色

作为任何适当的 Material Design 实现，Material for MkDocs 支持 Google 的原始[调色板]，可以通过 `mkdocs.yml` 轻松配置。此外，可以通过几行 CSS 使用[CSS 变量][自定义颜色]来自定义颜色，以适合您的品牌标识。

  [调色板]: http://www.materialui.co/colors
  [自定义颜色]: #custom-colors

## 配置

### 调色板

#### 配色方案

<!-- md:version 5.2.0 -->
<!-- md:default `default` -->

Material for MkDocs 支持两种配色方案：__浅色模式__，简称为 `default`，和 __深色模式__，简称为 `slate`。配色方案可以通过 `mkdocs.yml` 设置：

``` yaml
theme:
  palette:
    scheme: default
```

点击一个方块来更改配色方案：

<div class="mdx-switch">
  <button data-md-color-scheme="default"><code>default</code></button>
  <button data-md-color-scheme="slate"><code>slate</code></button>
</div>

<script>
  var buttons = document.querySelectorAll("button[data-md-color-scheme]")
  buttons.forEach(function(button) {
    button.addEventListener("click", function() {
      document.body.setAttribute("data-md-color-switching", "")
      var attr = this.getAttribute("data-md-color-scheme")
      document.body.setAttribute("data-md-color-scheme", attr)
      var name = document.querySelector("#__code_0 code span.l")
      name.textContent = attr
      setTimeout(function() {
        document.body.removeAttribute("data-md-color-switching")
      })
    })
  })
</script>

#### 主色调

<!-- md:version 0.2.0 -->
<!-- md:default `indigo` -->

主色调用于页眉、侧边栏、文本链接和几个其他组件。要更改主色调，请在 `mkdocs.yml` 中将以下值设置为有效的颜色名称：

``` yaml
theme:
  palette:
    primary: indigo
```

点击一个方块来更改主色调：

<div class="mdx-switch">
  <button data-md-color-primary="red"><code>red</code></button>
  <button data-md-color-primary="pink"><code>pink</code></button>
  <button data-md-color-primary="purple"><code>purple</code></button>
  <button data-md-color-primary="deep-purple"><code>deep purple</code></button>
  <button data-md-color-primary="indigo"><code>indigo</code></button>
  <button data-md-color-primary="blue"><code>blue</code></button>
  <button data-md-color-primary="light-blue"><code>light blue</code></button>
  <button data-md-color-primary="cyan"><code>cyan</code></button>
  <button data-md-color-primary="teal"><code>teal</code></button>
  <button data-md-color-primary="green"><code>green</code></button>
  <button data-md-color-primary="light-green"><code>light green</code></button>
  <button data-md-color-primary="lime"><code>lime</code></button>
  <button data-md-color-primary="yellow"><code>yellow</code></button>
  <button data-md-color-primary="amber"><code>amber</code></button>
  <button data-md-color-primary="orange"><code>orange</code></button>
  <button data-md-color-primary="deep-orange"><code>deep orange</code></button>
  <button data-md-color-primary="brown"><code>brown</code></button>
  <button data-md-color-primary="grey"><code>grey</code></button>
  <button data-md-color-primary="blue-grey"><code>blue grey</code></button>
  <button data-md-color-primary="black"><code>black</code></button>
  <button data-md-color-primary="white"><code>white</code></button>
</div>

<script>
  var buttons = document.querySelectorAll("button[data-md-color-primary]")
  buttons.forEach(function(button) {
    button.addEventListener("click", function() {
      var attr = this.getAttribute("data-md-color-primary")
      document.body.setAttribute("data-md-color-primary", attr)
      var name = document.querySelector("#__code_1 code span.l")
      name.textContent = attr.replace("-", " ")
    })
  })
</script>

查看下面的指南，了解如何设置[自定义颜色]。

#### 强调色

<!-- md:version 0.2.0 -->
<!-- md:default `indigo` -->

强调色用于表示可以交互的元素，例如悬停链接、按钮和滚动条。可以通过在 `mkdocs.yml` 中选择有效的颜色名称来更改：

``` yaml
theme:
  palette:
    accent: indigo
```

点击一个方块来更改强调色：

<style>
  .md-typeset button[data-md-color-accent] > code {
    background-color: var(--md-code-bg-color);
    color: var(--md-accent-fg-color);
  }
</style>

<div class="mdx-switch">
  <button data-md-color-accent="red"><code>red</code></button>
  <button data-md-color-accent="pink"><code>pink</code></button>
  <button data-md-color-accent="purple"><code>purple</code></button>
  <button data-md-color-accent="deep-purple"><code>deep purple</code></button>
  <button data-md-color-accent="indigo"><code>indigo</code></button>
  <button data-md-color-accent="blue"><code>blue</code></button>
  <button data-md-color-accent="light-blue"><code>light blue</code></button>
  <button data-md-color-accent="cyan"><code>cyan</code></button>
  <button data-md-color-accent="teal"><code>teal</code></button>
  <button data-md-color-accent="green"><code>green</code></button>
  <button data-md-color-accent="light-green"><code>light green</code></button>
  <button data-md-color-accent="lime"><code>lime</code></button>
  <button data-md-color-accent="yellow"><code>yellow</code></button>
  <button data-md-color-accent="amber"><code>amber</code></button>
  <button data-md-color-accent="orange"><code>orange</code></button>
  <button data-md-color-accent="deep-orange"><code>deep orange</code></button>
</div>

<script>
  var buttons = document.querySelectorAll("button[data-md-color-accent]")
  buttons.forEach(function(button) {
    button.addEventListener("click", function() {
      var attr = this.getAttribute("data-md-color-accent")
      document.body.setAttribute("data-md-color-accent", attr)
      var name = document.querySelector("#__code_2 code span.l")
      name.textContent = attr.replace("-", " ")
    })
  })
</script>

查看下面的指南，了解如何设置[自定义颜色]。

### 调色板切换

<!-- md:version 7.1.0 -->
<!-- md:default none -->
<!-- md:example color-palette-toggle -->

提供浅色和深色调色板使您的文档在不同时间阅读都很舒适，因此用户可以根据需要选择。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  palette: # (1)!

    # 浅色模式的调色板切换
    - scheme: default
      toggle:
        icon: material/brightness-7 # (2)!
        name: 切换到深色模式

    # 深色模式的调色板切换
    - scheme: slate
      toggle:
        icon: material/brightness-4
        name: 切换到浅色模式
```

1.  请注意，`theme.palette` 设置现在定义为列表。

2.  输入几个关键词来使用我们的[图标搜索]找到完美的图标，然后点击短代码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="搜索图标" data-mdx-component="iconsearch-query" value="brightness" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

此配置将在搜索栏旁边呈现调色板切换按钮。请注意，您还可以为每个调色板定义单独的 [`primary`][palette.primary] 和 [`accent`][palette.accent] 设置。

每个切换必须设置以下属性：

<!-- md:option palette.toggle.icon -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须指向引用主题捆绑的任何图标的有效图标路径，否则构建将不会成功。一些流行的组合：

    * :material-brightness-7: + :material-brightness-4: – `material/brightness-7` + `material/brightness-4`
    * :material-toggle-switch: + :material-toggle-switch-off-outline: – `material/toggle-switch` + `material/toggle-switch-off-outline`
    * :material-weather-night: + :material-weather-sunny: – `material/weather-night` + `material/weather-sunny`
    * :material-eye: + :material-eye-outline: – `material/eye` + `material/eye-outline`
    * :material-lightbulb: + :material-lightbulb-outline: – `material/lightbulb` + `material/lightbulb-outline`

<!-- md:option palette.toggle.name -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性用作切换的 `title` 属性，应设置为可识别的名称以提高可访问性。它作为[工具提示]呈现。

  [palette.scheme]: #color-scheme
  [palette.primary]: #primary-color
  [palette.accent]: #accent-color
  [图标搜索]: ../reference/icons-emojis.md#search
  [工具提示]: ../reference/tooltips.md

### 系统偏好

<!-- md:version 7.1.0 -->
<!-- md:default none -->
<!-- md:example color-palette-system-preference -->

每个调色板都可以通过使用媒体查询链接到用户对浅色和深色外观的系统偏好。只需在 `mkdocs.yml` 中的 `scheme` 定义旁边添加 `media` 属性：

``` yaml
theme:
  palette:

    # 浅色模式的调色板切换
    - media: "(prefers-color-scheme: light)"
```

#### Automatic light / dark mode

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->
<!-- md:example color-palette-system-preference -->

Newer operating systems allow to automatically switch between light and dark
appearance during day and night times. Material for MkDocs adds support for
automatic light / dark mode, delegating color palette selection to the user's
operating system. Add the following lines to `mkdocs.yml`:

``` yaml
theme:
  palette:

    # Palette toggle for automatic mode
    - media: "(prefers-color-scheme)"
      toggle:
        icon: material/brightness-auto
        name: Switch to light mode

    # Palette toggle for light mode
    - media: "(prefers-color-scheme: light)"
      scheme: default # (1)!
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode

    # Palette toggle for dark mode
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      toggle:
        icon: material/brightness-4
        name: Switch to system preference
```

1.  You can also define separate settings for [`primary`][palette.primary] and
    [`accent`][palette.accent] per color palette, i.e. different colors for
    light and dark mode.

Material for MkDocs will now change the color palette each time the operating
system switches between light and dark appearance, even when the user doesn't
reload the site.

  [Insiders]: ../insiders/index.md

## Customization

### Custom colors

<!-- md:version 5.0.0 -->
<!-- md:example custom-colors -->

Material for MkDocs implements colors using [CSS variables] (custom
properties). If you want to customize the colors beyond the palette (e.g. to
use your brand-specific colors), you can add an [additional style sheet] and
tweak the values of the CSS variables.

First, set the [`primary`][palette.primary] or [`accent`][palette.accent] values
in `mkdocs.yml` to `custom`, to signal to the theme that you want to define
custom colors, e.g., when you want to override the `primary` color:

``` yaml
theme:
  palette:
    primary: custom
```

Let's say you're :fontawesome-brands-youtube:{ style="color: #EE0F0F" }
__YouTube__, and want to set the primary color to your brand's palette. Just
add:

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    :root  > * {
      --md-primary-fg-color:        #EE0F0F;
      --md-primary-fg-color--light: #ECB7B7;
      --md-primary-fg-color--dark:  #90030C;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

See the file containing the [color definitions] for a list of all CSS variables.

  [CSS variables]: https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties
  [color definitions]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/assets/stylesheets/main/_colors.scss
  [additional style sheet]: ../customization.md#additional-css


### Custom color schemes

Besides overriding specific colors, you can create your own, named color scheme
by wrapping the definitions in a `[data-md-color-scheme="..."]`
[attribute selector], which you can then set via `mkdocs.yml` as described
in the [color schemes][palette.scheme] section:

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    [data-md-color-scheme="youtube"] {
      --md-primary-fg-color:        #EE0F0F;
      --md-primary-fg-color--light: #ECB7B7;
      --md-primary-fg-color--dark:  #90030C;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    theme:
      palette:
        scheme: youtube
    extra_css:
      - stylesheets/extra.css
    ```

Additionally, the `slate` color scheme defines all of it's colors via `hsla`
color functions and deduces its colors from the `--md-hue` CSS variable. You
can tune the `slate` theme with:

``` css
[data-md-color-scheme="slate"] {
  --md-hue: 210; /* (1)! */
}
```

1.  The `hue` value must be in the range of `[0, 360]`

  [attribute selector]: https://www.w3.org/TR/selectors-4/#attribute-selectors

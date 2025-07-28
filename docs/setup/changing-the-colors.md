# 更改颜色

作为任何适当的材料设计实施，MkDocs材料支持
谷歌的原始[调色板]，可以通过以下方式轻松配置
`mkdocs.yml`。此外，颜色可以通过几行CSS进行定制
通过使用[CSS变量][自定义颜色]来适应您的品牌标识。

  [color palette]: http://www.materialui.co/colors
  [custom colors]: #_11

## 配置

### 调色板

#### 配色方案

<!-- md:version 5.2.0 -->
<!-- md:default `default` -->

MkDocs的材质支持两种配色方案：一种是__light模式__，它只是
称为“默认”，以及一个名为“板岩”的__dark模式。配色方案
可以通过`mkdocs.yml`进行设置：

``` yaml
theme:
  palette:
    scheme: default
```

单击互动程序以更改配色方案：

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

#### 原色

<!-- md:version 0.2.0 -->
<!-- md:default `indigo` -->

主色用于标题、侧边栏、文本链接和几个
其他组件。要更改原色，请设置以下值
在`mkdocs.yml`中设置一个有效的颜色名称：

``` yaml
theme:
  palette:
    primary: indigo
```

单击互动程序以更改主色：

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

请参阅下面的指南，了解如何设置[自定义颜色]。

#### 重点色

<!-- md:version 0.2.0 -->
<!-- md:default `indigo` -->

强调色用于表示可以交互的元素，例如。
悬停的链接、按钮和滚动条。可以在`mkdocs.yml`中通过以下方式进行更改
选择有效的颜色名称：

``` yaml
theme:
  palette:
    accent: indigo
```

单击互动程序以更改重点颜色：

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

请参阅下面的指南，了解如何设置[自定义颜色]。

### 调色板切换

<!-- md:version 7.1.0 -->
<!-- md:default none -->
<!-- md:example color-palette-toggle -->

提供浅色和深色调色板使您的文档令人愉快
在一天中的不同时间阅读，因此用户可以相应地进行选择。添加
将以下行转换为`mkdocs.yml`：

``` yaml
theme:
  palette: # (1)!

    # Palette toggle for light mode
    - scheme: default
      toggle:
        icon: material/brightness-7 # (2)!
        name: Switch to dark mode

    # Palette toggle for dark mode
    - scheme: slate
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
```

1.  请注意，“theme.palette”设置现在被定义为列表。

2.  输入几个关键字，使用我们的[图标搜索]找到完美的图标，然后
    单击短代码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="brightness" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

此配置将在搜索栏旁边呈现调色板切换。
请注意，您还可以为[`primary][palette.primary]定义单独的设置
以及每个调色板的[重音][调色板.重音]。

必须为每个切换设置以下属性：

<!-- md:option palette.toggle.icon -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须指向引用任何捆绑图标的有效图标路径
    主题，否则构建将不会成功。一些流行的组合：

    * :material-brightness-7: + :material-brightness-4: – `material/brightness-7` + `material/brightness-4`
    * :material-toggle-switch: + :material-toggle-switch-off-outline: – `material/toggle-switch` + `material/toggle-switch-off-outline`
    * :material-weather-night: + :material-weather-sunny: – `material/weather-night` + `material/weather-sunny`
    * :material-eye: + :material-eye-outline: – `material/eye` + `material/eye-outline`
    * :material-lightbulb: + :material-lightbulb-outline: – `material/lightbulb` + `material/lightbulb-outline`

<!-- md:option palette.toggle.name -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性用作切换的“title”属性，应设置为
    一个可辨别的名称，以提高可访问性。它被渲染为[工具提示]。

  [palette.scheme]: #color-scheme
  [palette.primary]: #primary-color
  [palette.accent]: #accent-color
  [icon search]: ../reference/icons-emojis.md#_2
  [tooltip]: ../reference/tooltips.md

### 系统偏好

<!-- md:version 7.1.0 -->
<!-- md:default none -->
<!-- md:example color-palette-system-preference -->

每个调色板都可以链接到用户对光线的系统偏好
通过使用媒体查询来显示深色外观。只需在旁边添加一个“media”属性
mkdocs.yml中的“方案”定义：

``` yaml
theme:
  palette:

    # Palette toggle for light mode
    - media: "(prefers-color-scheme: light)"
      scheme: default
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode

    # Palette toggle for dark mode
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
```

当用户首次访问您的网站时，媒体查询将在
其定义的顺序。匹配的第一个媒体查询选择
默认调色板。

#### 自动亮/暗模式

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->
<!-- md:example color-palette-system-preference -->

较新的操作系统允许在亮暗之间自动切换
白天和晚上出现。MkDocs的材料增加了对
自动亮/暗模式，将调色板选择委托给用户
操作系统。将以下行添加到`mkdocs.yml`中：

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

1.  您还可以为[`primary][palette.primary]和
    每个调色板都有不同的颜色，即不同的颜色
    亮暗模式。

MkDocs的材料现在将在每次操作时更改调色板
系统在亮和暗外观之间切换，即使用户没有
重新加载网站。

  [Insiders]: ../insiders/index.md

## 自定义

### 自定义颜色

<!-- md:version 5.0.0 -->
<!-- md:example custom-colors -->

MkDocs的材质使用[CSS变量]实现颜色（自定义
属性）。如果你想自定义调色板之外的颜色（例如
使用您的品牌特定颜色），您可以添加[附加样式表]，然后
调整CSS变量的值。

首先，设置[`primary][palette.primary]或[`speech][paletter.speech]值
在`mkdocs.yml`到`custom`中，向要定义的主题发出信号
自定义颜色，例如，当你想覆盖“原色”时：

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

有关所有CSS变量的列表，请参阅包含[color-definitions]的文件。

  [CSS variables]: https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties
  [color definitions]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/assets/stylesheets/main/_colors.scss
  [additional style sheet]: ../customization.md#additional-css


### 自定义配色方案

除了覆盖特定颜色外，您还可以创建自己的命名配色方案
通过将定义包装在`[data-md配色方案=“…”]中`
[属性选择器]，然后您可以通过`mkdocs.yml`进行设置，如下所述
在[配色方案][调色板.方案]部分：

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

此外，“板岩”配色方案通过“hsla”定义了它的所有颜色`
color函数，并从`-md-hue` CSS变量推断其颜色。你
可以通过以下方式调整“slate”主题：

``` css
[data-md-color-scheme="slate"] {
  --md-hue: 210; /* (1)! */
}
```

1.  “色调”值必须在“[0，360]”范围内`

  [attribute selector]: https://www.w3.org/TR/selectors-4/#attribute-selectors

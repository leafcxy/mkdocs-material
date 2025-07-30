# 设置社交卡

MkDocs的材料可以自动为您创建漂亮的社交卡
文档，在社交媒体平台上显示为链接预览。你
可以从多个[预先设计的布局][默认布局]中选择或创建
[自定义布局]以匹配您独特的风格和品牌。

---

:fontawesome-brands-youtube:{ style="color: #EE0F0F" }
__[How to build custom social cards]__ by @james-willett – :octicons-clock-24:
24m – Learn how to create entirely custom social cards perfectly matching your
branding for each page automatically!

  [How to build custom social cards]: https://www.youtube.com/watch?v=4OjnOc6ftJ8

<figure markdown>

[![Layout default variant]][Layout default variant]

  <figcaption markdown>

Social card of our [formatting] reference

  </figcaption>
</figure>

  [default layouts]: ../plugins/social.md#layouts
  [custom layouts]: 
  [formatting]: ../reference/formatting.md
  [Layout default variant]: ../assets/screenshots/social-cards-variant.png

## 配置

### 内置社交插件

`version 8.5.0`
`plugin`
`flag experimental`
`demo create-social-cards`

内置的社交插件会自动生成自定义预览图像
每一页。安装所有[图像处理依赖项]并添加
将以下行转换为`mkdocs.yml`：

``` yaml
plugins:
  - social
```

有关所有设置的列表，请参阅[插件文档]。

  [plugin documentation]: ../plugins/social.md

!!! info "必须设置[`site_url`][site_url]设置"

    请注意，使用社交插件时必须设置[`site_url`][site_url]，
    否则生成的卡将无法正确链接。社交媒体服务
    像X和Facebook一样，要求社交预览指向绝对
    URL，插件只能在设置['site_URL][site_URL]时计算。
    例子：

    ``` yaml
    site_url: https://example.com
    ```

  [dependencies for image processing]: ../plugins/requirements/image-processing.md
  [site_url]: https://www.mkdocs.org/user-guide/configuration/#site_url

## 使用

如果你想调整社交卡的标题或设置自定义描述，
您可以设置标题[更改标题]和
[`description`][更改description]属性，其优先级高于
默认值，或使用：

- [`cards_layout_options.title`](../plugins/social.md)
- [`cards_layout_options.description`](../plugins/social.md)

  [Changing the title]: ../reference/index.md
  [Changing the description]: ../reference/index.md

### 选择字体

某些字体不包含CJK字符，例如
[默认字体，`Roboto`][font]。如果您的“site_name”、“site_description”或
页面标题包含CJK字符，请从[谷歌字体]中选择另一种字体
带有CJK字符，例如“Noto Sans”字体家族中的一个字符：

=== "Chinese (Simplified)"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            font_family: Noto Sans SC
    ```

=== "Chinese (Traditional)"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            font_family: Noto Sans TC
    ```

=== "Japanese"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            font_family: Noto Sans JP
    ```

=== "Korean"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            font_family: Noto Sans KR
    ```

  [font]: changing-the-fonts.md

### 更改布局

`version insiders-4.37.0`
`flag metadata`
`flag experimental`

如果你想对单个页面使用不同的布局（例如你的着陆
页面），您可以将“社会”前沿属性与
[`cards_layout`]（../plugins/social.md）键，与
在`mkdocs.yml`中：

``` yaml
---
social:
  cards_layout: custom
---

# Page title
...
```

您可以将这些更改应用于文档的整个子树，例如。，
为您的博客和API参考生成不同的社交卡，方法是使用
[内置元插件]。

  [built-in meta plugin]: ../plugins/meta.md

### Parametrizing the layout

`version insiders-4.37.0`
`flag metadata`
`flag experimental`

除了更改整个布局外，您还可以覆盖布局的所有选项
暴露。这意味着您可以使用自定义前件对社交卡进行参数化
属性，如标签、日期、作者或任何你能想到的东西。
只需定义[`cards_layout_options`]（../plugins/social.md）：

``` yaml
---
social:
  cards_layout_options:
    background_color: blue # Change background color
    background_image: null # Remove background image
---

# Page title
...
```

您可以将这些更改应用于文档的整个子树，例如。，
为您的博客和API参考生成不同的社交卡，方法是使用
[内置元插件]。

### 禁用社交卡

`version insiders-4.37.0`
`flag metadata`
`flag experimental`

如果您想禁用页面的社交卡，只需将以下内容添加到
Markdown文档的首页：

``` yaml
---
social:
  cards: false
---

# Page title
...
```

## 自定义

`sponsors`
`version insiders-4.33.0`
`flag experimental`

[内部人士]对[内置社交插件]进行了彻底的重写
介绍了一种基于YAML和.NET的全新布局系统
[Jinja模板]–MkDocs的Material引擎用于HTML
模板–允许创建复杂的自定义布局：

<div class="mdx-social">
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 0</span>
      <img src="../../assets/screenshots/social-cards-layer-0.png" />
    </div>
  </div>
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 1</span>
      <img src="../../assets/screenshots/social-cards-layer-1.png" />
    </div>
  </div>
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 2</span>
      <img src="../../assets/screenshots/social-cards-layer-2.png" />
    </div>
  </div>
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 3</span>
      <img src="../../assets/screenshots/social-cards-layer-3.png" />
    </div>
  </div>
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 4</span>
      <img src="../../assets/screenshots/social-cards-layer-4.png" />
    </div>
  </div>
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 5</span>
      <img src="../../assets/screenshots/social-cards-layer-5.png" />
    </div>
  </div>
</div>

社交卡片由多层组成，类似于它们在
图形设计软件，如Adobe Photoshop。由于许多层是常见的
在为每个页面生成的卡片（例如背景或徽标）中
内置的社交插件可以自动删除重复层并呈现它们
仅一次，大大加速了卡的生成。生成的卡片是
缓存以确保它们仅在内容更改时重新生成。

布局是用YAML语法编写的。在开始创建自定义布局之前，
[研究预先设计的布局]是个好主意（链接到[内部人士]
存储库），以便更好地了解它们是如何工作的。然后，
创建一个新布局并在`mkdocs.yml`中引用它：

=== ":octicons-file-code-16: `layouts/custom.yml`"

    ``` yaml
    size: { width: 1200, height: 630 }
    layers: []
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    plugins:
      - social:
          cards_layout_dir: layouts
          cards_layout: custom
          debug: true
    ```

请注意，应省略“.yml”文件扩展名。接下来，运行`mkdocs-serve`，
并查看如何用生成的卡填充“.cache”目录。打开
编辑器中的任何卡片，这样你就可以立即看到你的更改。因为我们
没有定义任何层，这些卡是透明的。

以下部分解释了如何创建自定义布局。

  [Insiders]: ../insiders/index.md
  [built-in social plugin]: ../plugins/social.md
  [Google Fonts]: https://fonts.google.com/
  [Jinja templates]: https://jinja.palletsprojects.com/en/3.1.x/
  [study the pre-designed layouts]: https://github.com/squidfunk/mkdocs-material-insiders/tree/master/src/plugins/social/layouts

### 尺寸和偏移

每一层都有一个相关的大小和偏移，以像素为单位定义。这个
`size由width和height属性定义，offset由x定义`
以及“y”属性：

``` yaml
size: { width: 1200, height: 630 }
layers:
  - size: { width: 1200, height: 630 }
    offset: { x: 0, y: 0 }
```

如果省略“大小”，则默认为布局的大小。如果'偏移`
如果省略，则默认为左上角，即默认的“原点”。
保存布局并重新加载渲染：

![Layer size]

层轮廓和网格是可见的，因为我们启用了['debug][debug]
mkdocs.yml中的模式。左上角显示了图层索引和偏移量，即
可用于对齐和构图。

  [Layer size]: ../assets/screenshots/social-cards-layer-size.png
  [debug]: ../plugins/social.md

#### 起源

`version insiders-4.35.0`
`flag experimental`

“x”和“y”值的“原点”可以更改，因此该层为
与布局的边缘或角落对齐，例如右下角
布局的一角：

``` yaml hl_lines="5"
size: { width: 1200, height: 630 }
layers:
  - size: { width: 1200, height: 630 }
    offset: { x: 0, y: 0 }
    origin: end bottom
```

下表显示了支持的值：

<figure markdown>

| Origin         |                 |              |
| -------------- | --------------- | ------------ |
| :material-arrow-top-left:    `start top`    | :material-arrow-up:     `center top`    | :material-arrow-top-right:    `end top`    |
| :material-arrow-left:        `start center` | :material-circle-small: `center`        | :material-arrow-right:        `end center` |
| :material-arrow-bottom-left: `start bottom` | :material-arrow-down:   `center bottom` | :material-arrow-bottom-right: `end bottom` |

  <figcaption>
    Supported values for origin
  </figcaption>
</figure>

### 背景

可以为每一层指定背景颜色和图像。如果两者都给出
颜色渲染在图像之上，允许半透明、着色
背景：

=== "Background color"

    ``` yaml
    size: { width: 1200, height: 630 }
    layers:
      - background:
          color: "#4051b5"
    ```

    ![Layer background color]

=== "Background image"

    ``` yaml
    size: { width: 1200, height: 630 }
    layers:
      - background:
          image: layouts/background.png
    ```

    ![Layer background image]

=== "Background image, tinted"

    ``` yaml
    size: { width: 1200, height: 630 }
    layers:
      - background:
          image: layouts/background.png
          color: "#4051b5ee" # (1)!
    ```

    1.  颜色值可以设置为[CSS颜色关键字]，或3、4、6或8
        字母HEX颜色代码，允许半透明层。

    ![Layer background]

背景图像会自动缩放以适应图层，同时保留
宽高比。请注意，我们省略了“size”和“offset”，因为我们想
填满社交卡的整个区域。

[Layer background color]: ../assets/screenshots/social-cards-layer-background-color.png
[Layer background image]: ../assets/screenshots/social-cards-layer-background-image.png
[Layer background]: ../assets/screenshots/social-cards-layer-background.png

### 字体排版

现在，我们可以添加来自Markdown文件的动态排版——这是
[内置社交插件]的实际存在理由。[Jinja模板]是
用于呈现文本字符串，然后将其添加到图像中：

``` yaml
size: { width: 1200, height: 630 }
layers:
  - size: { width: 832, height: 310 }
    offset: { x: 62, y: 160 }
    typography:
      content: "{{ page.title }}" # (1)!
      align: start
      color: white
      line:
        amount: 3
        height: 1.25
      font:
        family: Roboto
        style: Bold
```

1.  以下变量可用于[Jinja模板]：

    - [`config.*`][config variable]
    - [`page.*`][page variable]
    - [`layout.*`][layout options]

    作者可以自由定义“layout.*”选项，这些选项可用于传递
    从`mkdocs.yml`向布局添加任意数据。

这呈现了一个文本层，其中页面标题的行高为1.25，
最多3行。插件会自动计算字体大小
从行高、行数和字体度量（如ascender和
下行。[^2]这表示：

  [^2]:
    如果插件要求作者指定字体大小和行
    手动调整高度，无法保证文本适合
    进入该层。出于这个原因，我们实现了一种声明性方法，
    其中作者指定了所需的行高和行数，以及
    插件会自动计算字体大小。

![Layer typography]

  [config variable]: https://www.mkdocs.org/dev-guide/themes/#config
  [page variable]: https://www.mkdocs.org/dev-guide/themes/#page
  [Layer typography]: ../assets/screenshots/social-cards-layer-typography.png

#### 溢流

如果文本溢出图层，则有两种可能的行为：
文本会自动用省略号截断和缩短，或者
自动缩小以适应图层：

``` { .markdown .no-copy }
# 如果我们使用很长的标题，我们可以看到文本将如何被截断
```

=== ":octicons-ellipsis-16: Ellipsis"

    ![Layer typography ellipsis]

=== ":material-arrow-collapse: Shrink"

    ![Layer typography shrink]

虽然默认情况下使用省略号截断，但可以启用自动收缩
通过将“overflow”设置为“shrink”：

``` yaml hl_lines="7"
size: { width: 1200, height: 630 }
layers:
  - size: { width: 832, height: 310 }
    offset: { x: 62, y: 160 }
    typography:
      content: "{{ page.title }}"
      overflow: shrink
      align: start
      color: white
      line:
        amount: 3
        height: 1.25
      font:
        family: Roboto
        style: Bold
```

  [Layer typography ellipsis]: ../assets/screenshots/social-cards-layer-typography-ellipsis.png
  [Layer typography shrink]: ../assets/screenshots/social-cards-layer-typography-shrink.png

#### 对齐

文本可以与图层的所有角和边对齐。例如，如果我们
想要将文本对齐到层的中间，我们可以将`align`设置为`start-center`，这将呈现为：

![Layer typography align]

  [Layer typography align]: ../assets/screenshots/social-cards-layer-typography-align.png

下表显示了支持的值：

<figure markdown>

| Alignment      |                 |              |
| -------------- | --------------- | ------------ |
| :material-arrow-top-left:    `start top`    | :material-arrow-up:     `center top`    | :material-arrow-top-right:    `end top`    |
| :material-arrow-left:        `start center` | :material-circle-small: `center`        | :material-arrow-right:        `end center` |
| :material-arrow-bottom-left: `start bottom` | :material-arrow-down:   `center bottom` | :material-arrow-bottom-right: `end bottom` |

  <figcaption>
    Supported values for text alignment
  </figcaption>
</figure>

#### Font

[内置社交插件]与[谷歌字体]集成，并将
自动为您下载字体文件。`font`属性接受
`family和style属性，其中family必须设置为
将字体和“样式”转换为支持的字体样式之一。例如，设置
`family到Roboto会自动下载以下文件：

``` { .sh .no-copy #example }
.cache/plugins/social/fonts
└─ Roboto/
    ├─ Black.ttf
    ├─ Black Italic.ttf
    ├─ Bold.ttf
    ├─ Bold Italic.ttf
    ├─ Italic.ttf
    ├─ Light.ttf
    ├─ Light Italic.ttf
    ├─ Medium.ttf
    ├─ Medium Italic.ttf
    ├─ Regular.ttf
    ├─ Thin.ttf
    └─ Thin Italic.ttf
```

在这种情况下，作者可以使用“粗体”或“中斜体”作为“风格”。如果
图层中指定的字体样式不是字体族的一部分
font总是回退到“常规”，并在['debug][debug]中打印警告
模式，因为“常规”包含在所有字体系列中。

### 图标

作者可以利用Material附带的全系列图标
MkDocs，甚至通过使用主题扩展和浏览来提供自定义图标
[附加图标]指南中描述的过程。图标甚至可以
使用`color`属性着色：

``` yaml
size: { width: 1200, height: 630 }
layers:
  - background:
      color: "#4051b5"
  - size: { width: 144, height: 144 }
    offset: { x: 992, y: 64 }
    icon:
      value: material/cat
      color: white
```

这将显示社交卡右上角的图标：

![Layer icon]

可能性是无限的。例如，图标可用于绘制形状
像圆圈一样：

``` yaml
size: { width: 1200, height: 630 }
layers:
  - background:
      color: "#4051b5"
  - size: { width: 2400, height: 2400 }
    offset: { x: -1024, y: 64 }
    icon:
      value: material/circle
      color: "#5c6bc0"
  - size: { width: 1800, height: 1800 }
    offset: { x: 512, y: -1024 }
    icon:
      value: material/circle
      color: "#3949ab"
```

这将在背景中添加两个圆圈：

![Layer icon circles]

### 标签

新的[内置社交插件]为元标签提供了完全的灵活性
添加到您的网站，这是指导X等服务所必需的
或者不知道如何显示你的社交卡。所有默认布局都使用以下内容
标签集，您可以将其复制到布局中并进行调整：

``` yaml
definitions:

  - &page_title_with_site_name >-
    {%- if not page.is_homepage -%}
      {{ page.meta.get("title", page.title) }} - {{ config.site_name }}
    {%- else -%}
      {{ page.meta.get("title", page.title) }}
    {%- endif -%}

  - &page_description >-
    {{ page.meta.get("description", config.site_description) or "" }}

tags:

  og:type: website
  og:title: *page_title_with_site_name
  og:description: *page_description
  og:image: "{{ image.url }}"
  og:image:type: "{{ image.type }}"
  og:image:width: "{{ image.width }}"
  og:image:height: "{{ image.height }}"
  og:url: "{{ page.canonical_url }}"

  twitter:card: summary_large_image
  twitter:title: *page_title_with_site_name
  twitter:description: *page_description
  twitter:image: "{{ image.url }}"
```

请注意，此示例使用[YAML锚点]来减少重复。这个
`definitions属性仅用于定义别名
然后可以用锚点引用。

  [YAML anchors]: https://support.atlassian.com/bitbucket-cloud/docs/yaml-anchors/

__Are you missing something? Please [open a discussion] and let us know!__

  [additional icons]: ./changing-the-logo-and-icons.md#additional-icons
  [Layer icon]: ../assets/screenshots/social-cards-layer-icon.png
  [Layer icon circles]: ../assets/screenshots/social-cards-layer-icon-circles.png
  [open a discussion]: https://github.com/squidfunk/mkdocs-material/discussions/new

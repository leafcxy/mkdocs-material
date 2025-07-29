---
title: Built-in social plugin
icon: material/share-circle
---

# 内置社交插件

社交插件自动智能生成美丽和高度
每个页面都有不同[布局][默认布局]的可定制社交卡
在您或其他人共享时，将您的项目渲染为预览图像
社交媒体上的项目链接。

## 客观的

### 工作原理

该插件会自动为每个页面生成一张可定制的社交卡
您的项目，当共享到您的项目的链接时，它会显示为预览图像
项目在社交媒体上，无需使用外部服务，只需
[单行配置][配置]。

通过使用高效的[图像处理]库，该插件允许
为社交卡定义[自定义布局]，可以根据您的需求进行调整
项目的风格和品牌。虽然从技术上讲
通过使用网络浏览器和自动化框架生成社交卡，如
[Pupeter][^1]，这会给你的工具链增加更多的责任
有可能使管道建设更加复杂，资源更加密集，
并且明显较慢。

  [^1]:
    [GitHub在他们的博客中写道]他们使用[Pupeter]来生成社交媒体
    存储库、问题、提交、讨论和基本信息的卡片图像
    在社交媒体上分享时显示为预览图像的其他所有内容。

生成的社交卡被[缓存]并存储在
[`site`目录][mkdocs.site_dir]，因此是自托管的，确保您的
该项目不依赖于外部服务。为了生成社交卡
图像，您的系统上需要有一些[依赖项]可用。

  [configuration]: #configuration
  [image processing]: requirements/image-processing.md
  [custom layouts]: ../setup/setting-up-social-cards.md#customization
  [Puppeteer]: https://github.com/puppeteer/puppeteer
  [GitHub wrote in their blog]: https://github.blog/2021-06-22-framework-building-open-graph-images/
  [cached]: #caching
  [dependencies]: #configuration

### 何时使用

有一种特殊情况是我们不建议使用该插件：当你
构建[支持离线的文档]以提供下载。否则，它
启用插件总是有意义的，因为共享了指向文档的链接
在社交媒体上看起来会更有吸引力。

更有趣的是，该插件可以与其他内置插件结合使用
MkDocs提供的材料，用于创建复杂的构建
为您的项目量身定制的管道：

<div class="grid cards" markdown>

-   :material-newspaper-variant-outline: &nbsp; __[Built-in blog plugin][blog]__

    ---

    社交插件会自动生成美观且可定制的内容
    每个帖子和页面的社交卡片，在社交媒体上作为预览显示。

    ---

    __当在社交媒体上分享时，你博客的链接会呈现出精美的社交卡片__

-   :material-file-tree: &nbsp; __[Built-in meta plugin][meta]__

    ---

    元插件可用于[更改布局][meta.social.cards_layout]
    用于社交卡或[更改特定布局选项]
    [meta.social.cards_layout_options]类似于[background][option.background_color]
    或者对于页面子集使用[color][option.color]。

    ---

    __您的文档可以在每个部分使用完全不同的社交卡__

</div>

  [offline-capable documentation]: ../setup/building-for-offline-usage.md
  [blog]: blog.md
  [meta]: meta.md

## 配置

`version 8.5.0`
`plugin [social] – built-in`
`flag multiple`
`flag experimental`

为了开始使用社交插件，只需添加以下行即可
`mkdocs.yml`，并观察Material for mkdocs如何生成美丽的社交媒体
卡片给你：

``` yaml
plugins:
  - social
```

社交插件内置于MkDocs的Material中，不需要
安装。

但是，为了生成社交卡图像，有必要安装
[图像处理]的依赖关系，如果它们在您的
系统。链接的指南包括几个操作系统的说明
并提到了一些替代环境。

  [social]: social.md

### General

以下设置可用：

---

#### `setting config.enabled`

`version 8.5.0`
`default _true_`

使用此设置可在[构建项目]时启用或禁用插件。
如果你想禁用插件，例如，对于本地构建，你可以使用
`mkdocs.yml`中的[环境变量][mkdocs.env]：

``` yaml
plugins:
  - social:
      enabled: !ENV [CI, false]
```

此配置仅在持续集成（CI）期间启用插件。

  [building your project]: ../creating-your-site.md#building-your-site

---

#### `setting config.concurrency`

`sponsors`
`version insiders-4.33.0`
`default available CPUs - 1`

有了更多的CPU可用，插件可以并行执行更多的工作，因此
更快地完成社交卡生成。如果你想禁用并发
完全处理，使用：

``` yaml
plugins:
  - social:
      concurrency: 1
```

默认情况下，该插件使用所有可用的CPU-1，最小值为1。

### 缓存

该插件实现了[智能缓存]机制，确保社交
卡片只有在内容发生变化或尚未更新时才会重新生成
包含在缓存中。如果布局中使用的任何变量发生变化
插件检测到它并重新生成社交卡。

以下设置可用于缓存：

  [intelligent caching]: requirements/caching.md

---

#### `setting config.cache`

`sponsors`
`version insiders-4.33.0`
`default _true_`

使用此设置指示插件绕过缓存，以便
为所有页面重新生成社交卡，即使缓存可能不会过时。
通常不需要指定此设置，调试时除外
插件本身。可以通过以下方式禁用缓存：

``` yaml
plugins:
  - social:
      cache: false
```

---

#### `setting config.cache_dir`

`version 8.5.0`
`default _.cache/plugin/social_`

通常不需要指定此设置，除非您需要
更改根目录中社交卡图像的路径
缓存。如果你想更改它，请使用：

``` yaml
plugins:
  - social:
      cache_dir: my/custom/dir
```

如果你正在使用该插件的[多个实例]，这可能是一个好主意
为两个实例设置不同的缓存目录，这样它们就不会相互干扰
彼此。

  [multiple instances]: index.md#multiple-instances

### 登录中

以下设置可用于日志记录：

---

#### `setting config.log`

`sponsors`
`version insiders-4.40.2`
`default _true_`

使用此设置可控制插件是否仅在以下情况下记录错误
在不终止构建的情况下生成社交卡，例如无效的引用
到图标。要终止构建，请使用：

``` yaml
plugins:
  - social:
      log: false
```

---

#### `setting config.log_level`

`sponsors`
`version insiders-4.40.2`
`default _warn_`

使用此设置控制插件在以下情况下应采用的日志级别
遇到错误，这要求[`log`][config.log]设置为
启用。以下日志级别可用：

=== "`warn`"

    ``` yaml
    plugins:
      - social:
          log_level: warn
    ```

    错误报告为警告，终止内置程序
    [严格][mkdocs.strict]模式。

=== "`info`"

    ``` yaml
    plugins:
      - social:
          log_level: info
    ```

    错误仅作为信息性消息报告。

=== "`ignore`"

    ``` yaml
    plugins:
      - social:
          log_level: ignore
    ```

    只有在使用“--verbose”标志时才会报告错误。

### 社交卡

以下设置可用于社交卡生成：

---

#### `setting config.cards`

`version 8.5.0`
`default _true_`

使用此设置启用或禁用社交卡生成。目前
插件的唯一目的是生成社交卡，因此它相当于
[`enabled'][config.enabled]设置，但将来可能会有其他功能
补充。如果要禁用社交卡生成，请使用：

``` yaml
plugins:
  - social:
      cards: false
```

---

#### `setting config.cards_dir`

`version 8.5.0`
`default _assets/images/social_`

通常不需要指定此设置，除非您需要
更改[`site`目录][mkdocs.site_dir]中的路径，其中
存储社交卡。如果你想更改它，请使用：

``` yaml
plugins:
  - social:
      cards_dir: my/custom/dir
```

此配置将生成的图像存储在“my/custom/dir”中
[站点目录][mkdocs.site_dir]。

---

#### `setting config.cards_layout_dir`

`sponsors`
`version insiders-4.33.0`
`default _layouts_`

如果你想构建[自定义社交卡布局][自定义布局]，请使用此
设置以更改存储自定义布局的默认文件夹
是根目录中名为“layouts”的文件夹：

``` yaml
plugins:
  - social:
      cards_layout_dir: layouts
```

提供的路径是从根目录解析的。

!!! tip "在哪里存储自定义布局"

    我们的建议是将文件夹放在
    [`docs`目录][mkdocs.docs-dir]，以确保您的[自定义布局]
    在以下情况下，不会复制到[`site`目录][mkdocs.site_dir]
    [构建你的项目]，例如，通过遵循以下目录
    布局：

    ``` { .sh .no-copy }
    .
    ├─ docs/
    │  └─ *.md
    ├─ layouts/
    │  └─ *.yml
    └─ mkdocs.yml
    ```

---

#### `setting config.cards_layout`

`sponsors`
`version insiders-4.33.0`
`default _default_`

该插件提供了越来越多的[默认布局][默认布局]列表，用于
社交卡。如果您已经创建了[自定义社交卡布局][自定义布局]，
您可以指示插件将其完全用作包含的布局之一：

``` yaml
plugins:
  - social:
      cards_layout: my-custom-layout
```

提供的路径从以下位置解析[
`layouts目录][config.cadslayout_dir]。

!!! tip "如何解决自定义布局"

    默认情况下，插件将从名为的文件夹加载您的[自定义布局]
    `layouts位于您的根目录中。如果您的布局被调用
    `我的自定义布局，目录布局必须遵守：

    ``` { .sh .no-copy }
    .
    ├─ docs/
    │  └─ *.md
    ├─ layouts/
    │  └─ my-custom-layout.yml
    └─ mkdocs.yml
    ```

---

#### `setting config.cards_layout_options`

`version 9.1.10`
`default none`

使用此设置为通过[`cards_layout`]指定的布局设置选项
[config.cards_layout]（如果布局支持），它允许制作
布局简单且完全可配置：

``` yaml
plugins:
  - social:
      cards_layout_options:
        <option>: <value>
```

在创建[自定义布局][自定义布局]时，您可以完全自由地
定义布局的哪些部分可以参数化。[默认布局]
插件附带的[默认布局]支持以下选项：

<div class="mdx-columns" markdown>

- [`background_color`][option.background_color]
- [`background_image`][option.background_image]
- [`color`][option.color]
- [`font_family`][option.font_family]
- [`font_variant`][option.font_variant]
- [`logo`][option.logo]
- [`title`][option.title]
- [`description`][option.description]

</div>


  [default layouts]: #layouts

---

#### `setting config.cards_include`

`sponsors`
`version insiders-4.35.0`
`default none`

使用此设置为您的子部分启用社交卡生成
项目，例如，当使用插件的[多个实例]生成
不同子部分的不同社交卡：

``` yaml
plugins:
  - social:
      cards_include:
        - blog/*
```

此配置允许为以下所有页面生成社交卡
包含在[文档目录]中的博客文件夹及其子文件夹中
[mkdocs.docs_dir]。

---

#### `setting config.cards_exclude`

`sponsors`
`version insiders-4.35.0`
`default none`

使用此设置可禁用您的子部分的社交卡生成
项目，例如，当使用插件的[多个实例]生成
不同子部分的不同社交卡：

``` yaml
plugins:
  - social:
      cards_exclude:
        - changelog/*
```

此配置禁用以下所有页面的社交卡生成
包含在“changelog”文件夹及其子文件夹中
[文档目录][mkdocs.docs_dir]。

### 调试

该插件包括一个用于调试布局的特殊模式，这非常有用
在创建[自定义布局]时，因为它允许更快的迭代和更好的
理解构图。

以下设置可用于调试：

---

#### `setting config.debug`

`sponsors`
`version insiders-4.33.0`
`default _false_`

使用此设置启用调试布局的特殊模式
用彩色轮廓及其“x”和“y”偏移量渲染每一层，以及
覆盖一个点网格进行对齐，这样更容易理解
布局的不同层组成在一起：

``` yaml
plugins:
  - social:
      debug: true
```

---

#### `setting config.debug_on_build`

`sponsors`
`version insiders-4.34.1`
`default _false_`

默认情况下，当出现以下情况时，插件会自动禁用['debug][config.debug]模式
[构建你的项目]，这样你就可以确保调试覆盖永远不会
部署到生产。如果你想改变这一点，请使用：

``` yaml
plugins:
  - social:
      debug_on_build: true
```

通常不需要更改此设置，因为它只是为了
成为安全网。

---

#### `setting config.debug_grid`

`sponsors`
`version insiders-4.33.0`
`default _true_`

当启用[`debug`][config.debug]模式时，此设置指定是否
点网格渲染在所有层的顶部，以便更好地对齐。如果你
要关闭电网，请使用：

``` yaml
plugins:
  - social:
      debug_grid: false
```

---

#### `setting config.debug_grid_step`

`sponsors`
`version insiders-4.33.0`
`default _32_`

使用此设置指定点阵的步长（以像素为单位）（如果启用），
这可用于创建完美对齐的层以实现理想的构图。
如果你想更改它，请使用：

``` yaml
plugins:
  - social:
      debug_grid_step: 64
```

---

#### `setting config.debug_color`

`sponsors`
`version insiders-4.33.0`
`default _grey_`

使用此设置指定添加到每个轮廓的颜色
图层和渲染在所有图层上的点网格。如果你需要
更改它，使用：

``` yaml
plugins:
  - social:
      debug_color: yellow
```

在极少数情况下，如果点网格或
轮廓很难区分，因为插件会自动调整
如果没有明确设置颜色。

## 使用

### 元数据

该插件允许通过元数据覆盖设置的子集（front
事宜）以定制社交卡生成，例如设置[选项
单个页面的默认布局，甚至
通过利用[meta]插件，您的项目的[整个子部分]。

以下属性可用：

  [for an entire subsection]: meta.md#how-it-works
  [meta]: meta.md

---

#### `setting meta.social.cards`

`sponsors`
`version insiders-4.37.0`
`flag metadata`
`default none`

使用此属性覆盖给定的[`cards][config.cards]设置
页面：

``` yaml
---
social:
  cards: false
---

# Page title
...
```

---

#### `setting meta.social.cards_layout`

`sponsors`
`version insiders-4.37.0`
`flag metadata`
`default none`
`flag experimental`

使用此属性覆盖[`cards_layout`][config.cards_layout]设置
对于给定的页面：

``` yaml
---
social:
  cards_layout: my-custom-layout
---

# Page title
...
```

---

#### `setting meta.social.cards_layout_options`

`sponsors`
`version insiders-4.37.0`
`flag metadata`
`default none`

使用此属性覆盖[`cards_layout_options`]
给定页面的[config.cards_layout_options]设置：

``` yaml
---
social:
  cards_layout_options:
    background_color: blue             # Change background color
    background_image: null             # Remove background image
---

# Page title
...
```

将选项设置为`#！yaml null会重置该选项。

### 布局

`sponsors`
`version insiders-4.33.0`

虽然构建[自定义布局]是可能且简单的，但该插件附带了
几个预定义的布局，所有布局都以“默认”为前缀。这个
包括以下布局：

=== "`default`"

    ``` yaml
    plugins:
      - social:
          cards_layout: default
    ```

    <div class="result" markdown>

    ![Layout default]

    This layout sets the following defaults:

    - [`background_color`][option.background_color]
      – `default [_theme.palette.primary_][primary color]`

    - [`font_family`][option.font_family]
      – `default [_theme.font.text_][font]`

    </div>

=== "`default/variant`"

    ``` yaml
    plugins:
      - social:
          cards_layout: default/variant
    ```

    <div class="result" markdown>

    ![Layout default variant]

    This layout includes the [page icon] and sets the following defaults:

    - [`background_color`][option.background_color]
      – `default [_theme.palette.primary_][primary color]`

    - [`font_family`][option.font_family]
      – `default [_theme.font.text_][font]`

    </div>

=== "`default/accent`"

    ``` yaml
    plugins:
      - social:
          cards_layout: default/accent
    ```

    <div class="result" markdown>

    ![Layout default accent]

    This layout sets the following defaults:

    - [`background_color`][option.background_color]
      – `default [_theme.palette.accent_][accent color]`

    - [`font_family`][option.font_family]
      – `default [_theme.font.text_][font]`

    </div>

=== "`default/invert`"

    ``` yaml
    plugins:
      - social:
          cards_layout: default/invert
    ```

    <div class="result" markdown>

    ![Layout default invert]

    This layout sets the following defaults:

    - [`color`][option.background_color]
      – `default [_theme.palette.primary_][primary color]`

    - [`font_family`][option.font_family]
      – `default [_theme.font.text_][font]`

    </div>

=== "`default/only/image`"

    ``` yaml
    plugins:
      - social:
          cards_layout: default/only/image
          cards_layout_options:
            background_image: layouts/background.png

    ```

    <div class="result" markdown>

    此布局仅显示给定的背景图像，并将其缩放以覆盖。

    </div>

[默认布局][默认布局]非常灵活和舒适
当它们复制插件的原始行为时，使用默认的源代码
其他“主题”设置中所有选项的值。

以下选项可用：

  [Layout default]: ../assets/screenshots/social-cards.png
  [Layout default variant]: ../assets/screenshots/social-cards-variant.png
  [Layout default accent]: ../assets/screenshots/social-cards-accent.png
  [Layout default invert]: ../assets/screenshots/social-cards-invert.png

  [primary color]: ../setup/changing-the-colors.md#primary-color
  [page icon]: ../reference/index.md#setting-the-page-icon
  [accent color]: ../setup/changing-the-colors.md#accent-color
  [font]: ../setup/changing-the-fonts.md#regular-font

---

#### `setting option.background_color`

`version 9.1.10`
`default computed`

使用此选项更改生成的社交卡的背景颜色。
该值可以设置为有效的颜色值[枕头支持]，成像
用于卡片生成的库：

=== "Hexadecimal"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            background_color: "#ff1493" # (1)!
    ```

    1.  支持以下符号，但
        `#`必须是范围`#！css 0-F`：

        - `#!css #rgb` – Color (short)
        - `#!css #rgba` – Color + alpha (short)
        - `#!css #rrggbb` – Color
        - `#!css #rrggbbaa` – Color + alpha

=== "Color function"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            background_color: rgb(255, 20, 147) # (1)!
    ```

    1.  支持以下功能，列出了允许的最大值
        最小值均为“#！css 0或#！css 0%：

        - `#!css rgb(255, 255, 255)` – Red, green and blue
        - `#!css hsl(360, 100%, 100%)` – Hue, saturation and lightness
        - `#!css hsv(360, 100%, 100%)` – Hue, saturation and value

=== "Color name"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            background_color: deeppink # (1)!
    ```

    1.  请参阅[`<named color>`][named color=]CSS数据类型，以获取以下列表
        支持的颜色名称。请注意，有些可能不可用。

如果此选项与[背景图片]一起使用
[option.background_image]，颜色渲染在图像之上
允许对图像进行着色。如果要删除背景色，请使用：

``` yaml
plugins:
  - social:
      cards_layout_options:
        background_color: transparent
```

  [supported by pillow]: https://pillow.readthedocs.io/en/stable/reference/ImageColor.html#color-names
  [named-color]: https://developer.mozilla.org/en-US/docs/Web/CSS/named-color

---

#### `setting option.background_image`

`sponsors`
`version insiders-4.33.0`
`default none`

使用此选项为生成的社交卡定义背景图像。注：
图像用[背景颜色][选项.background_color]着色，
其也可以设置为“透明”：

=== "Image"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            background_image: layouts/background.png
            background_color: transparent
    ```

=== "Image with tint"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            background_image: layouts/background.png
            background_color: "#ff149366"
    ```

提供的路径是从根目录解析的。

---

#### `setting option.color`

`version 9.1.10`
`default computed`

使用此选项更改生成的社交卡的前景颜色。
该值可以设置为有效的颜色值[枕头支持]，成像
用于卡片生成的库：

=== "Hexadecimal"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            color: "#ffffff" # (1)!
    ```

    1.  支持以下符号，但
        `#`必须是范围`#！css 0-F`：

        - `#!css #rgb` – Color (short)
        - `#!css #rgba` – Color + alpha (short)
        - `#!css #rrggbb` – Color
        - `#!css #rrggbbaa` – Color + alpha

=== "Color function"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            color: rgb(255, 255, 255) # (1)!
    ```

    1.  支持以下功能，列出了允许的最大值
        最小值均为“#！css 0或#！css 0%：

        - `#!css rgb(255, 255, 255)` – Red, green and blue
        - `#!css hsl(360, 100%, 100%)` – Hue, saturation and lightness
        - `#!css hsv(360, 100%, 100%)` – Hue, saturation and value

=== "Color name"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            color: white # (1)!
    ```

    1.  请参阅[`<named color>`][named color=]CSS数据类型，以获取以下列表
        支持的颜色名称。请注意，有些可能不可用。

---

#### `setting option.font_family`

`version 9.1.10`
`default computed`

使用此选项更改生成的社交卡的字体系列。这个
插件会自动从[Google Fonts]下载字体，因此字体必须
指向现有的Google字体：

``` yaml
plugins:
  - social:
      cards_layout_options:
        font_family: Ubuntu
```

当你在[谷歌字体]上找到你喜欢的字体时，你可以复制
从字体的示例页面中选择名称，并将其用作此选项的值——
不需要进一步的配置。

  [Google Fonts]: https://fonts.google.com/

---

#### `setting option.font_variant`

`sponsors`
`version insiders-4.53.3`
`default none`

使用此选项更改用于生成社交卡的字体变体。
如果下载的字体有“压缩”或“扩展”等变体，您可以设置
他们与：

``` yaml
plugins:
  - social:
      cards_layout_options:
        font_variant: Condensed
```

该变体与自定义布局中使用的样式相结合，因此
插件被指示使用“压缩规则”或
`扩展粗体。

---

#### `setting option.logo`

`sponsors`
`version insiders-4.40.0`
`default computed`

使用此选项更改生成的社交卡中使用的徽标。
默认情况下，该插件使用[`theme.logo`][theme.logo]或[`theme.comp.logo`]
从`mkdocs.yml`设置[theme.icon.logo]。您可以通过以下方式进行更改：

``` yaml
plugins:
  - social:
      cards_layout_options:
        logo: layouts/logo.png
```

提供的路径是从根目录解析的。

  [theme.logo]: ../setup/changing-the-logo-and-icons.md#logo-image
  [theme.icon.logo]: ../setup/changing-the-logo-and-icons.md#logo-icon-bundled

---

#### `setting option.title`

`sponsors`
`version insiders-4.40.0`
`default computed`

使用此选项更改生成的社交卡的标题。这将覆盖
MkDocs分配的计算页面标题，以及[“标题”]
[meta.title]元数据属性：

``` yaml
plugins:
  - social:
      cards_layout_options:
        title: My custom title
```

  [meta.title]: ../reference/index.md#setting-the-page-title

---

#### `setting option.description`

`sponsors`
`version insiders-4.40.0`
`default computed`

使用此选项更改生成的社交卡的描述。这个
覆盖集合[`site_description][mkdocs.site_descripting]（如果已定义），如下所示
以及[`description][meta.description]元数据属性：

``` yaml
plugins:
  - social:
      cards_layout_options:
        description: My custom description
```

  [meta.description]: ../reference/index.md#setting-the-page-description

---

!!! question "缺少什么？"

    在设置社交卡时，你可能会发现自己错过了
    特定功能–我们很乐意考虑将其添加到插件中！
    您可以[展开讨论]提出问题，或创建[更改请求]
    在我们的[问题跟踪器]上，这样我们就可以知道它是否适合
    插件。

  [open a discussion]: https://github.com/squidfunk/mkdocs-material/discussions
  [change request]: ../contributing/requesting-a-change.md
  [issue tracker]: https://github.com/squidfunk/mkdocs-material/issues

# 更改字体

Material for MkDocs 使更改项目文档的字体变得简单，因为它直接集成了 [Google Fonts]。或者，如果出于数据隐私原因需要自托管或使用其他目标，可以自定义加载字体。

  [Google Fonts]: https://fonts.google.com

## 配置

### 常规字体

<!-- md:version 0.1.2 -->
<!-- md:default [`Roboto`][Roboto] -->

常规字体用于所有正文、标题，以及基本上所有不需要等宽字体的内容。可以通过 `mkdocs.yml` 将其设置为任何有效的 [Google Font][Google Fonts]：

``` yaml
theme:
  font:
    text: Roboto
```

字体将以 300、400、_400i_ 和 __700__ 的粗细加载。

  [Roboto]: https://fonts.google.com/specimen/Roboto

### 等宽字体

<!-- md:version 0.1.2 -->
<!-- md:default [`Roboto Mono`][Roboto Mono] -->

_等宽字体_ 用于代码块，可以单独配置。就像常规字体一样，可以通过 `mkdocs.yml` 将其设置为任何有效的 [Google Font][Google Fonts]：

``` yaml
theme:
  font:
    code: Roboto Mono
```

字体将以 400 的粗细加载。

  [Roboto Mono]: https://fonts.google.com/specimen/Roboto+Mono

### 自动加载

<!-- md:version 1.0.0 -->
<!-- md:default none -->

如果您想防止从 [Google Fonts] 加载字体，例如为了遵守[数据隐私]法规，并回退到系统字体，请在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  font: false
```

!!! tip "自动捆绑 Google Fonts"

    [内置隐私插件]使您可以在遵守 __通用数据保护条例__ (GDPR) 的同时轻松使用 Google Fonts，通过自动下载和自托管网络字体文件。

  [数据隐私]: https://developers.google.com/fonts/faq/privacy
  [内置隐私插件]:../plugins/privacy.md

## 自定义

### 额外字体

如果您想从其他目标加载（额外）字体或覆盖系统字体，可以使用[额外样式表]添加相应的 `@font-face` 定义：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    @font-face {
      font-family: "<font>";
      src: "...";
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

然后可以将字体应用于特定元素，例如仅标题，或全局用作网站范围的常规或等宽字体：

=== "常规字体"

    ``` css
    :root {
      --md-text-font: "<font>"; /* (1)! */
    }
    ```

    1.  始终通过 CSS 变量定义字体，而不是 `font-family`，因为这会禁用系统字体回退。

=== "等宽字体"

    ``` css
    :root {
      --md-code-font: "<font>";
    }
    ```

  [额外样式表]: ../customization.md#additional-css

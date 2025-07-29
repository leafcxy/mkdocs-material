# 更改字体

MkDocs的材料使更改项目的字体变得容易
文档，因为它直接与[谷歌字体]集成。或者，
如果出于数据隐私原因首选自托管，则可以自定义加载字体
或者应该使用另一个目的地。

  [Google Fonts]: https://fonts.google.com

## 配置

### 常规字体

`version 0.1.2`
`default [_Roboto_][Roboto]`

常规字体用于所有正文、标题和基本内容
所有不需要等宽的东西。它可以设置为任何
通过`mkdocs.yml`使用有效的[Google Font][Google Fonts]：

``` yaml
theme:
  font:
    text: Roboto
```

字体将加载为300、400、400i_和700__。

  [Roboto]: https://fonts.google.com/specimen/Roboto

### 等宽字体

`version 0.1.2`
`default [_Roboto Mono_][Roboto Mono]`

_monospace font_用于代码块，可以单独配置。
就像常规字体一样，它可以设置为任何有效的[谷歌字体]
[谷歌字体]通过`mkdocs.yml`：

``` yaml
theme:
  font:
    code: Roboto Mono
```

字体将加载400。

  [Roboto Mono]: https://fonts.google.com/specimen/Roboto+Mono

### 自动加载

`version 1.0.0`
`default none`

如果你想阻止从[谷歌字体]加载字体，例如。
要遵守[数据隐私]规定，并退回到系统字体，请添加
将以下行转换为`mkdocs.yml`：

``` yaml
theme:
  font: false
```

!!! tip "自动捆绑Google字体"

    [内置隐私插件]使使用谷歌字体变得容易
    在遵守《通用数据保护条例》（GDPR）的同时，
    通过自动下载和自托管网络字体文件。

  [data privacy]: https://developers.google.com/fonts/faq/privacy
  [built-in privacy plugin]:../plugins/privacy.md

## 自定义

### 附加字体

如果你想从另一个目标加载（额外）字体或覆盖
系统字体，您可以使用[附加样式表]添加
对应的“@font-face”定义：

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

然后，字体可以应用于特定元素，例如仅标题，或
在全球范围内用作全站常规或等宽字体：

=== "Regular font"

    ``` css
    :root {
      --md-text-font: "<font>"; /* (1)! */
    }
    ```

    1.  始终通过CSS变量定义字体，而不是“字体家族”，如
        这将禁用系统字体回退。

=== "Monospaced font"

    ``` css
    :root {
      --md-code-font: "<font>";
    }
    ```

  [additional style sheet]: ../customization.md#additional-css

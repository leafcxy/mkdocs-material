# 更改语言

MkDocs材料支持国际化（i18n），并提供
60多种语言的模板变量和标签翻译。另外，
如果满足以下条件，则可以将站点搜索配置为使用特定语言的词干分析器
可用。

## 配置

### 网站语言

<!-- md:version 1.12.0 -->
<!-- md:default `en` -->

您可以在`mkdocs.yml`中设置网站语言：

``` yaml
theme:
  language: en # (1)!
```

1.  HTML5只允许设置[每个文档一种语言]，这就是为什么
    MkDocs的材料仅支持为
    整个项目，即每个“mkdocs.yml”一个。

    构建多语言文档的最简单方法是创建一个
    按语言将项目放在子文件夹中，然后使用[语言选择器]
    将这些项目联系起来。

支持以下语言：

<!-- hooks/translations.py -->

请注意，由于某种方式，某些语言会产生不可读的锚链接
默认的slug函数有效。考虑使用[Unicode感知的slug函数]。

!!! tip "翻译缺失？帮帮我们，只需要5分钟"

    MkDocs的材料依赖于外部贡献来添加和更新
    它支持60多种语言的翻译。如果你的语言
    显示缺少某些翻译，请单击链接添加它们。如果
    您的语言不在列表中，请单击此处[添加新语言]。

  [single language per document]: https://www.w3.org/International/questions/qa-html-language-declarations.en#attributes
  [language selector]: #site-language-selector
  [Unicode-aware slug function]: extensions/python-markdown.md#+toc.slugify
  [add a new language]: https://github.com/squidfunk/mkdocs-material/issues/new?template=04-add-a-translation.yml&title=Add+translations+for+...

### 站点语言选择器

<!-- md:version 7.0.0 -->
<!-- md:default none -->

如果您的文档有多种语言版本，请使用语言选择器
指向这些语言的内容可以添加到标题中。替代语言
可以通过`mkdocs.yml`进行定义。

``` yaml
extra:
  alternate:
    - name: English
      link: /en/ # (1)!
      lang: en
    - name: Deutsch
      link: /de/
      lang: de
```

1.  请注意，这必须是一个绝对链接。如果它包含域部分，它是
    按定义使用。否则，['site_url][site_url]的域部分为
    在“mkdocs.yml”中设置的内容将添加到链接之前。

以下属性适用于每种备用语言：

<!-- md:option alternate.name -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性的值在语言选择器中用作
    语言的名称，并且必须设置为非空字符串。

<!-- md:option alternate.link -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须设置为绝对链接，该链接也可能指向
    不一定用MkDocs生成的另一个域或子域。

<!-- md:option alternate.lang -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须包含[ISO 639-1语言代码]，用于
    链接的hreflang属性，通过搜索提高可发现性
    发动机。

[![Language selector preview]][Language selector preview]

  [site_url]: https://www.mkdocs.org/user-guide/configuration/#site_url
  [ISO 639-1 language code]: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
  [Language selector preview]: ../assets/screenshots/language-selection.png

#### 停留在页面上

<!-- md:sponsors -->
<!-- md:version insiders-4.47.0 -->
<!-- md:flag experimental -->

[内部人员]改善了在语言之间切换时的用户体验。，
如果语言“en”和“de”包含具有相同路径名的页面，则用户将
停留在当前页面：

=== "Insiders"

    ```
    docs.example.com/en/     -> docs.example.com/de/
    docs.example.com/en/foo/ -> docs.example.com/de/foo/
    docs.example.com/en/bar/ -> docs.example.com/de/bar/
    ```

=== "Material for MkDocs"

    ```
    docs.example.com/en/     -> docs.example.com/de/
    docs.example.com/en/foo/ -> docs.example.com/de/
    docs.example.com/en/bar/ -> docs.example.com/de/
    ```

无需配置。我们正在努力提高多语言能力
2024年的支持，包括使语言之间的切换更加无缝
未来。

  [Insiders]: ../insiders/index.md

### 方向性

<!-- md:version 2.5.0 -->
<!-- md:default computed -->

虽然许多语言都是从左到右阅读“ltr”，但MkDocs的材料也是如此
支持“rtl”（从右到左）方向性，这是从
所选语言，但也可以设置为：

``` yaml
theme:
  direction: ltr
```

单击互动程序以更改方向：

<div class="mdx-switch">
  <button data-md-dir="ltr"><code>ltr</code></button>
  <button data-md-dir="rtl"><code>rtl</code></button>
</div>

<script>
  var buttons = document.querySelectorAll("button[data-md-dir]")
  buttons.forEach(function(button) {
    button.addEventListener("click", function() {
      var attr = this.getAttribute("data-md-dir")
      document.body.dir = attr
      var name = document.querySelector("#__code_2 code span.l")
      name.textContent = attr
    })
  })
</script>

## 自定义

### 自定义翻译

如果你想为一种语言定制一些翻译，只需按照以下步骤操作
关于[主题扩展]的指南，并在“覆盖”中创建一个新的部分`
文件夹。然后，导入该语言的[翻译]作为后备，并且仅
调整要覆盖的内容：

=== ":octicons-file-code-16: `overrides/partials/languages/custom.html`"

    ``` html
    <!-- Import translations for language and fallback -->
    {% import "partials/languages/de.html" as language %}
    {% import "partials/languages/en.html" as fallback %} <!-- (1)! -->

    <!-- Define custom translations -->
    {% macro override(key) %}{{ {
      "source.file.date.created": "Erstellt am", <!-- (2)! -->
      "source.file.date.updated": "Aktualisiert am"
    }[key] }}{% endmacro %}

    <!-- Re-export translations -->
    {% macro t(key) %}{{
      override(key) or language.t(key) or fallback.t(key)
    }}{% endmacro %}
    ```

    1.  Note that `en` must always be used as a fallback language, as it's the
        default theme language.

    2.  Check the [list of available languages], pick the translation you want
        to override for your language and add them here.

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    theme:
      language: custom
    ```

  [theme extension]: ../customization.md#extending-the-theme
  [translations]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/languages/
  [list of available languages]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/languages/

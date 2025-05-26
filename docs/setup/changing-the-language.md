# 更改语言

Material for MkDocs 支持国际化（i18n），并为 60 多种语言提供模板变量和标签的翻译。此外，如果可用，网站搜索可以配置为使用特定语言的词干提取器。

## 配置

### 网站语言

<!-- md:version 1.12.0 -->
<!-- md:default `en` -->

您可以在 `mkdocs.yml` 中设置网站语言：

``` yaml
theme:
  language: en # (1)!
```

1.  HTML5 只允许为每个文档设置[单一语言]，这就是为什么
    Material for MkDocs 只支持为整个项目设置规范语言，即每个 `mkdocs.yml` 一个。

    构建多语言文档最简单的方法是为每种语言在子文件夹中创建一个项目，然后使用[语言选择器]将这些项目相互链接。

支持以下语言：

<!-- hooks/translations.py -->

请注意，由于默认 slug 函数的工作方式，某些语言会产生不可读的锚点链接。考虑使用[支持 Unicode 的 slug 函数]。

!!! tip "缺少翻译？帮助我们，只需 5 分钟"

    Material for MkDocs 依靠外部贡献来添加和更新其支持的 60 多种语言的翻译。如果您的语言显示某些翻译缺失，请点击链接添加它们。如果您的语言不在列表中，请点击此处[添加新语言]。

  [单一语言]: https://www.w3.org/International/questions/qa-html-language-declarations.en#attributes
  [语言选择器]: #site-language-selector
  [支持 Unicode 的 slug 函数]: extensions/python-markdown.md#+toc.slugify
  [添加新语言]: https://github.com/squidfunk/mkdocs-material/issues/new?template=04-add-a-translation.yml&title=Add+translations+for+...

### 网站语言选择器

<!-- md:version 7.0.0 -->
<!-- md:default none -->

如果您的文档有多种语言版本，可以在页眉中添加指向这些语言的语言选择器。可以通过 `mkdocs.yml` 定义替代语言。

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

1.  请注意，这必须是一个绝对链接。如果包含域名部分，则按原样使用。否则，将 `mkdocs.yml` 中设置的 [`site_url`][site_url] 的域名部分添加到链接前面。

每个替代语言可以使用以下属性：

<!-- md:option alternate.name -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性的值在语言选择器中用作语言名称，必须设置为非空字符串。

<!-- md:option alternate.link -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须设置为绝对链接，也可以指向不一定由 MkDocs 生成的另一个域或子域。

<!-- md:option alternate.lang -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须包含 [ISO 639-1 语言代码]，用于链接的 `hreflang` 属性，通过搜索引擎提高可发现性。

[![语言选择器预览]][Language selector preview]

  [site_url]: https://www.mkdocs.org/user-guide/configuration/#site_url
  [ISO 639-1 语言代码]: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
  [Language selector preview]: ../assets/screenshots/language-selection.png

#### 停留在当前页面

<!-- md:sponsors -->
<!-- md:version insiders-4.47.0 -->
<!-- md:flag experimental -->

[Insiders] 改进了在语言之间切换时的用户体验，例如，如果语言 `en` 和 `de` 包含具有相同路径名称的页面，用户将停留在当前页面：

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

无需配置。我们正在努力改进 2024 年的多语言支持，包括在未来使语言之间的切换更加无缝。

  [Insiders]: ../insiders/index.md

### 方向性

<!-- md:version 2.5.0 -->
<!-- md:default computed -->

虽然许多语言是从左到右（`ltr`）阅读的，但 Material for MkDocs 也支持从右到左（`rtl`）的方向性，这是从所选语言推断出来的，但也可以通过以下方式设置：

``` yaml
theme:
  direction: ltr
```

点击一个方块来更改方向性：

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

如果您想自定义某种语言的一些翻译，只需按照[主题扩展]指南在 `overrides` 文件夹中创建一个新的部分。然后，导入该语言的[翻译]作为后备，只调整您想要覆盖的部分：

=== ":octicons-file-code-16: `overrides/partials/languages/custom.html`"

    ``` html
    <!-- 导入语言翻译和后备翻译 -->
    {% import "partials/languages/de.html" as language %}
    {% import "partials/languages/en.html" as fallback %} <!-- (1)! -->

    <!-- 定义自定义翻译 -->
    {% macro override(key) %}{{ {
      "source.file.date.created": "Erstellt am", <!-- (2)! -->
      "source.file.date.updated": "Aktualisiert am"
    }[key] }}{% endmacro %}

    <!-- 重新导出翻译 -->
    {% macro t(key) %}{{
      override(key) or language.t(key) or fallback.t(key)
    }}{% endmacro %}
    ```

    1.  请注意，`en` 必须始终用作后备语言，因为它是默认主题语言。

    2.  查看[可用语言列表]，选择您想要为您的语言覆盖的翻译并在此处添加。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    theme:
      language: custom
    ```

  [主题扩展]: ../customization.md#extending-the-theme
  [翻译]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/languages/
  [可用语言列表]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/languages/

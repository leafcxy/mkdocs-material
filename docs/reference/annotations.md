---
icon: material/plus-circle
---

# 注释

Material for MkDocs 的标志性功能之一就是能够插入注释 - 这些小标记可以添加到文档的几乎任何位置，并在点击或键盘聚焦时展开包含任意 Markdown 内容的工具提示。

## 配置

此配置允许向所有行内和块级元素以及代码块添加注释，并允许注释相互嵌套。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - attr_list
  - md_in_html
  - pymdownx.superfences
```

查看更多配置选项：

- [Attribute Lists]
- [Markdown in HTML]
- [SuperFences]

  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists
  [Markdown in HTML]: ../setup/extensions/python-markdown.md#markdown-in-html
  [SuperFences]: ../setup/extensions/python-markdown-extensions.md#superfences

### 注释图标

<!-- md:version 9.2.0 -->

注释图标可以更改为主题中包含的任何图标，甚至是[自定义图标]，例如 material/arrow-right-circle:。只需将以下行添加到 `mkdocs.yml`：

``` yaml
theme:
  icon:
    annotation: material/arrow-right-circle # (1)!
```

1.  输入几个关键词，使用我们的[图标搜索]找到完美的图标，然后点击短代码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="搜索图标" data-mdx-component="iconsearch-query" value="material circle" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

一些流行的选择：

- :material-plus-circle: - `material/plus-circle`
- :material-circle-medium: - `material/circle-medium`
- :material-record-circle: - `material/record-circle`
- :material-arrow-right-circle: - `material/arrow-right-circle`
- :material-arrow-right-circle-outline: - `material/arrow-right-circle-outline`
- :material-chevron-right-circle: - `material/chevron-right-circle`
- :material-star-four-points-circle: - `material/star-four-points-circle`
- :material-plus-circle-outline: - `material/plus-circle-outline`

  [custom icon]: ../setup/changing-the-logo-and-icons.md#additional-icons
  [icon search]: icons-emojis.md#search

## 使用方法

### 使用注释

<!-- md:version 9.2.0 -->
<!-- md:flag experimental -->

注释由两部分组成：一个标记，可以放在带有 `annotate` 类的块中的任何位置，以及位于包含标记的块下方的列表中的内容：

``` markdown title="带注释的文本"
Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: 我是一个注释！我可以包含 `代码`、__格式化文本__、图片等，基本上任何可以用 Markdown 表达的内容。
```

<div class="result" markdown>

Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: 我是一个注释！我可以包含 `代码`、__格式化文本__、图片等，基本上任何可以用 Markdown 表达的内容。

</div>

请注意，`annotate` 类只能添加到最外层的块。所有嵌套元素都可以使用同一个列表来定义注释，除非注释本身是嵌套的。

#### 在注释中

当启用 [SuperFences] 时，可以通过向托管注释内容的列表项添加 `annotate` 类来在注释中嵌套注释，重复此过程：

``` markdown title="带嵌套注释的文本"
Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: 我是一个注释！(1)
    { .annotate }

    1.  :woman_raising_hand: 我也是注释！
```

<div class="result" markdown>

Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: 我是一个注释！(1)
    { .annotate style="margin-bottom: 0" }

    1.  :woman_raising_hand: 我也是注释！

</div>

#### 在警告块中

[警告块]的标题和正文也可以通过添加 `annotate` 修饰符来托管注释，这与[内联块]的工作方式类似：

``` markdown title="带注释的警告块"
!!! note annotate "Phasellus posuere in sem ut cursus (1)"

    Lorem ipsum dolor sit amet, (2) consectetur adipiscing elit. Nulla et
    euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
    purus auctor massa, nec semper lorem quam in massa.

1.  :man_raising_hand: 我是一个注释！
2.  :woman_raising_hand: 我也是注释！
```

<div class="result" markdown>

!!! note annotate "Phasellus posuere in sem ut cursus (1)"

    Lorem ipsum dolor sit amet, (2) consectetur adipiscing elit. Nulla et
    euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
    purus auctor massa, nec semper lorem quam in massa.

1.  :man_raising_hand: 我是一个注释！
2.  :woman_raising_hand: 我也是注释！

</div>

  [admonitions]: admonitions.md
  [inline blocks]: admonitions.md#inline-blocks

#### 在内容标签页中

内容标签页可以通过向专用内容标签页的块（而不是容器，这是不支持的）添加 `annotate` 类来托管注释：

``` markdown title="带注释的内容标签页"
=== "标签页 1"

    Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
    { .annotate }

    1.  :man_raising_hand: 我是一个注释！

=== "标签页 2"

    Phasellus posuere in sem ut cursus (1)
    { .annotate }

    1.  :woman_raising_hand: 我也是注释！
```

<div class="result" markdown>

=== "标签页 1"

    Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
    { .annotate }

    1.  :man_raising_hand: 我是一个注释！

=== "标签页 2"

    Phasellus posuere in sem ut cursus (1)
    { .annotate }

    1.  :woman_raising_hand: 我也是注释！

</div>

#### 在其他所有地方

[Attribute Lists] 扩展是向大多数元素添加注释的关键，但它有一些[限制]。但是，始终可以利用 [Markdown in HTML] 扩展用带有 `annotate` 类的 `div` 包装任意元素：

```` html title="带注释的 HTML"
<div class="annotate" markdown>

> Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.

</div>

1.  :man_raising_hand: 我是一个注释！
````

<div class="result" markdown>
  <div class="annotate" markdown>

> Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.

  </div>

1.  :man_raising_hand: 我是一个注释！

</div>

通过这个技巧，注释也可以添加到引用块、列表和许多其他 [Attribute Lists] 扩展不支持的元素中。此外，请注意[代码块遵循不同的语义]。

!!! warning "已知限制"

    请注意，注释目前在[数据表格]中不起作用，如 #3453 中报告的那样，因为数据表格是可滚动元素，定位非常棘手。这可能会在未来修复。

  [limitations]: https://python-markdown.github.io/extensions/attr_list/#limitations
  [code blocks follow different semantics]: code-blocks.md#adding-annotations
  [data tables]: data-tables.md

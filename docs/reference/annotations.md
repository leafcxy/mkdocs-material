---
icon: material/plus-circle
---

# 注释

Material for MkDocs的旗舰功能之一是能够注入
注释——几乎可以在文档的任何地方添加的小标记
并在点击或键盘焦点时展开包含任意Markdown的工具提示。

## 配置

此配置允许向所有内联和块级别添加注释
元素，以及代码块和嵌套注释。添加
将以下行添加到`mkdocs.yml`：

``` yaml
markdown_extensions:
  - attr_list
  - md_in_html
  - pymdownx.superfences
```

请参阅其他配置选项：

- [Attribute Lists]
- [Markdown in HTML]
- [SuperFences]

  [Attribute Lists]: ../setup/extensions/python-markdown.md
  [Markdown in HTML]: ../setup/extensions/python-markdown.md
  [SuperFences]: ../setup/extensions/python-markdown-extensions.md#superfences

### 注释图标

`version 9.2.0`

注释图标可以更改为与主题绑定的任何图标，甚至
a[自定义图标]，例如指向材质/右箭头圆圈：。只需添加以下内容
指向`mkdocs.yml`的行：

``` yaml
theme:
  icon:
    annotation: material/arrow-right-circle # (1)!
```

1.  输入几个关键字，使用我们的[图标搜索]找到完美的图标，然后
    单击短代码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="material circle" />
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
  [icon search]: icons-emojis.md#_2

## 使用

### 使用注释

`version 9.2.0`
`flag experimental`

注释由两部分组成：一个标记，可以放置在
一个标记有“注释”类的块，以及位于下面列表中的内容
该块包含标记：

``` markdown title="Text with annotations"
Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: I'm an annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be expressed in Markdown.
```

<div class="result" markdown>

Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: I'm an annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be written in Markdown.

</div>

请注意，“comment”类只能添加到最外层的块中。全部
嵌套元素可以使用相同的列表来定义注释，除非
注释本身是嵌套的。

#### 在注释中

启用[SuperFences]后，可以通过以下方式将注释嵌套在注释中
将“注释”类添加到承载注释内容的列表项中，
重复该过程：

``` markdown title="Text with nested annotations"
Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: I'm an annotation! (1)
    { .annotate }

    1.  :woman_raising_hand: I'm an annotation as well!
```

<div class="result" markdown>

Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: I'm an annotation! (1)
    { .annotate style="margin-bottom: 0" }

    1.  :woman_raising_hand: I'm an annotation as well!

</div>

#### 警告

[警告]的标题和正文也可以通过添加注释来承载注释
`在类型限定符后注释修饰符，类似于
[内联块]工作：

``` markdown title="Admonition with annotations"
!!! note annotate "Phasellus posuere in sem ut cursus (1)"

    Lorem ipsum dolor sit amet, (2) consectetur adipiscing elit. Nulla et
    euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
    purus auctor massa, nec semper lorem quam in massa.

1.  :man_raising_hand: I'm an annotation!
2.  :woman_raising_hand: I'm an annotation as well!
```

<div class="result" markdown>

!!! note annotate "Phasellus posuere in sem ut cursus (1)"

    Lorem ipsum dolor sit amet, (2) consectetur adipiscing elit. Nulla et
    euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
    purus auctor massa, nec semper lorem quam in massa.

1.  :man_raising_hand: I'm an annotation!
2.  :woman_raising_hand: I'm an annotation as well!

</div>

  [admonitions]: admonitions.md
  [inline blocks]: admonitions.md

#### 在内容选项卡中

内容选项卡可以通过向块中添加“comment”类来承载注释
一个专用的内容选项卡（而不是容器，这是不支持的）：

``` markdown title="Content tabs with annotations"
=== "Tab 1"

    Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
    { .annotate }

    1.  :man_raising_hand: I'm an annotation!

=== "Tab 2"

    Phasellus posuere in sem ut cursus (1)
    { .annotate }

    1.  :woman_raising_hand: I'm an annotation as well!
```

<div class="result" markdown>

=== "Tab 1"

    Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
    { .annotate }

    1.  :man_raising_hand: I'm an annotation!

=== "Tab 2"

    Phasellus posuere in sem ut cursus (1)
    { .annotate }

    1.  :woman_raising_hand: I'm an annotation as well!

</div>

#### 在其他方面

[Attribute Lists]扩展是向添加注释的关键要素
大多数元素，但它有一些[局限性]。然而，总是有可能
利用HTML中的Markdown扩展名将任意元素包装成
`div与`comment`类：

```` html title="HTML with annotations"
<div class="annotate" markdown>

> Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.

</div>

1.  :man_raising_hand: I'm an annotation!
````

<div class="result" markdown>
  <div class="annotate" markdown>

> Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.

  </div>

1.  :man_raising_hand: I'm an annotation!

</div>

使用此技巧，还可以将注释添加到blockquotes、列表和许多其他文件中
[Attribute Lists]扩展不支持的其他元素。
此外，请注意[代码块遵循不同的语义]。

!!! warning "Known limitations"

    Please note that annotations currently don't work in [data tables] as
    reported in #3453, as data tables are scrollable elements and positioning
    is very tricky to get right. This might be fixed in the future.

  [limitations]: https://python-markdown.github.io/extensions/attr_list/#limitations
  [code blocks follow different semantics]: code-blocks.md
  [data tables]: data-tables.md

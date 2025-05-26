---
icon: material/image-frame
---

# 图片

虽然图片是 Markdown 的一等公民，也是核心语法的一部分，但处理它们可能会很困难。Material for MkDocs 让处理图片变得更加舒适，提供了图片对齐和图片说明的样式。

## 配置

此配置添加了图片对齐、为图片添加说明（将其渲染为图形）以及标记大图片以进行懒加载的功能。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - attr_list
  - md_in_html
  - pymdownx.blocks.caption
```

查看更多配置选项：

- [Attribute Lists]
- [Markdown in HTML]
- [Caption]

  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists
  [Markdown in HTML]: ../setup/extensions/python-markdown.md#markdown-in-html
  [Caption]: ../setup/extensions/python-markdown-extensions.md#caption

### 灯箱

<!-- md:version 0.1.0 -->
<!-- md:plugin [glightbox] -->

如果您想为文档添加图片缩放功能，[glightbox] 插件是一个很好的选择，因为它与 Material for MkDocs 完美集成。使用 `pip` 安装它：

```
pip install mkdocs-glightbox
```

然后，将以下行添加到 `mkdocs.yml`：

``` yaml
plugins:
  - glightbox
```

我们建议查看可用的[配置选项][glightbox options]。

  [glightbox]: https://github.com/blueswen/mkdocs-glightbox
  [glightbox options]: https://github.com/blueswen/mkdocs-glightbox#usage

## 使用方法

### 图片对齐

启用 [Attribute Lists] 后，可以通过 `align` 属性添加相应的对齐方向来对齐图片，即 `align=left` 或 `align=right`：

=== "左对齐"

    ``` markdown title="图片，左对齐"
    ![图片标题](https://dummyimage.com/600x400/eee/aaa){ align=left }
    ```

    <div class="result" markdown>

    ![图片标题](https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–){ align=left width=300 }

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

    </div>

=== "右对齐"

    ``` markdown title="图片，右对齐"
    ![图片标题](https://dummyimage.com/600x400/eee/aaa){ align=right }
    ```

    <div class="result" markdown>

    ![图片标题](https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–){ align=right width=300 }

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

    </div>

如果没有足够的空间在图片旁边渲染文本，图片将拉伸到视口的全宽，例如在移动端视口下。

??? question "为什么没有居中对齐？"

    [`align`][align] 属性不允许居中对齐，这就是为什么 Material for MkDocs 不支持此选项。[^1] 相反，可以使用[图片说明]语法，因为说明是可选的。

  [^1]:
    您可能还会意识到 [`align`][align] 属性在 HTML5 中已被弃用，那么为什么还要使用它呢？主要原因是可移植性——它仍然被所有浏览器和客户端支持，并且不太可能被完全删除，因为许多旧网站仍在使用它。这确保了当带有这些属性的 Markdown 文件在 Material for MkDocs 生成的网站之外查看时，外观保持一致。

  [align]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#deprecated_attributes
  [image captions]: #image-captions

### 图片说明

遗憾的是，Markdown 语法不提供对图片说明的原生支持，但始终可以使用 [Markdown in HTML] 扩展和字面 `figure` 和 `figcaption` 标签：

``` html title="带说明的图片"
<figure markdown="span">
  ![图片标题](https://dummyimage.com/600x400/){ width="300" }
  <figcaption>图片说明</figcaption>
</figure>
```

<div class="result">
  <figure>
    <img src="https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–" width="300" />
    <figcaption>图片说明</figcaption>
  </figure>
</div>

但是，[Caption] 提供了一种替代语法，可以为任何 Markdown 块元素（包括图片）添加说明：

``` markdown title="带说明的图片"
![图片标题](https://dummyimage.com/600x400/){ width="300" }
/// caption
图片说明
///
```

### 图片懒加载

现代浏览器通过 `loading=lazy` 指令提供[对图片懒加载的原生支持][lazy-loading]，在不支持的浏览器中会降级为立即加载：

``` markdown title="图片，懒加载"
![图片标题](https://dummyimage.com/600x400/){ loading=lazy }
```

<div class="result" markdown>
  <img src="https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–" width="300" />
</div>

  [lazy-loading]: https://caniuse.com/#feat=loading-lazy-attr

### 亮色和暗色模式

<!-- md:version 8.1.1 -->

如果您添加了[调色板切换]并想为亮色和暗色方案显示不同的图片，可以在图片 URL 后附加 `#only-light` 或 `#only-dark` 哈希片段：

``` markdown title="图片，亮色和暗色模式不同"
![图片标题](https://dummyimage.com/600x400/f5f5f5/aaaaaa#only-light)
![图片标题](https://dummyimage.com/600x400/21222c/d5d7e2#only-dark)
```

<div class="result" markdown>

![Zelda light world]{ width="300" }
![Zelda dark world]{ width="300" }

</div>

!!! warning "使用[自定义配色方案]时的要求"

    内置的[配色方案]定义了上述哈希片段，但如果您使用[自定义配色方案]，您还需要根据它是亮色还是暗色方案，将以下选择器添加到您的方案中：

    === "自定义亮色方案"

        ``` css
        [data-md-color-scheme="custom-light"] img[src$="#only-dark"],
        [data-md-color-scheme="custom-light"] img[src$="#gh-dark-mode-only"] {
          display: none; /* 在亮色模式下隐藏暗色图片 */
        }
        ```

    === "自定义暗色方案"

        ``` css
        [data-md-color-scheme="custom-dark"] img[src$="#only-light"],
        [data-md-color-scheme="custom-dark"] img[src$="#gh-light-mode-only"] {
          display: none; /* 在暗色模式下隐藏亮色图片 */
        }
        ```

    记住要将 `#!css "custom-light"` 和 `#!css "custom-dark"` 更改为您的方案名称。

  [color palette toggle]: ../setup/changing-the-colors.md#color-palette-toggle
  [Zelda light world]: ../assets/images/zelda-light-world.png#only-light
  [Zelda dark world]: ../assets/images/zelda-dark-world.png#only-dark
  [color schemes]: ../setup/changing-the-colors.md#color-scheme
  [custom color schemes]: ../setup/changing-the-colors.md#custom-color-schemes

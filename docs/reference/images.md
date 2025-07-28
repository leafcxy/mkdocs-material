---
icon: material/image-frame
---

# 图像

虽然图像是Markdown的一级公民，也是核心语法的一部分，
与他们合作可能很困难。MkDocs使用的材料
图像更舒适，提供图像对齐和图像样式
字幕。

## 配置

此配置增加了对齐图像、为图像添加字幕的能力
（将它们渲染为图形），并标记大图像以进行延迟加载。添加
将以下行转换为`mkdocs.yml`：

``` yaml
markdown_extensions:
  - attr_list
  - md_in_html
  - pymdownx.blocks.caption
```

请参阅其他配置选项：

- [Attribute Lists]
- [Markdown in HTML]
- [Caption]

  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists
  [Markdown in HTML]: ../setup/extensions/python-markdown.md#markdown-in-html
  [Caption]: ../setup/extensions/python-markdown-extensions.md#caption

### 灯箱

<!-- md:version 0.1.0 -->
<!-- md:plugin [glightbox] -->

如果您想在文档中添加图像缩放功能
[glightbox]插件是一个很好的选择，因为它完美地集成了
与MkDocs的材料。使用`pip `进行安装：

```
pip install mkdocs-glightbox
```

然后，在`mkdocs.yml`中添加以下行：

``` yaml
plugins:
  - glightbox
```

我们建议您查看可用的
[配置选项][glightbox选项]。

  [glightbox]: https://github.com/blueswen/mkdocs-glightbox
  [glightbox options]: https://github.com/blueswen/mkdocs-glightbox#_4

## 使用

### 图像对齐

启用[属性列表]后，可以通过添加
通过“align”属性指定相应的对齐方向，即“align=left”或
`align=right：

=== "Left"

    ``` markdown title="Image, aligned to left"
    ![Image title](https://dummyimage.com/600x400/eee/aaa){ align=left }
    ```

    <div class="result" markdown>

    ![Image title](https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–){ align=left width=300 }

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

    </div>

=== "Right"

    ``` markdown title="Image, aligned to right"
    ![Image title](https://dummyimage.com/600x400/eee/aaa){ align=right }
    ```

    <div class="result" markdown>

    ![Image title](https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–){ align=right width=300 }

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

    </div>

如果没有足够的空间来渲染图像旁边的文本
将拉伸到视口的整个宽度，例如在移动视口上。

??? question "为什么没有中心对齐？"

    [对齐][对齐]属性不允许居中对齐，这
    这就是为什么MkDocs材料不支持此选项的原因。[^1]相反，
    可以使用[image titles]语法，因为字幕是可选的。

  [^1]:
    您可能还意识到['alig`][align]属性已经
    HTML5已经弃用，那么为什么还要使用它呢？主要原因是
    可移植性——它仍然受到所有浏览器和客户端的支持，并且非常
    不太可能完全删除，因为许多旧网站仍在使用它
    确保具有这些属性的Markdown文件外观一致
    在Material for MkDocs生成的网站之外查看。

  [align]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#deprecated_attributes
  [image captions]: #image-captions

### 图片标题

遗憾的是，Markdown语法不提供对图像标题的原生支持，
但总是可以使用带有文字的[HTML中的Markdown]扩展名
`figure和figcaption标签：

``` html title="Image with caption"
<figure markdown="span">
  ![Image title](https://dummyimage.com/600x400/){ width="300" }
  <figcaption>Image caption</figcaption>
</figure>
```

<div class="result">
  <figure>
    <img src="https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–" width="300" />
    <figcaption>Image caption</figcaption>
  </figure>
</div>

但是，[Caption]提供了一种添加字幕的替代语法
任何Markdown块元素，包括图像：

``` markdown title="Image with caption"
![Image title](https://dummyimage.com/600x400/){ width="300" }
/// caption
Image caption
///
```

### 图像延迟加载

现代浏览器提供[对延迟加载图像的原生支持][延迟加载]
通过`loading=lazy `指令，该指令在中降级为渴望加载
不支持的浏览器：

``` markdown title="Image, lazy-loaded"
![Image title](https://dummyimage.com/600x400/){ loading=lazy }
```

<div class="result" markdown>
  <img src="https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–" width="300" />
</div>

  [lazy-loading]: https://caniuse.com/#feat=loading-lazy-attr

### 亮暗模式

<!-- md:version 8.1.1 -->

如果您添加了[调色板切换]并希望显示不同的图像
浅色和深色配色方案，您可以附加“仅浅色”或“仅深色”`
哈希片段到图像URL：

``` markdown title="Image, different for light and dark mode"
![Image title](https://dummyimage.com/600x400/f5f5f5/aaaaaa#only-light)
![Image title](https://dummyimage.com/600x400/21222c/d5d7e2#only-dark)
```

<div class="result" markdown>

![Zelda light world]{ width="300" }
![Zelda dark world]{ width="300" }

</div>

!!! warning "使用[自定义配色方案]时的要求"

    内置的[配色方案]定义了上述哈希片段，但
    如果你使用[自定义配色方案]，你还必须添加
    根据它是灯还是灯，在你的方案中跟随选择器
    暗方案：

    === "Custom light scheme"

        ``` css
        [data-md-color-scheme="custom-light"] img[src$="#only-dark"],
        [data-md-color-scheme="custom-light"] img[src$="#gh-dark-mode-only"] {
          display: none; /* Hide dark images in light mode */
        }
        ```

    === "Custom dark scheme"

        ``` css
        [data-md-color-scheme="custom-dark"] img[src$="#only-light"],
        [data-md-color-scheme="custom-dark"] img[src$="#gh-light-mode-only"] {
          display: none; /* Hide light images in dark mode */
        }
        ```

    记住要改#！css“自定义灯光”`和`#！css“自定义深色”
    你的计划名称。

  [color palette toggle]: ../setup/changing-the-colors.md#color-palette-toggle
  [Zelda light world]: ../assets/images/zelda-light-world.png#only-light
  [Zelda dark world]: ../assets/images/zelda-dark-world.png#only-dark
  [color schemes]: ../setup/changing-the-colors.md#color-scheme
  [custom color schemes]: ../setup/changing-the-colors.md#custom-color-schemes

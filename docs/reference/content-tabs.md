---
icon: material/tab
---

# 内容标签页

有时，我们希望将不同的内容分组到不同的标签页下，例如在描述如何从不同语言或环境访问 API 时。Material for MkDocs 提供了美观且功能强大的标签页，可以分组代码块和其他内容。

## 配置

此配置启用了内容标签页，并允许在内容标签页内嵌套任意内容，包括代码块和...更多内容标签页！将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true
```

查看更多配置选项：

- [SuperFences]
- [Tabbed]

  [SuperFences]: ../setup/extensions/python-markdown-extensions.md#superfences
  [Tabbed]: ../setup/extensions/python-markdown-extensions.md#tabbed

### 锚点链接

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->

为了链接到内容标签页并更容易地分享它们，每个内容标签页都会自动添加一个锚点链接，您可以通过右键点击复制或在新标签页中打开：

=== "在新标签页中打开我..."

=== "...或者我..."

=== "...甚至是我"

您可以复制标签页的链接，并在同一页面或任何其他页面上创建链接。例如，您可以[跳转到本段上方的第三个标签页][tab_1]或[跳转到 Insiders 的发布指南][tab_2]。

!!! tip "可读的锚点链接"

    [Python Markdown Extensions] 9.6 添加了对内容标签页的[slugification]支持，这会产生更好看和更易读的锚点链接。使用以下行启用 slugify 函数：

    ``` yaml
    markdown_extensions:
      - pymdownx.tabbed:
          slugify: !!python/object/apply:pymdownx.slugs.slugify
            kwds:
              case: lower
    ```

    更多信息，请[查看扩展指南][slugification]。

  [tab_1]: #anchor-links--or-even-me
  [tab_2]: ../publishing-your-site.md#with-github-actions-insiders
  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/
  [slugification]: ../setup/extensions/python-markdown-extensions.md#+pymdownx.tabbed.slugify

### 链接内容标签页

<!-- md:version 8.3.0 -->
<!-- md:feature -->

启用后，整个文档站点中的所有内容标签页将被链接，当用户点击标签页时，相同标签的标签页将一起切换。将以下行添加到 `mkdocs.yml`：

``` yaml
theme:
  features:
    - content.tabs.link
```

内容标签页基于其标签进行链接，而不是偏移量。这意味着当用户点击内容标签页时，所有具有相同标签的标签页都将被激活，而不管它们在容器中的顺序如何。此外，此功能与[即时加载]完全集成，并在页面加载之间保持状态。

=== "功能已启用"

    [![链接内容标签页已启用]][Linked content tabs enabled]

=== "功能已禁用"

    [![链接内容标签页已禁用]][Linked content tabs disabled]

  [instant loading]: ../setup/setting-up-navigation.md#instant-loading
  [Linked content tabs enabled]: ../assets/screenshots/content-tabs-link.png
  [Linked content tabs disabled]: ../assets/screenshots/content-tabs.png

## 使用方法

### 分组代码块

代码块是主要的分组目标之一，可以视为内容标签页的特殊情况，因为包含单个代码块的标签页总是渲染时没有水平间距：

``` title="带代码块的内容标签页"
=== "C"

    ``` c
    #include <stdio.h>

    int main(void) {
      printf("Hello world!\n");
      return 0;
    }
    ```

=== "C++"

    ``` c++
    #include <iostream>

    int main(void) {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
    ```
```

<div class="result" markdown>

=== "C"

    ``` c
    #include <stdio.h>

    int main(void) {
      printf("Hello world!\n");
      return 0;
    }
    ```

=== "C++"

    ``` c++
    #include <iostream>

    int main(void) {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
    ```

</div>

### 分组其他内容

当内容标签页包含多个代码块时，它会渲染时带有水平间距。永远不会添加垂直间距，但可以通过在其他块中嵌套标签页来实现：

``` title="内容标签页"
=== "无序列表"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "有序列表"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci
```

<div class="result" markdown>

=== "Unordered list"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "Ordered list"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci

</div>

### 嵌入内容

启用 [SuperFences] 后，内容标签页可以包含任意嵌套内容，包括更多内容标签页，并且可以嵌套在其他块中，如[警告块]或引用块：

``` title="警告块中的内容标签页"
!!! example

    === "无序列表"

        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```

    === "有序列表"

        ``` markdown
        1. Sed sagittis eleifend rutrum
        2. Donec vitae suscipit est
        3. Nulla tempor lobortis orci
        ```
```

<div class="result" markdown>

!!! example

    === "Unordered List"

        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```

    === "Ordered List"

        ``` markdown
        1. Sed sagittis eleifend rutrum
        2. Donec vitae suscipit est
        3. Nulla tempor lobortis orci
        ```

</div>

  [admonitions]: admonitions.md

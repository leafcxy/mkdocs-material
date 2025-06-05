---
icon: material/tab
---

# 内容选项卡

有时，人们希望将替代内容分组到不同的标签下，
例如，当描述如何从不同语言访问API时，或者
环境。MkDocs的材料允许使用美观实用的选项卡，
对代码块和其他内容进行分组。

## 配置

此配置启用内容选项卡，并允许嵌套任意内容
内容选项卡内部，包括代码块和。..更多内容标签！添加
将以下行转换为`mkdocs.yml`：

``` yaml
markdown_extensions:
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true
```

请参阅其他配置选项：

- [SuperFences]
- [Tabbed]

  [SuperFences]: ../setup/extensions/python-markdown-extensions.md#superfences
  [Tabbed]: ../setup/extensions/python-markdown-extensions.md#tabbed

### 锚链接

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->

为了链接到内容选项卡并更容易地共享它们，锚链接是
自动添加到每个内容选项卡中，您可以通过右键单击或
在新选项卡中打开：

=== "Open me in a new tab ..."

=== "... or me ..."

=== "... or even me"

您可以复制选项卡的链接，并在相同或任何其他选项卡上创建链接
页面。例如，您可以[跳转到本段上方的第三个选项卡][tab_1]
或访问[内幕人士发布指南][tab_2]。

!!! tip "可读锚链接"

    [Python Markdown扩展]9.6增加了对[slugification]的支持
    内容标签，它可以生成更美观、更易读的锚链接。
    使用以下行启用slugify功能：

    ``` yaml
    markdown_extensions:
      - pymdownx.tabbed:
          slugify: !!python/object/apply:pymdownx.slugs.slugify
            kwds:
              case: lower
    ```

    如需了解更多信息，请[参阅扩展指南][取消订阅]。

  [tab_1]: #anchor-links--or-even-me
  [tab_2]: ../publishing-your-site.md#with-github-actions-insiders
  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/
  [slugification]: ../setup/extensions/python-markdown-extensions.md#+pymdownx.tabbed.slugify

### 链接内容选项卡

<!-- md:version 8.3.0 -->
<!-- md:feature -->

启用后，整个文档站点上的所有内容选项卡都将
当用户单击选项卡时，链接并切换到同一标签。添加
将以下行转换为`mkdocs.yml`：

``` yaml
theme:
  features:
    - content.tabs.link
```

内容选项卡是基于其标签链接的，而不是偏移。这意味着所有
当用户单击内容选项卡时，具有相同标签的选项卡将被激活
无论集装箱内的顺序如何。此外，此功能完全
与[即时加载]集成，并在页面加载过程中保持不变。

=== "Feature enabled"

    [![Linked content tabs enabled]][Linked content tabs enabled]

=== "Feature disabled"

    [![Linked content tabs disabled]][Linked content tabs disabled]

  [instant loading]: ../setup/setting-up-navigation.md#instant-loading
  [Linked content tabs enabled]: ../assets/screenshots/content-tabs-link.png
  [Linked content tabs disabled]: ../assets/screenshots/content-tabs.png

## 使用

### 分组代码块

代码块是要分组的主要目标之一，可以考虑
内容选项卡的一种特殊情况，因为具有单个代码块的选项卡总是
无水平间距渲染：

``` title="带有代码块的内容选项卡"
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

当内容选项卡包含多个代码块时，将使用以下方式呈现
水平间距。垂直间距永远不会增加，但可以实现
通过在其他块中嵌套选项卡：

``` title="Content tabs"
=== "Unordered list"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "Ordered list"

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

### 嵌入式内容

启用[SuperFences]后，内容选项卡可以包含任意嵌套
内容，包括其他内容选项卡，可以嵌套在其他块中，如
[警告]或blockquotes：

``` title="警告中的内容选项卡"
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

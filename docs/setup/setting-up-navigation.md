# 设置导航

清晰简洁的导航结构是良好项目的重要方面
文档。MkDocs的材料提供了多种配置选项
导航元素的行为，包括[tabs]和[sections]，以及一个
其旗舰功能包括：[即时加载]。

  [tabs]: #navigation-tabs
  [sections]: #navigation-sections
  [instant loading]: #instant-loading

可以在[页脚]以及使用
[标签插件]。[blog插件]还设置了额外的导航。

[in the footer]: setting-up-the-footer.md#navigation
[tags plugin]: ../plugins/tags.md
[blog plugin]: ../plugins/blog.md

## 配置

### 即时加载

<!-- md:version 5.0.0 -->
<!-- md:feature -->

启用即时加载后，将单击所有内部链接
在没有完全重新加载页面的情况下，通过[XHR]拦截和发送。添加
将以下行添加到`mkdocs.yml`：

``` yaml
theme:
  features:
    - navigation.instant
```

解析并注入生成的页面以及所有事件处理程序和组件
是自动反弹的，即__MkDocs的Material现在表现得像Single
页面应用程序__。现在，搜索索引在导航中幸存下来，即
特别适用于大型文档网站。

!!! info "必须设置[`site_url`][mkdocs.site_url]设置"

    请注意，使用instant时必须设置[`site_url`][mkdocs.site_url]
    导航，因为即时导航依赖于生成的`sitemap.xml`
    如果省略此设置，则该字段将为空。例子：

    ``` yaml
    site_url: https://example.com
    ```

  [XHR]: https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest

#### 即时预取

<!-- md:sponsors -->
<!-- md:version insiders-4.36.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

即时预取是一种新的实验性功能，它将开始获取
一旦用户将鼠标悬停在链接上，页面就会自动弹出。这将减少感知负载
用户的时间，特别是在连接速度较慢的情况下，因为页面将可用
一旦航行。通过以下方式启用它：

``` yaml
theme:
  features:
    - navigation.instant
    - navigation.instant.prefetch
```

#### 进度指示器

<!-- md:version 9.4.3 -->
<!-- md:feature -->
<!-- md:flag experimental -->

为了在使用时在慢速连接上提供更好的用户体验
即时导航，可以启用进度指示器。它将在
页面顶部，页面完全加载后将隐藏。你可以
在`mkdocs.yml`中启用它，方法是：

``` yaml
theme:
  features:
    - navigation.instant
    - navigation.instant.progress
```

仅当页面在以下时间未完成加载时，进度指示器才会显示
400ms，因此快速连接永远不会在更好的时刻显示出来
经验。

### 即时预览

<!-- md:sponsors -->
<!-- md:version insiders-4.52.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

即时预览是一种全新的功能，允许用户预览另一个
无需导航到文档的网站。它们对
将用户置于上下文中。可以在任何标题链接上启用即时预览
使用“数据预览”属性：

```` markdown title="Link with instant preview"
``` markdown
[Attribute Lists](#){ data-preview }
```
````

<div class="result" markdown>

[Attribute Lists](extensions/python-markdown.md#attribute-lists){ data-preview }

</div>

!!! info "局限性"

    即时预览仍然是一个实验性功能，目前仅限于
    Headrlinks。这意味着，您可以在指向的任何内部链接上使用它们
    指向另一个页面上的标题，但不指向具有“id”属性的其他元素。
    在我们收集到足够的反馈后，我们将考虑扩展此功能
    特征可以是其他的并且可能是任意的元素。

#### 自动预览

<!-- md:sponsors -->
<!-- md:version insiders-4.53.0 -->
<!-- md:extension -->
<!-- md:flag experimental -->

使用即时预览的推荐方法是使用Markdown
MkDocs材料中包含的扩展，因为它允许您启用
文档的每页或每节级别的即时预览：

``` yaml
markdown_extensions:
  - material.extensions.preview:
      configurations:
        - targets:
            include:
              - changelog/index.md
              - customization.md
              - insiders/changelog/*
              - setup/extensions/*
```

上述配置是我们用于文档的配置。我们已启用
我们的变更日志、定制指南和内部人员部分的即时预览，
以及我们支持的所有Markdown扩展。

!!! info "完整配置示例"

    ``` yaml
    markdown_extensions:
      - material.extensions.preview:
          configurations:
            - sources: # (1)!
                include:
                  - ...
                exclude:
                  - ...
              targets: # (2)!
                include:
                  - ...
                exclude:
                  - ...
    ```

    1.  源指定应启用即时预览的页面_on_。
        如果省略此设置，将在所有设备上启用即时预览
        页。您可以使用模式来包含或排除页面。排除是
        在包含项的基础上进行评估，因此如果一个页面同时与包含项匹配，它将
        被排除在外。

        请注意，您可以在“配置”下定义多个项目`
        设置，允许精确控制即时预览的位置
        展示。

    2.  目标指定应启用即时预览的页面_to。
        这是启用即时预览的推荐方式。
---

通过添加以下行，也可以全局启用即时预览
`mkdocs.yml`，它将为所有标题链接提供即时预览，
减轻了添加数据属性的需要：

``` yaml
theme:
  features:
    - navigation.instant.preview
```

!!! info "必须设置[`site_url`][mkdocs.site_url]设置"

    请注意，使用instant时必须设置[`site_url`][mkdocs.site_url]
    预览，因为即时预览依赖于生成的`sitemap.xml`
    如果省略此设置，则该字段将为空。例子：

    ``` yaml
    site_url: https://example.com
    ```

### 锚点跟踪

<!-- md:version 8.0.0 -->
<!-- md:feature -->

启用锚点跟踪后，地址栏中的URL会自动
使用目录中突出显示的活动锚点进行更新。添加
将以下行转换为`mkdocs.yml`：

``` yaml
theme:
  features:
    - navigation.tracking
```

### 导航选项卡

<!-- md:version 1.1.0 -->
<!-- md:feature -->

启用选项卡后，顶级部分将在下面的菜单层中呈现
高于1220px的视口标题，但在移动设备上保持不变。[^1]添加
将以下行添加到`mkdocs.yml`：

  [^1]:
    之前<！--md:版本6.2.0-->，导航选项卡略有不同
    行为。所有顶级页面（即所有顶级条目直接
    引用mkdocs.yml的nav条目中定义的.md文件`
    被分组在收到第一页标题的第一个选项卡下。
    这使得无法将顶级页面（或外部链接）作为
    标签项，如#1884和#2072中所述。来自<！--md：版本6.2.0-->
    在上，导航选项卡包括所有顶级页面和部分。

``` yaml
theme:
  features:
    - navigation.tabs
```

=== "With tabs"

    [![Navigation tabs enabled]][Navigation tabs enabled]

=== "Without"

    [![Navigation tabs disabled]][Navigation tabs disabled]

  [Navigation tabs enabled]: ../assets/screenshots/navigation-tabs.png
  [Navigation tabs disabled]: ../assets/screenshots/navigation.png

#### 粘性导航标签

<!-- md:version 7.3.0 -->
<!-- md:feature -->

启用粘性标签后，导航标签将锁定在标题下方
向下滚动时始终可见。只需添加以下两个功能
标记为`mkdocs.yml`：

``` yaml
theme:
  features:
    - navigation.tabs
    - navigation.tabs.sticky
```

=== "With sticky tabs"

    [![Sticky navigation tabs enabled]][Sticky navigation tabs enabled]

=== "Without"

    [![Sticky navigation tabs disabled]][Sticky navigation tabs disabled]

  [Sticky navigation tabs enabled]: ../assets/screenshots/navigation-tabs-sticky.png
  [Sticky navigation tabs disabled]: ../assets/screenshots/navigation-tabs-collapsed.png

### 导航部分

<!-- md:version 6.2.0 -->
<!-- md:feature -->

启用分区后，顶级分区将在
侧边栏用于显示1220px以上的视口，但在移动设备上保持不变。添加
将以下行转换为`mkdocs.yml`：

``` yaml
theme:
  features:
    - navigation.sections
```

=== "With sections"

    [![Navigation sections enabled]][Navigation sections enabled]

=== "Without"

    [![Navigation sections disabled]][Navigation sections disabled]

  [Navigation sections enabled]: ../assets/screenshots/navigation-sections.png
  [Navigation sections disabled]: ../assets/screenshots/navigation.png

两个功能标志，[`navigation.tabs'][tabs]和
[`navigation.sections][sections]可以相互组合。如果两者都有
功能标志已启用，将为级别2导航项呈现部分。

### 导航扩展

<!-- md:version 6.2.0 -->
<!-- md:feature -->

启用扩展后，左侧边栏将展开所有可折叠的内容
默认情况下为子节，因此用户不必手动打开子节。
将以下行添加到`mkdocs.yml`中：

``` yaml
theme:
  features:
    - navigation.expand
```

=== "With expansion"

    [![Navigation expansion enabled]][Navigation expansion enabled]

=== "Without"

    [![Navigation expansion disabled]][Navigation expansion disabled]

  [Navigation expansion enabled]: ../assets/screenshots/navigation-expand.png
  [Navigation expansion disabled]: ../assets/screenshots/navigation.png

### Navigation path <small>Breadcrumbs</small> { id=navigation-path }

<!-- md:sponsors -->
<!-- md:version insiders-4.28.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

当导航路径被激活时，上面会呈现面包屑导航
每个页面的标题，这可能会让访问您的网站的用户更容易定位
屏幕较小的设备上的文档。将以下行添加到
`mkdocs.yml`：

``` yaml
theme:
  features:
    - navigation.path
```

=== "With navigation path"

    [![Navigation path enabled]][Navigation path enabled]

=== "Without"

    [![Navigation path disabled]][Navigation path disabled]

  [Navigation path enabled]: ../assets/screenshots/navigation-path-on.png
  [Navigation path disabled]: ../assets/screenshots/navigation-path-off.png

### 导航修剪

<!-- md:version 9.2.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

启用修剪后，只有可见的导航项才会包含在
渲染HTML，将构建网站的大小减少33%或更多。添加
将以下行转换为`mkdocs.yml`：

``` yaml
theme:
  features:
    - navigation.prune # (1)!
```

1.  此功能标志与不兼容
    [`navigation.explod][navigation.expland]，因为导航扩展需要
    完整的导航结构。

此功能标志对于拥有100多个甚至更多用户的文档网站特别有用
1000多个页面，因为导航占HTML的很大一部分。
导航修剪将用指向第一个部分的链接替换所有可扩展部分
该部分的页面（或部分索引页面）。

  [navigation.expand]: #navigation-expansion

### 章节索引页

<!-- md:version 7.3.0 -->
<!-- md:feature -->

启用节索引页后，文档可以直接附加到
部分，这对于提供概述页面特别有用。添加
将以下行转换为`mkdocs.yml`：

``` yaml
theme:
  features:
    - navigation.indexes # (1)!
```

1.  此功能标志与[toc.integrate][toc.integre]不兼容，
    由于缺少空间，部分无法承载目录。

=== "With section index pages"

    [![Section index pages enabled]][Section index pages enabled]

=== "Without"

    [![Section index pages disabled]][Section index pages disabled]

为了将页面链接到某个部分，请使用以下名称创建一个新文档
`在相应的文件夹中添加index.md，并将其添加到您的
导航部分：

``` yaml
nav:
  - Section:
    - section/index.md # (1)!
    - Page 1: section/page-1.md
    ...
    - Page n: section/page-n.md
```

1.  MkDocs还将名为“README.md”的文件视为[索引页]。

  [Section index pages enabled]: ../assets/screenshots/navigation-index-on.png
  [Section index pages disabled]: ../assets/screenshots/navigation-index-off.png
  [toc.integrate]: #navigation-integration
  [index pages]: https://www.mkdocs.org/user-guide/writing-your-docs/#index-pages

### 目录

#### 锚跟踪

<!-- md:version 8.5.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

当启用[目录]的锚点跟踪时，侧边栏为
自动滚动，以便活动锚点始终可见。添加
将以下行转换为`mkdocs.yml`：

``` yaml
theme:
  features:
    - toc.follow
```

#### 导航集成

<!-- md:version 6.2.0 -->
<!-- md:feature -->

当启用[目录]的导航集成时，它总是
呈现为左侧导航侧边栏的一部分。添加以下行
转到`mkdocs.yml`：

``` yaml
theme:
  features:
    - toc.integrate # (1)!
```

1.  此功能标志与不兼容
    [`navigation.indexs`][navigation.index]，因为节不能承载
    由于缺少空间，目录。

=== "With navigation integration"

    [![Navigation integration enabled]][Navigation integration enabled]

=== "Without"

    [![Navigation integration disabled]][Navigation integration disabled]

  [table of contents]: extensions/python-markdown.md#table-of-contents
  [Navigation integration enabled]: ../assets/screenshots/toc-integrate.png
  [Navigation integration disabled]: ../assets/screenshots/navigation-tabs.png
  [navigation.indexes]: #section-index-pages

### 返回顶部按钮

<!-- md:version 7.1.0 -->
<!-- md:feature -->

当用户向下滚动后开始时，可以显示一个返回顶部按钮
再次向上滚动。它被渲染在标题的正下方。添加
将以下行转换为`mkdocs.yml`：

``` yaml
theme:
  features:
    - navigation.top
```

## 使用

### 隐藏侧边栏

<!-- md:version 6.2.0 -->
<!-- md:flag metadata -->

文档的导航和/或目录侧栏可以隐藏
具有前体“隐藏”属性。在a的顶部添加以下行
Markdown文件：

``` yaml
---
hide:
  - navigation
  - toc
---

# Page title
...
```

=== "Hide navigation"

    [![Hide navigation enabled]][Hide navigation enabled]

=== "Hide table of contents"

    [![Hide table of contents enabled]][Hide table of contents enabled]

=== "Hide both"

    [![Hide both enabled]][Hide both enabled]

  [Hide navigation enabled]: ../assets/screenshots/hide-navigation.png
  [Hide table of contents enabled]: ../assets/screenshots/hide-toc.png
  [Hide both enabled]: ../assets/screenshots/hide-navigation-toc.png

### 隐藏导航路径

<!-- md:sponsors -->
<!-- md:version insiders-4.28.0 -->
<!-- md:flag metadata -->

虽然[导航路径]显示在主标题上方，但有时
可能需要为特定页面隐藏它，这可以通过以下方式实现
front matter的“hide”属性：

``` yaml
---
hide:
  - path
---

# Page title
...
```

  [navigation path]: #navigation-path

## 自定义

### 键盘快捷键

MkDocs的材料包括几个键盘快捷键，使其成为可能
通过键盘浏览项目文档。有两种模式：

<!-- md:option mode:search -->

:   当_search聚焦时，此模式处于活动状态。它提供了几个关键
    绑定使搜索可通过键盘访问和导航：

    * ++arrow-down++ , ++arrow-up++ : select next / previous result
    * ++esc++ , ++tab++ : close search dialog
    * ++enter++ : follow selected result

<!-- md:option mode:global -->

:   当_search未聚焦且没有其他模式时，此模式处于活动状态
    易受键盘输入影响的聚焦元件。以下按键
    已绑定：

    * ++f++ , ++s++ , ++slash++ : open search dialog
    * ++p++ , ++comma++ : go to previous page
    * ++n++ , ++period++ : go to next page

假设您想将某个操作绑定到++x++键。通过使用[附加
JavaScript]，您可以订阅“keyboard$”可观察对象并附加
您的自定义事件侦听器：

=== ":octicons-file-code-16: `docs/javascripts/shortcuts.js`"

    ``` js
    keyboard$.subscribe(function(key) {
      if (key.mode === "global" && key.type === "x") {
        /* Add custom keyboard handler here */
        key.claim() // (1)!
      }
    })
    ```

    1.  调用`key.claim（）`将在
        底层事件，因此按键不会进一步传播
        触摸其他事件听众。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_javascript:
      - javascripts/shortcuts.js
    ```

  [additional JavaScript]: ../customization.md#additional-javascript

### 内容区域宽度

设置内容区域的宽度，使每行的长度不超过
80-100个字符，具体取决于字符的宽度。虽然这个
这是一个合理的默认值，因为较长的行往往更难阅读，它可能
希望增加内容区域的整体宽度，甚至使其
延伸到整个可用空间。

这可以通过[附加样式表]和几行代码轻松实现
CSS：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    .md-grid {
      max-width: 1440px; /* (1)! */
    }
    ```

    1.  If you want the content area to always stretch to the available screen
        space, reset `max-width` with the following CSS:

        ``` css
        .md-grid {
          max-width: initial;
        }
        ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

  [additional style sheet]: ../customization.md#additional-css

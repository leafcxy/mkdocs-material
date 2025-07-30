# 基本社交卡

社交卡是其他系统（如社交媒体）可以显示的图像
链接到的内容预览。很容易开始使用社交媒体
插件，忠实于Material with MkDocs的座右铭：“包括电池。”

## 基本需要

在开始之前，只有几个[dependencies to install]。这些
是插件生成社交媒体所需的图像处理库
卡片，以及它们的Python绑定。

[dependencies to install]: https://squidfunk.github.io/mkdocs-material/plugins/requirements/image-processing/

满足这些先决条件后，只需激活插件即可，
这将：

* 为您网站的每个页面制作PNG格式的社交卡片；
* 在网站页面的标题中创建元数据，以提供
  社交媒体系统提供关键信息，并告诉他们如何找到
  社交卡图片。

!!! example "添加社交卡"

    只需将社交插件添加到您的插件列表中：

    ```yaml hl_lines="3"
        plugins:
            - search
            - social
            - ...
    ```

现在，当您运行`mkdocs-build`并查看`site`目录时，您将
请查看它在 `assets/images/social`下包含反映以下内容的子文件夹
Markdown文件的结构。每个页面都有一个对应的PNG文件
其中包含社交卡图像。

查看生成的HTML，您将看到在中生成的元数据
`head`元素，包括一个指向图像的条目。

## 背景颜色

社交插件具有用于改变方面的配置选项，
图像、字体、徽标、标题，甚至描述。您可以对其进行配置
对于`mkdocs.yml`和Insiders Edition中的所有社交卡，他们可以
在单个页面的页眉中被覆盖。

!!! example "更改背景颜色"

    为了将背景颜色更改为引人注目的艳粉色，
    您可以添加：

    ```yaml hl_lines="4-5"
    plugins:
    ...
    - social:
        cards_layout_options:
            background_color: "#ff1493"
    ```

## 标识

默认情况下，插件使用您为整个网站设置的徽标，或者
通过`theme.logo`或 `theme.icon.logo`设置。差异
两者之间的区别在于 `theme.icon.logo`版本将直接嵌入
将徽标的SVG代码转换为HTML，使其能够继承CSS颜色设置。什么时候
如果您使用`theme.logo`，则材料将徽标作为图像包含在内。

您也可以为社交卡设置自己的徽标。使用的路径
与项目根相关，需要指向SVG文件或像素
图像。它应该是矩形的，有透明的背景。

!!! example "设置自己的徽标"

    ```yaml hl_lines="3-4"
    plugins:
    - social:
        cards_layout_options:
          logo: docs/assets/images/ourlogo.png
    ```

## 背景图像

除了添加自己的徽标外，最有影响力的个性化方式是
社交卡将添加背景图像，而不是默认的纯色
背景确保你选择了一个能与另一个形成鲜明对比的
卡片的元素。

此外背景颜色被渲染在背景图像的顶部，
允许您使用透明颜色为图像着色。为了仅使用图像，
使用颜色值`transparent`。

!!! example "添加背景图像"

    ```yaml hl_lines="4 5"
    plugins:
    - social:
        cards_layout_options:
          background_image: layouts/background.png
          background_color: transparent
    ```

背景图像的路径是从项目的根解析的，
因此，您应该在这里创建`layouts`目录并放置
背景图像。插件中包含的社交卡的默认网站
是1200x630像素，因此请选择一个大小合适的图像或一个缩放良好的图像。

## 其他布局和样式

`sponsors`

Insiders Edition提供了额外的布局以及以下选项
为不同（类型）的页面配置不同的样式。

Insiders Edition为社交媒体提供了许多额外的布局
卡。例如，`default/variant`布局在卡片上添加了一个页面图标。
您可以使用此功能直观地区分社交卡，具体取决于哪种类型
您正在共享的页面。

例如，假设你有一组宣传活动的页面，你想要
包括日历图标作为卡片广告的视觉指示
活动。在下面，您将为事件页面设置一个目录并使用
元插件为他们分配一个日历图标。

!!! example "活动页面社交卡"

    首先，在`docs`目录中创建一个目录来保存事件页面：

    ```
    $ mkdir docs/events
    ```

    然后，在这个新目录中添加一个文件`.meta.yml`，并设置
    页面图标和醒目的粉红色背景色
    社会化媒体。请注意，您可以通过设置来覆盖背景图像
    此处为`null`，因为由于不透明的颜色，它无论如何都不可见。

    ```yaml
    ---
    icon: material/calendar-plus
    social:
      cards_layout_options:
        background_image: null
        background_color: "#ff1493"
    ---
    ```

    现在在`docs/events`目录中添加一个页面。它不需要有
    任何特殊内容，只要一个顶级标题。

    要在`mkdocs.yml`中启用`default/variat`布局，请添加
    `cards_layout选项，并添加元插件：

    ```yaml
    plugins:
      - meta
      - social:
          cards_layout: default/variant
    ```

    运行`mkdocs-build`后，您可以在以下位置看到社交卡
    `site/assets/images/social/events/index.png`具有页面图标。

请注意，该图标也将出现在导航元素旁边
页面。如果这不是你想要的，那么你需要修改社交
卡片模板从其他来源获取图标。你可以学习如何
在[custom social cards tutorial](custom.md)中执行此操作。

## Per-page设置

`sponsors`

使用Insiders Edition，您可以自定义每个卡的布局
通过在页眉中添加设置来创建页面。你有效地做到了这一点
在前面的练习中，但使用meta插件来影响一整套
页。

说除了常规活动外，你还有奇怪的网络研讨会和
为此，您需要设置一个不同的图标，并将描述设置为
表明该活动是网络研讨会系列的一部分。

!!! example "覆盖页眉中的卡片样式"

    将以下内容添加到“docs/events”页面的顶部，或创建一个新的
    一：

    ```yaml
    ---
    icon: material/web
    social:
      cards_layout_options:
        description: Our Webinar Series
    ---
    ```

## 接下来是什么？

使用Insiders Edition，如果满足以下条件，您还可以定义自定义布局
上面介绍的配置选项不足以满足您的需求。
如果你想继续 [custom social cards tutorial](custom.md)
找出如何做到这一点。

社交卡片对于博客文章特别有用。如果你有博客，
您只需打开两个插件即可创建社交卡
为你最新的博客帖子做广告。如果你还没有，但想
到，为什么不看看[blog tutorials](../index.md)呢？

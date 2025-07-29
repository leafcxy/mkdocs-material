# 自定义卡片

Insiders Edition允许您为社交卡定义自定义布局
如果配置选项不够，则可以满足您的特定需求。
例如，您可能想定义一张社交卡来宣传新版本
您的产品。它应该有一个图标，表示发布公告
以及卡上发布的版本号。

## 安装

您可以从头开始设计自定义布局，也可以使用现有布局
作为您添加或以其他方式修改的基础。在本教程中，您将
使用默认布局作为基础。

!!! example "复制默认布局以进行自定义 `sponsors`"

    从安装的Material复制默认社交卡布局
    将MkDocs添加到新目录`layouts`。以下说明假设您
    位于您的项目根目录中，并在其中拥有一个虚拟环境。这个
    当然，您机器上的路径可能会有所不同。

    ```
    $ mkdir layouts
    $ cp venv/lib/python3.12/site-packages/material/plugins/social/templates/default/variant.yml \
      layouts/release.yml
    ```

    在自定义社交卡之前，您需要告诉插件在哪里
    找到它们，并告诉MkDocs注意任何变化。添加以下内容
    转到`mkdocs.yml`中的插件配置：

    ``` yaml hl_lines="2-6"
    plugins:
      - social:
          cards_layout_dir: layouts

    watch:
      - layouts
    ```

请查看`release.yml`的内容。您将看到：

* 从网站提取的内容的多个定义，
* 最终出现在页眉中的`meta`元素中的标签的定义
  每一页，
* 由社交插件的多个层组成的规范
  按照定义的顺序相互叠加。

## 定义页面元数据

在下面，您将向社交卡添加版本号。这
假设您有一个包含每个版本信息的更改日志页面。
将最新版本的版本号添加到页眉中（确实如此
不需要从Markdown内容中解析出来）：

!!! example "定义发布数据 `sponsors`"

    创建一个包含以下内容的页面`docs/changelog.md`：

    ```yaml
    ---
    icon: material/rocket-launch-outline
    social:
      cards_layout: release
      cards_layout_options:
        title: New release!
    latest: 1.2.3
    ---

    # Releases
    ```

## 提取页面元数据

使用页眉中定义的数据，您现在可以向布局中添加代码
将其拉出，以便稍后渲染。这是为了分离
从实际布局指令中操作数据，从而使
布局文件更易于阅读。

!!! example "添加数据定义"

    在布局文件的顶部添加以下内容：

    ```yaml hl_lines="2-9"
    definitions:
      - &latest >-
        {%- if 'latest' in page.meta %}
            {{ page.meta['latest']}}
        {%- else -%}
            No release version data defined!
        {%- endif -%}
    ```

此处显示的代码检查页眉是否包含必要的
如果没有，则输入并向社交卡发送消息。不幸的是，那里
并不是引发异常或记录错误的直接方法，因此消息
仅仅出现在社交卡上。

## 添加发布版本层

下一步是在新图层中使用这些数据定义，并将其添加到
已经存在的。

!!! example "渲染发布版本"

    最后，将以下内容添加到自定义布局的末尾：

    ```yaml
      - size: { width: 990, height: 50 }
        offset: { x: 50, y: 360 }
        typography:
          content: *latest
          align: start
          color: *color
    ```

现在，您应该看到社交插件在更改日志页面上使用了自定义布局
你设置。

## 调整布局

最后，用于更改日志页面的火箭图标不太正确
位置。请找到`page_icon`变量用于创建
页面图标层，并将水平位置调整为600而不是800。

!!! tip "调试布局文件"

    如果你发现你的布局导致你的MkDocs构建失败，
    你可以做很多事情：

    1. 使用`--verbose`选项运行Mkdocs以获得更详细的报告。
    2. 评论你最近添加的内容或你怀疑是原因所在的内容
    3. 使用`pip Install jinja2`安装`jinja2`命令行工具
       在布局文件上运行它，例如：`jinja2-event.yml`。

## 接下来是什么？

如果你还没有博客，为什么不看看
[blog tutorials](../index.md#blogs)并学习如何设置？社会
插件将帮助您吸引人们对您在社交媒体上发布的帖子的关注。

查看我们为您准备的[other tutorials](../index.md)。
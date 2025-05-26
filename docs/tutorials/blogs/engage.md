# 参与和传播

您可以促进读者参与并改善内容的传播
通过提供人们可以订阅的RSS提要，在您的博客上发布
整合讨论系统。了解更多关于谁在阅读或不在阅读的信息
你的帖子，你可能想集成一个分析系统。你可能还想
当你发布一篇新的博客文章时，在社交媒体上发帖。本教程提供
你在所有这些话题上都领先一步。

__所需时间:__ 通常为30分钟

## RSS源

RSS提要允许用户订阅博客，以便在以下情况下收到通知
你发布新帖子。RSS源阅读器通常用于访问博客
用户跟随。他们通常支持离线下载博客内容
消费。

为您的博客创建RSS提要的一个简单方法是使用
[MkDocs RSS Plugin]，它与MkDocs的Material很好地集成在一起。
由于它是第三方插件，您需要在使用前安装它。

[MkDocs RSS Plugin]: https://guts.github.io/mkdocs-rss-plugin


!!! example "添加RSS源"

    将RSS插件安装到您的项目中：

    ```
    $ pip install mkdocs-rss-plugin
    ```

    重要的是要有“site_name”、“site_description”和
    `site_url`设置配置为[基本博客教程中的说明]。
    RSS插件利用这些信息来构建提要，因此
    确定您已经配置了它们。

    [instructed in the basic blog tutorial]: basic.md#setting-up-your-blog

    现在，在`mkdocs.yml`中配置插件。提供的选项限制
    为博客文章创建RSS条目的页面，即
    可能是你想要的。另请注意日期字段的配置
    匹配Material for MkDocs用于容纳
    创建日期和更新日期。

    ```yaml hl_lines="9"
    plugins:
        - ...
        - rss:
            match_path: "blog/posts/.*"
            date_from_meta:
              as_creation: date.created
              as_update: date.updated
    ```

    看一看 http://localhost:8000/feed_rss_created.xml 查看RSS
    尽情享受XML的荣耀。您可以使用Firefox或Chrome等浏览器
    可以显示原始RSS提要，也可以使用`curl`获取提要，使用`xmllint`获取提要
    格式化它。（您可能需要安装这些工具。）

    ```
    curl -s http://localhost:8000/feed_rss_created.xml | xmllint --format -
    ```

    您可能还想使用提要阅读器尝试提要。有各种各样的桌面
    以及移动应用程序和在线服务。当然，要使用后者，你
    将需要将您的项目部署到他们可以访问的地方。

如果您没有进行任何更改，这个最小配置应该可以很好地工作
设置为blog插件的默认配置。有关适应的更多信息
根据您的需求，请参阅[the RSS plugin's documentation]。

[the RSS plugin's documentation]: https://guts.github.io/mkdocs-rss-plugin/

## 社交媒体按钮

社交媒体按钮有两个用途：允许读者浏览
访问您的社交媒体资料或分享您通过他们发布的内容
自己的账户。

### 个人资料链接

社交媒体资料的链接通常位于页面的页脚和
Material for MkDocs使这变得容易。您需要做的就是提供
必要的链接并定义要使用的图标。

!!! example "添加社交媒体个人资料链接"

    在你的`mkdocs.yml`中添加一个`extra`部分，并在其中添加一个`社交`
    部分包含链接定义列表。这些由徽标组成
    使用和指向配置文件的链接。

    ```yaml
    extra:
      social:
        - icon: fontawesome/brands/mastodon
          name: squidfunk on Mastodon
          link: https://fosstodon.org/@squidfunk
    ```

    对于`icon`，您可以选择与捆绑在一起的图标的任何有效路径
    主题。`name`将用作图标的标题属性
    包括这一点提高了可访问性。
    对于流行的社交媒体系统，链接需要是绝对的
    需要包括该方案，最有可能是`https://`。

    您还可以使用其他方案。例如，要创建一个图标，允许
    要创建电子邮件，请添加以下内容：

    ```yaml
    extra:
      social:
      - icon: /fontawesome/regular/envelope
        name: send me an email
        link: mailto:<email-address>
    ```

    最后，您可以在网站中指定一个URL，例如指向您的联系人
    页面。可以仅指定页面的路径：

    ```yaml
    extra:
      social:
      - icon: /material/mailbox
        name: contact us
        link: /contact
    ```

### 分享和点赞按钮

添加按钮让人们在社交媒体上分享你的内容有点难
参与度更高，这就是为什么有公司为此提供组件。


!!! tip "数据保护"

    使用社交媒体提供的集成的“分享”和“点赞”按钮
    公司经常留下大量的数据痕迹，即使用户没有
    与这些按钮交互。如果您选择将此功能集成到
    您的网站请注意数据保护的影响和您的
    作为提供者的职责是确保处理只发生在用户一次
    已同意。

这种共享按钮的实现故意不使用第三方代码。
它支持在推特/X和脸书上共享，而不会导致数据流
每当有人浏览这些页面时，这些公司都会。只有当有人点击
共享按钮将与这些公司的服务器进行交互。

!!! example "添加共享按钮"

    为了添加共享按钮，您可以添加一个附加按钮的钩子
    用于共享当前页面。

    在项目根目录中创建一个目录`hooks`并对其进行配置
    在您的`mkdocs.yml`中：

    ```yaml
    hooks:
      - hooks/socialmedia.py
    ```

    使用以下Python代码添加文件`hooks/socialmedia.py`：

    ```python
    from textwrap import dedent
    import urllib.parse
    import re

    x_intent = "https://x.com/intent/tweet"
    fb_sharer = "https://www.facebook.com/sharer/sharer.php"
    include = re.compile(r"blog/[1-9].*")

    def on_page_markdown(markdown, **kwargs):
        page = kwargs['page']
        config = kwargs['config']
        if not include.match(page.url):
            return markdown

        page_url = config.site_url+page.url
        page_title = urllib.parse.quote(page.title+'\n')

        return markdown + dedent(f"""
        [Share on :simple-x:]({x_intent}?text={page_title}&url={page_url}){{ .md-button }}
        [Share on :simple-facebook:]({fb_sharer}?u={page_url}){{ .md-button }}
        """)
    ```

    钩子首先检查当前页面是否是博客文章，然后附加
    共享按钮的Markdown代码。按钮使用图标，因此您还需要
    配置以下markdown扩展：

    ```yaml
    markdown_extensions:
      - attr_list
      - pymdownx.emoji:
          emoji_index: !!python/name:material.extensions.emoji.twemoji
          emoji_generator: !!python/name:material.extensions.emoji.to_svg
    ```


## 添加讨论系统

让你的读者对你的帖子发表评论是一种很好的接收方式
反馈，学习一些东西，以及给读者机会
讨论内容和主题。

有很多讨论系统，你需要考虑
当你为你的博客选择一个合适的时。同样，你会
还需要考虑现有的沟通渠道承诺。如果你
例如，如果是Slack的重度用户，您可能对此有字符串偏好
系统。考虑到当你添加一个沟通渠道时，你需要
准备好定期使用它并主持讨论。

### Giscus整合

在本教程中，我们将使用[Giscus]，因为它是免费的、开源的，
并使用[GitHub Discussions]作为后端。因为Material的很多用户
对于使用GitHub的MkDocs来说，这似乎是一个显而易见的选择。

[Giscus]: https://giscus.app/
[GitHub Discussions]: https://docs.github.com/en/discussions

要将Giscuss添加到您的博客中，您需要经历多个步骤：

1. 如果还没有GitHub存储库，请创建一个GitHub存储库
2. 打开讨论并安装[Giscus app]
3. 配置将Giscus嵌入博客所需的代码
4. 将代码添加到您的MkDocs项目中

[Giscus app]: https://github.com/apps/giscus

您可能希望为本教程创建一个测试存储库，以便
稍后废弃。以下说明假设您是用户"example"
并创建一个存储库"giscus-test."。该存储库将需要
公开让人们能够使用讨论。

在下面给出的说明中，您需要至少替换用户名
而且，如果您选择了其他名称，例如当您
希望直接在现有存储库上工作。

!!! example "打开讨论并安装Giscus应用程序"

    设置存储库后，转到其设置页面并查找
    `Features`部分中的`General`。勾选`Discussions`复选框。
    您将看到`Discussions`出现在
    存储库。如果您正在使用实时存储库，那么您可能需要添加一些
    此时将讨论部分的内容最小化，然后回到
    辅导的。

    接下来，您需要按照以下链接安装[Giscus app]
    句子，选择“安装”，然后按照说明进行选择
    Giscus应用程序的安装位置：

    1. 为要使用的存储库选择帐户或组织。
    2. 选择仅在选定的存储库上安装，然后选择您要安装的存储库
       想要使用。请注意，您可以在此处选择多个存储库。
    3. 在末尾选择“安装”。您可能需要进行身份验证才能提供
       允许这种情况发生。
    4. 您最终将进入设置中的“应用程序”页面，在那里您
       可以控制Gicsus应用程序，并在需要时卸载它。

这就是存储库所需的所有准备工作。接下来，是时候了
生成一段代码，将Giscuss嵌入到您的网站中。生成的代码
代码片段看起来像这样：

```html
<script src="https://giscus.app/client.js"
        data-repo="<username>/<repository>"
        data-repo-id="..."
        data-category="Announcements"
        data-category-id="..."
        data-mapping="title"
        data-strict="1"
        data-reactions-enabled="1"
        data-emit-metadata="1"
        data-input-position="top"
        data-theme="preferred_color_scheme"
        data-lang="en"
        data-loading="lazy"
        crossorigin="anonymous"
        async>
</script>
```

!!! example "配置将Giscus嵌入博客所需的代码"

    转到[Giscus homepage]并配置嵌入代码。有一个
    设置数量：

    1. 选择语言
    2. 输入用户名/组织名称和存储库名称
    3. 选择如何将讨论映射到博客上的页面。
       因为对于博客文章来说，标题是URL的基础，它使
       使用“讨论标题包含页面<title>”选项的意义。
    4. 在“讨论类别”下选择“公告”以限制创建
       与Giscuss和维护人员或管理员进行新的讨论
       权限。
    5. 在“功能”下，选择以下内容：
         1. 启用主帖子的反应
         2. 发布讨论元数据
         3. 将评论框放在评论上方
    6. 在“主题”下，选择“首选配色方案”，以便Giscus匹配
       用户为您的网站选择的配色方案。

[Giscus homepage]: https://giscus.app/

有了这些设置，您现在需要将代码集成到您的
网站。为此目的，存在一个部分的“partials/comments.html”
默认为空。它包含在`content.html `部分中，因此
包含在您网站的每个页面中。你可能想要，也可能不想要。在这个
在教程中，您将把Giscus集成限制为仅限于博客文章，但它是
如果你想拥有Giscus，很容易省去实现这一点的代码
每页都有讨论。

!!! example "添加Giscus集成代码"

    首先，您需要创建一个“override”目录，其中包含
    您要覆盖的模板和部分。

    ```
    mkdir -p overrides/partials
    ```

    您需要在`mkdocs.yaml`中声明它：

    ```yaml hl_lines="3"
    theme:
      name: material
      custom_dir: overrides
    ```

    现在添加一个文件`overrides/particals/comments.html`并粘贴代码
    您从Giscus主页获得的片段。在本地查看结果
    您将看到集成在网站的所有页面上都是活动的。
    如果你想将其限制在你的博客文章中，你需要添加一个条件
    围绕Giscus脚本，测试是否应该包含注释。一个简单的
    这样做的方法是测试元数据标志：

    ```html
    {% if page.meta.comments %}
    <script>...</script>
    {% endif %}
    ```

    缺点是，您现在需要手动打开每个评论
    博客文章-除非你想在某些网站上关闭它们。获取评论
    在所有博客文章的部分，使用这样的代码：

    ```html
    {% if page.file.src_uri.startswith('blog/posts') %}
    <script>...</script>
    {% endif %}
    ```

    现在您应该看到Giscus评论已添加到您的
    博客文章，但不在其他页面上。

## 接下来是什么？

博客教程到此结束。我们希望您喜欢它，并设法
按照你喜欢的方式设置你的博客。还有许多其他功能和
我们在这里无法涵盖的选项。[blog plugin reference]
为插件提供了全面的文档。您可能还想
查看[social plugin tutorial]为您的博客生成社交卡
当你发布链接到社交媒体系统时显示的帖子。

[blog plugin reference]: https://squidfunk.github.io/mkdocs-material/plugins/blog/
[social plugin tutorial]: ../social/basic.md

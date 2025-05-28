# 设置站点分析

与网络上提供的任何其他服务一样，了解您的项目
文档的实际使用可能是成功的关键因素。材料用于
MkDocs与[Google Analytics]原生集成，并提供可定制的
[cookie consent]和[feedback widget]。

  [Google Analytics]: https://developers.google.com/analytics
  [cookie consent]: ensuring-data-privacy.md#cookie-consent
  [feedback widget]: #was-this-page-helpful

## 配置

### 谷歌分析

<!-- md:version 7.1.8 -->
<!-- md:default none -->

Material for MkDocs与Google Analytics 4原生集成[^1]。如果你
已设置Google Analytics并拥有属性，请通过添加
将以下行转换为`mkdocs.yml`：

  [^1]:
    在MkDocs 9.2.0版本的Material之前，支持通用分析
    好。然而，由于通用分析已经日落，这种集成
    在9.2.0中被删除。

``` yaml
extra:
  analytics:
    provider: google
    property: G-XXXXXXXXXX
```

??? question "如何衡量网站搜索使用情况？"

    除了页面浏览量和事件外，还可以更好地跟踪[网站搜索]
    了解人们如何使用您的文档以及他们希望找到什么。
    为了启用站点搜索跟踪，需要执行以下步骤：

    1. 转到您的Google Analytics __admin设置__
    2. 选择相应跟踪代码的属性
    3. 选择__data streams__选项卡并单击相应的URL
    4. 单击__增强测量__部分中的齿轮图标
    5. 确保启用了__site search__

  [site search]: setting-up-site-search.md

### 这个页面有用吗？

<!-- md:version 8.4.0 -->
<!-- md:default none -->

可以在每个页面的底部包括一个简单的[反馈小部件]，
鼓励用户即时反馈页面是否有用。
将以下行添加到`mkdocs.yml`中：

``` yaml
extra:
  analytics: # (1)!
    feedback:
      title: Was this page helpful?
      ratings:
        - icon: material/emoticon-happy-outline
          name: This page was helpful
          data: 1
          note: >-
            Thanks for your feedback!
        - icon: material/emoticon-sad-outline
          name: This page could be improved
          data: 0
          note: >- # (2)!
            Thanks for your feedback! Help us improve this page by
            using our <a href="..." target="_blank" rel="noopener">feedback form</a>.
```

1.  此功能与[Google Analytics][Analytics]原生集成，
    这就是为什么“提供者”和“财产”也是必需的。然而，它也是
    可以提供[自定义反馈集成]。

2.  您可以在用户之后显示的注释中添加任意HTML标签
    提交反馈，例如链接到反馈表单。

“title”和“ratings”这两个属性都是必需的。请注意，这是允许的
定义两个以上的评级，例如实现1-5星评级。自从
反馈小部件将数据发送到第三方服务，当然，它是原生的
与[cookie同意]功能集成[^2]。

  [^2]:
    如果用户不接受“分析”cookie，则反馈小部件为
    未示出。

??? question "如何可视化收集到的反馈评级？"

    要可视化反馈评级，您需要创建一个自定义报告
    [谷歌分析]，它将快速显示最差和最好的评分
    项目文档的页面。

    1.  转到您的谷歌分析仪表板__

    2.  转到左侧菜单（底部）上的__Admin__页面，然后选择
        __数据显示卡上的自定义定义

    3.  单击__自定义度量__选项卡，然后__创建自定义度量__，
        输入以下值：

        * 度量名称：页面有用
        * 描述：这个页面有用吗？
        * 事件参数：`data`
        * 计量单位：标准

    4.  转到左侧菜单上的__explore__页面，创建一个新的
        __空白勘探__

    5.  按如下方式配置报告：

        * 维度：添加“事件名称”和“页面位置”`
        * 指标：添加“事件计数”和“页面有用”`
          （步骤3中创建的自定义指标）
        * 行：`页面位置`
        * 值：拖动“事件计数”和“页面有用”`
        * 过滤器：为添加新过滤器
          `事件名称/完全匹配/反馈`

    !!! warning "数据可用性延迟"

        报告可能需要24小时或更长时间才能开始显示数据

    现在，在您保存了报告并收集了一些反馈评级后，
    您将获得一个包含所有页面的列表，其中包含评级总数，以及
    每页平均评分。这应该有助于您识别需要
    改进：

    !!! danger "Google Analytics 4不支持平均值"

        据我们所知，Google Analytics 4目前没有以下功能
        允许定义自定义计算指标来计算平均值
        页面的评级。见#5740。

    [![feedback report]][feedback report]

以下属性适用于每种评级：

<!-- md:option analytics.feedback.ratings.icon -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须指向引用[任何捆绑的图标]的有效图标路径
    使用[自定义图标]主题，否则构建将无法成功。一些流行
    组合：

    * :material-emoticon-happy-outline: + :material-emoticon-sad-outline: – `material/emoticon-happy-outline` + `material/emoticon-sad-outline`
    * :material-thumb-up-outline: + :material-thumb-down-outline: – `material/thumb-up-outline` + `material/thumb-down-outline`
    * :material-heart: + :material-heart-broken: – `material/heart` + `material/heart-broken`

<!-- md:option analytics.feedback.ratings.name -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性的值显示在用户交互上（即键盘焦点
    或鼠标悬停），解释图标后面的评级含义。

<!-- md:option analytics.feedback.ratings.data -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性的值作为数据值与自定义事件一起发送
    传输到谷歌分析[^3]（或任何自定义集成）。

  [^3]:
    请注意，对于Google Analytics，数据值必须是整数。

<!-- md:option analytics.feedback.ratings.note -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性的值在用户选择评级后显示。
    它可能包含任意HTML标签，这对于询问
    用户可以通过表单为当前页面提供更详细的反馈。
    也可以用当前页面的URL和标题预先填写表单
    使用以下占位符创建页面：

    - `{url}` – Page URL
    - `{title}` – Page title

    ```
    https://github.com/.../issues/new/?title=[Feedback]+{title}+-+{url}
    ```

    在这个例子中，当点击链接时，用户会被重定向到“新
    您的存储库的“issue”表单，带有预先填写的标题，包括路径
    当前文档，例如：

    ```
    [Feedback] Setting up site analytics – /setup/setting-up-site-analytics/
    ```

    GitHub问题的替代方案是[Google Forms]。

  [feedback widget]: #feedback
  [analytics]: #google-analytics
  [feedback report]: ../assets/screenshots/feedback-report.png
  [custom feedback integration]: #custom-site-feedback
  [custom icons]: https://github.com/squidfunk/mkdocs-material/tree/master/material/templates/.icons
  [Google Forms]: https://www.google.com/forms/about/

## 使用

### 隐藏反馈小部件

[反馈小部件]可以隐藏在带有“hide”字样的文档中`
财产。在Markdown文件的顶部添加以下行：

``` yaml
---
hide:
  - feedback
---

# Page title
...
```

## 自定义

### 自定义站点分析

为了整合另一家提供
基于JavaScript的跟踪解决方案，只需按照[主题扩展]的指南进行操作
并在“override”文件夹中创建一个新的分部。该部分的名称为
用于通过`mkdocs.yml`配置自定义集成：

=== ":octicons-file-code-16: `overrides/partials/integrations/analytics/custom.html`"

    ``` html
    <script>
      /* Add custom analytics integration here, e.g. */
      var property = "{{ config.extra.analytics.property }}" // (1)!

      /* Wait for page to load and application to mount */
      document.addEventListener("DOMContentLoaded", function() {
        location$.subscribe(function(url) {
          /* Add custom page event tracking here */ // (2)!
        })
      })
    </script>
    ```

    1.  例如，该变量接收在“mkdocs.yml”中设置的值，
        “foobar”代表“财产”。
    2.  如果你使用的是[即时加载]，你可以使用“位置”$`
        observable用于监听导航事件，该事件始终发出
        当前“URL”。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra:
      analytics:
        provider: custom
        property: foobar # (1)!
    ```

    1.  您可以添加任意键值组合来配置您的
        定制集成。如果你正在分享，这尤其有用
        跨多个存储库的自定义集成。

  [theme extension]: ../customization.md#extending-the-theme
  [instant loading]: setting-up-navigation.md#instant-loading

### 自定义网站反馈

自定义反馈小部件集成只需要处理以下事件
由用户在某些帮助下与反馈小部件交互生成
[附加JavaScript]：

=== ":octicons-file-code-16: `docs/javascripts/feedback.js`"

    ``` js
    var feedback = document.forms.feedback
    feedback.hidden = false // (1)!

    feedback.addEventListener("submit", function(ev) {
      ev.preventDefault()

      var page = document.location.pathname // (2)!
      var data = ev.submitter.getAttribute("data-md-value")

      console.log(page, data) // (3)!

      feedback.firstElementChild.disabled = true // (4)!

      var note = feedback.querySelector(
        ".md-feedback__note [data-md-value='" + data + "']"
      )
      if (note)
        note.hidden = false // (5)!
    })
    ```

    1.  默认情况下，反馈小部件是隐藏的，因此在以下情况下不会出现
        人们已经关闭了JavaScript。所以，这里需要打开它。

    2.  检索页面和反馈值。

    3.  用将数据发送到分析的代码替换它
        供应商。

    4.  提交后禁用表单。

    5.  显示已配置的注释。显示哪一个取决于用户
        反馈。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_javascript:
      - javascripts/feedback.js
    ```

&nbsp;
{ #feedback style="margin: 0; height: 0" }

  [additional JavaScript]: ../customization.md#additional-javascript

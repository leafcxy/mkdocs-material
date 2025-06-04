# 添加评论系统

MkDocs材料允许轻松添加您的第三方评论系统
使用[主题扩展]选择任何页面的页脚。例如，
我们将整合[Giscus]，它是开源的、免费的，并使用GitHub
讨论作为后端。

  [Giscus]: https://giscus.app/

## 自定义

### Giscus整合

在使用[Giscus]之前，您需要完成以下步骤：

1.  __安装[Giscus GitHub应用程序]__并授予对存储库的访问权限
    这应该作为GitHub讨论的主题。请注意，这可能是
    存储库与您的文档不同。
2.  __访问[Giscus]并通过其配置工具生成snippet__
    加载评论系统。复制片段以进行下一步。这个
    生成的代码片段应该类似于以下内容：

    ``` html
    <script
      src="https://giscus.app/client.js"
      data-repo="<username>/<repository>"
      data-repo-id="..."
      data-category="..."
      data-category-id="..."
      data-mapping="pathname"
      data-reactions-enabled="1"
      data-emit-metadata="1"
      data-theme="light"
      data-lang="en"
      crossorigin="anonymous"
      async
    >
    </script>
    ```

[`comments.html`][comments]部分（默认为空）是
添加由[Giscus]生成的代码段。遵循[主题扩展]的指南
和[覆盖`comments.html`部分][覆盖部分]：

``` html hl_lines="3"
{% if page.meta.comments %}
  <h2 id="__comments">{{ lang.t("meta.comments") }}</h2>
  <!-- Insert generated snippet here -->

  <!-- Synchronize Giscus theme with palette -->
  <script>
    var giscus = document.querySelector("script[src*=giscus]")

    // Set palette on initial load
    var palette = __md_get("__palette")
    if (palette && typeof palette.color === "object") {
      var theme = palette.color.scheme === "slate"
        ? "transparent_dark"
        : "light"

      // Instruct Giscus to set theme
      giscus.setAttribute("data-theme", theme) // (1)!
    }

    // Register event handlers after documented loaded
    document.addEventListener("DOMContentLoaded", function() {
      var ref = document.querySelector("[data-md-component=palette]")
      ref.addEventListener("change", function() {
        var palette = __md_get("__palette")
        if (palette && typeof palette.color === "object") {
          var theme = palette.color.scheme === "slate"
            ? "transparent_dark"
            : "light"

          // Instruct Giscus to change theme
          var frame = document.querySelector(".giscus-frame")
          frame.contentWindow.postMessage(
            { giscus: { setConfig: { theme } } },
            "https://giscus.app"
          )
        }
      })
    })
  </script>
{% endif %}
```

1.  此代码块确保[Giscus]在以下情况下以深色主题渲染
    调色板设置为“板岩”。注意，多个暗主题可用，
    所以你可以根据自己的喜好改变它。

用您使用[Giscus]生成的代码段替换突出显示的行
上一步中的配置工具。如果你从上面复制了片段，
您可以通过设置“comments”前台来启用页面上的评论
属性为“true”：

``` yaml
---
comments: true
---

# Page title
...
```

如果要为整个文件夹启用注释，可以使用
[built-in meta plugin].

  [Giscus GitHub App]: https://github.com/apps/giscus
  [theme extension]: ../customization.md#extending-the-theme
  [comments]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/comments.html
  [overriding partials]: ../customization.md#overriding-partials
  [built-in meta plugin]: ../plugins/meta.md

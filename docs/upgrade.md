# 如何升级

使用升级至最新版本:

```
pip install --upgrade --force-reinstall mkdocs-material
```

显示当前安装的版本:

```
pip show mkdocs-material
```

## 从8.x升级到9.x

此主要版本包括一个全新的搜索实现，速度更快
并允许丰富的预览、高级标记化和更好的突出显示。
它作为Insiders的一部分已经存在了一年多，现在资金
目标实现了，进入了社区版。

### 更改 `mkdocs.yml`

#### `content.code.copy`

复制到剪贴板按钮现在是可选的，可以启用或禁用
每个区块。如果要为所有代码块启用它们，请添加以下内容
指向`mkdocs.yml`的行：

``` yaml
theme:
  features:
    - content.code.copy
```

#### `content.action.*`

“查看源代码”按钮可以显示在“编辑此页面”按钮旁边，两者
现在必须明确启用该功能。将以下行添加到
`mkdocs.yml`：

``` yaml
theme:
  features:
    - content.action.edit
    - content.action.view
```

#### `navigation.footer`

页脚中的_prevous_和_next_按钮现在是可选的。如果你想
将它们保留在文档中，将以下行添加到`mkdocs.yml`中：

``` yaml
theme:
  features:
    - navigation.footer
```

#### `theme.language`

韩语和挪威语代码被重新命名，因为它们是非标准的：

- `kr` 切换到 `ko`
- `no` 切换到 `nb`

#### `feedback.ratings`

旧的、无名的占位符被删除了（在被弃用了几个占位符之后
月）。确保切换到新的命名占位符“{title}”和“{url}”：

```
https://github.com/.../issues/new/?title=[Feedback]+{title}+-+{url}
```

### Changes to `*.html` files

模板经历了一系列更改。如果你有定制
带有主题扩展的MkDocs材料，一定要包含最新的
更改模板。一个好的起点是[检查差异]。

！！！警告“升级后内置插件不工作？”

    如果其中一个内置插件（搜索或标签）在没有
    任何明显的错误或原因，都很可能与自定义覆盖有关。
    [MkDocs 1.4.1]及以上版本允许主题为内置插件命名
    Material for MkDocs 9现在允许作者使用第三方
    与内置插件同名的插件。在覆盖项中搜索
    [`"in config.plugins"`][in config.plugins]并添加`material/`命名空间。
    受影响的部分：

    - [`content.html`][content.html]
    - [`header.html`][header.html]

  [inspect the diff]: https://github.com/squidfunk/mkdocs-material/pull/4628/files#diff-3ca112736b9164701b599f34780107abf14bb79fe110c478cac410be90899828
  [MkDocs 1.4.1]: https://github.com/mkdocs/mkdocs/releases/tag/1.4.1
  [in config.plugins]: https://github.com/squidfunk/mkdocs-material/search?q=%22in+config.plugins%22
  [content.html]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/content.html
  [header.html]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/header.html

## Upgrading from 7.x to 8.x

### What's new?

- 添加了对代码注释的支持
- 增加了对锚点跟踪的支持
- 增加了对版本警告的支持
- 添加了`copyright`部分，便于覆盖
- 删除了过时的内容选项卡旧版实现
- 删除了弃用的`seealso`警告类型
- 删除了弃用的`site_keywords`设置（MkDocs不支持）
- 删除了已弃用的预构建搜索索引支持
- 删除了弃用的web应用程序清单-使用自定义
- 删除了`extracopyright`变量——使用新的`copyright`部分
- 删除Disqus集成-使用自定义
- 切换到简单选择器列表的`:is()`选择器
- 将autoprefixer从`last 4 years`切换到`last 2 years`
- 全面改进CSS以符合现代标准
- 改进了字体的CSS变量语义
- 通过重组部分来提高可扩展性
- 改进打印时对`details`的处理
- 改进了脚注的键盘导航
- 修复#3214:搜索突出显示会在网站为空时中断网站

### Changes to `mkdocs.yml`

#### `pymdownx.tabbed`

放弃了对[Tabbed]扩展的传统风格的支持，转而支持
新的替代实现在移动设备上具有更好的性能
视口]：

=== "8.x"

    ``` yaml
    markdown_extensions:
      - pymdownx.tabbed:
          alternate_style: true
    ```

=== "7.x"

    ``` yaml
    markdown_extensions:
      - pymdownx.tabbed
    ```

  [Tabbed]: setup/extensions/python-markdown-extensions.md#tabbed
  [better behavior on mobile viewports]: https://x.com/squidfunk/status/1424740370596958214

#### `pymdownx.superfences`

必须从[custom fence][SuperFences]中删除`*-experimental`后缀
类属性，用于将代码块定位为[diagrams]
使用[Meamaid.js]：

=== "8.x"

    ``` yaml
    markdown_extensions:
      - pymdownx.superfences:
          custom_fences:
            - name: mermaid
              class: mermaid
              format: !!python/name:pymdownx.superfences.fence_code_format
    ```

=== "7.x"

    ``` yaml
    markdown_extensions:
      - pymdownx.superfences:
          custom_fences:
            - name: mermaid
              class: mermaid-experimental
              format: !!python/name:pymdownx.superfences.fence_code_format
    ```

  [SuperFences]: setup/extensions/python-markdown-extensions.md#superfences
  [diagrams]: reference/diagrams.md
  [Mermaid.js]: https://mermaid-js.github.io/mermaid/

#### `google_analytics`

此选项[在MkDocs 1.2.0中已弃用]，作为
基于JavaScript的分析集成是一个主题的责任。
必须更改以下行：

=== "8.x"

    ``` yaml
    extra:
      analytics:
        provider: google
        property: UA-XXXXXXXX-X
    ```

=== "7.x"

    ``` yaml
    google_analytics:
      - UA-XXXXXXXX-X
      - auto
    ```

  [在MkDocs 1.2.0中已弃用]: https://www.mkdocs.org/about/release-notes/#backward-incompatible-changes-in-12

### 对`*.html`文件的更改{data-search-exclude}

模板经过了一系列更改，使其经得起未来考验。如果
您已使用主题扩展来覆盖块或模板，请确保它
匹配新结构：

- 如果你已经覆盖了 __block__ ，请检查`base.html`以了解潜在的更改
- 如果你覆盖了 __template__ ，请检查相应的`*.html`文件
  潜在变化

=== ":octicons-file-code-16: `base.html`"

    ``` diff
    @@ -13,11 +13,6 @@
           {% elif config.site_description %}
             <meta name="description" content="{{ config.site_description }}">
           {% endif %}
    -      {% if page and page.meta and page.meta.keywords %}
    -        <meta name="keywords" content="{{ page.meta.keywords }}">
    -      {% elif config.site_keywords %}
    -        <meta name="keywords" content="{{ config.site_keywords }}">
    -      {% endif %}
           {% if page and page.meta and page.meta.author %}
             <meta name="author" content="{{ page.meta.author }}">
           {% elif config.site_author %}
    @@ -61,15 +56,13 @@
                 font.text | replace(' ', '+') + ':300,400,400i,700%7C' +
                 font.code | replace(' ', '+')
               }}&display=fallback">
    -        <style>:root{--md-text-font-family:"{{ font.text }}";--md-code-font-family:"{{ font.code }}"}</style>
    +        <style>:root{--md-text-font:"{{ font.text }}";--md-code-font:"{{ font.code }}"}</style>
           {% endif %}
         {% endblock %}
    -    {% if config.extra.manifest %}
    -      <link rel="manifest" href="{{ config.extra.manifest | url }}" crossorigin="use-credentials">
    -    {% endif %}
         {% for path in config["extra_css"] %}
           <link rel="stylesheet" href="{{ path | url }}">
         {% endfor %}
    +    {% include "partials/javascripts/base.html" %}
         {% block analytics %}
           {% include "partials/integrations/analytics.html" %}
         {% endblock %}
    @@ -89,7 +82,6 @@
         <body dir="{{ direction }}">
       {% endif %}
         {% set features = config.theme.features or [] %}
    -    {% include "partials/javascripts/base.html" %}
         {% if not config.theme.palette is mapping %}
           {% include "partials/javascripts/palette.html" %}
         {% endif %}
    @@ -106,13 +98,25 @@
         </div>
         <div data-md-component="announce">
           {% if self.announce() %}
    -        <aside class="md-banner md-announce">
    -          <div class="md-banner__inner md-announce__inner md-grid md-typeset">
    +        <aside class="md-banner">
    +          <div class="md-banner__inner md-grid md-typeset">
                 {% block announce %}{% endblock %}
               </div>
             </aside>
           {% endif %}
         </div>
    +    {% if config.extra.version %}
    +      <div data-md-component="outdated" hidden>
    +        <aside class="md-banner md-banner--warning">
    +          {% if self.outdated() %}
    +            <div class="md-banner__inner md-grid md-typeset">
    +              {% block outdated %}{% endblock %}
    +            </div>
    +            {% include "partials/javascripts/outdated.html" %}
    +          {% endif %}
    +        </aside>
    +      </div>
    +    {% endif %}
         {% block header %}
           {% include "partials/header.html" %}
         {% endblock %}
    @@ -156,25 +160,7 @@
               <div class="md-content" data-md-component="content">
                 <article class="md-content__inner md-typeset">
                   {% block content %}
    -                {% if page.edit_url %}
    -                  <a href="{{ page.edit_url }}" title="{{ lang.t('edit.link.title') }}" class="md-content__button md-icon">
    -                    {% include ".icons/material/pencil.svg" %}
    -                  </a>
    -                {% endif %}
    -                {% if not "\x3ch1" in page.content %}
    -                  <h1>{{ page.title | d(config.site_name, true)}}</h1>
    -                {% endif %}
    -                {{ page.content }}
    -                {% if page and page.meta %}
    -                  {% if page.meta.git_revision_date_localized or
    -                        page.meta.revision_date
    -                  %}
    -                    {% include "partials/source-file.html" %}
    -                  {% endif %}
    -                {% endif %}
    -              {% endblock %}
    -              {% block disqus %}
    -                {% include "partials/integrations/disqus.html" %}
    +                {% include "partials/content.html" %}
                   {% endblock %}
                 </article>
               </div>
    ```

    ``` diff
    @@ -38,13 +38,6 @@
             <meta name="description" content="{{ config.site_description }}" />
           {% endif %}

    -      <!-- Page keywords -->
    -      {% if page and page.meta and page.meta.keywords %}
    -        <meta name="keywords" content="{{ page.meta.keywords }}" />
    -      {% elif config.site_keywords %}
    -        <meta name="keywords" content="{{ config.site_keywords }}" />
    -      {% endif %}
    -
           <!-- Page author -->
           {% if page and page.meta and page.meta.author %}
             <meta name="author" content="{{ page.meta.author }}" />
    @@ -120,27 +113,21 @@
             />
             <style>
               :root {
    -            --md-text-font-family: "{{ font.text }}";
    -            --md-code-font-family: "{{ font.code }}";
    +            --md-text-font: "{{ font.text }}";
    +            --md-code-font: "{{ font.code }}";
               }
             </style>
           {% endif %}
         {% endblock %}

    -    <!-- Progressive Web App Manifest -->
    -    {% if config.extra.manifest %}
    -      <link
    -        rel="manifest"
    -        href="{{ config.extra.manifest | url }}"
    -        crossorigin="use-credentials"
    -      />
    -    {% endif %}
    -
         <!-- Custom style sheets -->
         {% for path in config["extra_css"] %}
           <link rel="stylesheet" href="{{ path | url }}" />
         {% endfor %}

    +    <!-- Helper functions for inline scripts -->
    +    {% include "partials/javascripts/base.html" %}
    +
         <!-- Analytics -->
         {% block analytics %}
           {% include "partials/integrations/analytics.html" %}
    @@ -172,7 +159,6 @@

         <!-- Retrieve features from configuration -->
         {% set features = config.theme.features or [] %}
    -    {% include "partials/javascripts/base.html" %}

         <!-- User preference: color palette -->
         {% if not config.theme.palette is mapping %}
    @@ -214,14 +200,28 @@
         <!-- Announcement bar -->
         <div data-md-component="announce">
           {% if self.announce() %}
    -        <aside class="md-banner md-announce">
    -          <div class="md-banner__inner md-announce__inner md-grid md-typeset">
    +        <aside class="md-banner">
    +          <div class="md-banner__inner md-grid md-typeset">
                 {% block announce %}{% endblock %}
               </div>
             </aside>
           {% endif %}
         </div>

    +    <!-- Version warning -->
    +    {% if config.extra.version %}
    +      <div data-md-component="outdated" hidden>
    +        <aside class="md-banner md-banner--warning">
    +          {% if self.outdated() %}
    +            <div class="md-banner__inner md-grid md-typeset">
    +              {% block outdated %}{% endblock %}
    +            </div>
    +            {% include "partials/javascripts/outdated.html" %}
    +          {% endif %}
    +        </aside>
    +      </div>
    +    {% endif %}
    +
         <!-- Header -->
         {% block header %}
           {% include "partials/header.html" %}
    @@ -295,49 +295,11 @@
                   {% block content %}
    -
    -                <!-- Edit button -->
    -                {% if page.edit_url %}
    -                  <a
    -                    href="{{ page.edit_url }}"
    -                    title="{{ lang.t('edit.link.title') }}"
    -                    class="md-content__button md-icon"
    -                  >
    -                    {% include ".icons/material/pencil.svg" %}
    -                  </a>
    -                {% endif %}
    -
    -                <!--
    -                  Hack: check whether the content contains a h1 headline. If it
    -                  doesn't, the page title (or respectively site name) is used
    -                  as the main headline.
    -                -->
    -                {% if not "\x3ch1" in page.content %}
    -                  <h1>{{ page.title | d(config.site_name, true)}}</h1>
    -                {% endif %}
    -
    -                <!-- Markdown content -->
    -                {{ page.content }}
    -
    -                <!-- Last update of source file -->
    -                {% if page and page.meta %}
    -                  {% if page.meta.git_revision_date_localized or
    -                        page.meta.revision_date
    -                  %}
    -                    {% include "partials/source-file.html" %}
    -                  {% endif %}
    -                {% endif %}
    -              {% endblock %}
    -
    -              <!-- Disqus integration -->
    -              {% block disqus %}
    -                {% include "partials/integrations/disqus.html" %}
    +                {% include "partials/content.html" %}
                   {% endblock %}
                 </article>
               </div>
    ```

=== ":octicons-file-code-16: `partials/copyright.html`"

    ``` diff
    @@ -0,0 +1,16 @@
    +{#-
    +  This file was automatically generated - do not edit
    +-#}
    +<div class="md-copyright">
    +  {% if config.copyright %}
    +    <div class="md-copyright__highlight">
    +      {{ config.copyright }}
    +    </div>
    +  {% endif %}
    +  {% if not config.extra.generator == false %}
    +    Made with
    +    <a href="https://squidfunk.github.io/mkdocs-material/" target="_blank" rel="noopener">
    +      Material for MkDocs
    +    </a>
    +  {% endif %}
    +</div>
    ```

=== ":octicons-file-code-16: `partials/footer.html`"

    ``` diff
    @@ -41,21 +40,10 @@
       {% endif %}
       <div class="md-footer-meta md-typeset">
         <div class="md-footer-meta__inner md-grid">
    -      <div class="md-footer-copyright">
    -        {% if config.copyright %}
    -          <div class="md-footer-copyright__highlight">
    -            {{ config.copyright }}
    -          </div>
    -        {% endif %}
    -        {% if not config.extra.generator == false %}
    -          Made with
    -          <a href="https://squidfunk.github.io/mkdocs-material/" target="_blank" rel="noopener">
    -            Material for MkDocs
    -          </a>
    -        {% endif %}
    -        {{ extracopyright }}
    -      </div>
    -      {% include "partials/social.html" %}
    +      {% include "partials/copyright.html" %}
    +      {% if config.extra.social %}
    +        {% include "partials/social.html" %}
    +      {% endif %}
         </div>
       </div>
     </footer>
    ```

=== ":octicons-file-code-16: `partials/social.html`"

    ``` diff
    @@ -4,17 +4,15 @@
    -{% if config.extra.social %}
    -  <div class="md-footer-social">
    -    {% for social in config.extra.social %}
    -      {% set title = social.name %}
    -      {% if not title and "//" in social.link %}
    -        {% set _,url = social.link.split("//") %}
    -        {% set title = url.split("/")[0] %}
    -      {% endif %}
    -      <a href="{{ social.link }}" target="_blank" rel="noopener" title="{{ title | e }}" class="md-footer-social__link">
    -        {% include ".icons/" ~ social.icon ~ ".svg" %}
    -      </a>
    -    {% endfor %}
    -  </div>
    -{% endif %}
    +<div class="md-social">
    +  {% for social in config.extra.social %}
    +    {% set title = social.name %}
    +    {% if not title and "//" in social.link %}
    +      {% set _, url = social.link.split("//") %}
    +      {% set title  = url.split("/")[0] %}
    +    {% endif %}
    +    <a href="{{ social.link }}" target="_blank" rel="noopener" title="{{ title | e }}" class="md-social__link">
    +      {% include ".icons/" ~ social.icon ~ ".svg" %}
    +    </a>
    +  {% endfor %}
    +</div>
    ```

## 从6.x升级到7.x

### 有什么新鲜事吗？

- 增加了对部署多个版本的支持
- 添加了对集成语言选择器的支持
- 添加了对将警告呈现为内联块的支持
- 重写底层反应式架构
- 删除Webpack，转而采用响应式构建策略（-480个依赖项）
- 修复了内容选项卡切换后代码块的键盘导航问题

### 更改 `mkdocs.yml`

#### `extra.version.method`

版本控制方法配置已重命名为`extra.version.provider`
允许未来采用不同的版本控制策略：

=== "7.x"

    ``` yaml
    extra:
      version:
        provider: mike
    ```

=== "6.x"

    ``` yaml
    extra:
      version:
        method: mike
    ```

### 对`*.html`文件的更改{ data-search-exclude }

模板经过了一系列更改，使其经得起未来考验。如果
您已使用主题扩展来覆盖块或模板，请确保它
匹配新结构：

- 如果你已经覆盖了 __block__ ，请检查`base.html`以了解潜在的更改
- 如果你覆盖了 __template__ ，请检查相应的`*.html`文件
  潜在变化

=== ":octicons-file-code-16: `base.html`"

    ``` diff
    @@ -61,7 +61,7 @@
                 font.text | replace(' ', '+') + ':300,400,400i,700%7C' +
                 font.code | replace(' ', '+')
               }}&display=fallback">
    -        <style>body,input{font-family:"{{ font.text }}",-apple-system,BlinkMacSystemFont,Helvetica,Arial,sans-serif}code,kbd,pre{font-family:"{{ font.code }}",SFMono-Regular,Consolas,Menlo,monospace}</style>
    +        <style>:root{--md-text-font-family:"{{ font.text }}";--md-code-font-family:"{{ font.code }}"}</style>
           {% endif %}
         {% endblock %}
         {% if config.extra.manifest %}
    @@ -131,7 +131,7 @@
                   {% if page and page.meta and page.meta.hide %}
                     {% set hidden = "hidden" if "navigation" in page.meta.hide %}
                   {% endif %}
    -              <div class="md-sidebar md-sidebar--primary" data-md-component="navigation" {{ hidden }}>
    +              <div class="md-sidebar md-sidebar--primary" data-md-component="sidebar" data-md-type="navigation" {{ hidden }}>
                     <div class="md-sidebar__scrollwrap">
                       <div class="md-sidebar__inner">
                         {% include "partials/nav.html" %}
    @@ -143,7 +143,7 @@
                   {% if page and page.meta and page.meta.hide %}
                     {% set hidden = "hidden" if "toc" in page.meta.hide %}
                   {% endif %}
    -              <div class="md-sidebar md-sidebar--secondary" data-md-component="toc" {{ hidden }}>
    +              <div class="md-sidebar md-sidebar--secondary" data-md-component="sidebar" data-md-type="toc" {{ hidden }}>
                     <div class="md-sidebar__scrollwrap">
                       <div class="md-sidebar__inner">
                         {% include "partials/toc.html" %}
    @@ -152,7 +152,7 @@
                   </div>
                 {% endif %}
               {% endblock %}
    -          <div class="md-content">
    +          <div class="md-content" data-md-component="content">
                 <article class="md-content__inner md-typeset">
                   {% block content %}
                     {% if page.edit_url %}
    @@ -183,10 +183,18 @@
             {% include "partials/footer.html" %}
           {% endblock %}
         </div>
    -    {% block scripts %}
    -      <script src="{{ 'assets/javascripts/vendor.18f0862e.min.js' | url }}"></script>
    -      <script src="{{ 'assets/javascripts/bundle.994580cf.min.js' | url }}"></script>
    -      {%- set translations = {} -%}
    +    <div class="md-dialog" data-md-component="dialog">
    +      <div class="md-dialog__inner md-typeset"></div>
    +    </div>
    +    {% block config %}
    +      {%- set app = {
    +        "base": base_url,
    +        "features": features,
    +        "translations": {},
    +        "search": "assets/javascripts/workers/search.217ffd95.min.js" | url,
    +        "version": config.extra.version or None
    +      } -%}
    +      {%- set translations = app.translations -%}
           {%- for key in [
             "clipboard.copy",
             "clipboard.copied",
    @@ -204,19 +212,12 @@
           ] -%}
             {%- set _ = translations.update({ key: lang.t(key) }) -%}
           {%- endfor -%}
    -      <script id="__lang" type="application/json">
    -        {{- translations | tojson -}}
    -      </script>
    -      {% block config %}{% endblock %}
    -      <script>
    -        app = initialize({
    -          base: "{{ base_url }}",
    -          features: {{ features or [] | tojson }},
    -          search: Object.assign({
    -            worker: "{{ 'assets/javascripts/worker/search.9c0e82ba.min.js' | url }}"
    -          }, typeof search !== "undefined" && search)
    -        })
    +      <script id="__config" type="application/json">
    +        {{- app | tojson -}}
           </script>
    +    {% endblock %}
    +    {% block scripts %}
    +      <script src="{{ 'assets/javascripts/bundle.926459b3.min.js' | url }}"></script>
           {% for path in config["extra_javascript"] %}
             <script src="{{ path | url }}"></script>
           {% endfor %}
    ```

=== ":octicons-file-code-16: `partials/footer.html`"

    ``` diff
    -    <div class="md-footer-nav">
    -      <nav class="md-footer-nav__inner md-grid" aria-label="{{ lang.t('footer.title') }}">
    -        {% if page.previous_page %}
    -          <a href="{{ page.previous_page.url | url }}" class="md-footer-nav__link md-footer-nav__link--prev" rel="prev">
    -            <div class="md-footer-nav__button md-icon">
    -              {% include ".icons/material/arrow-left.svg" %}
    -            </div>
    -            <div class="md-footer-nav__title">
    -              <div class="md-ellipsis">
    -                <span class="md-footer-nav__direction">
    -                  {{ lang.t("footer.previous") }}
    -                </span>
    -                {{ page.previous_page.title }}
    -              </div>
    -            </div>
    -          </a>
    -        {% endif %}
    -        {% if page.next_page %}
    -          <a href="{{ page.next_page.url | url }}" class="md-footer-nav__link md-footer-nav__link--next" rel="next">
    -            <div class="md-footer-nav__title">
    -              <div class="md-ellipsis">
    -                <span class="md-footer-nav__direction">
    -                  {{ lang.t("footer.next") }}
    -                </span>
    -                {{ page.next_page.title }}
    -              </div>
    +    <nav class="md-footer__inner md-grid" aria-label="{{ lang.t('footer.title') }}">
    +      {% if page.previous_page %}
    +        <a href="{{ page.previous_page.url | url }}" class="md-footer__link md-footer__link--prev" rel="prev">
    +          <div class="md-footer__button md-icon">
    +            {% include ".icons/material/arrow-left.svg" %}
    +          </div>
    +          <div class="md-footer__title">
    +            <div class="md-ellipsis">
    +              <span class="md-footer__direction">
    +                {{ lang.t("footer.previous") }}
    +              </span>
    +              {{ page.previous_page.title }}
                 </div>
    -            <div class="md-footer-nav__button md-icon">
    -              {% include ".icons/material/arrow-right.svg" %}
    +          </div>
    +        </a>
    +      {% endif %}
    +      {% if page.next_page %}
    +        <a href="{{ page.next_page.url | url }}" class="md-footer__link md-footer__link--next" rel="next">
    +          <div class="md-footer__title">
    +            <div class="md-ellipsis">
    +              <span class="md-footer__direction">
    +                {{ lang.t("footer.next") }}
    +              </span>
    +              {{ page.next_page.title }}
                 </div>
    -          </a>
    -        {% endif %}
    -      </nav>
    -    </div>
    +          </div>
    +          <div class="md-footer__button md-icon">
    +            {% include ".icons/material/arrow-right.svg" %}
    +          </div>
    +        </a>
    +      {% endif %}
    +    </nav>
       {% endif %}
       <div class="md-footer-meta md-typeset">
         <div class="md-footer-meta__inner md-grid">
    ```

=== ":octicons-file-code-16: `partials/header.html`"

    ``` diff
    @@ -6,21 +6,21 @@
       {% set site_url = site_url ~ "/index.html" %}
     {% endif %}
     <header class="md-header" data-md-component="header">
    -  <nav class="md-header-nav md-grid" aria-label="{{ lang.t('header.title') }}">
    -    <a href="{{ site_url }}" title="{{ config.site_name | e }}" class="md-header-nav__button md-logo" aria-label="{{ config.site_name }}">
    +  <nav class="md-header__inner md-grid" aria-label="{{ lang.t('header.title') }}">
    +    <a href="{{ site_url }}" title="{{ config.site_name | e }}" class="md-header__button md-logo" aria-label="{{ config.site_name }}">
           {% include "partials/logo.html" %}
         </a>
    -    <label class="md-header-nav__button md-icon" for="__drawer">
    +    <label class="md-header__button md-icon" for="__drawer">
           {% include ".icons/material/menu" ~ ".svg" %}
         </label>
    -    <div class="md-header-nav__title" data-md-component="header-title">
    -      <div class="md-header-nav__ellipsis">
    -        <div class="md-header-nav__topic">
    +    <div class="md-header__title" data-md-component="header-title">
    +      <div class="md-header__ellipsis">
    +        <div class="md-header__topic">
               <span class="md-ellipsis">
                 {{ config.site_name }}
               </span>
             </div>
    -        <div class="md-header-nav__topic">
    +        <div class="md-header__topic" data-md-component="header-topic">
               <span class="md-ellipsis">
                 {% if page and page.meta and page.meta.title %}
                   {{ page.meta.title }}
    @@ -31,14 +31,35 @@
             </div>
           </div>
         </div>
    +    <div class="md-header__options">
    +      {% if config.extra.alternate %}
    +        <div class="md-select">
    +          {% set icon = config.theme.icon.alternate or "material/translate" %}
    +          <span class="md-header__button md-icon">
    +            {% include ".icons/" ~ icon ~ ".svg" %}
    +          </span>
    +          <div class="md-select__inner">
    +            <ul class="md-select__list">
    +              {% for alt in config.extra.alternate %}
    +                <li class="md-select__item">
    +                  <a href="{{ alt.link | url }}" class="md-select__link">
    +                    {{ alt.name }}
    +                  </a>
    +                </li>
    +                {% endfor %}
    +            </ul>
    +          </div>
    +        </div>
    +      {% endif %}
    +    </div>
         {% if "search" in config["plugins"] %}
    -      <label class="md-header-nav__button md-icon" for="__search">
    +      <label class="md-header__button md-icon" for="__search">
             {% include ".icons/material/magnify.svg" %}
           </label>
           {% include "partials/search.html" %}
         {% endif %}
         {% if config.repo_url %}
    -      <div class="md-header-nav__source">
    +      <div class="md-header__source">
             {% include "partials/source.html" %}
           </div>
         {% endif %}
    ```

=== ":octicons-file-code-16: `partials/source.html`"

    ``` diff
    @@ -4,5 +4,5 @@
     {% import "partials/language.html" as lang with context %}
    -<a href="{{ config.repo_url }}" title="{{ lang.t('source.link.title') }}" class="md-source">
    +<a href="{{ config.repo_url }}" title="{{ lang.t('source.link.title') }}"  class="md-source" data-md-component="source">
       <div class="md-source__icon md-icon">
         {% set icon = config.theme.icon.repo or "fontawesome/brands/git-alt" %}
         {% include ".icons/" ~ icon ~ ".svg" %}
    ```

=== ":octicons-file-code-16: `partials/toc.html`"

    ``` diff
    @@ -12,7 +12,7 @@
           <span class="md-nav__icon md-icon"></span>
           {{ lang.t("toc.title") }}
         </label>
    -    <ul class="md-nav__list" data-md-scrollfix>
    +    <ul class="md-nav__list" data-md-component="toc" data-md-scrollfix>
           {% for toc_item in toc %}
             {% include "partials/toc-item.html" %}
           {% endfor %}
    ```

## 从5.x升级到6.x

### 有什么新鲜事吗？

- 改进了搜索结果的外观和感觉
- 键入时提高了搜索结果的稳定性
- 改进了搜索结果分组（页面+标题）
- 提高了搜索结果的相关性和评分
- 在搜索结果中添加了缺失查询词的显示
- 供应商捆绑包的大小减少了25%（84kb→ 67kb)
- 减小Docker镜像的大小以提高CI构建性能
- 删除英雄部分，支持自定义实现
- 删除了已弃用的前端功能

### 更改 `mkdocs.yml`

以下是需要对`mkdocs.yml`进行的更改列表。注意
如果您定义了该值，则只需调整它，因此如果您的配置
不包含密钥，可以跳过它。

#### `theme.features`

所有可以从`mkdocs.yml`设置的功能标志，如[tabs]和
[instant loading]，现在前缀为组件的名称或
它们所应用的功能，例如`navigation.*`：

=== "6.x"

    ``` yaml
    theme:
      features:
        - navigation.tabs
        - navigation.instant
    ```

=== "5.x"

    ``` yaml
    theme:
      features:
        - tabs
        - instant
    ```

  [tabs]: setup/setting-up-navigation.md#_9
  [instant loading]: setup/setting-up-navigation.md#_3

### 对`*.html`文件的更改{ data-search-exclude }

模板经过了一系列更改，使其经得起未来考验。如果
您已使用主题扩展来覆盖块或模板，请确保它
匹配新结构：

- 如果你已经覆盖了 __block__ ，请检查`base.html`以了解潜在的更改
- 如果你覆盖了 __template__ ，请检查相应的`*.html`文件
  潜在变化

=== ":octicons-file-code-16: `base.html`"

    ``` diff
    @@ -22,13 +22,6 @@

     {% import "partials/language.html" as lang with context %}

    -<!-- Theme options -->
    -{% set palette = config.theme.palette %}
    -{% if not palette is mapping %}
    -  {% set palette = palette | first %}
    -{% endif %}
    -{% set font = config.theme.font %}
    -
     <!doctype html>
     <html lang="{{ lang.t('language') }}" class="no-js">
       <head>
    @@ -45,21 +38,8 @@
             <meta name="description" content="{{ config.site_description }}" />
           {% endif %}

    -      <!-- Redirect -->
    -      {% if page and page.meta and page.meta.redirect %}
    -        <script>
    -          var anchor = window.location.hash.substr(1)
    -          location.href = '{{ page.meta.redirect }}' +
    -            (anchor ? '#' + anchor : '')
    -        </script>
    -
    -        <!-- Fallback in case JavaScript is not available -->
    -        <meta http-equiv="refresh" content="0; url={{ page.meta.redirect }}" />
    -        <meta name="robots" content="noindex" />
    -        <link rel="canonical" href="{{ page.meta.redirect }}" />
    -
           <!-- Canonical -->
    -      {% elif page.canonical_url %}
    +      {% if page.canonical_url %}
             <link rel="canonical" href="{{ page.canonical_url }}" />
           {% endif %}

    @@ -96,20 +76,21 @@
           <link rel="stylesheet" href="{{ 'assets/stylesheets/main.css' | url }}" />

           <!-- Extra color palette -->
    -      {% if palette.scheme or palette.primary or palette.accent %}
    +      {% if config.theme.palette %}
    +        {% set palette = config.theme.palette %}
             <link
               rel="stylesheet"
               href="{{ 'assets/stylesheets/palette.css' | url }}"
             />
    -      {% endif %}

    -      <!-- Theme-color meta tag for Android -->
    -      {% if palette.primary %}
    -        {% import "partials/palette.html" as map %}
    -        {% set primary = map.primary(
    -          palette.primary | replace(" ", "-") | lower
    -        ) %}
    -        <meta name="theme-color" content="{{ primary }}" />
    +        <!-- Theme-color meta tag for Android -->
    +        {% if palette.primary %}
    +          {% import "partials/palette.html" as map %}
    +          {% set primary = map.primary(
    +            palette.primary | replace(" ", "-") | lower
    +          ) %}
    +          <meta name="theme-color" content="{{ primary }}" />
    +        {% endif %}
           {% endif %}
         {% endblock %}

    @@ -120,7 +101,8 @@
         {% block fonts %}

           <!-- Load fonts from Google -->
    -      {% if font != false %}
    +      {% if config.theme.font != false %}
    +        {% set font = config.theme.font %}
             <link href="https://fonts.gstatic.com" rel="preconnect" crossorigin />
             <link
              rel="stylesheet"
    @@ -169,8 +151,12 @@

       <!-- Text direction and color palette, if defined -->
       {% set direction = config.theme.direction or lang.t('direction') %}
    -  {% if palette.scheme or palette.primary or palette.accent %}
    -    {% set scheme  = palette.scheme | lower %}
    +  {% if config.theme.palette %}
    +    {% set palette = config.theme.palette %}
    +    {% if not palette is mapping %}
    +      {% set palette = palette | first %}
    +    {% endif %}
    +    {% set scheme  = palette.scheme  | replace(" ", "-") | lower %}
         {% set primary = palette.primary | replace(" ", "-") | lower %}
         {% set accent  = palette.accent  | replace(" ", "-") | lower %}
         <body
    @@ -179,18 +165,19 @@
           data-md-color-primary="{{ primary }}"
           data-md-color-accent="{{ accent }}"
         >
    +
    +      <!-- Experimental: set color scheme based on preference -->
    +      {% if "preference" == scheme %}
    +        <script>
    +          if (matchMedia("(prefers-color-scheme: dark)").matches)
    +            document.body.setAttribute("data-md-color-scheme", "slate")
    +        </script>
    +      {% endif %}
    +
       {% else %}
         <body dir="{{ direction }}">
       {% endif %}

    -    <!-- Experimental: set color scheme based on preference -->
    -    {% if "preference" == palette.scheme %}
    -      <script>
    -        if (matchMedia("(prefers-color-scheme: dark)").matches)
    -          document.body.setAttribute("data-md-color-scheme", "slate")
    -      </script>
    -    {% endif %}
    -
         <!--
           State toggles - we need to set autocomplete="off" in order to reset the
           drawer on back button invocation in some browsers
    @@ -243,15 +230,11 @@
         <div class="md-container" data-md-component="container">

           <!-- Hero teaser -->
    -      {% block hero %}
    -        {% if page and page.meta and page.meta.hero %}
    -          {% include "partials/hero.html" with context %}
    -        {% endif %}
    -      {% endblock %}
    +      {% block hero %}{% endblock %}

           <!-- Tabs navigation -->
           {% block tabs %}
    -        {% if "tabs" in config.theme.features %}
    +        {% if "navigation.tabs" in config.theme.features %}
               {% include "partials/tabs.html" %}
             {% endif %}
           {% endblock %}
    @@ -310,13 +293,6 @@
                       </a>
                     {% endif %}

    -                <!-- Link to source file -->
    -                {% block source %}
    -                  {% if page and page.meta and page.meta.source %}
    -                    {% include "partials/source-link.html" %}
    -                  {% endif %}
    -                {% endblock %}
    -
                     <!--
                       Hack: check whether the content contains a h1 headline. If it
                       doesn't, the page title (or respectively site name) is used
    @@ -370,7 +346,10 @@
             "search.result.placeholder",
             "search.result.none",
             "search.result.one",
    -        "search.result.other"
    +        "search.result.other",
    +        "search.result.more.one",
    +        "search.result.more.other",
    +        "search.result.term.missing"
           ] -%}
             {%- set _ = translations.update({ key: lang.t(key) }) -%}
           {%- endfor -%}
    ```

=== ":octicons-file-code-16: `partials/hero.html`"

    ``` diff
    @@ -1,12 +0,0 @@
    -{#-
    -  This file was automatically generated - do not edit
    --#}
    -{% set class = "md-hero" %}
    -{% if "tabs" not in config.theme.features %}
    -  {% set class = "md-hero md-hero--expand" %}
    -{% endif %}
    -<div class="{{ class }}" data-md-component="hero">
    -  <div class="md-hero__inner md-grid">
    -    {{ page.meta.hero }}
    -  </div>
    -</div>
    ```

=== ":octicons-file-code-16: `partials/source-link`"

    ``` diff
    @@ -1,14 +0,0 @@
    -{#-
    -  This file was automatically generated - do not edit
    --#}
    -{% import "partials/language.html" as lang with context %}
    -{% set repo = config.repo_url %}
    -{% if repo | last == "/" %}
    -  {% set repo = repo[:-1] %}
    -{% endif %}
    -{% set path = page.meta.path | default("") %}
    -<a href="{{ [repo, path, page.meta.source] | join('/') }}" title="{{ page.meta.source }}" class="md-content__button md-icon">
    -  {{ lang.t("meta.source") }}
    -  {% set icon = config.theme.icon.repo or "fontawesome/brands/git-alt" %}
    -  {% include ".icons/" ~ icon ~ ".svg" %}
    -</a>
    ```

## 从4.x升级到5.x

### 有什么新鲜事吗？

- 反应式架构——试试`#!js app.dialog$.next("Hi!")`在控制台中
- [Instant loading] – 使Material表现得像单页应用程序
- 使用[CSS variables]改进CSS自定义-设置品牌的颜色
- 提高了CSS的弹性，例如对自定义标题进行适当的侧边栏锁定
- 改进了[icon integration]和配置-现在包括超过5k个图标
- 添加了使用任何图标作为徽标、存储库和社交链接的可能性
- 搜索UI不再冻结（移动到web worker）
- 使用即时加载时只构建一次搜索索引
- 改进了可扩展键盘处理
- 支持[prebuilt search indexes]
- 支持显示GitLab存储库的stars和forks
- 支持侧边栏和搜索结果的滚动捕捉
- 由于不再支持Internet Explorer，减少了HTML和CSS的占用空间
- 一些UI元素（警告、表格等）略有改进

  [CSS variables]: setup/changing-the-colors.md#_11
  [icon integration]: reference/icons-emojis.md#_2
  [prebuilt search indexes]: plugins/search.md

### 更改 `mkdocs.yml`

以下是需要对`mkdocs.yml`进行的更改列表。注意
如果您定义了该值，则只需调整它，因此如果您的配置
不包含密钥，可以跳过它。

#### `theme.feature`

[tabs]和[instant loading]等可选功能现在实现为
标志，可以通过在`theme.features`下的`mkdocs.yml`中列出它们来启用：

=== "5.x"

    ``` yaml
    theme:
      features:
        - tabs
        - instant
    ```

=== "4.x"

    ``` yaml
    theme:
      feature:
        tabs: true
    ```

#### `theme.logo.icon`

徽标图标配置集中在`theme.icon.logo`下，现在可以
设置为[icons bundled with the theme][icon integration]中的任何一个：

=== "5.x"

    ``` yaml
    theme:
      icon:
        logo: material/cloud
    ```

=== "4.x"

    ``` yaml
    theme:
      logo:
        icon: cloud
    ```

#### `extra.repo_icon`

repo图标配置集中在`theme.icon.repo`下，现在可以
设置为[icons bundled with the theme][icon integration]中的任何一个：

=== "5.x"

    ``` yaml
    theme:
      icon:
        repo: fontawesome/brands/gitlab
    ```

=== "4.x"

    ``` yaml
    extra:
      repo_icon: gitlab
    ```

#### `extra.search.*`

搜索现在已配置为[plugin options]的一部分。请注意
搜索语言现在必须以字符串数组和“标记器”的形式列出`
已重命名为`separator`：

=== "5.x"

    ``` yaml
    plugins:
      - search:
          separator: '[\s\-\.]+'
          lang:
            - en
            - de
            - ru
    ```

=== "4.x"

    ``` yaml
    extra:
      search:
        language: en, de, ru
        tokenizer: '[\s\-\.]+'
    ```

  [plugin options]: plugins/search.md

#### `extra.social.*`

社交链接保持不变，但`type`键被重命名为`icon`
为了匹配指定要使用哪个图标的新方式：

=== "5.x"

    ``` yaml
    extra:
      social:
        - icon: fontawesome/brands/github-alt
          link: https://github.com/squidfunk
    ```

=== "4.x"

    ``` yaml
    extra:
      social:
        - type: github
          link: https://github.com/squidfunk
    ```

### 对`*.html`文件的更改{ data-search-exclude }

模板经过了一系列更改，使其经得起未来考验。如果
您已使用主题扩展来覆盖块或模板，请确保它
匹配新结构：

- 如果你已经覆盖了 __block__ ，请检查`base.html`以了解潜在的更改
- 如果你覆盖了 __template__ ，请检查相应的`*.html`文件
  潜在变化

=== ":octicons-file-code-16: `base.html`"

    ``` diff
    @@ -4,7 +4,6 @@
     {% import "partials/language.html" as lang with context %}
    -{% set feature = config.theme.feature %}
     {% set palette = config.theme.palette %}
     {% set font = config.theme.font %}
     <!doctype html>
    @@ -30,19 +29,6 @@
           {% elif config.site_author %}
             <meta name="author" content="{{ config.site_author }}">
           {% endif %}
    -      {% for key in [
    -        "clipboard.copy",
    -        "clipboard.copied",
    -        "search.language",
    -        "search.pipeline.stopwords",
    -        "search.pipeline.trimmer",
    -        "search.result.none",
    -        "search.result.one",
    -        "search.result.other",
    -        "search.tokenizer"
    -      ] %}
    -        <meta name="lang:{{ key }}" content="{{ lang.t(key) }}">
    -      {% endfor %}
           <link rel="shortcut icon" href="{{ config.theme.favicon | url }}">
           <meta name="generator" content="mkdocs-{{ mkdocs_version }}, mkdocs-material-5.0.0">
         {% endblock %}
    @@ -56,9 +42,9 @@
           {% endif %}
         {% endblock %}
         {% block styles %}
    -      <link rel="stylesheet" href="{{ 'assets/stylesheets/application.********.css' | url }}">
    +      <link rel="stylesheet" href="{{ 'assets/stylesheets/main.********.min.css' | url }}">
           {% if palette.primary or palette.accent %}
    -        <link rel="stylesheet" href="{{ 'assets/stylesheets/application-palette.********.css' | url }}">
    +        <link rel="stylesheet" href="{{ 'assets/stylesheets/palette.********.min.css' | url }}">
           {% endif %}
           {% if palette.primary %}
             {% import "partials/palette.html" as map %}
    @@ -69,20 +55,17 @@
           {% endif %}
         {% endblock %}
         {% block libs %}
    -      <script src="{{ 'assets/javascripts/modernizr.********.js' | url }}"></script>
         {% endblock %}
         {% block fonts %}
           {% if font != false %}
             <link href="https://fonts.gstatic.com" rel="preconnect" crossorigin>
             <link rel="stylesheet" href="https://fonts.googleapis.com/css?family={{
                 font.text | replace(' ', '+') + ':300,400,400i,700%7C' +
                 font.code | replace(' ', '+')
               }}&display=fallback">
             <style>body,input{font-family:"{{ font.text }}","Helvetica Neue",Helvetica,Arial,sans-serif}code,kbd,pre{font-family:"{{ font.code }}","Courier New",Courier,monospace}</style>
           {% endif %}
         {% endblock %}
    -    <link rel="stylesheet" href="{{ 'assets/fonts/material-icons.css' | url }}">
         {% if config.extra.manifest %}
           <link rel="manifest" href="{{ config.extra.manifest | url }}" crossorigin="use-credentials">
         {% endif %}
    @@ -95,47 +77,50 @@
         {% endblock %}
         {% block extrahead %}{% endblock %}
       </head>
    +  {% set direction = config.theme.direction | default(lang.t('direction')) %}
       {% if palette.primary or palette.accent %}
         {% set primary = palette.primary | replace(" ", "-") | lower %}
         {% set accent  = palette.accent  | replace(" ", "-") | lower %}
    -    <body dir="{{ lang.t('direction') }}" data-md-color-primary="{{ primary }}" data-md-color-accent="{{ accent }}">
    +    <body dir="{{ direction }}" data-md-color-primary="{{ primary }}" data-md-color-accent="{{ accent }}">
       {% else %}
    -    <body dir="{{ lang.t('direction') }}">
    +    <body dir="{{ direction }}">
       {% endif %}
    -    <svg class="md-svg">
    -      <defs>
    -        {% set platform = config.extra.repo_icon or config.repo_url %}
    -        {% if "github" in platform %}
    -          {% include "assets/images/icons/github.f0b8504a.svg" %}
    -        {% elif "gitlab" in platform %}
    -          {% include "assets/images/icons/gitlab.6dd19c00.svg" %}
    -        {% elif "bitbucket" in platform %}
    -          {% include "assets/images/icons/bitbucket.1b09e088.svg" %}
    -        {% endif %}
    -      </defs>
    -    </svg>
         <input class="md-toggle" data-md-toggle="drawer" type="checkbox" id="__drawer" autocomplete="off">
         <input class="md-toggle" data-md-toggle="search" type="checkbox" id="__search" autocomplete="off">
    -    <label class="md-overlay" data-md-component="overlay" for="__drawer"></label>
    +    <label class="md-overlay" for="__drawer"></label>
    +    <div data-md-component="skip">
    +      {% if page.toc | first is defined %}
    +        {% set skip = page.toc | first %}
    +        <a href="{{ skip.url | url }}" class="md-skip">
    +          {{ lang.t('skip.link.title') }}
    +        </a>
    +      {% endif %}
    +    </div>
    +    <div data-md-component="announce">
    +      {% if self.announce() %}
    +        <aside class="md-announce">
    +          <div class="md-announce__inner md-grid md-typeset">
    +            {% block announce %}{% endblock %}
    +          </div>
    +        </aside>
    +      {% endif %}
    +    </div>
         {% block header %}
           {% include "partials/header.html" %}
         {% endblock %}
    -    <div class="md-container">
    +    <div class="md-container" data-md-component="container">
           {% block hero %}
             {% if page and page.meta and page.meta.hero %}
               {% include "partials/hero.html" with context %}
             {% endif %}
           {% endblock %}
    -      {% if feature.tabs %}
    -        {% include "partials/tabs.html" %}
    -      {% endif %}
    +      {% block tabs %}
    +        {% if "tabs" in config.theme.features %}
    +          {% include "partials/tabs.html" %}
    +        {% endif %}
    +      {% endblock %}
    -      <main class="md-main" role="main">
    -        <div class="md-main__inner md-grid" data-md-component="container">
    +      <main class="md-main" data-md-component="main">
    +        <div class="md-main__inner md-grid">
               {% block site_nav %}
                 {% if nav %}
                   <div class="md-sidebar md-sidebar--primary" data-md-component="navigation">
    @@ -160,41 +141,25 @@
                 <article class="md-content__inner md-typeset">
                   {% block content %}
                     {% if page.edit_url %}
    -                  <a href="{{ page.edit_url }}" title="{{ lang.t('edit.link.title') }}" class="md-icon md-content__icon">&#xE3C9;</a>
    +                  <a href="{{ page.edit_url }}" title="{{ lang.t('edit.link.title') }}" class="md-content__button md-icon">
    +                    {% include ".icons/material/pencil.svg" %}
    +                  </a>
                     {% endif %}
    +                {% block source %}
    +                  {% if page and page.meta and page.meta.source %}
    +                    {% include "partials/source-link.html" %}
    +                  {% endif %}
    +                {% endblock %}
                     {% if not "\x3ch1" in page.content %}
                       <h1>{{ page.title | default(config.site_name, true)}}</h1>
                     {% endif %}
                     {{ page.content }}
    -                {% block source %}
    -                  {% if page and page.meta and page.meta.source %}
    -                    <h2 id="__source">{{ lang.t("meta.source") }}</h2>
    -                    {% set repo = config.repo_url %}
    -                    {% if repo | last == "/" %}
    -                      {% set repo = repo[:-1] %}
    -                    {% endif %}
    -                    {% set path = page.meta.path | default([""]) %}
    -                    {% set file = page.meta.source %}
    -                    <a href="{{ [repo, path, file] | join('/') }}" title="{{ file }}" class="md-source-file">
    -                      {{ file }}
    -                    </a>
    -                  {% endif %}
    -                {% endblock %}
    +                {% if page and page.meta %}
    +                  {% if page.meta.git_revision_date_localized or
    +                        page.meta.revision_date
    +                  %}
    +                    {% include "partials/source-date.html" %}
    -                {% if page and page.meta and (
    -                      page.meta.git_revision_date_localized or
    -                      page.meta.revision_date
    -                ) %}
    -                  {% set label = lang.t("source.revision.date") %}
    -                  <hr>
    -                  <div class="md-source-date">
    -                    <small>
    -                      {% if page.meta.git_revision_date_localized %}
    -                        {{ label }}: {{ page.meta.git_revision_date_localized }}
    -                      {% elif page.meta.revision_date %}
    -                        {{ label }}: {{ page.meta.revision_date }}
    -                      {% endif %}
    -                    </small>
    -                  </div>
                     {% endif %}
                   {% endblock %}
                   {% block disqus %}
    @@ -208,29 +174,35 @@
             {% include "partials/footer.html" %}
           {% endblock %}
         </div>
         {% block scripts %}
    -      <script src="{{ 'assets/javascripts/application.********.js' | url }}"></script>
    -      {% if lang.t("search.language") != "en" %}
    -        {% set languages = lang.t("search.language").split(",") %}
    -        {% if languages | length and languages[0] != "" %}
    -          {% set path = "assets/javascripts/lunr/" %}
    -          <script src="{{ (path ~ 'lunr.stemmer.support.js') | url }}"></script>
    -          {% for language in languages | map("trim") %}
    -            {% if language != "en" %}
    -              {% if language == "ja" %}
    -                <script src="{{ (path ~ 'tinyseg.js') | url }}"></script>
    -              {% endif %}
    -              {% if language in ("ar", "da", "de", "es", "fi", "fr", "hu", "it", "ja", "nl", "no", "pt", "ro", "ru", "sv", "th", "tr", "vi") %}
    -                <script src="{{ (path ~ 'lunr.' ~ language ~ '.js') | url }}"></script>
    -              {% endif %}
    -            {% endif %}
    -          {% endfor %}
    -          {% if languages | length > 1 %}
    -            <script src="{{ (path ~ 'lunr.multi.js') | url }}"></script>
    -          {% endif %}
    -        {% endif %}
    -      {% endif %}
    -      <script>app.initialize({version:"{{ mkdocs_version }}",url:{base:"{{ base_url }}"}})</script>
    +      <script src="{{ 'assets/javascripts/vendor.********.min.js' | url }}"></script>
    +      <script src="{{ 'assets/javascripts/bundle.********.min.js' | url }}"></script>
    +      {%- set translations = {} -%}
    +      {%- for key in [
    +        "clipboard.copy",
    +        "clipboard.copied",
    +        "search.config.lang",
    +        "search.config.pipeline",
    +        "search.config.separator",
    +        "search.result.placeholder",
    +        "search.result.none",
    +        "search.result.one",
    +        "search.result.other"
    +      ] -%}
    +        {%- set _ = translations.update({ key: lang.t(key) }) -%}
    +      {%- endfor -%}
    +      <script id="__lang" type="application/json">
    +        {{- translations | tojson -}}
    +      </script>
    +      {% block config %}{% endblock %}
    +      <script>
    +        app = initialize({
    +          base: "{{ base_url }}",
    +          features: {{ config.theme.features | tojson }},
    +          search: Object.assign({
    +            worker: "{{ 'assets/javascripts/worker/search.********.min.js' | url }}"
    +          }, typeof search !== "undefined" && search)
    +        })
    +      </script>
           {% for path in config["extra_javascript"] %}
             <script src="{{ path | url }}"></script>
           {% endfor %}
    ```

=== ":octicons-file-code-16: `partials/footer.html`"

    ``` diff
    @@ -5,34 +5,34 @@
         <div class="md-footer-nav">
    -      <nav class="md-footer-nav__inner md-grid">
    +      <nav class="md-footer-nav__inner md-grid" aria-label="{{ lang.t('footer.title') }}">
             {% if page.previous_page %}
    -          <a href="{{ page.previous_page.url | url }}" title="{{ page.previous_page.title | striptags }}" class="md-flex md-footer-nav__link md-footer-nav__link--prev" rel="prev">
    -            <div class="md-flex__cell md-flex__cell--shrink">
    -              <i class="md-icon md-icon--arrow-back md-footer-nav__button"></i>
    +          <a href="{{ page.previous_page.url | url }}" title="{{ page.previous_page.title | striptags }}" class="md-footer-nav__link md-footer-nav__link--prev" rel="prev">
    +            <div class="md-footer-nav__button md-icon">
    +              {% include ".icons/material/arrow-left.svg" %}
                 </div>
    -            <div class="md-flex__cell md-flex__cell--stretch md-footer-nav__title">
    -              <span class="md-flex__ellipsis">
    +            <div class="md-footer-nav__title">
    +              <div class="md-ellipsis">
                     <span class="md-footer-nav__direction">
                       {{ lang.t("footer.previous") }}
                     </span>
                     {{ page.previous_page.title }}
    -              </span>
    +              </div>
                 </div>
               </a>
             {% endif %}
             {% if page.next_page %}
    -          <a href="{{ page.next_page.url | url }}" title="{{ page.next_page.title | striptags }}" class="md-flex md-footer-nav__link md-footer-nav__link--next" rel="next">
    -            <div class="md-flex__cell md-flex__cell--stretch md-footer-nav__title">
    -              <span class="md-flex__ellipsis">
    +          <a href="{{ page.next_page.url | url }}" title="{{ page.next_page.title | striptags }}" class="md-footer-nav__link md-footer-nav__link--next" rel="next">
    +            <div class="md-footer-nav__title">
    +              <div class="md-ellipsis">
                     <span class="md-footer-nav__direction">
                       {{ lang.t("footer.next") }}
                     </span>
                     {{ page.next_page.title }}
    -              </span>
    +              </div>
                 </div>
    -            <div class="md-flex__cell md-flex__cell--shrink">
    -              <i class="md-icon md-icon--arrow-forward md-footer-nav__button"></i>
    +            <div class="md-footer-nav__button md-icon">
    +              {% include ".icons/material/arrow-right.svg" %}
                 </div>
               </a>
             {% endif %}
    ```

=== ":octicons-file-code-16: `partials/header.html`"

    ``` diff
    @@ -4,51 +4,43 @@
     <header class="md-header" data-md-component="header">
    -  <nav class="md-header-nav md-grid">
    -    <div class="md-flex">
    -      <div class="md-flex__cell md-flex__cell--shrink">
    -        <a href="{{ config.site_url | default(nav.homepage.url, true) | url }}" title="{{ config.site_name }}" aria-label="{{ config.site_name }}" class="md-header-nav__button md-logo">
    -          {% if config.theme.logo.icon %}
    -            <i class="md-icon">{{ config.theme.logo.icon }}</i>
    -          {% else %}
    -            <img alt="logo" src="{{ config.theme.logo | url }}" width="24" height="24">
    -          {% endif %}
    -        </a>
    -      </div>
    -      <div class="md-flex__cell md-flex__cell--shrink">
    -        <label class="md-icon md-icon--menu md-header-nav__button" for="__drawer"></label>
    -      </div>
    -      <div class="md-flex__cell md-flex__cell--stretch">
    -        <div class="md-flex__ellipsis md-header-nav__title" data-md-component="title">
    -          {% if config.site_name == page.title %}
    -            {{ config.site_name }}
    -          {% else %}
    -            <span class="md-header-nav__topic">
    -              {{ config.site_name }}
    -            </span>
    -            <span class="md-header-nav__topic">
    -              {% if page and page.meta and page.meta.title %}
    -                {{ page.meta.title }}
    -              {% else %}
    -                {{ page.title }}
    -              {% endif %}
    -            </span>
    -          {% endif %}
    +  <nav class="md-header-nav md-grid" aria-label="{{ lang.t('header.title') }}">
    +    <a href="{{ config.site_url | default(nav.homepage.url, true) | url }}" title="{{ config.site_name }}" class="md-header-nav__button md-logo" aria-label="{{ config.site_name }}">
    +      {% include "partials/logo.html" %}
    +    </a>
    +    <label class="md-header-nav__button md-icon" for="__drawer">
    +      {% include ".icons/material/menu" ~ ".svg" %}
    +    </label>
    +    <div class="md-header-nav__title" data-md-component="header-title">
    +      {% if config.site_name == page.title %}
    +        <div class="md-header-nav__ellipsis md-ellipsis">
    +          {{ config.site_name }}
             </div>
    -      </div>
    -      <div class="md-flex__cell md-flex__cell--shrink">
    -        {% if "search" in config["plugins"] %}
    -          <label class="md-icon md-icon--search md-header-nav__button" for="__search"></label>
    -          {% include "partials/search.html" %}
    -        {% endif %}
    -      </div>
    -      {% if config.repo_url %}
    -        <div class="md-flex__cell md-flex__cell--shrink">
    -          <div class="md-header-nav__source">
    -            {% include "partials/source.html" %}
    -          </div>
    +      {% else %}
    +        <div class="md-header-nav__ellipsis">
    +          <span class="md-header-nav__topic md-ellipsis">
    +            {{ config.site_name }}
    +          </span>
    +          <span class="md-header-nav__topic md-ellipsis">
    +            {% if page and page.meta and page.meta.title %}
    +              {{ page.meta.title }}
    +            {% else %}
    +              {{ page.title }}
    +            {% endif %}
    +          </span>
             </div>
           {% endif %}
         </div>
    +    {% if "search" in config["plugins"] %}
    +      <label class="md-header-nav__button md-icon" for="__search">
    +        {% include ".icons/material/magnify.svg" %}
    +      </label>
    +      {% include "partials/search.html" %}
    +    {% endif %}
    +    {% if config.repo_url %}
    +      <div class="md-header-nav__source">
    +        {% include "partials/source.html" %}
    +      </div>
    +    {% endif %}
       </nav>
     </header>
    ```

=== ":octicons-file-code-16: `partials/hero.html`"

    ``` diff
    @@ -4,9 +4,8 @@
    -{% set feature = config.theme.feature %}
     {% set class = "md-hero" %}
    -{% if not feature.tabs %}
    +{% if "tabs" not in config.theme.features %}
       {% set class = "md-hero md-hero--expand" %}
     {% endif %}
     <div class="{{ class }}" data-md-component="hero">
    ```

=== ":octicons-file-code-16: `partials/language.html`"

    ``` diff
    @@ -4,12 +4,4 @@
     {% import "partials/language/" + config.theme.language + ".html" as lang %}
     {% import "partials/language/en.html" as fallback %}
    -{% macro t(key) %}{{ {
    -  "direction": config.theme.direction,
    -  "search.language": (
    -    config.extra.search | default({})
    -  ).language,
    -  "search.tokenizer": (
    -    config.extra.search | default({})
    -  ).tokenizer | default("", true),
    -}[key] or lang.t(key) or fallback.t(key) }}{% endmacro %}
    +{% macro t(key) %}{{ lang.t(key) | default(fallback.t(key)) }}{% endmacro %}
    ```

=== ":octicons-file-code-16: `partials/logo.html`"

    ``` diff
    @@ -0,0 +1,9 @@
    +{#-
    +  This file was automatically generated - do not edit
    +-#}
    +{% if config.theme.logo %}
    +  <img src="{{ config.theme.logo | url }}" alt="logo">
    +{% else %}
    +  {% set icon = config.theme.icon.logo or "material/library" %}
    +  {% include ".icons/" ~ icon ~ ".svg" %}
    +{% endif %}
    ```

=== ":octicons-file-code-16: `partials/nav-item.html`"

    ``` diff
    @@ -14,9 +14,15 @@
         {% endif %}
         <label class="md-nav__link" for="{{ path }}">
           {{ nav_item.title }}
    +      <span class="md-nav__icon md-icon">
    +        {% include ".icons/material/chevron-right.svg" %}
    +      </span>
         </label>
    -    <nav class="md-nav" data-md-component="collapsible" data-md-level="{{ level }}">
    +    <nav class="md-nav" aria-label="{{ nav_item.title }}" data-md-level="{{ level }}">
           <label class="md-nav__title" for="{{ path }}">
    +        <span class="md-nav__icon md-icon">
    +          {% include ".icons/material/arrow-left.svg" %}
    +        </span>
             {{ nav_item.title }}
           </label>
           <ul class="md-nav__list" data-md-scrollfix>
    @@ -39,6 +45,9 @@
         {% if toc | first is defined %}
           <label class="md-nav__link md-nav__link--active" for="__toc">
             {{ nav_item.title }}
    +        <span class="md-nav__icon md-icon">
    +          {% include ".icons/material/table-of-contents.svg" %}
    +        </span>
           </label>
         {% endif %}
         <a href="{{ nav_item.url | url }}" title="{{ nav_item.title | striptags }}" class="md-nav__link md-nav__link--active">
    ```

=== ":octicons-file-code-16: `partials/nav.html`"

    ``` diff
    @@ -4,14 +4,10 @@
    -<nav class="md-nav md-nav--primary" data-md-level="0">
    -  <label class="md-nav__title md-nav__title--site" for="__drawer">
    -    <a href="{{ config.site_url | default(nav.homepage.url, true) | url }}" title="{{ config.site_name }}" class="md-nav__button md-logo">
    -      {% if config.theme.logo.icon %}
    -        <i class="md-icon">{{ config.theme.logo.icon }}</i>
    -      {% else %}
    -        <img alt="logo" src="{{ config.theme.logo | url }}" width="48" height="48">
    -      {% endif %}
    +<nav class="md-nav md-nav--primary" aria-label="{{ lang.t('nav.title') }}" data-md-level="0">
    +  <label class="md-nav__title" for="__drawer">
    +    <a href="{{ config.site_url | default(nav.homepage.url, true) | url }}" title="{{ config.site_name }}" class="md-nav__button md-logo" aria-label="{{ config.site_name }}">
    +      {% include "partials/logo.html" %}
         </a>
         {{ config.site_name }}
       </label>
    ```

=== ":octicons-file-code-16: `partials/search.html`"

    ``` diff
    @@ -6,15 +6,18 @@
       <label class="md-search__overlay" for="__search"></label>
       <div class="md-search__inner" role="search">
         <form class="md-search__form" name="search">
    -      <input type="text" class="md-search__input" name="query" aria-label="Search" placeholder="{{ lang.t('search.placeholder') }}" autocapitalize="off" autocorrect="off" autocomplete="off" spellcheck="false" data-md-component="query" data-md-state="active">
    +      <input type="text" class="md-search__input" name="query" aria-label="{{ lang.t('search.placeholder') }}" placeholder="{{ lang.t('search.placeholder') }}" autocapitalize="off" autocorrect="off" autocomplete="off" spellcheck="false" data-md-component="search-query" data-md-state="active">
           <label class="md-search__icon md-icon" for="__search">
    +        {% include ".icons/material/magnify.svg" %}
    +        {% include ".icons/material/arrow-left.svg" %}
           </label>
    -      <button type="reset" class="md-icon md-search__icon" data-md-component="reset" tabindex="-1">
    -        &#xE5CD;
    +      <button type="reset" class="md-search__icon md-icon" aria-label="{{ lang.t('search.reset') }}" data-md-component="search-reset" tabindex="-1">
    +        {% include ".icons/material/close.svg" %}
           </button>
         </form>
         <div class="md-search__output">
           <div class="md-search__scrollwrap" data-md-scrollfix>
    -        <div class="md-search-result" data-md-component="result">
    +        <div class="md-search-result" data-md-component="search-result">
               <div class="md-search-result__meta">
                 {{ lang.t("search.result.placeholder") }}
               </div>
    ```

=== ":octicons-file-code-16: `partials/social.html`"

    ``` diff
    @@ -4,9 +4,12 @@
     {% if config.extra.social %}
       <div class="md-footer-social">
    -    <link rel="stylesheet" href="{{ 'assets/fonts/font-awesome.css' | url }}">
         {% for social in config.extra.social %}
    -      <a href="{{ social.link }}" target="_blank" rel="noopener" title="{{ social.type }}" class="md-footer-social__link fa fa-{{ social.type }}"></a>
    +      {% set _,rest = social.link.split("//") %}
    +      {% set domain = rest.split("/")[0] %}
    +      <a href="{{ social.link }}" target="_blank" rel="noopener" title="{{ domain }}" class="md-footer-social__link">
    +        {% include ".icons/" ~ social.icon ~ ".svg" %}
    +      </a>
         {% endfor %}
       </div>
     {% endif %}
    ```

=== ":octicons-file-code-16: `partials/source-date.html`"

    ``` diff
    @@ -0,0 +1,15 @@
    +{#-
    +  This file was automatically generated - do not edit
    +-#}
    +{% import "partials/language.html" as lang with context %}
    +{% set label = lang.t("source.revision.date") %}
    +<hr>
    +<div class="md-source-date">
    +  <small>
    +    {% if page.meta.git_revision_date_localized %}
    +      {{ label }}: {{ page.meta.git_revision_date_localized }}
    +    {% elif page.meta.revision_date %}
    +      {{ label }}: {{ page.meta.revision_date }}
    +    {% endif %}
    +  </small>
    +</div>
    ```

=== ":octicons-file-code-16: `partials/source-link.html`"

    ``` diff
    @@ -0,0 +1,13 @@
    +{#-
    +  This file was automatically generated - do not edit
    +-#}
    +{% import "partials/language.html" as lang with context %}
    +{% set repo = config.repo_url %}
    +{% if repo | last == "/" %}
    +  {% set repo = repo[:-1] %}
    +{% endif %}
    +{% set path = page.meta.path | default([""]) %}
    +<a href="{{ [repo, path, page.meta.source] | join('/') }}" title="{{ file }}" class="md-content__button md-icon">
    +  {{ lang.t("meta.source") }}
    +  {% include ".icons/" ~ config.theme.icon.repo ~ ".svg" %}
    +</a>
    ```

=== ":octicons-file-code-16: `partials/source.html`"

    ``` diff
    @@ -4,24 +4,11 @@
     {% import "partials/language.html" as lang with context %}
    -{% set platform = config.extra.repo_icon or config.repo_url %}
    -{% if "github" in platform %}
    -  {% set repo_type = "github" %}
    -{% elif "gitlab" in platform %}
    -  {% set repo_type = "gitlab" %}
    -{% elif "bitbucket" in platform %}
    -  {% set repo_type = "bitbucket" %}
    -{% else %}
    -  {% set repo_type = "" %}
    -{% endif %}
    -<a href="{{ config.repo_url }}" title="{{ lang.t('source.link.title') }}" class="md-source" data-md-source="{{ repo_type }}">
    -  {% if repo_type %}
    -    <div class="md-source__icon">
    -      <svg viewBox="0 0 24 24" width="24" height="24">
    -        <use xlink:href="#__{{ repo_type }}" width="24" height="24"></use>
    -      </svg>
    -    </div>
    -  {% endif %}
    +<a href="{{ config.repo_url }}" title="{{ lang.t('source.link.title') }}" class="md-source">
    +  <div class="md-source__icon md-icon">
    +    {% set icon = config.theme.icon.repo or "fontawesome/brands/git-alt" %}
    +    {% include ".icons/" ~ icon ~ ".svg" %}
    +  </div>
       <div class="md-source__repository">
         {{ config.repo_name }}
       </div>
    ```

=== ":octicons-file-code-16: `partials/tabs-item.html`"

    ``` diff
    @@ -4,7 +4,7 @@
    -{% if nav_item.is_homepage %}
    +{% if nav_item.is_homepage or nav_item.url == "index.html" %}
       <li class="md-tabs__item">
         {% if not page.ancestors | length and nav | selectattr("url", page.url) %}
           <a href="{{ nav_item.url | url }}" class="md-tabs__link md-tabs__link--active">
    ```

=== ":octicons-file-code-16: `partials/tabs.html`"

    ``` diff
    @@ -5,7 +5,7 @@
     {% if page.ancestors | length > 0 %}
       {% set class = "md-tabs md-tabs--active" %}
     {% endif %}
    -<nav class="{{ class }}" data-md-component="tabs">
    +<nav class="{{ class }}" aria-label="{{ lang.t('tabs.title') }}" data-md-component="tabs">
       <div class="md-tabs__inner md-grid">
         <ul class="md-tabs__list">
           {% for nav_item in nav %}
    ```

=== ":octicons-file-code-16: `partials/toc-item.html`"

    ``` diff
    @@ -6,7 +6,7 @@
         {{ toc_item.title }}
       </a>
       {% if toc_item.children %}
    -    <nav class="md-nav">
    +    <nav class="md-nav" aria-label="{{ toc_item.title }}">
           <ul class="md-nav__list">
             {% for toc_item in toc_item.children %}
               {% include "partials/toc-item.html" %}
    ```

=== ":octicons-file-code-16: `partials/toc.html`"

    ``` diff
    @@ -4,35 +4,22 @@
     {% import "partials/language.html" as lang with context %}
    -<nav class="md-nav md-nav--secondary">
    +<nav class="md-nav md-nav--secondary" aria-label="{{ lang.t('toc.title') }}">
       {% endif %}
       {% if toc | first is defined %}
         <label class="md-nav__title" for="__toc">
    +      <span class="md-nav__icon md-icon">
    +        {% include ".icons/material/arrow-left.svg" %}
    +      </span>
           {{ lang.t("toc.title") }}
         </label>
         <ul class="md-nav__list" data-md-scrollfix>
           {% for toc_item in toc %}
             {% include "partials/toc-item.html" %}
           {% endfor %}
    -      {% if page.meta.source and page.meta.source | length > 0 %}
    -        <li class="md-nav__item">
    -          <a href="#__source" class="md-nav__link md-nav__link--active">
    -            {{ lang.t("meta.source") }}
    -          </a>
    -        </li>
    -      {% endif %}
    -      {% set disqus = config.extra.disqus %}
    -      {% if page and page.meta and page.meta.disqus is string %}
    -        {% set disqus = page.meta.disqus %}
    -      {% endif %}
    -      {% if not page.is_homepage and disqus %}
    -        <li class="md-nav__item">
    -          <a href="#__comments" class="md-nav__link md-nav__link--active">
    -            {{ lang.t("meta.comments") }}
    -          </a>
    -        </li>
    -      {% endif %}
         </ul>
       {% endif %}
     </nav>
    ```

## 从3.x升级到4.x

### 有什么新鲜事吗？

MkDocs 4的Material修复了中国系统上的错误布局。修复
包括将基本字体大小从`10px`强制更改为`20px`
表示需要更新的所有`rem` 值。在主题中，从`px`到`rem`
计算现在被封装在一个名为`px2rem`的新函数中，该函数是
SASS代码库。

如果你使用基于`rem` 值的自定义CSS的MkDocs材质，
请注意，这些值现在必须除以2。现在，`1.0rem`不能映射到
`10px`，但`20px`。要了解有关问题和影响的更多信息，请
请参阅发现并修复问题的#911。

### 更改 `mkdocs.yml`

没有。

### 对`*.html`文件的更改

没有。

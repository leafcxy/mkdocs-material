# 设置页脚

项目文档的页脚是添加链接的好地方
您或您的公司用作额外营销的网站或平台
渠道，例如：fontawesome品牌乳齿象：{ style="color: #5A4CE0" }或
：fontawesome brands youtube:{ style="color: #EE0F0F" }，您可以轻松访问
通过`mkdocs.yml`进行配置。

## 配置

### 导航

<!-- md:version 9.0.0 -->
<!-- md:feature -->

页脚可以包含指向当前页面上一页和下一页的链接。
如果要启用此行为，请在`mkdocs.yml`中添加以下行：

``` yaml
theme:
  features:
    - navigation.footer
```

### 社交链接

<!-- md:version 1.0.0 -->
<!-- md:default none -->

社交链接作为版权声明的一部分显示在版权声明旁边
项目文档的页脚。在`mkdocs.yml`中添加社交链接列表
与：

``` yaml
extra:
  social:
    - icon: fontawesome/brands/mastodon # (1)!
      link: https://fosstodon.org/@squidfunk
```

1.  输入几个关键字，使用我们的[图标搜索]找到完美的图标，然后
    单击短代码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="mastodon" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

每个链接都有以下属性：

<!-- md:option social.icon -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须包含指向与主题绑定的任何图标的有效路径，
    否则构建将不会成功。一些流行的选择：

    * :fontawesome-brands-github: – `fontawesome/brands/github`
    * :fontawesome-brands-gitlab: – `fontawesome/brands/gitlab`
    * :fontawesome-brands-x-twitter: – `fontawesome/brands/x-twitter`
    * :fontawesome-brands-mastodon: – `fontawesome/brands/mastodon`
      <small>automatically adds [`rel=me`][rel=me]</small>
    * :fontawesome-brands-docker: – `fontawesome/brands/docker`
    * :fontawesome-brands-facebook: – `fontawesome/brands/facebook`
    * :fontawesome-brands-instagram: – `fontawesome/brands/instagram`
    * :fontawesome-brands-linkedin: – `fontawesome/brands/linkedin`
    * :fontawesome-brands-slack: – `fontawesome/brands/slack`
    * :fontawesome-brands-discord: – `fontawesome/brands/discord`
    * :fontawesome-brands-pied-piper-alt: – `fontawesome/brands/pied-piper-alt`

<!-- md:option social.link -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须设置为包含URI的相对或绝对URL
    方案。支持所有URI方案，包括“mailto”和“bitcoin”：

    === ":fontawesome-brands-mastodon: Mastodon"

        ``` yaml
        extra:
          social:
            - icon: fontawesome/brands/mastodon
              link: https://fosstodon.org/@squidfunk
        ```

    === ":octicons-mail-16: Email"

        ``` yaml
        extra:
          social:
            - icon: fontawesome/solid/paper-plane
              link: mailto:<email-address>
        ```

<!-- md:option social.name -->

:   <!-- md:default _domain name from_ `link`_, if available_ -->
    此属性用作链接的“title”属性，可以设置为
    可辨别的名称，以提高可访问性：

    ``` yaml
    extra:
      social:
        - icon: fontawesome/brands/mastodon
          link: https://fosstodon.org/@squidfunk
          name: squidfunk on Fosstodon
    ```

  [icon search]: ../reference/icons-emojis.md#search
  [rel=me]: https://docs.joinmastodon.org/user/profile/#verification

### 版权声明

<!-- md:version 0.1.0 -->
<!-- md:default none -->

自定义版权横幅可以作为页脚的一部分呈现，即
显示在社交链接旁边。它可以被定义为“mkdocs.yml”的一部分：

``` yaml
copyright: Copyright &copy; 2016 - 2020 Martin Donath
```

### 发电机通知

<!-- md:version 7.3.0 -->
<!-- md:default `true` -->

页脚显示了一个_Made with Material for MkDocs_通知，表示如何
该网站已生成。可以通过以下选项删除通知
通过`mkdocs.yml`：

``` yaml
extra:
  generator: false
```

!!! info "请在删除发电机通知之前阅读此内容"

    页脚中微妙的__Made with Material for MkDocs__提示是
    这个项目如此受欢迎的原因，因为它告诉用户
    生成网站，帮助新用户发现此项目。之前
    删除请考虑您正在享受@squidfunk的好处
    免费工作，因为这个项目是开源的，有许可证。
    这个项目花了数千个小时，其中大部分
    没有任何经济回报。

    Thus, if you remove this notice, please consider [sponsoring][Insiders] the
    project. __Thank you__ :octicons-heart-fill-24:{ .mdx-heart .mdx-insiders }

  [Insiders]: ../insiders/index.md

## 使用

### 隐藏上一页/下一页链接

显示上一页和下一页链接的页脚导航可以隐藏
具有前体“隐藏”属性。在a的顶部添加以下行
Markdown文件：

``` yaml
---
hide:
  - footer
---

# Page title
...
```

## 自定义

### 自定义版权

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

In order to customize and override the [copyright notice], [extend the theme]
and [override the `copyright.html` partial][overriding partials], which normally
includes the `copyright` property set in `mkdocs.yml`.

  [copyright notice]: #copyright-notice
  [generator notice]: #generator-notice
  [extend the theme]: ../customization.md#extending-the-theme
  [overriding partials]: ../customization.md#overriding-partials

# 设置页脚

项目文档的页脚是添加链接到您或您公司网站或平台（如社交媒体）的好地方，可作为额外的宣传渠道。这些链接可以通过 `mkdocs.yml` 轻松配置。

## 配置

### 导航

<!-- md:version 9.0.0 -->
<!-- md:feature -->

页脚可以包含指向当前页面上一页和下一页的链接。要启用此功能，在 `mkdocs.yml` 中添加如下内容：

``` yaml
theme:
  features:
    - navigation.footer
```

### 社交链接

<!-- md:version 1.0.0 -->
<!-- md:default none -->

社交链接会显示在页脚的版权声明旁边。在 `mkdocs.yml` 中添加社交链接列表：

``` yaml
extra:
  social:
    - icon: fontawesome/brands/mastodon # (1)!
      link: https://fosstodon.org/@squidfunk
```

1.  输入关键字，使用我们的[图标搜索]找到合适的图标，然后点击短代码复制：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="搜索图标" data-mdx-component="iconsearch-query" value="mastodon" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

每个链接有以下属性：

<!-- md:option social.icon -->

:   <!-- md:default none --> <!-- md:flag required -->
    必须包含指向主题内图标的有效路径，否则构建不会成功。常见选择：

    * :fontawesome-brands-github: – `fontawesome/brands/github`
    * :fontawesome-brands-gitlab: – `fontawesome/brands/gitlab`
    * :fontawesome-brands-x-twitter: – `fontawesome/brands/x-twitter`
    * :fontawesome-brands-mastodon: – `fontawesome/brands/mastodon` <small>自动添加 [`rel=me`][rel=me]</small>
    * :fontawesome-brands-docker: – `fontawesome/brands/docker`
    * :fontawesome-brands-facebook: – `fontawesome/brands/facebook`
    * :fontawesome-brands-instagram: – `fontawesome/brands/instagram`
    * :fontawesome-brands-linkedin: – `fontawesome/brands/linkedin`
    * :fontawesome-brands-slack: – `fontawesome/brands/slack`
    * :fontawesome-brands-discord: – `fontawesome/brands/discord`
    * :fontawesome-brands-pied-piper-alt: – `fontawesome/brands/pied-piper-alt`

<!-- md:option social.link -->

:   <!-- md:default none --> <!-- md:flag required -->
    必须设置为包含 URI 的相对或绝对 URL，支持所有 URI 协议，包括"mailto"和"bitcoin"：

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
    用作链接的"title"属性，可设置为可辨别的名称以提升可访问性：

    ``` yaml
    extra:
      social:
        - icon: fontawesome/brands/mastodon
          link: https://fosstodon.org/@squidfunk
          name: squidfunk on Fosstodon
    ```

  [图标搜索]: ../reference/icons-emojis.md#search
  [rel=me]: https://docs.joinmastodon.org/user/profile/#verification

### 版权声明

<!-- md:version 0.1.0 -->
<!-- md:default none -->

自定义版权横幅可作为页脚的一部分显示，在社交链接旁边。可在 `mkdocs.yml` 中设置：

``` yaml
copyright: Copyright &copy; 2016 - 2020 Martin Donath
```

### 生成器提示

<!-- md:version 7.3.0 -->
<!-- md:default `true` -->

页脚会显示 _Made with Material for MkDocs_ 提示，表明网站由本项目生成。可通过如下方式移除：

``` yaml
extra:
  generator: false
```

!!! info "请在移除生成器提示前阅读"

    页脚中的 __Made with Material for MkDocs__ 提示是本项目受欢迎的重要原因之一，因为它帮助新用户发现本项目。移除前请考虑您正在享受 @squidfunk 免费开源工作的成果。该项目耗费了数千小时，大部分没有经济回报。

    因此，如果您移除了该提示，请考虑[赞助][Insiders]本项目。__感谢支持__ :octicons-heart-fill-24:{ .mdx-heart .mdx-insiders }

  [Insiders]: ../insiders/index.md

## 使用

### 隐藏上一页/下一页链接

页脚导航中的上一页/下一页链接可通过 front matter 的 `hide` 属性隐藏。在 Markdown 文件顶部添加如下内容：

``` yaml
---
hide:
  - footer
---

# 页面标题
...
```

## 自定义

### 自定义版权

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如需自定义和覆盖[版权声明]，请[扩展主题]并[覆盖 `copyright.html` partial][覆盖 partials]，该 partial 通常包含 `mkdocs.yml` 中设置的 copyright 属性。

  [版权声明]: #copyright-notice
  [生成器提示]: #generator-notice
  [扩展主题]: ../customization.md#extending-the-theme
  [覆盖 partials]: ../customization.md#overriding-partials

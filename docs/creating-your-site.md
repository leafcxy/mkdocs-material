# 创建您的网站

[installed] Material for MkDocs后，您可以引导您的项目
使用`mkdocs`可执行文件的文档。转到所需的目录
您的项目将被定位并输入：

```
mkdocs new .
```

或者，如果你在Docker中运行Material for MkDocs，请使用：

=== "Unix, Powershell"

    ```
    docker run --rm -it -v ${PWD}:/docs squidfunk/mkdocs-material new .
    ```

=== "Windows (cmd)"

    ```
    docker run --rm -it -v "%cd%":/docs squidfunk/mkdocs-material new .
    ```

这将创建以下结构：

``` { .sh .no-copy }
.
├─ docs/
│  └─ index.md
└─ mkdocs.yml
```

  [installed]: getting-started.md

## 配置

### 最小配置

只需设置`site_name`并将以下行添加到`mkdocs.yml`中即可启用主题：

``` yaml hl_lines="2-5"
site_name: My site
site_url: https://mydomain.org/mysite
theme:
  name: material
```

`site_url`设置很重要，原因有很多。
默认情况下，MkDocs将假设您的网站托管在
您的域名。例如，当[publishing to GitHub pages]时，情况并非如此
页面-除非您使用自定义域。另一个原因是，一些
插件需要设置`site_url`，所以你应该始终这样做。

  [publishing to GitHub pages]: publishing-your-site.md#github-pages
  [installation methods]: getting-started.md#installation

???+ tip "建议: [configuration validation and auto-complete]"

    为了最大限度地减少摩擦并提高生产率，Material for MkDocs
    为`mkdocs.yml`提供了自己的[schema.json][^1]。如果你的编辑器支持
    YAML模式验证，强烈建议进行设置：

    === "Visual Studio Code"

        1.  安装[`vscode-yaml`][vscode-yaml]以获得yaml语言支持。
        2.  在用户的`yaml.schemas`键下添加模式，或
            工作区[`settings.json`][settings.json]：

            ``` json
            {
              "yaml.schemas": {
                "https://squidfunk.github.io/mkdocs-material/schema.json": "mkdocs.yml"
              },
              "yaml.customTags": [ // (1)!
                "!ENV scalar",
                "!ENV sequence",
                "!relative scalar",
                "tag:yaml.org,2002:python/name:material.extensions.emoji.to_svg",
                "tag:yaml.org,2002:python/name:material.extensions.emoji.twemoji",
                "tag:yaml.org,2002:python/name:pymdownx.superfences.fence_code_format",
                "tag:yaml.org,2002:python/object/apply:pymdownx.slugs.slugify mapping"
              ]
            }
            ```

            1.  如果您计划使用[图标和表情符号]，则此设置是必要的，
                或者Visual Studio代码将在某些行上显示错误。

    === "Other"

        1.  确保您选择的编辑器支持YAML模式验证。
        2.  在`mkdocs.yml`的顶部添加以下行：

            ``` yaml
            # yaml-language-server: $schema=https://squidfunk.github.io/mkdocs-material/schema.json
            ```

  [^1]:
    如果你是MkDocs插件或Markdown扩展的作者，并且你的项目
    与MkDocs的Material合作，我们诚挚地邀请您贡献
    作为GitHub上pull请求的一部分，您的[extension]或[plugin]的模式。
    如果您已经定义了架构，或者希望将架构自托管到
    减少重复，您可以通过[$ref]添加它。

  [configuration validation and auto-complete]: https://x.com/squidfunk/status/1487746003692400642
  [schema.json]: schema.json
  [vscode-yaml]: https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml
  [settings.json]: https://code.visualstudio.com/docs/getstarted/settings
  [extension]: https://github.com/squidfunk/mkdocs-material/tree/master/docs/schema/extensions
  [plugin]: https://github.com/squidfunk/mkdocs-material/tree/master/docs/schema/plugins
  [$ref]: https://json-schema.org/understanding-json-schema/structuring.html#ref
  [icons and emojis]: reference/icons-emojis.md

### 高级配置

Material for MkDocs有许多配置选项。设置部分
详细解释了如何配置和自定义颜色、字体、图标
还有更多：

<div class="mdx-columns" markdown>

- [Changing the colors]
- [Changing the fonts]
- [Changing the language]
- [Changing the logo and icons]
- [Ensuring data privacy]
- [Setting up navigation]
- [Setting up site search]
- [Setting up site analytics]
- [Setting up social cards]
- [Setting up a blog]
- [Setting up tags]
- [Setting up versioning]
- [Setting up the header]
- [Setting up the footer]
- [Adding a git repository]
- [Adding a comment system]
- [Building an optimized site]
- [Building for offline usage]

</div>

此外，请参阅本机支持的[Markdown extensions]列表
与Material for MkDocs集成，实现了前所未有的低成本
技术写作经验。

  [Changing the colors]: setup/changing-the-colors.md
  [Changing the fonts]: setup/changing-the-fonts.md
  [Changing the language]: setup/changing-the-language.md
  [Changing the logo and icons]: setup/changing-the-logo-and-icons.md
  [Ensuring data privacy]: setup/ensuring-data-privacy.md
  [Setting up navigation]: setup/setting-up-navigation.md
  [Setting up site search]: setup/setting-up-site-search.md
  [Setting up site analytics]: setup/setting-up-site-analytics.md
  [Setting up social cards]: setup/setting-up-social-cards.md
  [Setting up a blog]: setup/setting-up-a-blog.md
  [Setting up tags]: setup/setting-up-tags.md
  [Setting up versioning]: setup/setting-up-versioning.md
  [Setting up the header]: setup/setting-up-the-header.md
  [Setting up the footer]: setup/setting-up-the-footer.md
  [Adding a git repository]: setup/adding-a-git-repository.md
  [Adding a comment system]: setup/adding-a-comment-system.md
  [Building for offline usage]: setup/building-for-offline-usage.md
  [Building an optimized site]: setup/building-an-optimized-site.md
  [Markdown extensions]: setup/extensions/index.md

## 模板

如果你想启动一个新项目，你可以使用我们不断增长的
模板集合：

<div class="grid cards" markdown>

-   :octicons-repo-template-24: &nbsp; __[Blog][blog-template]__

    ---

    Create a blog

-   :octicons-repo-template-24: &nbsp; __[Social cards][social-cards-template]__

    ---

    Create documentation with social cards

</div>

[blog-template]: https://github.com/mkdocs-material/create-blog
[social-cards-template]: https://github.com/mkdocs-material/create-social-cards

## 写作时预览

MkDocs包括一个实时预览服务器，因此您可以在使用时预览您的更改
写你的文件。服务器将在以下情况下自动重建站点
储蓄。从以下内容开始：

``` sh
mkdocs serve # (1)!
```

1.  如果您有一个大型文档项目，可能需要几分钟的时间，直到
    MkDocs已重建所有页面供您预览。如果你只感兴趣
    在当前页面中，[`--dirtyreload`][--dirtyleroad]标志将使
    重建速度更快：

    ```
    mkdocs serve --dirtyreload
    ```

如果你在Docker中运行Material for MkDocs，请使用：

=== "Unix, Powershell"

    ```
    docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material
    ```

=== "Windows"

    ```
    docker run --rm -it -p 8000:8000 -v "%cd%":/docs squidfunk/mkdocs-material
    ```

将浏览器指向[localhost:8000][live preview]，您应该看到：

[![Creating your site]][Creating your site]

  [--dirtyreload]: https://www.mkdocs.org/about/release-notes/#support-for-dirty-builds-990
  [live preview]: http://localhost:8000
  [Creating your site]: assets/screenshots/creating-your-site.png

## 构建您的网站

编辑完成后，您可以从Markdown构建一个静态网站
文件包含：

```
mkdocs build
```

如果你在Docker中运行Material for MkDocs，请使用：

=== "Unix, Powershell"

    ```
    docker run --rm -it -v ${PWD}:/docs squidfunk/mkdocs-material build
    ```

=== "Windows"

    ```
    docker run --rm -it -v "%cd%":/docs squidfunk/mkdocs-material build
    ```

此目录的内容构成了您的项目文档。没有
需要操作数据库或服务器，因为它是完全独立的。
该网站可以托管在[GitHub Pages]、[GitLab Pages]上，这是您选择的CDN
或您的私人网络空间。

  [GitHub Pages]: publishing-your-site.md#github-pages
  [GitLab pages]: publishing-your-site.md#gitlab-pages

如果您打算将文档作为一组文件分发给
从本地文件系统而不是web服务器读取（例如在
`.zip`文件），请阅读以下注意事项[building for offline
usage].

  [building for offline usage]: setup/building-for-offline-usage.md

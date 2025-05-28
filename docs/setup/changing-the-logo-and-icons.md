# 更改徽标和图标

安装MkDocs材料时，您可以立即访问8000多个
icons _可用于定制主题的特定部分和/或
在Markdown中编写文档时。不够？您还可以添加
[附加图标]只需最小的努力。

  [additional icons]: #additional-icons

## 配置

### 标志

<!-- md:version 0.1.0 -->
<!-- md:default `material/library` -->

徽标可以更改为用户提供的图像（任何类型，包括“*.png”和
`*.svg），或与主题捆绑在一起的任何图标。
将以下行添加到`mkdocs.yml`中：

=== ":octicons-image-16: Image"

    ``` yaml
    theme:
      logo: assets/logo.png
    ```

=== ":octicons-package-16: Icon, bundled"

    ``` yaml
    theme:
      icon:
        logo: material/library # (1)!
    ```

    1.  Enter a few keywords to find the perfect icon using our [icon search] and
        click on the shortcode to copy it to your clipboard:

        <div class="mdx-iconsearch" data-mdx-component="iconsearch">
          <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="material library" />
          <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
            <div class="mdx-iconsearch-result__meta"></div>
            <ol class="mdx-iconsearch-result__list"></ol>
          </div>
        </div>

  [icon search]: ../reference/icons-emojis.md#search

通常，标题和侧边栏中的徽标链接到
文档，与“site_url”相同。此行为可以更改
具有以下配置：

``` yaml
extra:
  homepage: https://example.com
```

### 图标

<!-- md:version 0.1.0 -->
<!-- md:default [`assets/images/favicon.png`][Favicon default] -->

favicon可以更改为指向用户提供的图像的路径
必须位于“文档”文件夹中。将以下行添加到`mkdocs.yml`中：

``` yaml
theme:
  favicon: images/favicon.png
```

  [Favicon default]: https://github.com/squidfunk/mkdocs-material/blob/master/material/templates/assets/images/favicon.png

### 网站图标

[:octicons-tag-24: 9.2.0][Site icon support]

您在网站上看到的大多数图标，如导航图标，也可以更改。例如，
要更改页脚中的导航箭头，请在`mkdocs.yml`中添加以下行：

```yaml
theme:
  icon:
    previous: fontawesome/solid/angle-left
    next: fontawesome/solid/angle-right
```

以下是主题使用的可自定义图标的完整列表：

| Icon name    | Purpose                                                                       |
|:-------------|:------------------------------------------------------------------------------|
| `logo`       | See [Logo](#logo)                                                             |
| `menu`       | Open drawer                                                                   |
| `alternate`  | Change language                                                               |
| `search`     | Search icon                                                                   |
| `share`      | Share search                                                                  |
| `close`      | Reset search, dismiss announcements                                           |
| `top`        | Back-to-top button                                                            |
| `edit`       | Edit current page                                                             |
| `view`       | View page source                                                              |
| `repo`       | Repository icon                                                               |
| `admonition` | See [Admonition icons](../reference/admonitions.md#admonition-icons)          |
| `tag`        | See [Tag icons and identifiers](setting-up-tags.md#tag-icons-and-identifiers) |
| `previous`   | Previous page in footer, hide search on mobile                                |
| `next`       | Next page in footer                                                           |

  [Site icon support]: https://github.com/squidfunk/mkdocs-material/releases/tag/9.2.0

## 自定义

### 其他图标

为了使用自定义图标，[扩展主题]并创建一个名为的新文件夹
`要用于覆盖的[custom_dir][custom_dir]中的.icons。
接下来，将您的`*.svg`图标添加到`.icons`文件夹的子文件夹中。比如说
您下载并解压缩了[Bootstrap]图标集，并希望将其添加到
您的项目文档。项目的结构应该如下：

``` { .sh .no-copy }
.
├─ overrides/
│  └─ .icons/
│     └─ bootstrap/
│        └─ *.svg
└─ mkdocs.yml
```

然后，在`mkdocs.yml`中添加以下行：

``` yaml
markdown_extensions:
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
      options:
        custom_icons:
          - overrides/.icons
```

现在，您可以在任何地方使用所有：fontawesome brands bootstrap：bootstrap图标
Markdown文件以及任何地方的图标都可以在`mkdocs.yml`中使用。
但是，请注意，语法略有不同：

- __在configuration__中使用图标：采用`*.svg`图标文件的路径
  从“.icons”文件夹开始，删除文件扩展名，例如for
  `.icons/bootstrap/信封纸.svg，使用：

    ``` yaml
    theme:
      icon:
        logo: bootstrap/envelope-paper
    ```

- __在Markdown文件中使用图标__：除了从
  `如上所述，将.icons文件夹中的所有“/”替换为“-”，并将图标括起来
  用两个冒号表示的短代码：

    ```
    :bootstrap-envelope-paper:
    ```

有关图标使用的更多说明，请参阅[图标参考]。

  [extend the theme]: ../customization.md#extending-the-theme
  [custom_dir]: https://www.mkdocs.org/user-guide/configuration/#custom_dir
  [Bootstrap]: https://icons.getbootstrap.com/
  [icon reference]: ../reference/icons-emojis.md#using-icons

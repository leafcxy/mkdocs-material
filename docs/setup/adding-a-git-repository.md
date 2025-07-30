# 添加git存储库

如果您的文档与源代码有关，MkDocs材料提供
作为项目存储库的一部分显示信息的能力
静态站点，包括星和叉。此外
可以显示[上次更新和创建日期]以及[贡献者]。

## 配置

### 存储库

`version 0.1.0`
`default none`

为了在您的项目中显示指向项目存储库的链接
documentation，将`mkdocs.yml`中的[`repo_url`][repo_url]设置为以下内容的公共url
您的存储库，例如：

``` yaml
repo_url: https://github.com/squidfunk/mkdocs-material
```

指向存储库的链接将显示在big上的搜索栏旁边
屏幕，并在较小屏幕尺寸上作为主导航抽屉的一部分。

此外，对于托管在[GitHub]或[GitLab]上的公共存储库
最新发布标签[^1]，以及星和叉的数量
自动请求和呈现。

  [^1]:
    遗憾的是，GitHub只提供了一个API端点来获取[最新
    release]-不是最新标签。因此，请确保[创建一个版本]（而不是
    预发布），用于在编号旁边显示您要显示的最新标签
    星星和叉子。对于GitLab，虽然可以获得[标签列表
    按更新时间排序]，则使用[等效API端点]。所以，一定要
    您还可以[为GitLab存储库创建一个版本]。

  [repo_url]: https://www.mkdocs.org/user-guide/configuration/#repo_url
  [latest release]: https://docs.github.com/en/rest/reference/releases#get-the-latest-release
  [create a release]: https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository#creating-a-release
  [list of tags sorted by update time]: https://docs.gitlab.com/ee/api/tags.html#list-project-repository-tags
  [equivalent API endpoint]: https://docs.gitlab.com/ee/api/releases/#get-the-latest-release
  [create a release for GitLab repositories]: https://docs.gitlab.com/ee/user/project/releases/#create-a-release

#### 存储库名称

`version 0.1.0`
`default _automatically set to_ _GitHub_, _GitLab_ _or_ _Bitbucket_`

MkDocs将通过检查URL来推断源提供者，并尝试设置
_存储库名称_自动。如果要自定义名称，请设置
在`mkdocs.yml`中的[`repo_name`][repo_name]：

``` yaml
repo_name: squidfunk/mkdocs-material
```

  [repo_name]: https://www.mkdocs.org/user-guide/configuration/#repo_name

#### 存储库图标

`version 5.0.0`
`default computed`

虽然默认存储库图标是通用的git图标，但可以将其设置为
通过引用中的有效图标路径与主题捆绑在一起的任何图标
`mkdocs.yml`：

``` yaml
theme:
  icon:
    repo: fontawesome/brands/git-alt # (1)!
```

1.  输入几个关键字，使用我们的[图标搜索]找到完美的图标，然后
    单击短代码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="git" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

一些流行的选择：

- :fontawesome-brands-git: – `fontawesome/brands/git`
- :fontawesome-brands-git-alt: – `fontawesome/brands/git-alt`
- :fontawesome-brands-github: – `fontawesome/brands/github`
- :fontawesome-brands-github-alt: – `fontawesome/brands/github-alt`
- :fontawesome-brands-gitlab: – `fontawesome/brands/gitlab`
- :fontawesome-brands-gitkraken: – `fontawesome/brands/gitkraken`
- :fontawesome-brands-bitbucket: – `fontawesome/brands/bitbucket`
- :fontawesome-solid-trash: – `fontawesome/solid/trash`

  [icon search]: ../reference/icons-emojis.md#_2

#### 代码操作

`version 9.0.0`
`feature`

如果[存储库URL]指向有效的[GitHub]、[GitLab]或[Bitbucket]
存储库中，[MkDocs]提供了一个名为[`edit_uri`][edit_uri]的设置
解析到承载文档的子文件夹。

如果您的默认分支名为“main”，请将设置更改为：

``` yaml
edit_uri: edit/main/docs/
```

在确保“edit_uri”配置正确后，代码按钮
可以添加动作。支持两种类型的代码操作：“编辑”和“查看”`
（仅限GitHub）：

=== ":material-file-edit-outline: Edit this page"

    ``` yaml
    theme:
      features:
        - content.action.edit
    ```

=== ":material-file-eye-outline: View source of this page"

    ``` yaml
    theme:
      features:
        - content.action.view
    ```

编辑和查看按钮的图标可以用以下行更改：

``` yaml
theme:
  icon:
    edit: material/pencil # (1)!
    view: material/eye
```

1.  输入几个关键字，使用我们的[图标搜索]找到完美的图标，然后
    单击短代码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="material pencil" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

  [repository URL]: #repository
  [GitHub]: https://github.com/
  [GitLab]: https://about.gitlab.com/
  [Bitbucket]: https://bitbucket.org/
  [MkDocs]: https://www.mkdocs.org
  [edit_uri]: https://www.mkdocs.org/user-guide/configuration/#edit_uri

### 修订

以下插件与Material for MkDocs完全集成，允许
用于显示文档的[上次更新和创建日期]，以及
所有相关[贡献者]或[作者]的链接。

  [date of last update and creation]: #document-dates
  [contributors]: 
  [authors]: #document-authors

#### 文件日期

`version 4.6.0`
`plugin [git-revision-date-localized]`

[git修订日期本地化]插件增加了对添加日期的支持
最后更新和创建每页底部的文档。安装它
使用`pip `：

```
pip install mkdocs-git-revision-date-localized-plugin
```

然后，在`mkdocs.yml`中添加以下行：

``` yaml
plugins:
  - git-revision-date-localized:
      enable_creation_date: true
```

支持以下配置选项：

`option git-revision-date-localized.enabled`

:   `default _true_` 此选项指定是否
    在构建项目时启用该插件。如果你想切换
    关闭插件，例如对于本地构建，使用[环境变量]：

    ``` yaml
    plugins:
      - git-revision-date-localized:
          enabled: !ENV [CI, false]
    ```

`option git-revision-date-localized.type`

:   `default _date_` 日期格式为
    显示。有效值为“date”、“datetime”、“iso_date”、“iso _datetime”`
    以及“timeago”：

    ``` yaml
    plugins:
      - git-revision-date-localized:
          type: date
    ```

`option git-revision-date-localized.enable_creation_date`

:   `default _false_` 启用显示
    与上次更新页面旁边的页面关联的文件的创建日期
    页面底部的日期：

    ``` yaml
    plugins:
      - git-revision-date-localized:
          enable_creation_date: true
    ```

    !!! note "使用构建环境时"

        如果您通过CI系统进行部署，可能需要调整您的
        获取代码时的CI设置。有关更多信息，请参见
        [git修订日期本地化]。

`option git-revision-date-localized.fallback_to_build_date`

:   `default _false_` 允许回退到
    执行mkdocs-build的时间。在以下情况下可以用作后备
    构建是在git存储库之外执行的：

    ``` yaml
    plugins:
      - git-revision-date-localized:
          fallback_to_build_date: true
    ```

此扩展的其他配置选项不受官方支持
MkDocs的材料，这就是为什么它们可能会产生意想不到的结果。使用
他们的风险由你自己承担。

  [git-revision-date-localized]: https://github.com/timvink/mkdocs-git-revision-date-localized-plugin

#### 文档贡献者

`version 9.5.0`
`plugin [git-committers]`
`flag experimental`

[git committers][^2]插件呈现所有贡献者的GitHub头像，
链接到每个页面底部的GitHub配置文件。一如既往，它可以
使用`pip `进行安装：

  [^2]:
    我们目前建议使用[git committers]插件的一个分支，因为它
    包含许多尚未合并回的改进
    原始插件。更多信息请参见byrnesee/mkdocs git committers插件#12
    信息。

```
pip install mkdocs-git-committers-plugin-2
```

然后，在`mkdocs.yml`中添加以下行：

``` yaml
plugins:
  - git-committers:
      repository: squidfunk/mkdocs-material
      branch: main
```

支持以下配置选项：

`option git-committers.enabled`

:   `default _true_` 此选项指定是否
    在构建项目时启用该插件。如果你想切换
    关闭插件，例如对于本地构建，使用[环境变量]：

    ``` yaml
    plugins:
      - git-committers:
          enabled: !ENV [CI, false]
    ```

`option git-committers.repository`

:   `default none` `flag required`
    此属性必须设置为包含您的存储库的slug
    文档。slug必须遵循“<username>/<repository>”模式：

    ``` yaml
    plugins:
      - git-committers:
          repository: squidfunk/mkdocs-material
    ```

`option git-committers.branch`

:   `default _master_` 此属性应设置为
    从中检索贡献者的存储库分支。要使用“main”分支：

    ``` yaml
    plugins:
      - git-committers:
          branch: main
    ```

此扩展的其他配置选项不受官方支持
MkDocs的材料，这就是为什么它们可能会产生意想不到的结果。使用
他们的风险由你自己承担。

  [Insiders]: ../insiders/index.md
  [git-committers]: https://github.com/ojacques/mkdocs-git-committers-plugin-2
  [environment variable]: https://www.mkdocs.org/user-guide/configuration/#environment-variables
  [rate limits]: https://docs.github.com/en/rest/overview/resources-in-the-rest-api#rate-limiting

#### 文档作者

`version 9.5.0`
`plugin [git-authors]`
`flag experimental`

[git authors]插件是轻量级的替代品
[git committers]插件，从git中提取文档的作者以显示
它们位于每页的底部。

MkDocs的材料为[git作者]提供了深度集成。这意味着
[自定义覆盖](https://timvink.github.io/mkdocs-git-authors-plugin/usage.html#mkdocs-材料主题）
并且添加了额外的样式（如漂亮的图标）。
只需使用`pip `进行安装：

```
pip install mkdocs-git-authors-plugin
```

然后，在`mkdocs.yml`中添加以下行：

``` yaml
plugins:
  - git-authors
```

  [git-authors]: https://github.com/timvink/mkdocs-git-authors-plugin/

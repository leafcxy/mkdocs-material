---
title: Getting started with Insiders
---

# 开始与Insiders合作

MkDocs Insiders的材料是材料的兼容直接替代品
对于MkDocs，可以使用[`pip`][pip]进行类似的安装，
〔docker〕〔docker〕或〔git〕〔git〕。请注意，为了访问内部人员
在GitHub上，你需要[成为@squidfunk的合格赞助商]。

  [pip]: #with-pip
  [docker]: #with-docker
  [git]: #with-git
  [become an eligible sponsor]: how-to-sponsor.md

## 必要条件

在您被添加到合作者列表并接受后
存储库邀请，下一步是为创建一个[个人访问令牌]
您的GitHub帐户，以便以编程方式访问Insiders存储库
（来自命令行或GitHub Actions工作流）：

1.  Go to https://github.com/settings/tokens
2.  Click on [Generate a new token]
3.  Enter a name and select the [`repo`][scopes] scope
4.  Generate the token and store it in a safe place

  [personal access token]: https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token
  [Generate a new token]: https://github.com/settings/tokens/new
  [scopes]: https://docs.github.com/en/developers/apps/scopes-for-oauth-apps#available-scopes

以下一些说明要求“GH_TOKEN”环境
变量设置为您的个人访问令牌的值
在前面的步骤中生成的。请注意，个人访问令牌
必须始终保密，因为它允许所有者访问
您的私人存储库。

## 安装

### 使用pip

MkDocs Insider的材料可以用pip安装。你会
通常希望安装最新版本，但也可以安装
特定的旧版本，甚至最新的开发版本。
确保按照上述指示设置了“GH_TOKEN”变量。

=== "Specific release"

    从[标签列表]中为Insiders选择相应的标签
    存储库。在下面的`pip `命令中，替换
    用您想要的URL结尾。

    ``` sh
    pip install git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git@9.4.2-insiders-4.42.0
    ```

=== "Latest"

    ``` sh
    pip install git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git
    ```

[list of tags]: https://github.com/squidfunk/mkdocs-material-insiders/tags

### 使用docker

如果你想在Docker中为MkDocs Insider使用Material
需要额外的步骤。虽然我们无法提供托管的Docker镜像
对于内部人员[^2]，[GitHub容器注册表]允许简单和
舒适的自托管：

1.  [Fork the Insiders repository]
2.  Enable [GitHub Actions] on your fork[^3]
3.  Create a new personal access token[^4]
    1.  Go to https://github.com/settings/tokens
    2.  Click on [Generate a new token]
    3.  Enter a name and select the [`write:packages`][scopes] scope
    4.  Generate the token and store it in a safe place
4.  Add a [GitHub Actions secret] on your fork
    1.  Set the name to `GHCR_TOKEN`
    2.  Set the value to the personal access token created in the previous step
5.  [Create a new release] to build and publish the Docker image
6.  Install [Pull App] on your fork to stay in-sync with upstream

当有新标记时，[`build`][build]工作流会自动运行
（release）已创建。当新的Insiders版本在上游发布时
在仓库中，[Pull App]将创建一个包含更改的Pull请求
拉入新标签，该标签由[`build][build]工作流获取
自动构建Docker镜像并将其发布到您的私有
注册表。

现在，您应该能够从私有注册表中提取Docker映像：

```
docker login -u ${GH_USERNAME} -p ${GHCR_TOKEN} ghcr.io
docker pull ghcr.io/${GH_USERNAME}/mkdocs-material-insiders
```

如果您希望在内部人员容器映像中添加其他插件，请按照以下步骤操作
在[入门指南]中概述（../geting-Started.md#with docker）。

  [^2]:
    早些时候，Insiders提供了一个专门的Docker镜像，可供
    所有赞助商。2021年3月21日，该图像因以下原因被弃用
    在#2442中进行了概述和讨论。它于2021年6月1日被删除。

  [^3]:
    分叉存储库时，GitHub将禁用所有工作流。虽然这个
    是一个合理的默认设置，您需要启用GitHub Actions
    能够在上自动构建和发布Docker镜像
    [GitHub容器注册表]。

  [^4]:
    虽然你可以将“write:packages”范围添加到个人访问中
    创建令牌以访问Insiders存储库，创建令牌更安全
    专用令牌，您将仅用于发布Docker映像。

### 使用git

当然，您可以直接从“git”使用MkDocs Insider的材料：

```
git clone git@github.com:squidfunk/mkdocs-material-insiders.git mkdocs-material
```

主题将位于“mkdocs material/material”文件夹中。克隆时
从`git `开始，必须安装主题，这样MkDocs才能找到内置的
插件：

```
pip install -e mkdocs-material
```

  [GitHub Container Registry]: https://docs.github.com/en/packages/guides/about-github-container-registry
  [Fork the Insiders repository]: https://github.com/squidfunk/mkdocs-material-insiders/fork
  [GitHub Actions]: https://docs.github.com/en/github/administering-a-repository/disabling-or-limiting-github-actions-for-a-repository
  [packages scope]: https://docs.github.com/en/developers/apps/scopes-for-oauth-apps#available-scopes
  [GitHub Actions secret]: https://docs.github.com/en/actions/reference/encrypted-secrets#creating-encrypted-secrets-for-a-repository
  [Create a new release]: https://docs.github.com/en/github/administering-a-repository/managing-releases-in-a-repository#creating-a-release
  [Pull App]: https://github.com/apps/pull
  [build]: https://github.com/squidfunk/mkdocs-material-insiders/blob/master/.github/workflows/build.yml

## 内置插件

当你使用仅通过Insiders提供的内置插件时，
外部贡献者将无法在他们的基础上构建您的文档项目
本地机器。这就是我们开发[内置组插件]的原因
允许有条件地加载插件：

``` yaml
plugins:
  - search
  - social

  # CI=true mkdocs build
  - group:
      enabled: !ENV CI
      plugins:
        - git-revision-date-localized
        - git-committers

  # INSIDERS=true mkdocs build
  - group:
      enabled: !ENV INSIDERS
      plugins:
        - optimize
        - privacy
```

当然，您也可以通过以下方式启用这两个组：

``` shell
CI=true INSIDERS=true mkdocs build
```

  [built-in group plugin]: ../plugins/group.md
  [configuration inheritance]: https://www.mkdocs.org/user-guide/configuration/#configuration-inheritance

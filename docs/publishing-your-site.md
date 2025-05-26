# 发布您的网站

在`git`存储库中托管项目文档的好处是
在推送新更改时自动部署它的能力。MkDocs
这让事情变得简单得可笑。

## GitHub Pages

如果你已经在GitHub上托管你的代码，那么[GitHub Pages]肯定是
发布项目文档的最便捷方式。它是免费的
充电和设置非常容易。

  [GitHub Pages]: https://pages.github.com/

### with GitHub Actions

使用[GitHub Actions]，您可以自动部署项目
文档。在存储库的根目录下，创建一个新的GitHub Actions
工作流，例如`.github/workflows/ci.yml`，并复制粘贴以下内容
内容：

=== "Material for MkDocs"

    ``` yaml
    name: ci # (1)!
    on:
      push:
        branches:
          - master # (2)!
          - main
    permissions:
      contents: write
    jobs:
      deploy:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v4
          - name: Configure Git Credentials
            run: |
              git config user.name github-actions[bot]
              git config user.email 41898282+github-actions[bot]@users.noreply.github.com
          - uses: actions/setup-python@v5
            with:
              python-version: 3.x
          - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV # (3)!
          - uses: actions/cache@v4
            with:
              key: mkdocs-material-${{ env.cache_id }}
              path: .cache # (4)!
              restore-keys: |
                mkdocs-material-
          - run: pip install mkdocs-material # (5)!
          - run: mkdocs gh-deploy --force
    ```

    1.  你可以根据自己的喜好更改名称。

    2.  在某个时候，GitHub将`master`重命名为`main`。如果您的默认分支
        如果名为`master`，则可以安全地删除`main`，反之亦然。

    3.  存储`cache_id`环境变量，以便以后在缓存期间访问它
        创建`key`。该名称区分大小写，因此请确保将其与`${{ env.cache_id }}`对齐。

        - `--utc`选项确保每个工作流运行器使用相同的时区。
        - `%V`格式确保每周进行一次缓存更新。
        - 您可以将格式更改为`%F`以进行每日缓存更新。

        您可以阅读[manual page]以了解有关`date`命令的格式选项的更多信息。

    4.  Material for MkDocs插件使用[caching]来加速重复
        构建并将结果存储在`.cache`目录中。

    5.  这是安装更多[MkDocs plugins]或Markdown的地方
        在构建过程中使用带有`pip`的扩展：

        ``` sh
        pip install \
          mkdocs-material \
          mkdocs-awesome-pages-plugin \
          ...
        ```

=== "Insiders"

    ``` yaml
    name: ci
    on:
      push:
        branches:
          - master
          - main
    permissions:
      contents: write
    jobs:
      deploy:
        runs-on: ubuntu-latest
        if: github.event.repository.fork == false
        steps:
          - uses: actions/checkout@v4
          - name: Configure Git Credentials
            run: |
              git config user.name github-actions[bot]
              git config user.email 41898282+github-actions[bot]@users.noreply.github.com
          - uses: actions/setup-python@v5
            with:
              python-version: 3.x
          - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV
          - uses: actions/cache@v4
            with:
              key: mkdocs-material-${{ env.cache_id }}
              path: .cache # (1)!
              restore-keys: |
                mkdocs-material-
          - run: apt-get install pngquant # (2)!
          - run: pip install git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git
          - run: mkdocs gh-deploy --force
    env:
      GH_TOKEN: ${{ secrets.GH_TOKEN }} # (3)!
    ```

    1.  Material for MkDocs插件使用[caching]来加速重复
        构建并将结果存储在`.cache`目录中。

    2.  只有当您想使用
        [built-in optimize plugin]自动压缩图像。

    3.  记得将`GH_TOKEN`存储库密钥设置为您的值
        部署[Insiders]时，可以使用[personal access token]
        使用[GitHub secrets]。

现在，当一个新的提交被推送到`master`或`main`分支时，
静态站点会自动构建和部署。推送您的更改以查看
工作流程正在运行。

如果GitHub页面在几分钟后未显示，请转到以下设置
您的存储库，并确保您的GitHub的[publishing source branch]
页面设置为`gh-pages`。

您的文档很快就会出现在`<username>.github.io/<repository>`中。

要在自定义域上发布您的网站，请参阅[MkDocs documentation]。

  [GitHub Actions]: https://github.com/features/actions
  [MkDocs plugins]: https://github.com/mkdocs/mkdocs/wiki/MkDocs-Plugins
  [personal access token]: https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token
  [Insiders]: insiders/index.md
  [built-in optimize plugin]: plugins/optimize.md
  [GitHub secrets]: https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets
  [publishing source branch]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
  [manual page]: https://man7.org/linux/man-pages/man1/date.1.html
  [caching]: plugins/requirements/caching.md
  [MkDocs documentation]: https://www.mkdocs.org/user-guide/deploying-your-docs/#custom-domains

### with MkDocs

如果您更喜欢手动部署项目文档，则可以调用
从包含`mkdocs.yml`文件的目录中执行以下命令：

```
mkdocs gh-deploy --force
```

这将构建您的文档并将其部署到分支
`gh-pages`在您的存储库中。请参阅[this overview in the MkDocs
documentation]以获取更多信息。关于
参数，请参阅[the documentation for the command]。

  [this overview in the MkDocs documentation]: https://www.mkdocs.org/user-guide/deploying-your-docs/#project-pages
  [the documentation for the command]: https://www.mkdocs.org/user-guide/cli/#mkdocs-gh-deploy

## GitLab Pages

如果你在GitLab上托管代码，可以部署到[GitLab Pages]
通过使用[GitLab CI]任务运行器。在存储库的根目录下，创建一个
名为`.gitlab-ci.yml`的任务定义，并复制粘贴以下内容
内容：

=== "Material for MkDocs"

    ``` yaml
    pages:
      stage: deploy
      image: python:latest
      script:
        - pip install mkdocs-material
        - mkdocs build --site-dir public
      cache:
        key: ${CI_COMMIT_REF_SLUG}
        paths:
          - .cache/ # (1)!
      artifacts:
        paths:
          - public
      rules:
        - if: '$CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH'

    ```

    1.  Material for MkDocs插件使用[caching]来加速重复
        构建并将结果存储在`.cache`目录中。

=== "Insiders"

    ``` yaml
    pages:
      stage: deploy
      image: python:latest
      script: # (1)!
        - pip install git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git
        - mkdocs build --site-dir public
      cache:
        key: ${CI_COMMIT_REF_SLUG}
        paths:
          - .cache/ # (2)!
      artifacts:
        paths:
          - public
      rules:
        - if: '$CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH'
    ```

    1.  记得将`GH_TOKEN`存储库密钥设置为您的值
        部署[Insiders]时，可以使用[personal access token]
        使用[masked custom variables]。

    2.  Material for MkDocs插件使用[caching]来加速重复
        构建并将结果存储在`.cache`目录中。

现在，当一个新的提交被推送到[default branch]（通常是`master`或
`main`），静态站点会自动构建和部署。承诺并推动
将文件保存到您的存储库中，以查看正在运行的工作流。

您的文档未在`<username>.gitlab.io/<repository>`下发布
默认情况下，自**GitLab 17.4** [^1]以来。但是，如果您更喜欢更干净的URL
结构，如`<username>.gitlab.io/<repository>`，您需要调整
您的配置。

要从唯一域切换到传统URL结构，请执行以下操作
这些步骤：

1.  查找您的存储库
2.  转到存储库菜单中的**Settings › Pages**。
3.  在**Unique domain settings**部分，**uncheck**标记的框
4.  **Use unique domain**.
5.  单击**Save changes**以应用更新。

现在，您可以在`<username>.gitlab.io/<repository>`下访问您的文档。

[^1]: [Release notes for Gitlab 17.4](https://about.gitlab.com/releases/2024/09/19/gitlab-17-4-released/)

## 其他

由于我们无法覆盖所有可能的平台，我们依赖社区贡献
解释如何将使用Material for MkDocs构建的网站部署到
其他供应商：

<div class="mdx-columns" markdown>

- [:simple-cloudflarepages: Cloudflare Pages][Cloudflare Pages]
- [:material-airballoon-outline: Fly.io][Flyio]
- [:simple-netlify: Netlify][Netlify]
- [:simple-scaleway: Scaleway][Scaleway]

</div>

  [GitLab Pages]: https://gitlab.com/pages
  [GitLab CI]: https://docs.gitlab.com/ee/ci/
  [masked custom variables]: https://docs.gitlab.com/ee/ci/variables/#mask-a-cicd-variable
  [default branch]: https://docs.gitlab.com/ee/user/project/repository/branches/default.html
  [Cloudflare Pages]: https://deborahwrites.com/guides/deploy-host-mkdocs/deploy-mkdocs-material-cloudflare/
  [Flyio]: https://documentation.breadnet.co.uk/cloud/fly/mkdocs-on-fly/
  [Netlify]: https://deborahwrites.com/guides/deploy-host-mkdocs/deploy-mkdocs-material-netlify/
  [Scaleway]: https://www.scaleway.com/en/docs/tutorials/using-bucket-website-with-mkdocs/


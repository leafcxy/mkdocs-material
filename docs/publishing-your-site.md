# 发布您的网站

在 `git` 仓库中托管项目文档的好处之一是能够在推送新更改时自动部署。MkDocs 让这一切变得非常简单。

## GitHub Pages

如果你已经在 GitHub 上托管代码，[GitHub Pages] 无疑是发布项目文档最便捷的方式。它是免费的，设置也非常容易。

  [GitHub Pages]: https://pages.github.com/

### 使用 GitHub Actions

通过 [GitHub Actions]，你可以自动部署项目文档。在仓库根目录下，创建一个新的 GitHub Actions 工作流，例如 `.github/workflows/ci.yml`，并复制粘贴以下内容：

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
          - name: 配置 Git 凭据
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

    2.  GitHub 曾将 `master` 重命名为 `main`。如果你的默认分支名为 `master`，可以安全地删除 `main`，反之亦然。

    3.  存储 `cache_id` 环境变量，以便后续缓存创建时访问。该名称区分大小写，请确保与 `${{ env.cache_id }}` 保持一致。

        - `--utc` 选项确保每个工作流运行器使用相同的时区。
        - `%V` 格式确保每周进行一次缓存更新。
        - 你可以将格式更改为 `%F` 以进行每日缓存更新。

        你可以阅读 [manual page] 了解 `date` 命令的格式选项。

    4.  Material for MkDocs 插件使用 [caching] 加速重复构建，并将结果存储在 `.cache` 目录中。

    5.  这里可以安装更多 [MkDocs 插件] 或 Markdown 扩展：

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
          - name: 配置 Git 凭据
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

    1.  Material for MkDocs 插件使用 [caching] 加速重复构建，并将结果存储在 `.cache` 目录中。

    2.  仅当你想使用 [内置优化插件] 自动压缩图片时需要。

    3.  记得将 `GH_TOKEN` 仓库密钥设置为你的值。部署 [Insiders] 时，可以使用 [personal access token] 并通过 [GitHub secrets] 配置。

现在，每当有新提交推送到 `master` 或 `main` 分支时，静态站点会自动构建和部署。推送更改后即可看到工作流运行。

如果 GitHub Pages 在几分钟后未显示，请前往仓库设置，确保 GitHub Pages 的 [发布源分支] 设置为 `gh-pages`。

你的文档很快会出现在 `<username>.github.io/<repository>`。

如需在自定义域名上发布网站，请参阅 [MkDocs 文档]。

  [GitHub Actions]: https://github.com/features/actions
  [MkDocs 插件]: https://github.com/mkdocs/mkdocs/wiki/MkDocs-Plugins
  [personal access token]: https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token
  [Insiders]: insiders/index.md
  [内置优化插件]: plugins/optimize.md
  [GitHub secrets]: https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets
  [发布源分支]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
  [manual page]: https://man7.org/linux/man-pages/man1/date.1.html
  [caching]: plugins/requirements/caching.md
  [MkDocs 文档]: https://www.mkdocs.org/user-guide/deploying-your-docs/#custom-domains

### 使用 MkDocs

如果你更喜欢手动部署项目文档，可以在包含 `mkdocs.yml` 文件的目录下执行以下命令：

```
mkdocs gh-deploy --force
```

这将构建文档并将其部署到仓库的 `gh-pages` 分支。更多信息请参阅 [MkDocs 文档中的相关说明][this overview in the MkDocs documentation]。关于参数说明，请参阅 [命令文档][the documentation for the command]。

  [this overview in the MkDocs documentation]: https://www.mkdocs.org/user-guide/deploying-your-docs/#project-pages
  [the documentation for the command]: https://www.mkdocs.org/user-guide/cli/#mkdocs-gh-deploy

## GitLab Pages

如果你在 GitLab 上托管代码，可以通过 [GitLab CI] 任务运行器部署到 [GitLab Pages]。在仓库根目录下创建一个名为 `.gitlab-ci.yml` 的任务定义文件，并复制粘贴以下内容：

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

    1.  Material for MkDocs 插件使用 [caching] 加速重复构建，并将结果存储在 `.cache` 目录中。

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

    1.  记得将 `GH_TOKEN` 仓库密钥设置为你的值。部署 [Insiders] 时，可以使用 [personal access token] 并通过 [masked custom variables] 配置。

    2.  Material for MkDocs 插件使用 [caching] 加速重复构建，并将结果存储在 `.cache` 目录中。

现在，每当有新提交推送到 [默认分支][default branch]（通常是 `master` 或 `main`），静态站点会自动构建和部署。提交并推送文件到仓库后即可看到工作流运行。

自 **GitLab 17.4** [^1] 起，文档不会默认发布在 `<username>.gitlab.io/<repository>` 下。如果你更喜欢更简洁的 URL 结构，如 `<username>.gitlab.io/<repository>`，需要调整配置。

要从唯一域切换到传统 URL 结构，请执行以下步骤：

1.  找到你的仓库
2.  转到仓库菜单中的 **Settings › Pages**
3.  在 **Unique domain settings** 部分，**取消勾选** “Use unique domain”
4.  点击 **Save changes** 应用更新

现在，你可以在 `<username>.gitlab.io/<repository>` 下访问文档。

[^1]: [Gitlab 17.4 发布说明](https://about.gitlab.com/releases/2024/09/19/gitlab-17-4-released/)

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


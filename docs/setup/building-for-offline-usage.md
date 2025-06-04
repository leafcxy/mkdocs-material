# 为离线使用而构建

如果您想将文档与产品一起发货，MkDocs有
你涵盖了——在主题的支持下，[MkDocs]允许构建
离线功能文档。值得注意的是，Material for MkDocs提供离线
支持其许多功能。

  [MkDocs]: https://www.mkdocs.org

## 配置

### 内置离线插件

<!-- md:version 9.0.0 -->
<!-- md:plugin [offline] – built-in -->

内置的离线插件确保[网站搜索]在您
将[站点目录]的内容作为下载分发。只需添加
将以下行添加到`mkdocs.yml`：

``` yaml
plugins:
  - offline
```

有关所有设置的列表，请参阅[插件文档]。

  [offline]: ../plugins/offline.md
  [plugin documentation]: ../plugins/offline.md

!!! tip "自动捆绑所有外部资产"

    [内置隐私插件]使使用外部资产变得容易
    在构建离线使用的文档时，因为它会自动
    下载所有外部资产，并将其与您的文档一起分发。

  [site search]: setting-up-site-search.md
  [site directory]: https://www.mkdocs.org/user-guide/configuration/#site_dir
  [built-in privacy plugin]:../plugins/privacy.md

#### 局限性

MkDocs的材料提供了许多交互功能，其中一些功能不会
由于现代浏览器的限制，从文件系统工作：全部
使用“fetch”API的功能将出错。

因此，在构建离线使用时，请确保禁用以下功能
配置设置：[即时加载]，[站点分析]，[git仓库]，
[版本控制]和[评论系统]。

  [Instant loading]: setting-up-navigation.md#instant-loading
  [Site analytics]: setting-up-site-analytics.md
  [Versioning]: setting-up-versioning.md
  [Git repository]: adding-a-git-repository.md
  [Comment systems]: adding-a-comment-system.md

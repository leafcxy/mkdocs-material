---
title: Built-in offline plugin
icon: material/connection
---


# 内置离线插件

[MkDocs][MkDocs]是为数不多的允许构建离线功能的框架之一
用户可以直接查看的文档，无需服务器。具有
离线插件，您可以分发['site`目录][mkdocs.site_dir]
作为可下载的.zip文件，同时保留了大多数交互功能。

## Objective

### 工作原理

[构建项目]后，切换到[`site`目录][mkdocs.site_dir]
然后在浏览器中打开`index.html`——您现在正在查看文档
从您的本地文件系统！大多数浏览器会通过显示`file://`
在地址栏中。然而，你会意识到网站搜索已经消失了。

MkDocs的材料提供了许多交互功能，其中一些功能不会
由于现代浏览器的限制，无法从本地文件系统工作。更多
具体来说，从技术上讲，所有对[Fetch API]的调用都会出现错误
消息类似：

```
Cross origin requests are only supported for protocol schemes: http, [...]
```

虽然浏览器出于安全原因施加了这些限制，但它减少了
你的项目的交互性。离线插件确保网站搜索
通过将搜索索引移动到JavaScript文件并利用
@squidfunk的[iframe worker]垫片。

此外，该插件会自动禁用[`use_directory_urls`]
[mkdocs.use_directory_urls]设置，确保用户可以打开您的
直接从本地文件系统获取文档。

有一些[限制]。

  [building your project]: ../creating-your-site.md#building-your-site
  [Fetch API]: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
  [iframe-worker]: https://github.com/squidfunk/iframe-worker
  [limitations]: #limitations

### 何时使用

正如名称所示，该插件只应在以下情况下使用
[构建你的项目]用于离线分发。知道这一点也很好
离线插件与以下其他插件配合良好，有助于
创建更好的离线文档：

<div class="grid cards" markdown>

-   :material-shield-account: &nbsp; __[Built-in privacy plugin][privacy]__

    ---

    隐私插件使在构建时可以轻松使用外部资产
    离线使用，因为它会自动下载它们进行分发
    您的文档。

    ---

    __Your documentation can work without connectivity to the internet[^1]__

-   :material-rabbit: &nbsp; __[Built-in optimize plugin][optimize]__

    ---

    优化插件自动识别并优化所有媒体文件
    通过使用压缩和转换在项目中引用
    技术。

    ---

    __Your documentation can be distributed as a smaller `.zip` download__

</div>

  [^1]:
    你可能会想知道为什么需要[privacy plugin][privacy]来构建
    使用离线插件的真正离线功能文档。虽然它是
    当然也可以添加对下载外部资产的支持
    离线插件，此功能已在
    隐私插件，这是它存在的理由。

    MkDocs的材料遵循其插件系统的模块化方法——许多
    的插件可以完美地协同工作，并相互增强
    功能，允许用几行代码解决复杂问题
    配置。

  [privacy]: privacy.md
  [optimize]: optimize.md

## 配置

<!-- md:version 9.0.0 -->
<!-- md:plugin [offline] – built-in -->

与所有[内置插件]一样，开始使用离线插件是
直截了当。只需将以下行添加到`mkdocs.yml`中，然后开始
构建支持离线的文档：

``` yaml
plugins:
  - offline
```

离线插件内置于MkDocs的Material中，不需要
安装。

  [offline]: offline.md
  [built-in plugins]: index.md

### 一般的

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:version 9.0.0 -->
<!-- md:default `true` -->

使用此设置可在[构建项目]时启用或禁用插件。
如果你想构建在线和离线文档，这是一个
使用[环境变量][mkdocs.env]是个好主意：

``` yaml
plugins:
  - offline:
      enabled: !ENV [OFFLINE, false]
```

## 局限性

启用离线插件时，请确保禁用以下设置，
因为他们使用[Fetch API，当从本地调用时会出错
文件系统：

- [Instant loading]
- [Site analytics]
- [Versioning]
- [Comment systems]

  [Instant loading]: ../setup/setting-up-navigation.md#_3
  [Site analytics]: ../setup/setting-up-site-analytics.md
  [Versioning]: ../setup/setting-up-versioning.md
  [Comment systems]: ../setup/adding-a-comment-system.md

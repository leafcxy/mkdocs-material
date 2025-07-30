---
title: Built-in privacy plugin
icon: material/shield-account
---


# 内置隐私插件

隐私插件为自动自托管提供了一个简化的解决方案
外部资产。只需一行配置，插件就可以
自动识别和下载外部资产，使GDPR合规
尽可能轻松。

## Objective

### 工作原理

该插件扫描生成的HTML以查找外部资源，即脚本、样式
工作表、图像和web字体，下载并存储在
[`site`目录][mkdocs.site_dir]，并将所有引用替换为指向的链接
下载的副本可以轻松地进行自托管。例如：

``` html
<script src="https://example.com/script.js"></script>
```

下载此外部脚本后，链接将替换为：

``` html
<script src="assets/external/example.com/script.js"></script>
```

当然，脚本和样式表可以引用其他外部资产，
这就是为什么这个过程会递归重复，直到没有进一步的外部
检测到资产：

- 扫描脚本以获取更多脚本、样式表和JSON文件
- 扫描样式表以查找图像和web字体

此外，在以下情况下，使用[`preconnect][preconnect]等提示来减少延迟
请求的外部资产将从输出中删除，因为它们不是
自托管时需要。插件完成工作后，您的项目
将无需请求外部服务。

有一些[限制]。

  [preconnect]: https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/rel/preconnect
  [limitations]: #limitations

### 何时使用

该插件的开发是为了符合2018年欧洲
__《通用数据保护条例》（GDPR）尽可能简单，同时
保持Material for MkDocs提供的灵活性和强大功能，如
例如，它与[谷歌字体]的紧密集成。

但是，这只是开始。例如，如果你的项目包括很多
图像，启用插件可以将它们移出存储库，如
插件将自动下载并将其存储在['site`目录]中
[构建项目]时使用[mkdocs.site_dir]。

更有趣的是，该插件可以与其他内置插件结合使用
MkDocs提供的材料，用于创建复杂的构建
为您的项目量身定制的管道：

<div class="grid cards" markdown>

-   :material-rabbit: &nbsp; __[Built-in optimize plugin][optimize]__

    ---

    优化插件允许优化所有下载的外部资产
    隐私插件通过压缩和转换检测
    技术。

    ---

    __外部媒体文件会自动下载和优化__

-   :material-connection: &nbsp; __[Built-in offline plugin][offline]__

    ---

    离线插件增加了对构建[离线功能文档]的支持，
    因此，您可以将[`site`目录][mkdocs.site_dir]作为`.zip分发`
    可以下载的文件。

    ---

    __您的文档可以在没有连接到互联网的情况下工作__

</div>

  [Google Fonts]: ../setup/changing-the-fonts.md
  [building your project]: ../creating-your-site.md#building-your-site
  [optimize]: optimize.md
  [offline]: offline.md
  [offline-capable documentation]: ../setup/building-for-offline-usage.md

## 配置

`version 9.5.0`
`plugin [privacy] – built-in`
`flag multiple`
`flag experimental`

与所有[内置插件]一样，开始使用隐私插件是
直截了当。只需将以下行添加到`mkdocs.yml`中，然后开始
轻松自托管外部资产：

``` yaml
plugins:
  - privacy
```

隐私插件内置于MkDocs的Material中，不需要
安装。

  [privacy]: privacy.md
  [built-in plugins]: index.md

### 一般的

以下设置可用：

---

#### `setting config.enabled`

`version 9.5.0`
`default _true_`

使用此设置可在[构建项目]时启用或禁用插件。
如果你想禁用插件，例如，对于本地构建，你可以使用
`mkdocs.yml`中的[环境变量][mkdocs.env]：

``` yaml
plugins:
  - privacy:
      enabled: !ENV [CI, false]
```

此配置仅在持续集成（CI）期间启用插件。

---

#### `setting config.concurrency`

`version 9.5.0`
`default available CPUs - 1`

有了更多的CPU可用，插件可以并行执行更多的工作，因此
更快地完成外部资产的处理。如果你想禁用并发
完全处理，使用：

``` yaml
plugins:
  - privacy:
      concurrency: 1
```

默认情况下，该插件使用所有可用的CPU-1，最小值为1。

### 缓存

该插件实现了[智能缓存]机制，确保外部
只有当资产尚未包含在缓存中时，才会下载它们。
虽然初始构建可能需要一些时间，但使用缓存是个好主意，
因为它将加速连续构建。

以下设置可用于缓存：

  [intelligent caching]: requirements/caching.md

---

#### `setting config.cache`

`version 9.5.0`
`default _true_`

使用此设置指示插件绕过缓存，以便
重新安排所有外部资产的下载，即使缓存可能不是
陈腐。通常不需要指定此设置，除非
调试插件本身。可以通过以下方式禁用缓存：

``` yaml
plugins:
  - privacy:
      cache: false
```

---

#### `setting config.cache_dir`

`version 9.5.0`
`default _.cache/plugin/privacy_`

通常不需要指定此设置，除非您需要
更改根目录中下载副本的路径
缓存。如果你想更改它，请使用：

``` yaml
plugins:
  - privacy:
      cache_dir: my/custom/dir
```

如果你正在使用该插件的[多个实例]，这可能是一个好主意
为两个实例设置不同的缓存目录，这样它们就不会相互干扰
彼此。

  [multiple instances]: index.md#multiple-instances

### 登录中

以下设置可用于日志记录：

---

#### `setting config.log`

`sponsors`
`version insiders-4.50.0`
`default _true_`

使用此设置可控制插件在以下情况下是否应显示日志消息
构建您的网站。虽然不建议使用，但您可以通过以下方式禁用日志记录：

``` yaml
plugins:
  - privacy:
      log: false
```

---

#### `setting config.log_level`

`sponsors`
`version insiders-4.50.0`
`default _info_`

使用此设置控制插件在以下情况下应采用的日志级别
遇到错误，这要求[`log`][config.log]设置为
启用。以下日志级别可用：

=== "`error`"

    ``` yaml
    plugins:
      - privacy:
          log_level: error
    ```

    只报告错误。

=== "`warn`"

    ``` yaml
    plugins:
      - privacy:
          log_level: warn
    ```

    报告错误和警告，终止内置程序
    [严格][mkdocs.strict]模式。这包括符号链接无法执行时的警告
    由于在Windows系统上缺乏权限而创建（#6550）。

=== "`info`"

    ``` yaml
    plugins:
      - privacy:
          log_level: info
    ```

    报告错误、警告和信息性消息，包括
    插件已成功下载资产。

=== "`debug`"

    ``` yaml
    plugins:
      - privacy:
          log_level: debug
    ```

    仅当MkDocs时，才会报告所有消息，包括调试消息
    以“--verbose”标志开头。请注意，这将打印很多
    消息，仅对调试有用。

### 外部资产

以下设置可用于外部资产：

---

#### `setting config.assets`

`version 9.5.0`
`default _true_`

使用此设置控制插件是否应下载外部
资产。如果你只想让插件处理[外部链接]，你可以禁用
通过以下方式处理外部资产：

``` yaml
plugins:
  - privacy:
      assets: false
```

  [external links]: 

---

#### `setting config.assets_fetch`

`version 9.5.0`
`default _true_`

使用此设置控制插件是应该下载还是只报告
当遇到外部资产时。如果您已经自行托管所有外部
资产，此设置可用作检测外部链接的安全网
作者在页面中放置的资产：

``` yaml
plugins:
  - privacy:
      assets_fetch: true
```

---

#### `setting config.assets_fetch_dir`

`version 9.5.0`
`default _assets/external_`

通常不需要指定此设置，除非您需要
更改[`site`目录][mkdocs.site_dir]中的路径，其中
存储外部资产。如果你想更改它，请使用：

``` yaml
plugins:
  - privacy:
      assets_fetch_dir: my/custom/dir
```

此配置将下载的副本存储在“my/custom/dir”中
[站点目录][mkdocs.site_dir]。

---

#### `setting config.assets_include`

`sponsors`
`version insiders-4.37.0`
`default none`

使用此设置启用特定来源的外部资产下载，
例如，当使用插件的[多个实例]来微调处理时
不同来源的外部资产：

``` yaml
plugins:
  - privacy:
      assets_include:
        - unsplash.com/*
```

---

#### `setting config.assets_exclude`

`sponsors`
`version insiders-4.37.0`
`default none`

使用此设置可禁用下载特定来源的外部资源，
例如，当使用插件的[多个实例]来微调处理时
不同来源的外部资产：

``` yaml
plugins:
  - privacy:
      assets_exclude: # (1)!
        - unpkg.com/mathjax@3/*
        - giscus.app/*
```

1.  [MathJax]加载用于数学内容排版的web字体
    通过相对URL，因此不能由
    隐私插件。[MathJax可以自托管]。

    我们建议将Giscus]用作[评论系统]，它使用了一种技术
    称为代码拆分，只加载必要的代码
    通过相对URL实现。Giscus也可以自托管。

  [MathJax]: ../reference/math.md
  [MathJax can be self-hosted]: https://docs.mathjax.org/en/latest/web/hosting.html
  [Giscus]: https://giscus.app/
  [comment system]: ../setup/adding-a-comment-system.md
  [Giscus can be self-hosted]: https://github.com/giscus/giscus/blob/main/SELF-HOSTING.md

---

### 外部链接

以下设置可用于外部链接：

---

#### `setting config.links`

`sponsors`
`version insiders-4.37.0`
`default _true_`

使用此设置指示插件解析和处理外部链接
对它们进行注释以[提高安全性]，或自动添加其他
外部链接的属性。如果你想禁用外部处理
链接，使用：

``` yaml
plugins:
  - privacy:
      links: false
```

  [improved security]: https://developer.chrome.com/en/docs/lighthouse/best-practices/external-anchors-use-rel-noopener/

---

#### `setting config.links_attr_map`

`sponsors`
`version insiders-4.37.0`
`default none`

使用此设置指定应添加到的其他属性
例如，外部链接，将`target=“_blank”`添加到所有外部链接中
因此，它们在一个新选项卡中打开：

``` yaml
plugins:
  - privacy:
      links_attr_map:
        target: _blank
```

---

#### `setting config.links_noopener`

`sponsors`
`version insiders-4.37.0`
`default _true_`

通常不建议更改此设置，因为它会自动更改
使用`rel=“noopener”`为在新窗口中打开的外部链接添加注释
[提高安全性]：

``` yaml
plugins:
  - privacy:
      links_noopener: true
```

## 局限性

### 简化动态网址

未检测到作为脚本一部分的动态创建的URL，因此无法
自动下载，因为插件不执行脚本——它只检测用于下载和替换的完全合格的URL。简而言之，不要这样做：

``` js
const host = "https://example.com"
const path = `${host}/script.js`
```

相反，请始终使用完全限定的URL：

``` js
const url ="https://example.com/script.js"
```

### 嵌入HTML

默认情况下，不会扫描嵌入的HTML文件（例如iframe中的文件）以查找外部
资产。这是MkDocs的一个局限性，因为它认为“.html”文件是
模板，必须明确列在
[`extra_templates][mkdocs.extra_template]。因此，自行托管外部资产
嵌入式HTML文件：

``` yaml
extra_templates:
  - iframe.html
```

请注意，`iframe.html `的路径是相对于
[`docs_dir`][mkdocs.docs_dir]目录。

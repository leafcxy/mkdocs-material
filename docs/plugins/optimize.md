---
title: Built-in optimize plugin
icon: material/rabbit
---

# 内置优化插件

当发生以下情况时，优化插件会自动识别并优化所有媒体文件
[构建你的项目]通过使用常见的压缩和转换技术。
因此，您的网站加载速度明显更快，并在以下方面产生更好的排名
搜索引擎。

---

`sponsors` __Sponsors only__ – this plugin is currently reserved to
[our awesome sponsors].

  [building your project]: ../creating-your-site.md#building-your-site
  [our awesome sponsors]: ../insiders/index.md

## Objective

### 工作原理

该插件扫描[`docs`目录][mkdocs.docs_dir]中的媒体文件
资产，自动优化它们以减少最终的规模
[站点目录][mkdocs.site_dir]。这会使您的加载时间更快
为用户提供更少的字节数，以及更小的下载量
[支持离线的文档]。

优化后的图像被[智能缓存][智能缓存]，这就是为什么
该插件将仅优化自上次构建以来更改的媒体文件。
这使得更换或更新图像成为可能，而无需担心
优化它们，甚至更糟糕的是，忘记这样做。

为了优化媒体文件，需要提供一些[依赖关系]
你的系统。

  [offline-capable documentation]: ../setup/building-for-offline-usage.md
  [dependencies]: #configuration

### 何时使用

通常建议使用插件，因为媒体文件已经过优化
无需干预即可自动加载，确保您的网站加载
尽可能快。优化的媒体文件是
在搜索引擎中排名高且一致。

此外，该插件可以与其他内置插件结合使用
MkDocs提供的材料，以创建复杂的
为您的项目量身定制管道：

<div class="grid cards" markdown>

-   :material-shield-account: &nbsp; __[Built-in privacy plugin][privacy]__

    ---

    隐私插件使使用未优化的外部资产变得容易
    在将它们复制到[`site`目录]之前，先将它们添加到优化插件中
    [mkdocs.site_dir]。

    ---

    __External media files can be automatically downloaded and optimized__

-   :material-connection: &nbsp; __[Built-in offline plugin][offline]__

    ---

    离线插件增加了对构建离线文档的支持，
    因此，您可以将[`site`目录][mkdocs.site_dir]作为`.zip分发`
    可以下载的文件。

    ---

    __Your documentation can be distributed as a smaller `.zip` download__

</div>

  [privacy]: privacy.md
  [offline]: offline.md

## 配置

`sponsors`
`version insiders-4.29.0`
`plugin [optimize] – built-in`
`flag multiple`
`flag experimental`

与所有[内置插件]一样，开始使用优化插件是
直截了当。只需将以下行添加到`mkdocs.yml`中，并观察如何
媒体文件会自动优化：

``` yaml
plugins:
  - optimize
```

优化插件内置于MkDocs的Material中，不需要
安装。

但是，为了优化所有媒体文件，有必要安装
[图像处理]的依赖关系，如果它们在您的
系统。链接的指南包括几个操作系统的说明
并提到了一些替代环境。

  [optimize]: optimize.md
  [built-in plugins]: index.md
  [image processing]: requirements/image-processing.md

### 一般的

以下设置可用：

---

#### `setting config.enabled`

`sponsors`
`version insiders-4.29.0`
`default _true_`

使用此设置可在[构建项目]时启用或禁用插件。
如果你想禁用插件，例如，对于本地构建，你可以使用
`mkdocs.yml`中的[环境变量][mkdocs.env]：

``` yaml
plugins:
  - optimize:
      enabled: !ENV [CI, false]
```

此配置仅在持续集成（CI）期间启用插件。

---

#### `setting config.concurrency`

`sponsors`
`version insiders-4.29.0`
`default available CPUs - 1`

有了更多的CPU可用，插件可以并行执行更多的工作，因此
更快地完成媒体文件优化。如果你想禁用并发
完全处理，使用：

``` yaml
plugins:
  - optimize:
      concurrency: 1
```

默认情况下，该插件使用所有可用的CPU-1，最小值为1。

### 缓存

该插件实现了一种[智能缓存]机制，确保媒体
只有当文件或资源的内容满足以下条件时，才会通过优化管道传递文件或资源
改变。如果您更换或更新图像，插件会检测到它并进行更新
媒体文件的优化版本。

以下设置可用于缓存：

  [intelligent caching]: requirements/caching.md

---

#### `setting config.cache`

`sponsors`
`version insiders-4.29.0`
`default _true_`

使用此设置指示插件绕过缓存，以便
重新优化所有媒体文件，即使缓存可能不会过时。it is 的常用口语形式
通常不需要指定此设置，调试时除外
插件本身。可以通过以下方式禁用缓存：

``` yaml
plugins:
  - optimize:
      cache: false
```

---

#### `setting config.cache_dir`

`sponsors`
`version insiders-4.29.0`
`default _.cache/plugin/optimize_`

通常不需要指定此设置，除非您需要
更改根目录中缓存媒体文件的路径。
如果你想更改它，请使用：

``` yaml
plugins:
  - optimize:
      cache_dir: my/custom/dir
```

如果你正在使用该插件的[多个实例]，这可能是一个好主意
为两个实例设置不同的缓存目录，这样它们就不会相互干扰
彼此。

  [multiple instances]: index.md#multiple-instances

### 优化

文档通常使用屏幕截图或图表来更好地
事物的可视化，这两者都是优化的主要候选者。
该插件使用[pngquant]自动优化“.png”文件的图像，
[Phillow]用于“.jpg”文件。

以下设置可用于优化：

  [pngquant]: https://pngquant.org/
  [Pillow]: https://pillow.readthedocs.io/

---

#### `setting config.optimize`

`sponsors`
`version insiders-4.41.0`
`default _true_`

使用此设置启用或禁用媒体文件优化。目前，
该插件的唯一目的是优化媒体文件，因此它相当于
[`enabled'][config.enabled]设置，但在不久的将来，其他功能
可以添加。如果要禁用优化，请使用：

``` yaml
plugins:
  - optimize:
      optimize: false
```

---

#### `setting config.optimize_png`

`sponsors`
`version insiders-4.29.0`
`default _true_`

使用此设置启用或禁用“.png”文件的优化。it is 的常用口语形式
通常不需要指定此设置，但如果要禁用
优化.png文件，使用：

``` yaml
plugins:
  - optimize:
      optimize_png: false
```

---

#### `setting config.optimize_png_speed`

`sponsors`
`version insiders-4.29.0`
`default _3_ of _1-10_`

使用此设置指定[pngquant]应用的速度/质量折衷
优化.png文件时。数字越低，攻击性越强
[pngquant]将尝试优化：

=== "Slower <small>smaller</small>"

    ``` yaml
    plugins:
      - optimize:
          optimize_png_speed: 1
    ```

=== "Faster <small>larger</small>"

    ``` yaml
    plugins:
      - optimize:
          optimize_png_speed: 10
    ```

因子“10”的质量降低了5%，但比默认的“3”快8倍。

---

#### `setting config.optimize_png_strip`

`sponsors`
`version insiders-4.29.0`
`default _true_`

使用此设置指定[pngquant]是否应删除可选元数据
来自不需要显示图像的.png文件，例如[EXIF]。
如果要保留元数据，请使用：

``` yaml
plugins:
  - optimize:
      optimize_png_strip: false
```

  [EXIF]: https://en.wikipedia.org/wiki/Exif

---

#### `setting config.optimize_jpg`

`sponsors`
`version insiders-4.29.0`
`default _true_`

使用此设置启用或禁用“.jpg”文件的优化。it is 的常用口语形式
通常不需要指定此设置，但如果要禁用
要优化.jpg文件，请使用：

``` yaml
plugins:
  - optimize:
      optimize_jpg: false
```

---

#### `setting config.optimize_jpg_quality`

`sponsors`
`version insiders-4.29.0`
`default _60_ of _0-100_`

使用此设置指定[Phillow]在以下情况下应用的图像质量
优化.jpg文件。如果图像看起来模糊，最好
微调并更改此设置：

``` yaml
plugins:
  - optimize:
      optimize_jpg_quality: 75
```

---

#### `setting config.optimize_jpg_progressive`

`sponsors`
`version insiders-4.29.0`
`default _true_`

使用此设置指定[Phillow]是否应使用渐进编码
优化.jpg文件时，在慢速连接上渲染速度更快。如果你想要我
要禁用渐进编码，请使用：

``` yaml
plugins:
  - optimize:
      optimize_jpg_progressive: false
```

  [progressive encoding]: https://medium.com/hd-pro/jpeg-formats-progressive-vs-baseline-73b3938c2339

---

#### `setting config.optimize_include`

`sponsors`
`version insiders-4.41.0`
`default none`

使用此设置可为特定目录启用媒体文件优化
例如，当使用插件的[多个实例]进行优化时
媒体文件不同：

``` yaml
plugins:
  - optimize:
      optimize_include:
        - screenshots/*
```

此配置可优化包含的所有媒体文件
在[文档目录]中的“截图”文件夹及其子文件夹中
[mkdocs.docs_dir]。

---

#### `setting config.optimize_exclude`

`sponsors`
`version insiders-4.41.0`
`default none`

使用此设置可禁用特定目录的媒体文件优化
例如，当使用插件的[多个实例]进行优化时
媒体文件不同：

``` yaml
plugins:
  - social:
      optimize_exclude:
        - vendor/*
```

此配置禁用所包含的所有媒体文件的优化
在[文档目录]中的“vendor”文件夹及其子文件夹中
[mkdocs.docs_dir]。

### Reporting

以下设置可用于报告：

---

#### `setting config.print_gain`

`sponsors`
`version insiders-4.29.0`
`default _true_`

使用此设置控制插件是否应打印字节数
优化每个文件后获得。如果要禁用此行为，请使用：

``` yaml
plugins:
  - optimize:
      print_gain: false
```

---

#### `setting config.print_gain_summary`

`sponsors`
`version insiders-4.29.0`
`default _true_`

使用此设置控制插件是否应打印
优化所有文件后获得的字节数。如果你想禁用此行为，
使用：

``` yaml
plugins:
  - optimize:
      print_gain_summary: false
```

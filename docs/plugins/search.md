---
title: Built-in search plugin
icon: material/magnify
---

# 内置搜索插件

搜索插件在标题中添加了一个搜索栏，允许用户搜索您的
文档。它由[lunr.js]提供支持，这是一个轻量级的全文搜索引擎
对于浏览器来说，消除了对外部服务的需求，甚至可以工作
在构建[支持离线的文档]时。

  [lunr.js]: https://lunrjs.com/
  [offline-capable documentation]: ../setup/building-for-offline-usage.md

## 客观的

### 工作原理

该插件扫描生成的HTML，并从所有页面构建搜索索引
通过提取章节标题和内容。它保留了一些内联
格式类似于代码块和列表，但会删除所有其他格式，因此
搜索索引尽可能小。

当用户访问您的网站时，搜索索引会被发送到浏览器，
使用[lunr.js]进行索引，并可用于快速简单的查询-否
需要服务器。这确保了搜索索引始终保持最新
您的文档，产生准确的结果。

### 何时使用

通常建议使用插件作为交互式搜索功能
是每一份好文件的重要组成部分。此外，该插件还集成了
与MkDocs的其他几个[内置插件]完美配合
提供：

<div class="grid cards" markdown>

-   :material-connection: &nbsp; __[Built-in offline plugin][offline]__

    ---

    离线插件增加了对构建离线文档的支持，
    因此，您可以将[`site`目录][mkdocs.site_dir]作为`.zip分发`
    可以下载的文件。

    ---

    __您的文档可以在没有连接到互联网的情况下工作__

-   :material-file-tree: &nbsp; __[Built-in meta plugin][meta]__

    ---

    元插件使[boost][meta.search.boost]特定变得容易
    搜索结果中的部分或[排除][元.搜索.排除]它们
    完全不被索引，从而对搜索进行更精细的控制。

    ---

    __简化不同子部分的搜索组织和管理__

</div>

  [offline]: offline.md
  [meta]: meta.md
  [built-in plugins]: index.md

## 配置

`version 9.0.0`
`plugin [search] – built-in`

与所有[内置插件]一样，开始使用搜索插件是
直截了当。只需将以下行添加到`mkdocs.yml`和您的用户
将能够搜索您的文档：

``` yaml
plugins:
  - search
```

搜索插件内置于MkDocs的Material中，不需要
安装。

  [search]: search.md
  [built-in plugins]: index.md

### 一般的

以下设置可用：

---

#### `setting config.enabled`

`version 9.3.2`
`default _true_`

使用此设置可在[构建项目]时启用或禁用插件。
通常不需要指定此设置，但如果要禁用
插件，使用：

``` yaml
plugins:
  - search:
      enabled: false
```

  [building your project]: ../creating-your-site.md#building-your-site

### 搜索

以下设置可供搜索：

---

#### `setting config.lang`

`version 9.0.0`
`default computed`

使用此设置指定搜索索引的语言，启用[词干]
支持英语以外的其他语言。默认值为自动
根据[站点语言]计算，但可以显式设置为另一种语言
甚至支持多种语言，包括：

=== "Set language"

    ``` yaml
    plugins:
      - search:
          lang: en
    ```

=== "Add further languages"

    ``` yaml
    plugins:
      - search:
          lang: # (1)!
            - en
            - de
    ```

    1.  请注意，包括对其他语言的支持会增加
        基础JavaScript有效负载减少约20kb，每增加15-30kb
        语言，都在gzip之前。

  [stemming]: https://en.wikipedia.org/wiki/Stemming
  [site language]: ../setup/changing-the-language.md
  [lunr languages]: https://github.com/MihaiValentin/lunr-languages

语言支持由[lunr languages]提供，这是一个
由[lunr.js]维护的特定于语言的词干分析器和停用词
开源社区。

---

[lunr languages]目前支持以下语言：

<div class="mdx-columns" markdown>

- `ar` – Arabic
- `da` – Danish
- `de` – German
- `du` – Dutch
- `en` – English
- `es` – Spanish
- `fi` – Finnish
- `fr` – French
- `hi` – Hindi
- `hu` – Hungarian
- `hy` – Armenian
- `it` – Italian
- `ja` – Japanese
- `kn` - Kannada
- `ko` – Korean
- `no` – Norwegian
- `pt` – Portuguese
- `ro` – Romanian
- `ru` – Russian
- `sa` – Sanskrit
- `sv` – Swedish
- `ta` – Tamil
- `te` – Telugu
- `th` – Thai
- `tr` – Turkish
- `vi` – Vietnamese
- `zh` – Chinese

</div>

如果[lunr languages]不支持所选的[站点语言]，
该插件退回到另一种能产生最佳词干结果的语言。
如果你发现搜索结果不令人满意，你可以做出贡献
通过添加对您的语言的支持，将其添加到[lunr languages]。

---

#### `setting config.separator`

`version 9.0.0`
`default computed`

使用此设置指定构建时用于拆分单词的分隔符
客户端的搜索索引。默认值是自动计算的
来自[site language]，但也可以通过以下方式显式设置为另一个值：

``` yaml
plugins:
  - search:
      separator: '[\s\-,:!=\[\]()"/]+|(?!\b)(?=[A-Z][a-z])|\.(?!\d)|&[lg]t;'
```

分隔符支持[正向和反向前瞻断言]，这允许
用于精确控制单词表达方式的相当复杂的表达式
在构建搜索索引时进行拆分。

该分离器被分解为多个部分，从而引发以下行为：

=== "Special characters"

    ```
    [\s\-,:!=\[\]()"/]+
    ```

    表达式的第一部分为每个对象插入标记边界
    文档前后有空格、连字符、逗号、括号和
    其他特殊字符。如果其中几个特殊字符是
    相邻，它们被视为一体。

=== "Case changes"

    ```
    (?!\b)(?=[A-Z][a-z])
    ```

    许多编程语言都有命名约定，如“PascalCase”或
    `camelCase”。通过将该子表达式添加到分隔符中，
    [单词在大小写变化时被拆分]，对单词“PascalCase”进行标记`
    分为“Pascal”和“Case”。

=== "Version strings"

    ```
    \.(?!\d)
    ```

    添加“时。`对于分隔符，像“1.2.3”这样的版本字符串被拆分
    分为“1”、“2”和“3”，这使得它们无法通过搜索发现。什么时候
    使用这个子表达式，引入了一个小的前瞻，它将
    [保留版本字符串]并保持它们可被发现。

=== "HTML/XML tags"

    ```
    &[lg]t;
    ```

    如果您的文档包含HTML/XML代码示例，您可能希望允许
    用户可以找到[特定的标签名称]。不幸的是，“<”和“>”控件
    字符在代码块中编码为`&lt；`以及`&gt；`.添加此
    分隔符的子表达式允许这样做。

  [positive and negative lookahead assertions]: https://www.regular-expressions.info/lookaround.html
  [words are split at case changes]: ?q=searchHighlight
  [preserve version strings]: ?q=9.0.0
  [specific tag names]: ?q=script

---

#### `setting config.pipeline`

`version 9.0.0`
`default computed`
`flag experimental`

使用此设置指定用于过滤和
使用[`separate][config.separate]对令牌进行标记后展开令牌，以及
在将它们添加到搜索索引之前。默认值为自动
根据[site language]计算，但也可以显式设置为：

``` yaml
plugins:
  - search:
      pipeline:
        - stemmer
        - stopWordFilter
        - trimmer
```

可以使用以下管道功能：

- `stemmer` – 茎标记到其根形式, e.g. `running` to `run`
- `stopWordFilter` – 根据以下条件过滤常用词, e.g. `a`, `the`, etc.
- `trimmer` – 修剪标记中的空格

  [pipeline functions]: https://lunrjs.com/guides/customising.html#pipeline-functions

### 市场细分

该插件支持通过[jieba]进行中文文本分割，这是一个流行的
中文文本分割库。其他语言，如日语和韩语
目前在客户端进行细分，但我们正在考虑将其转移
未来插件的功能。

以下设置可用于分段：

  [jieba]: https://pypi.org/project/jieba/

---

#### `setting config.jieba_dict`

`version 9.2.0`
`default none`
`flag experimental`

使用此设置指定[jieba]使用的[自定义词典]
分割文本，替换默认词典。[jieba]来了
几本词典，可以与以下词典一起使用：

``` yaml
plugins:
  - search:
      jieba_dict: dict.txt
```

以下词典由[jieba]提供：

- [dict.txt.small] – 占用内存较小的词典文件
- [dict.txt.big] – 支持繁体分词更好的词典文件

提供的路径是从根目录解析的。

  [custom dictionary]: https://github.com/fxsjy/jieba#%E5%85%B6%E4%BB%96%E8%AF%8D%E5%85%B8
  [dict.txt.small]: https://github.com/fxsjy/jieba/raw/master/extra_dict/dict.txt.small
  [dict.txt.big]: https://github.com/fxsjy/jieba/raw/master/extra_dict/dict.txt.big

---

#### `setting config.jieba_dict_user`

`version 9.2.0`
`default none`
`flag experimental`

使用此设置指定要使用的其他[用户词典]
[jieba]用于分割文本，扩充默认词典。用户
字典是调整分段器的理想选择：

``` yaml
plugins:
  - search:
      jieba_dict_user: user_dict.txt
```

提供的路径是从根目录解析的。

  [user dictionary]: https://github.com/fxsjy/jieba#%E8%BD%BD%E5%85%A5%E8%AF%8D%E5%85%B8

## 使用

### 元数据

以下属性可用：

---

#### `setting meta.search.boost`

`version 8.3.0`
`flag metadata`
`default none`

使用此属性可增加或减少搜索中页面的相关性
结果，给他们更多的权重。使用高于“1”的值进行排名
低于“1”进行排名：

=== ":material-arrow-up-circle: Rank up"

    ``` yaml
    ---
    search:
      boost: 2 # (1)!
    ---

    # Page title
    ...
    ```

    1.  在增强页面时，始终从低值开始。

=== ":material-arrow-down-circle: Rank down"

    ``` yaml
    ---
    search:
      boost: 0.5
    ---

    # Page title
    ...
    ```

---

#### `setting meta.search.exclude`

`version 9.0.0`
`flag metadata`
`default none`

使用此属性可从搜索结果中排除页面。请注意，这将
不仅删除页面，还从搜索中删除页面的所有子部分
结果：

``` yaml
---
search:
  exclude: true
---

# Page title
...
```

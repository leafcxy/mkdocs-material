# 确保数据隐私

MkDocs的材料使遵守数据隐私法规变得非常容易，
因为它提供了一种原生的[cookie同意]解决方案，以寻求明确的同意
用户在设置[分析]之前。此外，外部资产可以是
自动下载[自托管]。

  [cookie consent]: 
  [analytics]: setting-up-site-analytics.md
  [self-hosting]: 

## 配置

### Cookie同意

`version 8.4.0`
`default none`
`flag experimental`
`example cookie-consent`

MkDocs的材料附带了一份本地和可扩展的cookie同意书
在向第三方发送请求之前征求用户的同意。添加
在`mkdocs.yml`之后：

``` yaml
extra:
  consent:
    title: Cookie consent
    description: >- # (1)!
      We use cookies to recognize your repeated visits and preferences, as well
      as to measure the effectiveness of our documentation and whether users
      find what they're searching for. With your consent, you're helping us to
      make our documentation better.
```

1.  您可以在“描述”中添加任意HTML标签，例如链接到您的
    服务条款或网站的其他部分。

以下属性可用：

`option consent.title`

:   `default none` `flag required`
    此属性设置cookie同意的标题，该标题在
    必须设置为非空字符串。

`option consent.description`

:   `default none` `flag required`
    此属性设置cookie同意的描述，如下所示
    并且可以包括原始HTML（例如到服务条款的链接）。

`option consent.cookies`

:   `default none` 此属性允许添加自定义
    Cookie或更改内置Cookie的初始“已检查”状态和名称。
    目前，内置了以下Cookie：

    - __Google Analytics__ – `analytics` (enabled by default)
    - __GitHub__ – `github` (enabled by default)

    每个cookie都必须接收一个唯一的标识符，该标识符用作
    `Cookie映射，可以设置为字符串，也可以设置为定义
    `name和checked状态：

    ===  "Custom cookie name"

        ``` yaml
        extra:
          consent:
            cookies:
              analytics: Custom name
        ```

    ===  "Custom initial state"

        ``` yaml
        extra:
          consent:
            cookies:
              analytics:
                name: Google Analytics
                checked: false
        ```

    ===  "Custom cookie"

        ``` yaml
        extra:
          consent:
            cookies:
              analytics: Google Analytics # (1)!
              custom: Custom cookie
        ```

        1.  如果您将自定义cookie定义为“cookie”属性的一部分，
            必须显式添加“analytics”cookie，否则分析
            不会被触发。

    如果Google Analytics是通过`mkdocs.yml`配置的，则cookie同意将
    自动包含一个设置，供用户禁用。[自定义Cookie]
    可以从JavaScript中使用。

`option consent.actions`

:   `default _[accept, manage]_` 此属性定义
    显示哪些按钮以及以何种顺序显示，例如允许用户接受
    Cookie和管理设置：

    ``` yaml
    extra:
      consent:
        actions:
          - accept
          - manage # (1)!
    ```

    1.  如果从“actions”属性中省略了“management”设置按钮，
        设置始终显示。

    cookie同意书包括三种类型的按钮：

    - `accept` – 接受所选Cookie的按钮
    - `reject` – 拒绝所有Cookie的按钮
    - `manage` – 管理设置的按钮

当用户首次访问您的网站时，会显示cookie同意书：

[![Cookie consent enabled]][Cookie consent enabled]

  [Custom cookies]: #custom-cookies
  [Cookie consent enabled]: ../assets/screenshots/consent.png

#### 更改cookie设置

为了遵守GDPR，用户必须能够更改其cookie设置
在任何时候。这可以通过在您的[版权声明]中添加一个简单的链接来实现
在`mkdocs.yml`中：

``` yaml
copyright: >
  Copyright &copy; 2016 - 2024 Martin Donath –
  <a href="#__consent">Change cookie settings</a>
```

  [copyright notice]: setting-up-the-footer.md

### 内置隐私插件

`version 9.5.0`
`plugin [privacy][built-in privacy plugin]`
`flag experimental`

内置的隐私插件会自动将外部资产识别为一部分
构建过程，并下载所有资产，以实现非常简单的自托管。添加
将以下行添加到`mkdocs.yml`：

``` yaml
plugins:
  - privacy
```

有关所有设置的列表，请参阅[插件文档]。

  [plugin documentation]: ../plugins/privacy.md

!!! tip "在外部托管图像并自动优化它们"

    此选项使[内置隐私插件]成为
    当你想在git存储库之外托管图像等资产时
    在另一个位置，以保持它们的新鲜感和存储库的精简。

    此外，截至<！--md：内部版本-4.30.0-->
    内置的隐私插件被完全重写，现在工作得很好
    使用[内置优化插件]，这意味着外部资产
    可以通过与您的其他部分相同的优化管道传递
    文档。这意味着您可以存储和编辑未优化的文件
    在您的存储库之外，让这两个插件构建一个高度
    为您优化网站。

    如果你想实现单独的管道，即优化一些图像
    与其他图片不同，或者从下载中排除某些图片，您可以
    使用[内置隐私插件]的多个实例。

!!! question "为什么Material for MkDocs不能按设计捆绑所有资产？"

    MkDocs材料不能捆绑所有自己的主要原因
    assets是与[Google Fonts]的集成，后者提供超过一千种字体
    可用于呈现文档的不同字体。大部分
    字体包含多个权重，并被拆分为不同的字符集
    为了保持下载大小较小，浏览器只下载
    真的需要。对于Roboto，我们的默认[常规字体]，这将导致[42
    `*总共.woff2`个文件][示例]。

    如果MkDocs的材料将捆绑所有字体文件，下载大小将
    数百兆字节，减缓了自动构建的速度。此外，
    作者可能会添加外部资产，如第三方脚本或样式表
    需要记住，这将被定义为进一步的本地资产。

    这就是[内置隐私插件]存在的原因——它自动化了
    手动下载所有外部资产以确保合规性的过程
    GDPR有一些[技术限制]。

  [Google Fonts]: changing-the-fonts.md
  [regular font]: changing-the-fonts.md
  [example]: #example
  [built-in optimize plugin]: ../plugins/optimize.md
  [technical limitations]: ../plugins/privacy.md#limitations

??? example "展开以检查示例"

    对于官方文档，[内置隐私插件]下载
    以下资源：

    ``` { .sh .no-copy #example }
    .
    └─ assets/external/
       ├─ unpkg.com/tablesort@5.3.0/dist/tablesort.min.js
       ├─ fonts.googleapis.com/css
       └─ fonts.gstatic.com/s/
          ├─ roboto/v29/
          │  ├─ KFOjCnqEu92Fr1Mu51TjASc-CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TjASc0CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TjASc1CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TjASc2CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TjASc3CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TjASc5CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TjASc6CsQ.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TzBic-CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TzBic0CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TzBic1CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TzBic2CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TzBic3CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TzBic5CsTKlA.woff2
          │  ├─ KFOjCnqEu92Fr1Mu51TzBic6CsQ.woff2
          │  ├─ KFOkCnqEu92Fr1Mu51xEIzIFKw.woff2
          │  ├─ KFOkCnqEu92Fr1Mu51xFIzIFKw.woff2
          │  ├─ KFOkCnqEu92Fr1Mu51xGIzIFKw.woff2
          │  ├─ KFOkCnqEu92Fr1Mu51xHIzIFKw.woff2
          │  ├─ KFOkCnqEu92Fr1Mu51xIIzI.woff2
          │  ├─ KFOkCnqEu92Fr1Mu51xLIzIFKw.woff2
          │  ├─ KFOkCnqEu92Fr1Mu51xMIzIFKw.woff2
          │  ├─ KFOlCnqEu92Fr1MmSU5fABc4EsA.woff2
          │  ├─ KFOlCnqEu92Fr1MmSU5fBBc4.woff2
          │  ├─ KFOlCnqEu92Fr1MmSU5fBxc4EsA.woff2
          │  ├─ KFOlCnqEu92Fr1MmSU5fCBc4EsA.woff2
          │  ├─ KFOlCnqEu92Fr1MmSU5fCRc4EsA.woff2
          │  ├─ KFOlCnqEu92Fr1MmSU5fChc4EsA.woff2
          │  ├─ KFOlCnqEu92Fr1MmSU5fCxc4EsA.woff2
          │  ├─ KFOlCnqEu92Fr1MmWUlfABc4EsA.woff2
          │  ├─ KFOlCnqEu92Fr1MmWUlfBBc4.woff2
          │  ├─ KFOlCnqEu92Fr1MmWUlfBxc4EsA.woff2
          │  ├─ KFOlCnqEu92Fr1MmWUlfCBc4EsA.woff2
          │  ├─ KFOlCnqEu92Fr1MmWUlfCRc4EsA.woff2
          │  ├─ KFOlCnqEu92Fr1MmWUlfChc4EsA.woff2
          │  ├─ KFOlCnqEu92Fr1MmWUlfCxc4EsA.woff2
          │  ├─ KFOmCnqEu92Fr1Mu4WxKOzY.woff2
          │  ├─ KFOmCnqEu92Fr1Mu4mxK.woff2
          │  ├─ KFOmCnqEu92Fr1Mu5mxKOzY.woff2
          │  ├─ KFOmCnqEu92Fr1Mu72xKOzY.woff2
          │  ├─ KFOmCnqEu92Fr1Mu7GxKOzY.woff2
          │  ├─ KFOmCnqEu92Fr1Mu7WxKOzY.woff2
          │  └─ KFOmCnqEu92Fr1Mu7mxKOzY.woff2
          └─ robotomono/v13/
             ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSV0mf0h.woff2
             ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSZ0mf0h.woff2
             ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSd0mf0h.woff2
             ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSh0mQ.woff2
             ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSt0mf0h.woff2
             ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSx0mf0h.woff2
             ├─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtElOUlYIw.woff2
             ├─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtEleUlYIw.woff2
             ├─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtEluUlYIw.woff2
             ├─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtEm-Ul.woff2
             ├─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtEmOUlYIw.woff2
             └─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtEn-UlYIw.woff2
    ```

  [built-in privacy plugin]: ../plugins/privacy.md
  [preconnect]: https://developer.mozilla.org/en-US/docs/Web/Performance/dns-prefetch

#### 高级设置

`sponsors`
`version insiders-4.50.0`

以下高级设置目前保留给我们的[赞助商]
[内部人士]。它们完全是可选的，不会影响
博客，但可能有助于自定义：

- [`log`][config.log]
- [`log_level`][config.log_level]

随着我们发现新的用例，我们将在此处添加更多设置。

  [Insiders]: ../insiders/index.md
  [config.log]: ../plugins/privacy.md
  [config.log_level]: ../plugins/privacy.md

## 自定义

### 自定义Cookie

`version 8.4.0`
`example custom-cookies`

如果您自定义了[cookie同意]并添加了“自定义”cookie，则用户
系统将提示您接受或拒绝您的自定义cookie。一旦用户接受
或者拒绝cookie同意，或者[更改设置]，页面将重新加载[^1]。
使用[附加JavaScript]查询结果：

  [^1]:
    我们重新加载页面，使与自定义Cookie的互操作更简单。如果材料
    因为MkDocs将实现基于回调的方法，作者需要
    确保正确更新所有使用Cookie的脚本。另外，
    cookie同意仅在最初得到答复，这就是我们考虑的原因
    这是DX和UX的良好权衡。

=== ":octicons-file-code-16: `docs/javascripts/consent.js`"

    ``` js
    var consent = __md_get("__consent")
    if (consent && consent.custom) {
      /* The user accepted the cookie */
    } else {
      /* The user rejected the cookie */
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_javascript:
      - javascripts/consent.js
    ```

  [additional JavaScript]: ../customization.md
  [changes the settings]: #change-cookie-settings

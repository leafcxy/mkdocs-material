# 浏览器支持

Material for MkDocs竭尽全力支持尽可能大的范围
浏览器，同时保留最简单的定制可能性
现代CSS功能，如[custom properties]和[mask images]。

  [custom properties]: https://caniuse.com/css-variables
  [mask images]: https://caniuse.com/mdn-css_properties_mask-image

## 支持的浏览器

下表列出了Material for MkDocs提供完整内容的所有浏览器
支持，因此可以假设所有功能都能正常工作而不会降级。如果你
发现某些内容在支持的浏览器中看起来不正确
版本范围，请[open an issue]：

<figure markdown>

| Browser                              | Version | Release date |         |        |      Usage |
| ------------------------------------ | ------: | -----------: | ------: | -----: | ---------: |
|                                      |         |              | desktop | mobile |    overall |
| :fontawesome-brands-chrome: Chrome   |     49+ |      03/2016 | 25.65%  | 38.33% |     63.98% |
| :fontawesome-brands-safari: Safari   |     10+ |      09/2016 |  4.63%  | 14.96% |     19.59% |
| :fontawesome-brands-edge: Edge       |     79+ |      01/2020 |  3.95%  |    n/a |      3.95% |
| :fontawesome-brands-firefox: Firefox |     53+ |      04/2017 |  3.40%  |   .30% |      3.70% |
| :fontawesome-brands-opera: Opera     |     36+ |      03/2016 |  1.44%  |   .01% |      1.45% |
|                                      |         |              |         |        | __92.67%__ |

  <figcaption markdown>

浏览器支持矩阵来源于[caniuse.com].[^1]

  </figcaption>
</figure>

  [^1]:
    这些数据是在2022年1月从[caniuse.com]收集的，主要是
    基于浏览器对[custom properties]、[mask images]和
    [:is pseudo selector] ，它不是完全可填充的。带有a的浏览器
    不考虑累计市场份额低于1%，但仍可能
    完全或部分得到支持。

请注意，使用数据基于全球浏览器市场份额，因此可以
事实上，对于你的目标人群来说，情况完全不同。这是个好主意
检查浏览器类型和版本在用户中的分布情况。

  [open an issue]: https://github.com/squidfunk/mkdocs-material/issues/new/choose
  [caniuse.com]: https://caniuse.com/
  [:is pseudo selector]: https://caniuse.com/css-matches-pseudo
  [browser support]: #supported-browsers
  [built-in privacy plugin]: plugins/privacy.md

## 其他浏览器

尽管你的网站可能看起来不像用现代浏览器浏览时那么完美，
以下较旧的浏览器版本可能需要额外的努力才能使用：

- :fontawesome-brands-firefox: __Firefox 31-52__ – 图标将尽可能小地呈现
  由于缺少对[mask images]的支持，框。虽然这不可能
  polyfilled，可以通过完全隐藏图标来缓解。
- :fontawesome-brands-edge: __Edge 16-18__ – 某些元素的间距可能
  由于缺少对[:is pseudo selector]的支持，这有点不合适
  可以通过一些额外的努力来缓解。
- :fontawesome-brands-internet-explorer: __Internet Explorer__ - 没有支持，
  主要是由于缺少对[custom properties]的支持。最后一个版本
  MkDocs支持Internet Explorer的材料是`4.6.3`

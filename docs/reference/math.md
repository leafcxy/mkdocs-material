---
icon: material/alphabet-greek
---

# 数学公式

[MathJax] 和 [KaTeX] 是两个流行的用于在浏览器中显示数学内容的库。虽然这两个库提供类似的功能，但它们使用不同的语法并具有不同的配置选项。本文档站点提供了如何轻松地将它们与 Material for MkDocs 集成的信息。

  [MathJax]: https://www.mathjax.org/
  [LaTeX]: https://en.wikibooks.org/wiki/LaTeX/Mathematics
  [MathML]: https://en.wikipedia.org/wiki/MathML
  [AsciiMath]: http://asciimath.org/
  [KaTeX]: https://katex.org/


## 配置

以下配置启用了使用 [MathJax] 和 [KaTeX] 渲染块级和内联块级方程的支持。

### MathJax

[MathJax] 是一个强大而灵活的库，支持多种输入格式，如 [LaTeX]、[MathML]、[AsciiMath]，以及各种输出格式，如 HTML、SVG、MathML。要在项目中使用 MathJax，请将以下行添加到 `mkdocs.yml` 中。

=== ":octicons-file-code-16: `docs/javascripts/mathjax.js`"

    ``` js
    window.MathJax = {
      tex: {
        inlineMath: [["\\(", "\\)"]],
        displayMath: [["\\[", "\\]"]],
        processEscapes: true,
        processEnvironments: true
      },
      options: {
        ignoreHtmlClass: ".*|",
        processHtmlClass: "arithmatex"
      }
    };

    document$.subscribe(() => { // (1)!
      MathJax.startup.output.clearCache()
      MathJax.typesetClear()
      MathJax.texReset()
      MathJax.typesetPromise()
    })
    ```

    1. 这将 MathJax 与[即时加载]集成。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    markdown_extensions:
      - pymdownx.arithmatex:
          generic: true

    extra_javascript:
      - javascripts/mathjax.js
      - https://unpkg.com/mathjax@3/es5/tex-mml-chtml.js
    ```

查看其他配置选项：

- [Arithmatex]

  [Arithmatex]: ../setup/extensions/python-markdown-extensions.md#arithmatex
  [instant loading]: ../setup/setting-up-navigation.md#instant-loading

<script id="MathJax-script" async src="https://unpkg.com/mathjax@3/es5/tex-mml-chtml.js"></script>
<script>
  window.MathJax = {
    tex: {
      inlineMath: [["\\(", "\\)"]],
      displayMath: [["\\[", "\\]"]],
      processEscapes: true,
      processEnvironments: true
    },
    options: {
      ignoreHtmlClass: ".*|",
      processHtmlClass: "arithmatex"
    }
  };
</script>

### KaTeX

[KaTeX] 是一个轻量级库，专注于速度和简单性。它支持 LaTeX 语法的子集，可以将数学公式渲染为 HTML 和 SVG。要在项目中使用 [KaTeX]，请将以下行添加到 `mkdocs.yml` 中。

=== ":octicons-file-code-16: `docs/javascripts/katex.js`"

    ``` js
    document$.subscribe(({ body }) => { // (1)!
      renderMathInElement(body, {
        delimiters: [
          { left: "$$",  right: "$$",  display: true },
          { left: "$",   right: "$",   display: false },
          { left: "\\(", right: "\\)", display: false },
          { left: "\\[", right: "\\]", display: true }
        ],
      })
    })
    ```

    1. 这将 KaTeX 与[即时加载]集成。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    markdown_extensions:
      - pymdownx.arithmatex:
          generic: true

    extra_javascript:
      - javascripts/katex.js
      - https://unpkg.com/katex@0/dist/katex.min.js
      - https://unpkg.com/katex@0/dist/contrib/auto-render.min.js

    extra_css:
      - https://unpkg.com/katex@0/dist/katex.min.css
    ```

## 使用方法

### 使用块级语法

块级公式必须用 `#!latex $$...$$` 或 `#!latex \[...\]` 在单独的行中括起来：

``` latex title="块级语法"
$$
\cos x=\sum_{k=0}^{\infty}\frac{(-1)^k}{(2k)!}x^{2k}
$$
```

<div class="result" markdown>

$$
\cos x=\sum_{k=0}^{\infty}\frac{(-1)^k}{(2k)!}x^{2k}
$$

</div>

### 使用内联块语法

内联块必须用 `#!latex $...$` 或 `#!latex \(...\)` 括起来：

``` latex title="内联语法"
同态 $f$ 是单射当且仅当其核仅为单元素集 $e_G$，否则 $\exists a,b\in G$ 且 $a\neq b$ 使得 $f(a)=f(b)$。
```

<div class="result" markdown>

同态 $f$ 是单射当且仅当其核仅为单元素集 $e_G$，否则 $\exists a,b\in G$ 且 $a\neq b$ 使得 $f(a)=f(b)$。

</div>

## 比较 MathJax 和 KaTeX

在决定使用 MathJax 还是 KaTeX 时，需要考虑以下几个关键因素：

- __速度__：KaTeX 通常比 MathJax 更快。如果您的站点需要快速渲染大量复杂方程，KaTeX 可能是更好的选择。

- __语法支持__：MathJax 支持更广泛的 LaTeX 命令，可以处理各种数学标记语言（如 AsciiMath 和 MathML）。如果您需要高级 LaTeX 功能，MathJax 可能更合适。

- __输出格式__：两个库都支持 HTML 和 SVG 输出。但是，MathJax 还提供 MathML 输出，这对于可访问性至关重要，因为它可以被屏幕阅读器读取。

- __可配置性__：MathJax 提供了一系列配置选项，允许对其行为进行更精确的控制。如果您有特定的渲染要求，MathJax 可能是更灵活的选择。

- __浏览器支持__：虽然两个库在现代浏览器中都能很好地工作，但 MathJax 与旧版浏览器有更广泛的兼容性。如果您的受众使用各种浏览器，包括旧版浏览器，MathJax 可能是更安全的选择。

总之，KaTeX 以其速度和简单性而著称，而 MathJax 则以牺牲速度为代价提供更多功能和更好的兼容性。两者之间的选择主要取决于您的具体需求和约束。

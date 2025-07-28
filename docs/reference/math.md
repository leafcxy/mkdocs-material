---
icon: material/alphabet-greek
---

# 数学

[MathJax]和[KaTeX]是两个流行的库，用于显示
浏览器中的数学内容。尽管这两个库提供了类似的功能
功能，它们使用不同的语法并具有不同的配置
选项。本文档网站提供有关如何集成它们的信息
轻松使用MkDocs材料。

  [MathJax]: https://www.mathjax.org/
  [LaTeX]: https://en.wikibooks.org/wiki/LaTeX/Mathematics
  [MathML]: https://en.wikipedia.org/wiki/MathML
  [AsciiMath]: http://asciimath.org/
  [KaTeX]: https://katex.org/


## 配置

以下配置支持渲染块和
使用[MathJax]和[KaTeX]的内联块方程。

### MathJax

[MathJax]是一个强大而灵活的库，支持多种输入格式，
例如[LaTeX]、[MathML]、[AsciiMath]，以及各种输出格式，如
HTML、SVG、MathML。要在项目中使用MathJax，请添加以下行
到你的mkdocs.yml。

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

    1. This integrates MathJax with [instant loading].

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    markdown_extensions:
      - pymdownx.arithmatex:
          generic: true

    extra_javascript:
      - javascripts/mathjax.js
      - https://unpkg.com/mathjax@3/es5/tex-mml-chtml.js
    ```

请参阅其他配置选项：

- [Arithmatex]

  [Arithmatex]: ../setup/extensions/python-markdown-extensions.md#arithmatex
  [instant loading]: ../setup/setting-up-navigation.md#_3

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

[KaTeX]是一个轻量级的库，专注于速度和简单性。它
支持LaTeX语法的一个子集，可以将数学渲染为HTML和SVG。使用
[KaTeX]在您的项目中，将以下行添加到您的`mkdocs.yml`中。

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

    1. This integrates KaTeX with [instant loading].

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

## 使用

### 使用块语法

块必须用`#！乳胶$$。..$$或#！单独使用乳胶
线：

``` latex title="block syntax"
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

Inline blocks must be enclosed in `#!latex $...$` or `#!latex \(...\)`:

``` latex title="inline syntax"
The homomorphism $f$ is injective if and only if its kernel is only the
singleton set $e_G$, because otherwise $\exists a,b\in G$ with $a\neq b$ such
that $f(a)=f(b)$.
```

<div class="result" markdown>

The homomorphism $f$ is injective if and only if its kernel is only the
singleton set $e_G$, because otherwise $\exists a,b\in G$ with $a\neq b$ such
that $f(a)=f(b)$.

</div>

## MathJax和KaTeX的比较

在MathJax和KaTeX之间做出选择时，有几个关键因素
考虑：

- __速度__:KaTeX通常比MathJax快。如果您的网站需要
  快速渲染大量复杂的方程，KaTeX可能是
  更好的选择。

- __语法支持__:MathJax支持更广泛的LaTeX命令，可以
  处理各种数学标记语言（如AsciiMath和MathML）。
  如果你需要高级LaTeX功能，MathJax可能更合适。

- __输出格式__：这两个库都支持HTML和SVG输出。然而，
  MathJax还提供MathML输出，这对可访问性至关重要，
  因为它可以被屏幕阅读器读取。

- __可配置性__：MathJax提供了一系列配置选项，
  从而允许对其行为进行更精确的控制。如果你有具体的
  根据渲染要求，MathJax可能是一个更灵活的选择。

- __浏览器支持__：虽然这两个库在现代浏览器中都运行良好，
  MathJax与旧浏览器具有更广泛的兼容性。如果你的听众使用
  对于各种浏览器，包括较旧的浏览器，MathJax可能是一个更安全的选择。

总之，KaTeX以其速度和简单性而闻名，而MathJax则提供
以牺牲速度为代价，提供更多功能和更好的兼容性。选择
两者之间的差异在很大程度上取决于你的具体需求和限制。

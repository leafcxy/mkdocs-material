---
icon: material/format-font
---

# 格式化

Material for MkDocs 提供了对多种 HTML 元素的支持，这些元素可用于突出显示文档的某些部分或应用特定的格式化。此外，还支持 [Critic Markup]，它添加了显示文档建议更改的功能。

  [Critic Markup]: https://github.com/CriticMarkup/CriticMarkup-toolkit

## 配置

此配置启用了对键盘按键、文档更改跟踪、定义上下标和文本高亮的支持。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - pymdownx.critic
  - pymdownx.caret
  - pymdownx.keys
  - pymdownx.mark
  - pymdownx.tilde
```

查看更多配置选项：

- [Critic]
- [Caret, Mark & Tilde]
- [Keys]

  [Critic]: ../setup/extensions/python-markdown-extensions.md#critic
  [Caret, Mark & Tilde]: ../setup/extensions/python-markdown-extensions.md#caret-mark-tilde
  [Keys]: ../setup/extensions/python-markdown-extensions.md#keys

## 使用方法

### 高亮更改

启用 [Critic] 后，可以使用 [Critic Markup]，它添加了高亮建议更改以及在文档中添加内联注释的功能：

``` title="带建议更改的文本"
文本可以 {--删除--} 并替换为 {++添加++} 的文本。这也可以组合成 {~~一个~>单个~~} 操作。{==高亮==} 也是可能的 {>>并且可以添加内联注释<<}。

{==

通过将开始和结束标签放在单独的行上，并在标签和内容之间添加新行，也可以将格式化应用于块。

==}
```

<div class="result" markdown>

Text can be <del class="critic">deleted</del> and replacement text
<ins class="critic">added</ins>. This can also be combined into
<del class="critic">one</del><ins class="critic">a single</ins> operation.
<mark class="critic">Highlighting</mark> is also possible
<span class="critic comment">and comments can be added inline</span>.

<div>
  <mark class="critic block">
    <p>
      Formatting can also be applied to blocks by putting the opening and
      closing tags on separate lines and adding new lines between the tags and
      the content.
    </p>
  </mark>
</div>

</div>

### 高亮文本

启用 [Caret, Mark & Tilde] 后，可以使用简单的语法高亮文本，这比直接使用相应的 [`mark`][mark]、[`ins`][ins] 和 [`del`][del] HTML 标签更方便：

``` title="带高亮的文本"
- ==这是标记（高亮）==
- ^^这是插入（下划线）^^
- ~~这是删除（删除线）~~
```

<div class="result" markdown>

- ==This was marked (highlight)==
- ^^This was inserted (underline)^^
- ~~This was deleted (strikethrough)~~

</div>

  [mark]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/mark
  [ins]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ins
  [del]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/del

### 上下标

启用 [Caret & Tilde][Caret, Mark & Tilde] 后，可以使用简单的语法添加上下标，这比直接使用相应的 [`sub`][sub] 和 [`sup`][sup] HTML 标签更方便：

``` markdown title="带上下标的文本"
- H~2~O
- A^T^A
```

<div class="result" markdown>

- H~2~O
- A^T^A

</div>

  [sub]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/sub
  [sup]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/sup

### 添加键盘按键

启用 [Keys] 后，可以使用简单的语法渲染键盘按键。请查阅 [Python Markdown Extensions] 文档以了解所有可用的短代码：

``` markdown title="键盘按键"
++ctrl+alt+del++
```

<div class="result" markdown>

++ctrl+alt+del++

</div>

  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/extensions/keys/#extendingmodifying-key-map-index

---
icon: material/button-cursor
---

# 按钮

MkDocs的材质为主按钮和辅助按钮提供了专用样式
可以添加到任何链接、标签或按钮元素中。这尤其
对于具有专用“从呼叫到操作”的文档或登录页面非常有用。

## 配置

此配置允许向所有内联和块级别添加属性
使用简单语法的元素，将任何链接转换为按钮。添加
将以下行转换为`mkdocs.yml`：

``` yaml
markdown_extensions:
  - attr_list
```

请参阅其他配置选项：

- [Attribute Lists]

  [Attribute Lists]: ../setup/extensions/python-markdown.md#attribute-lists

## 使用

### 添加按钮

为了将链接呈现为按钮，请在其后面加上花括号并添加
`.md按钮`类选择器。该按钮将接收所选内容
[原色]和[强调色]（如果激活）。

``` markdown title="Button"
[Subscribe to our newsletter](#){ .md-button }
```

<div class="result" markdown>

[Subscribe to our newsletter][Demo]{ .md-button }

</div>

  [primary color]: ../setup/changing-the-colors.md#primary-color
  [accent color]: ../setup/changing-the-colors.md#accent-color
  [Demo]: javascript:alert$.next("Demo")

### 添加主按钮

如果你想显示一个填充的主按钮（如[登录页面]上）
MkDocs的Material），添加“.md按钮”和“.md”按钮--主`
CSS类选择器。

``` markdown title="Button, primary"
[Subscribe to our newsletter](#){ .md-button .md-button--primary }
```

<div class="result" markdown>

[Subscribe to our newsletter][Demo]{ .md-button .md-button--primary }

</div>

  [landing page]: ../index.md

### 添加图标按钮

当然，可以使用[icon语法]将图标添加到所有类型的按钮中
以及任何有效的图标短代码，只需通过我们的[图标搜索]按键即可轻松找到。

``` markdown title="Button with icon"
[Send :fontawesome-solid-paper-plane:](#){ .md-button }
```

<div class="result" markdown>

[Send :fontawesome-solid-paper-plane:][Demo]{ .md-button }

</div>

  [icon syntax]: icons-emojis.md#using-icons
  [icon search]: icons-emojis.md#search
